# Strudel Sounds & Samples Reference

## Playing Sounds

`s()` (or `sound()`) plays samples by name:

```javascript
s("bd hh sd oh")
sound("casio")
```

`n()` selects the sample number within a sound bank:

```javascript
n("0 1 2 3").s("jazz")
s("hh*8").n("0 1 2 3")
```

`:N` shorthand selects sample inline:

```javascript
s("hh:0 hh:1 hh:2 hh:3")
```

---

## Default Drum Sounds

Strudel uses the [tidal-drum-machines](https://github.com/ritchse/tidal-drum-machines) library:

| Sound | Abbreviation |
|-------|-------------|
| Bass drum / Kick | `bd` |
| Snare drum | `sd` |
| Rimshot | `rim` |
| Clap | `cp` |
| Closed hi-hat | `hh` |
| Open hi-hat | `oh` |
| Crash | `cr` |
| Ride | `rd` |
| High tom | `ht` |
| Medium tom | `mt` |
| Low tom | `lt` |
| Shakers/maracas | `sh` |
| Cowbell | `cb` |
| Tambourine | `tb` |
| Other percussion | `perc` |
| Miscellaneous | `misc` |
| Effects | `fx` |

Also available: `insect wind jazz metal east crow casio space numbers`

Check available sounds in the REPL's `sounds` tab.

---

## Drum Machine Banks

Use `bank()` to switch between different drum machines:

```javascript
s("bd hh sd oh").bank("RolandTR909")
s("bd sd, hh*8").bank("RolandTR808")
s("bd sd, hh*8").bank("<RolandTR808 RolandTR909>")  // pattern the bank
```

Common banks: `RolandTR808`, `RolandTR909`, `RolandTR707`, `RolandTR505`,
`AkaiLinn`, `RhythmAce`, `ViscoSpaceDrum`, `RolandCompurhythm1000`

Full names in the `sounds` tab follow `<Bank>_<drum>` pattern (e.g., `RolandTR808_bd`).

---

## Creating a Sound Alias

```javascript
soundAlias('RolandTR808_bd', 'kick')
s("kick")
```

---

## Loading Custom Samples

### From URLs

```javascript
samples({
  bassdrum: 'bd/BT0AADA.wav',
  hihat: 'hh27/000_hh27closedhh.wav',
  snaredrum: ['sd/rytm-01-classic.wav', 'sd/rytm-00-hard.wav'],
}, 'https://raw.githubusercontent.com/tidalcycles/Dirt-Samples/master/')

s("bassdrum snaredrum:0 bassdrum snaredrum:1, hihat*16")
```

Array values let you select samples with `:N` or `.n()`.

### From a strudel.json file

```javascript
samples('https://raw.githubusercontent.com/tidalcycles/Dirt-Samples/master/strudel.json')
s("bd sd bd sd, hh*16")
```

The JSON format:
```json
{
  "_base": "https://base-url/",
  "name": "path/to/file.wav",
  "name2": ["path/to/file1.wav", "path/to/file2.wav"]
}
```

### GitHub shortcut

```javascript
samples('github:tidalcycles/dirt-samples')   // uses main branch
samples('github:user/repo/branch')
s("bd sd bd sd, hh*16")
```

Requires a `strudel.json` at the repo root.

### From Disk (browser)

Use the REPL's `sounds → import-sounds` tab → "import sounds folder". Subfolders become sound names. Samples are zero-indexed alphabetically.

### From local server (@strudel/sampler)

```bash
cd samples
npx @strudel/sampler    # serves at http://localhost:5432/
```

```javascript
samples('http://localhost:5432/')
n("<0 1 2>").s("swoop smash")
```

### Shabda (freesound.org query tool)

```javascript
samples('shabda:bass:4,hihat:4,rimshot:2')

$: n("0 1 2 3").s('bass')
$: n("0 1*2 2 3*2").s('hihat').clip(1)
$: n("~ 0 ~ 1 ~ 0 0 1").s('rimshot')
```

Also generates speech samples:
```javascript
samples('shabda/speech:the_drum,forever')
samples('shabda/speech/fr-FR/m:magnifique')
```

---

## Specifying Pitch for Samples

```javascript
samples({
  'gtr': 'gtr/0001_cleanC.wav',
  'moog': { 'g3': 'moog/005_Mighty%20Moog%20G3.wav' },
}, 'github:tidalcycles/dirt-samples')

note("g3 [bb3 c4] <g4 f4 eb4 f3>@2").s("gtr,moog").clip(1)
```

Multi-region mapping (sampler picks closest match):
```javascript
samples({
  'moog': {
    'g2': 'moog/004_Mighty%20Moog%20G2.wav',
    'g3': 'moog/005_Mighty%20Moog%20G3.wav',
    'g4': 'moog/006_Mighty%20Moog%20G4.wav',
  }
}, 'github:tidalcycles/dirt-samples')
```

---

## Sampler Effects

### begin / end
Cut the start or end of a sample (0–1, where 1 = whole sample):
```javascript
s("bd*2").end("<.1 .2 .5 1>")
```

### loop / loopBegin / loopEnd
```javascript
s("casio").loop(1)
s("space").loop(1).loopBegin("<0 .125 .25>").loopEnd("<1 .75 .5>")
```
Samples prefixed with `wt_` loop automatically (wavetables).

### cut
Mutes the same cut group — classic open/closed hi-hat behavior:
```javascript
s("[oh hh]*4").cut(1)
```

### clip (legato)
Multiplies duration; cuts sample at event end:
```javascript
note("c a f e").s("piano").clip("<.5 1 2>")
```

### speed
Changes playback speed (and pitch). Negative = reverse:
```javascript
s("bd*6").speed("1 2 4 1 -2 -4")
speed("1 1.5*2 [2 1.1]").s("piano").clip(1)
```

### loopAt
Fits sample to N cycles by changing speed:
```javascript
s("rhodes").loopAt(2)
```

### fit
Fits sample to its event duration:
```javascript
s("rhodes/2").fit()
```

### chop
Cuts sample into N parts (granular synthesis):
```javascript
s("rhodes").chop(4).rev().loopAt(2)
```

### slice
Triggers specific slices with a pattern:
```javascript
s("breaks165").slice(8, "0 1 <2 2*2> 3 [4 0] 5 6 7").slow(0.75)
// also accepts position list:
s("breaks125").fit().slice([0,.25,.5,.75], "0 1 1 <2 3>")
```

### splice
Like slice but adjusts playback speed to match event duration:
```javascript
s("breaks165").splice(8, "0 1 [2 3 0]@2 3 0@2 7")
```

### striate
Cuts sample into N parts, playing progressive portions each loop:
```javascript
s("numbers:0 numbers:1 numbers:2").striate(6).slow(3)
```

### scrub
Scrub through a sample like a tape loop:
```javascript
s("swpad:0").scrub("{0.1!2 .25@3 0.7!2 <0.8:1.5>}%8")
```
