# Strudel Mini-Notation Reference

Mini-notation is the rhythmic pattern language used inside double-quoted strings in Strudel. It is inherited from Tidal Cycles.

**Key rule**: Use `"double quotes"` for mini-notation patterns, `'single quotes'` for plain strings (not parsed), `` `backticks` `` for multi-line patterns.

---

## Sequences

Space-separated events are divided equally into one cycle:

```
note("c e g b")        // 4 notes, each 1/4 cycle
note("c d e f g a b")  // 7 notes, each 1/7 cycle
```

Adding events doesn't change the cycle length — it makes each event shorter.

---

## Rests

`~` or `-` creates silence:

```
s("bd ~ sd ~")         // bd on beat 1, sd on beat 3
note("[b4 [~ c5] d5 e5]")
```

---

## Sub-sequences: `[]`

Nest sequences inside brackets — the bracket content fills one event's duration:

```
note("e5 [b4 c5] d5")        // b4 and c5 share the slot of one event
note("e5 [b4 c5] d5 [c5 b4 [d5 e5]]")  // deeply nested
```

---

## Multiplication: `*`

Speed up a sequence (plays N times per cycle):

```
note("[e5 b4 d5 c5]*2")      // plays twice per cycle
s("hh*8")                     // 8 hi-hats per cycle
s("bd*2.75")                  // decimal multipliers work
```

---

## Division: `/`

Slow down a sequence (plays over N cycles):

```
note("[e5 b4 d5 c5]/2")      // plays once every 2 cycles
note("[c d e f g]/2.75")     // decimal divisors work
```

---

## Angle Brackets: `<>`

Play one event per cycle (sequence length = number of elements):

```
note("<e5 b4 d5 c5>")        // same as [e5 b4 d5 c5]/4
note("<e5 b4 d5 c5 a4>")     // adding events doesn't change tempo
note("<e5 b4 d5 c5>*8")      // 8 events per cycle from the slow sequence
s("<bd hh rim oh bd rim>")   // one drum hit per cycle
```

Angle brackets are useful for chord progressions and long-form variations.

---

## Polyphony / Chords: `,`

Play events simultaneously (comma inside or outside brackets):

```
note("[g3,b3,e4]")           // G major chord
note("g3,b3,e4")             // same without brackets
note("<[g3,b3,e4] [a3,c3,e4] [b3,d3,f#4] [b3,e4,g4]>*2")
s("bd*4, hh*8, [~ sd]*2")    // parallel patterns (polyphony)
```

---

## Elongation: `@`

Sets the temporal weight (duration) of an event relative to others:

```
note("<[g3,b3,e4]@2 [a3,c3,e4] [b3,d3,f#4]>")  // first chord is 2x longer
note("c@3 eb")               // c is 3 units, eb is 1 unit
```

Default weight is 1. `@` does not affect tempo — it stretches within the slot.

---

## Replication: `!`

Repeats without speeding up (unlike `*`):

```
note("<[g3,b3,e4]!2 [a3,c3,e4]>")  // first chord plays twice at normal speed
note("c!3 e")                         // c repeats 3 times
```

Difference: `*` fills the same slot faster; `!` adds more slots of the same length.

---

## Randomness: `?` and `|`

`?` — 50% chance an event is silenced:

```
note("[g3,b3,e4]*8?")         // 50% chance each event is dropped
note("[g3,b3,e4]*8?0.1")      // 10% chance of being dropped (0–1 range)
```

`|` — choose one event at random:

```
note("[g3,b3,e4] | [a3,c3,e4] | [b3,d3,f#4]")  // random chord each cycle
s("bd | rim | cp")
```

---

## Sample Selection: `:`

Select a specific sample number within a sound bank:

```
s("hh:0 hh:1 hh:2 hh:3")    // explicit sample numbers
s("bd*4, hh:0 hh:1 hh:2 hh:3")
```

Equivalent to using `.n()` function.

---

## Euclidean Rhythms: `(beats,segments,offset)`

Distributes N beats evenly over M segments using Bjorklund's algorithm:

```
s("bd(3,8)")       // 3 kicks spread over 8 steps (clave/pop rhythm)
s("bd(5,8)")       // 5 over 8 (common in world music)
s("hh(7,16)")      // 7 over 16
```

Parameters:
- **beats**: how many events to trigger
- **segments**: total time slots to fill
- **offset** (optional): rotation/starting position

```
s("bd(3,8,0), hh cp")    // offset 0
s("bd(3,8,3), hh cp")    // offset 3 (shifted right by 3 steps)
s("bd(3,8,5), hh cp")    // offset 5
```

Written out: `s("bd(3,8)")` is equivalent to `s("bd ~ ~ bd ~ ~ bd ~")`

---

## Underscore `_`: Hold/Continue

`_` sustains the previous note (hold notation):

```
note("<[g3,b3,e4] _ [a3,c3,e4] [b3,d3,f#4]>*2")  // first chord holds for 2 slots
```

---

## Combining Everything

Mini-notation elements can be freely combined:

```
note("<[g3,b3,e4]@2 [a3,c3,e4]!2 [b3,d3,f#4]? [b3|e4|g4]>*2")
s("bd(3,8), [hh*2 oh?]*2, ~ [sd:0|sd:1] ~ sd")
```

---

## Multi-line Patterns (backticks)

Use backticks for multi-line mini-notation:

```javascript
note(`<
  [e5 [b4 c5] d5 [c5 b4]]
  [a4 [a4 c5] e5 [d5 c5]]
  [b4 [~ c5] d5 e5]
  [c5 a4 a4 ~]
>`)
```

---

## Quick Reference Table

| Syntax | Name | Effect |
|--------|------|--------|
| `a b c` | Sequence | Equal division in one cycle |
| `~` or `-` | Rest | Silence |
| `[a b]` | Sub-sequence | Nest inside one event slot |
| `*N` | Multiply | Play N times per cycle |
| `/N` | Divide | Play over N cycles |
| `<a b c>` | Angle brackets | One event per cycle |
| `a,b,c` | Parallel | Play simultaneously |
| `@N` | Elongate | Weight = N times normal |
| `!N` | Replicate | Repeat N times (same speed) |
| `?` | Random chance | 50% chance of silence |
| `?0.N` | Weighted chance | N chance of silence (0–1) |
| `a\|b\|c` | Random pick | Choose one at random |
| `:N` | Sample number | Select nth sample |
| `(b,s,o)` | Euclidean | b beats in s segments, offset o |
| `_` | Hold | Sustain previous event |
