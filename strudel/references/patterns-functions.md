# Strudel Pattern Functions Reference

Patterns are the core abstraction in Strudel. Everything is a pattern that maps time to values.

## Core Concepts

- A **pattern** generates events when queried for a time range (called a **cycle**)
- Patterns are pure functions — they are transformed by wrapping, not mutating
- **Mini-notation** (double-quoted strings) and **JS functions** can be freely mixed
- The scheduler queries patterns repeatedly and triggers sounds/events

---

## Running Multiple Patterns

Use `$:` before each pattern to run them simultaneously. `_$:` mutes a pattern:

```javascript
$: s("bd*4, [~ sd]*2")
$: note("<c e g b>*4").s("piano")
_$: note("c2 e2").s("bass")   // muted
```

---

## Combining Patterns

### stack()
Plays all patterns simultaneously:

```javascript
stack(
  note("c2 eb2(3,8)").s('sawtooth').cutoff(800),
  s("bd(5,8), hh*8")
)
```

### cat()
Plays patterns in sequence, one per cycle:

```javascript
cat(
  "g3,b3,e4",
  "a3,c3,e4",
  "b3,d3,f#4",
  "b3,e4,g4"
).note()
```

### sequence()
Creates a sequence of events (the underlying function for mini-notation):

```javascript
const pattern = sequence("c3", ["e3", "g3"])
```

### layer()
Apply different transformations to the same pattern in parallel:

```javascript
note("<g1 bb1 d2 f1>").layer(
  x => x.s("sawtooth").vib(4),
  x => x.s("square").add(note(12))
)
```

---

## Tempo Control

### setcpm(N)
Sets tempo in cycles per minute:

```javascript
setcpm(90/4)       // 90 BPM in 4/4 (each cycle = 1 bar)
setcpm(120/2)      // 120 BPM
setcpm(30)         // default: 30 cpm = 1 cycle every 2 seconds
```

### setcps(N)
Sets tempo in cycles per second:

```javascript
setcps(.75)
```

### fast(N) / slow(N)
Speed up or slow down a pattern:

```javascript
sound("bd*4, ~ rim ~ cp").slow(2)
sound("bd*4").fast("<1 [2 4]>")   // patternable
```

Inside mini-notation: `*` = fast, `/` = slow.

---

## Pitch and Notes

### note()
Set pitch as MIDI number or note name:

```javascript
note("48 52 55 59").s("piano")    // MIDI numbers
note("c e g b").s("piano")        // note names
note("c2 e3 g4 b5").s("piano")    // with octave
note("db eb gb ab bb").s("piano") // flats
note("c# d# f# g#").s("piano")    // sharps
```

### n() + scale()
Use scale degrees (0 = root):

```javascript
n("0 2 4 <[6,8] [7,9]>").scale("C:minor").s("piano")
n("<0 -3>, 2 4 <[6,8] [7,9]>").scale("<C:major D:mixolydian>/4").s("piano")
```

Available scales: `major`, `minor`, `dorian`, `mixolydian`, `pentatonic`, `major:pentatonic`, `minor:pentatonic`, and many more.

Scale format: `"Root:type"` e.g. `"C:minor"`, `"A2:minor:pentatonic"`, `"D:dorian"`

### chord() + voicing()
Play chord voicings using chord symbols:

```javascript
n("0 1 2 3").chord("Cm").mode("above:c3").voicing().s("gm_electric_guitar_clean")
chord("<Bbm9 Fm9>/4").dict('ireal').voicing().s("gm_epiano1:1")
```

---

## Arithmetic Pattern Manipulation

### add() / sub() / mul() / div()
Arithmetic on note values — accepts patterns:

```javascript
note("c e g").add(note("0 7 12"))   // add intervals
note("c2 e2").add(note(12))          // octave up
n("0 2 4").scale("C:minor").add(note("<0 1>/8"))  // chromatic addition
```

### offset / transpose
```javascript
chord("<Bbm9 Fm9>/4").offset(-1).voicing()   // shift chord voicing down
```

---

## Pattern Transformations

### rev()
Reverse the pattern:

```javascript
s("bd lt [~ ht] mt cp ~ bd hh").rev()
n(run(8)).scale("D:pentatonic").s("sawtooth").jux(rev)
```

### every(N, fn)
Apply a function every N cycles:

```javascript
s("bd*4").every(4, fast(2))
s("bd*4, hh*8").every(3, rev)
```

### sometimes() / sometimesBy(p, fn)
Randomly apply a transformation:

```javascript
s("hh*8").sometimes(mul(speed("2")))
s("amen/4").chop(16).sometimesBy(.5, ply("2"))
```

### rarely() / often()
Shorthand for `sometimesBy(.25, ...)` and `sometimesBy(.75, ...)`:

```javascript
s("amen").slice(8, "0 1 2 3 4 5 6 7").rarely(ply("2"))
n(run(8)).s('wt_flute').often(n => n.ply(2))
```

### ply(N)
Repeat each event N times within its time slot:

```javascript
s("bd sd").ply(2)     // each hit plays twice
s("hh*4").ply("<1 2 3>")
```

### off(t, fn)
Apply a function to the pattern offset by t cycles:

```javascript
"0".off(1/3, add(2)).off(1/2, add(4)).n().scale("C:minor")
```

### chunk(N, fn)
Apply a function to 1/N of the pattern, rotating each cycle:

```javascript
note("c e g b g e").chunk(4, fast(2))
```

### segment(N)
Sample the pattern N times per cycle:

```javascript
s("supersaw").seg(16).lpf(tri.range(100, 5000).slow(2))
```

### iter(N)
Rotate the pattern by 1/N each cycle:

```javascript
s("bd lt [~ ht] mt cp ~ bd hh").jux(iter(4))
```

### press
Push each event to the end of its time slot (offbeat swing):

```javascript
s("bd lt [~ ht] mt cp ~ bd hh").jux(press)
```

### early(t) / late(t)
Shift events earlier or later by t cycles:

```javascript
n(run(8)).s("ftabla").early(2/8)
```

### beat(positions, steps)
Place events at specific step positions:

```javascript
s("bd:4").beat("0,4,8,11,14", 16)
```

---

## Signals (Continuous Modulation)

Signals produce continuous values for modulation:

| Signal | Description |
|--------|-------------|
| `sine` | Sine wave (0–1) |
| `saw` | Sawtooth wave (0–1) |
| `square` | Square wave (0–1) |
| `tri` | Triangle wave (0–1) |
| `rand` | Random values |
| `perlin` | Smooth random (Perlin noise) |

```javascript
sound("hh*16").gain(sine)
sound("hh*16").lpf(saw.range(500, 2000))
note("c e g").s("sawtooth").lpf(sine.range(100, 2000).slow(4))
```

### irand(N)
Random integer 0 to N-1:

```javascript
s("triangle*4").n(irand(12)).scale("C minor")
```

### run(N)
Sequence 0 to N-1:

```javascript
n(run(8)).s("ftabla")   // cycle through 8 samples
n(run(8)).scale("D:pentatonic").s("sawtooth")
```

### randL(N) / binaryL(N)
Produce lists of N random/binary values (for `partials`):

```javascript
note("c2").s("user").partials(randL(10))
```

---

## Custom Functions with register()

Create reusable chained functions:

```javascript
const effectChain = register('effectChain', (pat) => pat
  .s("sawtooth")
  .cutoff(500)
  .room(0.5)
)

note("a3 c#4 e4 a4").effectChain()
```

---

## JS Integration

Strudel runs in JavaScript — you can use any JS:

```javascript
const numHarmonics = 22
note("c2").s("saw").partials(new Array(numHarmonics).fill(1))

// Computed values
const myScale = "C:minor"
n("0 2 4").scale(myScale).s("piano")

// Constants and variables
let chords = chord("<Bbm9 Fm9>/4").dict('ireal')
stack(
  chords.voicing().s("gm_epiano1:1").phaser(4).room(.5),
  chords.offset(-1).voicing().s("gm_acoustic_bass")
)
```

---

## Pattern Technical Details

- Patterns are time functions: given a time span, they output events with begin/end times and values
- Time is rational arithmetic (fractions): `0/1 -> 1/2` means "first half of cycle"
- Transformations wrap patterns in new patterns that modify the query/result
- The REPL scheduler repeatedly queries patterns and schedules audio events
