# Strudel Recipes: Common Musical Techniques

Practical solutions for common musical goals in Strudel. Multiple approaches are shown — each gives different creative impulses when improvising.

---

## Drum Beats

### Basic Rock Beat
```javascript
setcpm(100/4)
s("[bd sd]*2, hh*8").bank("RolandTR505")
```

### Classic House
```javascript
s("bd*4, [~ cp]*2, [~ hh]*4").bank("RolandTR909")
```

### 16-Step Sequencer Style
```javascript
setcpm(90/4)
s(`
[- - oh -] [- - - -] [- - - -] [- - - -],
[hh hh - -] [hh - hh -] [hh - hh -] [hh - hh -],
[- - - -] [cp - - -] [- - - -] [cp - - -],
[bd - - -] [- - - bd] [- - bd -] [- - - bd]
`)
```

### Euclidean Drum Patterns
```javascript
s("bd(3,8), hh(5,8), sd(2,8,2)")
s("bd(5,8), [hh hh:1](7,16), rim(3,8,1), oh(2,8,5)")
```

---

## Arpeggios

### Notes by hand
```javascript
note("c eb g c4").clip(2).s("gm_electric_guitar_clean")
```

### From a scale
```javascript
n("0 2 4 7").scale("C:minor").clip(2).s("gm_electric_guitar_clean")
```

### From chord symbols
```javascript
n("0 1 2 3").chord("Cm").mode("above:c3").voicing()
  .clip(2).s("gm_electric_guitar_clean")
```

### Using off() for rolling arpeggios
```javascript
"0"
  .off(1/3, add(2))
  .off(1/2, add(4))
  .n().scale("C:minor")
  .s("gm_electric_guitar_clean")
```

---

## Basslines

### Classic Bassline
```javascript
note("<[c2 c3]*4 [bb1 bb2]*4 [f2 f3]*4 [eb2 eb3]*4>")
  .s("gm_synth_bass_1").lpf(800)
```

### Synth Bass with Filter
```javascript
note("g1 bb1 <c2 eb2> d2")
  .s("sawtooth").lpf(400).lpenv(4)
```

### Sub Bass
```javascript
note("c2*4").s("sine").pdec(.3).penv(12).gain(.8)
```

---

## Melodies

### Chord Progression + Melody
```javascript
$: note("<[c2 c3]*4 [bb1 bb2]*4 [f2 f3]*4 [eb2 eb3]*4>")
   .s("gm_synth_bass_1").lpf(800)

$: n(`<
  [~ 0] 2 [0 2] [~ 2]
  [~ 0] 1 [0 1] [~ 1]
  [~ 0] 3 [0 3] [~ 3]
  [~ 0] 2 [0 2] [~ 2]
>*4`).scale("C4:minor").s("gm_synth_strings_1")
```

### Scales and Degrees
```javascript
setcpm(60)
n("0 2 4 <[6,8] [7,9]>").scale("C:minor").s("piano")
```

---

## Filter Envelopes

Default (decay-style) filter envelope:
```javascript
note("g1 bb1 <c2 eb2> d2").s("sawtooth").lpf(400).lpenv(4)
```

Attack-style envelope:
```javascript
note("g1 bb1 <c2 eb2> d2").s("sawtooth").lpq(8)
  .lpf(400).lpa(.2).lpenv(4)
```

Both attack and decay:
```javascript
note("g1 bb1 <c2 eb2> d2").s("sawtooth").lpq(8)
  .lpf(400).lpa(.1).lpd(.1).lpenv(4)
```

---

## Layering Sounds

### Simple layering with `,` in `s()`
```javascript
note("<g1 bb1 d2 f1>").s("sawtooth, square")
```

### Control gain per layer
```javascript
note("<g1 bb1 d2 f1>").s("sawtooth, square:0:.5")  // "name:number:gain"
```

### Full control with layer()
```javascript
note("<g1 bb1 d2 f1>").layer(
  x => x.s("sawtooth").vib(4),
  x => x.s("square").add(note(12))
)
```

---

## Chopping Breaks

### Basic looped break
```javascript
samples('github:yaxu/clean-breaks')
s("amen/4").fit().chop(32)
```

### With randomized manipulation
```javascript
samples('github:yaxu/clean-breaks')
s("amen/4").fit().chop(16).cut(1)
  .sometimesBy(.5, ply("2"))
  .sometimesBy(.25, mul(speed("-1")))
```

### Specific slice order with slice()
```javascript
samples('github:yaxu/clean-breaks')
s("amen/4").fit()
  .slice(8, "<0 1 2 3 4*2 5 6 [6 7]>*2")
  .cut(1).rarely(ply("2"))
```

### splice() — auto-adjusts speed to fit events
```javascript
samples('github:yaxu/clean-breaks')
s("amen").splice(8, "<0 1 2 3 4*2 5 6 [6 7]>*2")
  .cut(1).rarely(ply("2"))
```

---

## Oscillator Detune (Chorus Effect)

```javascript
note("<g1 bb1 d2 f1>")
  .add(note("0,.1"))  // add detuned copy
  .s("sawtooth")
```

Try `"0,.1,.2"` for a thicker chorus.

---

## Polyrhythm and Polymeter

### Polyrhythm (two different tempos)
```javascript
s("bd*2, hh*3")
```

### Polymeter (two different bar lengths, same tempo)
```javascript
s("<bd rim, hh hh oh>*4")
```

### Phasing (same sequence at slightly different speeds)
```javascript
note("<C D G A Bb D C A G D Bb A>*[6,6.1]").piano()
```

---

## Tape Warble

```javascript
note("<c4 bb f eb>*8")
  .add(note(perlin.range(0,.5)))  // pitch warble
  .clip(2).s("gm_electric_guitar_clean")
```

---

## Sound Duration Control

Relative to event duration:
```javascript
note("f ab bb c").clip("<2 1 .5 .25>")   // clip: cuts at event end
note("f ab bb c").release("<2 1 .5 .25>") // release: fades out
note("f ab bb c").decay("<2 1 .5 .25>")   // decay: shorter envelope
```

For samples, also use `.end()`:
```javascript
s("oh*4").end("<1 .5 .25 .1>")   // cut relative to sample length
```

---

## Wavetable Synthesis

Loop the beginning of a sample as a synth:
```javascript
note("<c eb g f>").s("bd").loop(1).loopEnd(.05).gain(.2)
```

Using `wt_` prefix (auto-loops):
```javascript
samples('github:bubobubobubobubo/dough-waveforms')
note("c eb g bb").s("wt_dbass").clip(2)
```

Scanning through wavetables:
```javascript
samples('github:bubobubobubobubo/dough-waveforms')
note("c2*8").s("wt_dbass").n(run(8)).fast(2)
```

With filter envelope and reverb:
```javascript
samples('github:bubobubobubobubo/dough-waveforms')
note("c2*8").s("wt_dbass").n(run(8))
  .lpf(perlin.range(100,1000).slow(8))
  .lpenv(-3).lpa(.1).room(.5).fast(2)
```

---

## Running Through Sample Banks

```javascript
samples('bubo:fox')
n(run(8)).s("ftabla")               // run through 8 samples
n(run(8)).s("ftabla").early(2/8)    // shift phrase start
n(run(8)).s("ftabla").early(2/8).sometimes(mul(speed("1.5")))  // add variation
```

---

## Dub / Delay Effects

```javascript
$: note("[~ [<[d3,a3,f4]!2 [d3,bb3,g4]!2> ~]]*2")
   .s("gm_electric_guitar_muted").delay(.5)

$: s("bd rim").bank("RolandTR707").delay(.5)

$: n("<4 [3@3 4] [<2 0> ~@16] ~>")
   .scale("D4:minor").s("gm_accordion:2")
   .room(2).gain(.5)
```

---

## Sidechain Ducking

```javascript
$: n(run(16)).scale("c:minor:pentatonic").s("sawtooth").delay(.7).orbit(2)
$: s("bd:4!4").beat("0,4,8,11,14",16).duckorbit(2).duckattack(0.2).duckdepth(1)
```

---

## Full Song Structure

Use `<>` for bar-by-bar changes, `every()` for periodic variation:

```javascript
setcps(.75)
let chords = chord("<Bbm9 Fm9>/4").dict('ireal')

stack(
  stack(  // DRUMS
    s("bd").struct("<[x*<1 2> [~@3 x]] x>"),
    s("~ [rim, sd:<2 3>]").room("<0 .2>"),
    n("[0 <1 3>]*<2!3 4>").s("hh"),
  ).bank('crate'),
  chords.voicing().s("gm_epiano1:1").phaser(4).room(.5),
  chords.offset(-1).voicing().s("gm_acoustic_bass"),
)
```
