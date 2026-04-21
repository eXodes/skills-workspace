# Strudel Synths Reference

Strudel has a built-in synthesizer for creating sounds on the fly, in addition to the sample-based engine.

---

## Basic Waveforms

Selected via `s()` or `sound()`:

```javascript
note("c2 <eb2 <g2 g1>>".fast(2)).s("<sawtooth square triangle sine>")
```

Available waveforms: `sine`, `sawtooth` (`saw`), `square`, `triangle`

If you set `note()` without a `sound()`, the default waveform is `triangle`.

---

## Noise Sources

```javascript
sound("<white pink brown>")       // white = harshest, brown = softest
sound("bd*2, <white pink brown>*8").decay(.04).sustain(0)  // noise hihats
```

Add noise to any oscillator with `noise`:
```javascript
note("c3").noise("<0.1 0.25 0.5>")
```

Crackle noise (controlled with `density`):
```javascript
s("crackle*4").density("<0.01 0.04 0.2 0.5>".slow(2))
```

---

## Vibrato

### vib (vibrato)
Applies pitch vibrato at the given frequency in Hz:
```javascript
note("a e").vib("<.5 1 2 4 8 16>")
note("a e").vib("<.5 1 2 4 8 16>:12")  // ":depth" sets modulation depth
```

### vibmod
Sets vibrato depth in semitones (requires `vib` to be set):
```javascript
note("a e").vib(4).vibmod("<.25 .5 1 2 12>")
note("a e").vibmod("<.25 .5 1 2 12>:8")  // ":freq" sets vibrato frequency
```

---

## FM Synthesis

FM (Frequency Modulation) changes the frequency of a waveform rapidly to alter timbre.

### fm
Sets the FM amount/depth:
```javascript
note("c e g b g e").fm(4)
note("c e g b g e").fm("<0 1 2 4 8 16>")
```

### fmh (FM harmonicity)
Controls the timbre. Whole numbers = natural; decimals = metallic:
```javascript
note("c e g b g e").fm(4).fmh("<1 2 1.5 1.61>")
```

### FM Envelope
Controls the shape of FM modulation over time:

```javascript
note("c e g b g e").fm(4).fmattack("<0 .05 .1 .2>")     // attack
note("c e g b g e").fm(4).fmdecay("<.01 .05 .1 .2>").fmsustain(.4)  // decay+sustain
note("c e g b g e").fm(4).fmsustain("<1 .75 .5 0>")      // sustain level
note("c e g b g e").fm(4).fmdecay(.2).fmsustain(0).fmenv("<exp lin>")  // envelope type
```

Aliases: `fmatt`, `fmdec`, `fmsus`, `fme`

Up to 8 independent FM operators (append number: `fmh2`, `fmatt5`, etc.)

---

## Additive Synthesis

### partials
Controls the magnitude of harmonics (overtones):

```javascript
// Filter harmonics on a sawtooth
note("c2").s("sawtooth").partials([1, 1, "<1 0>", "<1 0>", "<1 0>"])

// Build custom waveforms with 'user' source
note("c2").s("user").partials([1, 0, 0.3, 0, 0.1, 0, 0, 0.3])

// Algorithmically generate harmonics
const numHarmonics = 22
note("c2").s("saw").partials(new Array(numHarmonics).fill(1))
```

Compatible with pattern functions like `randL` and `binaryL`:
```javascript
note("c2").s("user").partials(randL(10))
```

### phases
Controls the phase of each harmonic:
```javascript
s("saw").seg(16).n(irand(12)).scale("F1:minor")
  .partials(randL(200)).phases(randL(200))
```

---

## Wavetable Synthesis

Any sample prefixed with `wt_` is loaded as a wavetable (loops automatically):

```javascript
// Built-in AKWF wavetables (1000+ available)
note("<[g3,b3,e4]!2 [a3,c3,e4]>")
  .n("<1 2 3 4 5>/2").s('wt_flute')
  .release(0.125).decay("<0.1 0.25>")

// Custom wavetable packs
samples('github:bubobubobubobubo/dough-waveforms')
note("c eb g bb").s("wt_dbass").clip(2)
```

Scan through wavetables with `n(run(8))`:
```javascript
samples('github:bubobubobubobubo/dough-waveforms')
note("c2*8").s("wt_dbass").n(run(8)).fast(2)
```

---

## ZZFX ("Zuper Zmall Zound Zynth")

A compact synth engine. Sources: `z_sawtooth`, `z_tan`, `z_noise`, `z_sine`, `z_square`

```javascript
note("c2 eb2 f2 g2")
  .s("{z_sawtooth z_tan z_noise z_sine z_square}%4")
  .zrand(0)         // randomization
  .attack(0.001).decay(0.1).sustain(.8).release(.1)
  .curve(1)         // waveshape 1–3
  .slide(0)         // pitch slide
  .deltaSlide(0)    // secondary pitch slide
  .noise(0)         // dirtiness
  .zmod(0)          // FM speed
  .zcrush(0)        // bit crush 0–1
  .zdelay(0)        // simple delay
  .pitchJump(0)     // pitch jump after pitchJumpTime
  .pitchJumpTime(0)
  .lfo(0)           // LFO speed
  .tremolo(0.5)     // LFO volume mod amount
```

ZZFX can be combined with all standard audio effects.

---

## General Synthesis Tips

- Use `note()` to set pitch for any synth
- `sound()` / `s()` selects the waveform/synth type
- Chain effects (`.lpf()`, `.adsr()`, `.room()`, etc.) after the sound source
- FM works with any waveform, not just the default triangle
- Wavetables are great for lush pads and bass sounds
- ZZFX is good for retro/chiptune and game sounds
