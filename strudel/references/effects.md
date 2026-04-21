# Strudel Audio Effects Reference

All effects chain with `.` after a sound source. Effects accept patterns as arguments.

## Signal Chain Order (simplified)

Sound source → (stretch) → gain/ADSR → lpf → hpf → bpf → vowel → coarse → crush → shape → distort → tremolo → compressor → pan → phaser → postgain → [delay | reverb] → orbit/mixer

Note: effects in this chain are **single-use per pattern** — calling lpf twice overrides the first.

---

## Filters

### lpf (low-pass filter)
Synonyms: `cutoff`, `ctf`, `lp`

Allows frequencies **below** cutoff to pass. Higher value = brighter sound.

```javascript
s("bd sd hh*8").lpf("<4000 2000 1000 500 200 100>")
s("bd*16").lpf("1000:0 1000:10 1000:30")  // ":lpq" inline
note("c2 e2").s("sawtooth").lpf(sine.range(100, 2000).slow(4))  // LFO sweep
```

### lpq (low-pass resonance)
Synonyms: `resonance`

Resonance/Q factor for the low-pass filter (0–50):
```javascript
s("bd sd").lpf(2000).lpq("<0 10 20 30>")
```

### hpf (high-pass filter)
Synonyms: `hp`, `hcutoff`

Allows frequencies **above** cutoff to pass:
```javascript
s("bd sd hh*8").hpf("<4000 2000 1000 500 200 100>")
s("bd sd").hpf("<2000 2000:25>")  // ":hpq" inline
```

### hpq (high-pass resonance)
Synonyms: `hresonance`

```javascript
s("bd sd hh*8").hpf(2000).hpq("<0 10 20 30>")
```

### bpf (band-pass filter)
Synonyms: `bandf`, `bp`

Allows only a frequency band to pass:
```javascript
s("bd sd hh*6").bpf("<1000 2000 4000 8000>")
s("bd sd").bpf(500).bpq("<0 1 2 3>")
```

### vowel
Formant filter simulating vowel sounds. Values: `a e i o u ae aa oe ue y uh un en an on`

```javascript
note("[c2 <eb2 <g2 g1>>]*2").s("sawtooth").vowel("<a e i <o u>>")
s("bd sd mt ht bd [~ cp] ht lt").vowel("[a|e|i|o|u]")
```

### ftype
Filter type. `12db` (0), `ladder` (1), `24db` (2):
```javascript
note("{f g g c}%8").s("sawtooth").lpf(500).ftype("<0 1 2>").lpq(1)
note("c f g a").s("sawtooth").lpf(200).ftype("<ladder 12db 24db>")
```

---

## Amplitude Envelope (ADSR)

Controls the dynamic shape of a sound over time:
- **Attack**: time to reach peak level
- **Decay**: time from peak to sustain level
- **Sustain**: level held until note ends (0–1)
- **Release**: time to fade after note ends

```javascript
note("c3 e3 f3 g3").attack("<0 .1 .5>")
note("c3 e3 f3 g3").decay("<.1 .2 .3 .4>").sustain(0)
note("c3 e3 f3 g3").decay(.2).sustain("<0 .1 .4 .6 1>")
note("c3 e3 g3 c4").release("<0 .1 .4 .6 1>/2")
```

Shortcuts: `att`, `dec`, `sus`, `rel`

Combined shorthand `.adsr("attack:decay:sustain:release")`:
```javascript
note("[c3 bb2 f3 eb3]*2").s("sawtooth").lpf(600).adsr(".1:.1:.5:.2")
```

---

## Filter Envelopes

Each filter (lpf, hpf, bpf) has its own ADSR envelope to modulate cutoff dynamically.

Prefix: `lp`, `hp`, `bp` + parameter name:

```javascript
// Low-pass filter envelope
note("c2 e2 f2 g2").s("sawtooth")
  .lpf(300)
  .lpa(.5)       // attack
  .lpd(.2)       // decay  
  .lps(.5)       // sustain
  .lpr(.3)       // release
  .lpenv(4)      // depth in octaves
```

`.lpenv(N)` sets modulation depth (positive = up, negative = down).

Aliases: `lpattack/lpa`, `lpdecay/lpd`, `lpsustain/lps`, `lprelease/lpr`, `lpenv/lpe`
Same pattern for `hpattack/hpa`, `hpdecay/hpd`, etc. and `bpattack/bpa`, etc.

Complex example:
```javascript
note("[c eb g <f bb>](3,8,<0 1>)".sub(12))
  .s("<sawtooth>/64")
  .lpf(sine.range(300,2000).slow(16))
  .lpa(0.005).lpd(perlin.range(.02,.2))
  .lps(perlin.range(0,.5).slow(3))
  .lpq(sine.range(2,10).slow(32))
  .release(.5).lpenv(perlin.range(1,8).slow(2))
  .ftype('24db').room(1)
```

---

## Pitch Envelope

Controls pitch (in semitones) over time:

```javascript
note("c").penv("<12 7 1 .5 0 -1 -7 -12>")
note("c3 e3 f3 g3").pattack("0 .1 .25 .5").slow(2)
note("<c eb g bb>").pdecay("<0 .1 .25 .5>")
note("<c eb g bb> ~").release(.5).prelease("<0 .1 .25 .5>")
```

`penv`: depth in semitones (negative flips direction)
`pcurve`: 0 = linear, 1 = exponential (good for kicks)
`panchor`: 0 = note is bottom of range, 1 = note is top of range

```javascript
note("g1*4").s("sine").pdec(.5).penv(32).pcurve("<0 1>")   // kick drum pitch
```

Aliases: `patt`, `pdec`, `prel`

---

## Dynamics

### gain
Exponential gain control:
```javascript
s("hh*8").gain(".4!2 1 .4!2 1 .4 1")
```

### velocity (vel)
Velocity 0–1, multiplied with gain:
```javascript
s("hh*8").gain(".4!2 1 .4!2 1 .4 1").velocity(".4 1")
```

### compressor
`compressor("threshold:ratio:knee:attack:release")`:
```javascript
s("bd sd [~ bd] sd, hh*8").compressor("-20:20:10:.002:.02")
```

### postgain
Gain after all effects:
```javascript
s("bd sd hh*8").compressor("-20:20:10:.002:.02").postgain(1.5)
```

### xfade
Cross-fades between two patterns (0 = full left, 1 = full right):
```javascript
xfade(s("bd*2"), "<0 .25 .5 .75 1>", s("hh*8"))
```

---

## Panning

### pan
Position in stereo field (0 = left, 0.5 = center, 1 = right):
```javascript
s("[bd hh]*2").pan("<.5 1 .5 0>")
s("bd rim sd rim bd ~ cp rim").pan(sine.slow(2))
```

### jux
Apply a function to only the right channel (creates stereo effects):
```javascript
s("bd lt [~ ht] mt cp ~ bd hh").jux(rev)
s("bd lt [~ ht] mt cp ~ bd hh").jux(press)
s("bd lt [~ ht] mt cp ~ bd hh").jux(iter(4))
```

### juxBy (juxby)
Like jux with adjustable stereo width (0 = mono, 1 = full stereo):
```javascript
s("bd lt [~ ht] mt cp ~ bd hh").juxBy("<0 .5 1>/2", rev)
```

---

## Reverb

### room
Level of reverb (0–1). Optionally add size with `:`:
```javascript
s("bd sd [~ bd] sd").room("<0 .2 .4 .6 .8 1>")
s("bd sd [~ bd] sd").room("<0.9:1 0.9:4>")  // ":size"
```

### roomsize (rsize, sz, size)
Room size (0–10). Changing recalculates the reverb — use sparingly:
```javascript
s("bd sd").room(.8).rsize(4)
```

### roomfade (rfade)
Reverb fade time in seconds:
```javascript
s("bd sd").room(0.5).rfade(4)
```

### roomlp (rlp)
Reverb lowpass frequency (Hz):
```javascript
s("bd sd").room(0.5).rlp(5000)
```

### roomdim (rdim)
Reverb lowpass at -60dB:
```javascript
s("bd sd").room(0.5).rlp(10000).rdim(8000)
```

### iresponse (ir)
Use an audio sample as an impulse response:
```javascript
s("bd sd").room(.8).ir("<shaker_large:0 shaker_large:2>")
```

---

## Delay

### delay
Level of delay signal (0–1). Optionally: `"level:time:feedback"`:
```javascript
s("bd bd").delay("<0 .25 .5 1>")
s("bd bd").delay("0.65:0.25:0.9")
```

### delaytime (delayt, dt)
Delay time in seconds:
```javascript
note("d d a# a".fast(2)).s("sawtooth").delay(.8).delaytime(1/2)
```

### delayfeedback (delayfb, dfb)
Feedback amount (keep < 1 to avoid runaway):
```javascript
s("bd").delay(.25).delayfeedback("<.25 .5 .75>")
```

---

## Waveshaping / Distortion

### coarse
Fake bit-rate reduction (Chromium only):
```javascript
s("bd sd hh*8").coarse("<1 4 8 16 32>")
```

### crush
Bit crusher (1 = extreme, 16 = barely audible):
```javascript
s("<bd sd>, hh*3").fast(2).crush("<16 8 7 6 5 4 3 2>")
```

### distort (dist)
Wave-shaping distortion. `"amount:postgain:type"`:
```javascript
s("bd sd hh*8").distort("<0 2 3 10:.5>")
note("d1!8").s("sine").penv(36).pdecay(.12).distort("8:.4")
s("bd:4*4").bank("tr808").distort("3:0.5:diode")
```

### shape
Waveshape distortion:
```javascript
s("bd*4").shape(.3)
```

---

## Amplitude Modulation (Tremolo)

### tremolosync (tremsync)
Speed of amplitude modulation in cycles:
```javascript
note("d d d# d".fast(4)).s("supersaw").tremolosync("4").tremoloskew("<1 .5 0>")
```

### tremolodepth (tremdepth)
Depth of amplitude modulation:
```javascript
note("a1 a1 a#1 a1".fast(4)).s("pulse").tremsync(4).tremolodepth("<1 2 .7>")
```

### tremoloskew (tremskew)
Shape of modulation waveform (0–1):
```javascript
note("{f a c e}%16").s("sawtooth").tremsync(4).tremoloskew("<.5 0 1>")
```

### tremoloshape (tremshape)
Shape type: `tri`, `square`, `sine`, `saw`, `ramp`:
```javascript
note("{f g c d}%16").tremsync(4).tremoloshape("<sine tri square>").s("sawtooth")
```

---

## Phaser

```javascript
n(run(8)).scale("D:pentatonic").s("sawtooth").release(0.5).phaser("<1 2 4 8>")
n(run(8)).scale("D:pentatonic").s("sawtooth").phaser(2).phaserdepth("<0 .5 .75 1>")
n(run(8)).scale("D:pentatonic").s("sawtooth").phaser(2).phasercenter("<800 2000 4000>")
n(run(8)).scale("D:pentatonic").s("sawtooth").phaser(2).phasersweep("<800 2000 4000>")
```

Aliases: `ph`, `phd/phasdp`, `phc`, `phs`

---

## Orbits (Global Effect Routing)

Orbits group patterns for shared delay/reverb. Use `orbit(N)` to assign:

```javascript
stack(
  s("hh*6").delay(.5).delaytime(.25).orbit(1),
  s("~ sd ~ sd").delay(.5).delaytime(.125).orbit(2)
)
```

Default orbit is 1. Changing reverb params on two patterns sharing an orbit causes conflicts — use separate orbits.

Multi-orbit output (with Multi Channel Orbits setting): orbit `i` → channels `2i` and `2i+1`.

---

## Ducking (Sidechain)

### duckorbit (duck)
Modulate volume of another orbit (sidechain-like effect):
```javascript
$: n(run(16)).scale("c:minor:pentatonic").s("sawtooth").delay(.7).orbit(2)
$: s("bd:4!4").beat("0,4,8,11,14",16).duckorbit(2).duckattack(0.2).duckdepth(1)
```

### duckattack (datt)
Time for ducked signal to return to normal volume:
```javascript
s("bd*4").duckorbit(2).duckattack("<0.2 0 0.4>").duckdepth(1)
```

### duckdepth
Amount of ducking (0–1):
```javascript
s("bd*4").duckorbit(2).duckattack(0.2).duckdepth("<1 .9 .6 0>")
```

Syntax `:` applies different values to multiple orbits:
```javascript
s("bd*4").duckorbit("2:3").duckattack("0.4:0.1").duckdepth("1:0.5")
```

---

## Continuous Modulation with Signals

Some parameters support continuous modulation (LFO-style) — use signal functions:

```javascript
sound("hh*16").gain(sine)                    // gain modulated by sine wave
sound("hh*16").lpf(saw.range(500, 2000))     // filter sweep
note("c e").s("sawtooth").lpf(sine.range(100, 2000).slow(4))
```

Signal sources: `sine`, `saw`, `square`, `tri`, `rand`, `perlin`

`rand`: random values; `perlin`: smooth random (Perlin noise)

Use `.range(min, max)` to set modulation range. Use `.slow(N)` / `.fast(N)` to change rate.

**Note**: Most effects only update when a new event triggers. To fake a continuous LFO, increase event density:
```javascript
s("supersaw").seg(16).lpf(tri.range(100, 5000).slow(2))
```

Effects that truly update continuously: ADSR curves, pitch envelope, FM envelope, filter envelopes, tremolo, phaser, vibrato, ducking.
