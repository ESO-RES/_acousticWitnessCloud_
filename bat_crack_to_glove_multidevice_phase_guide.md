
# Bat Crack → Glove Thud  
## A Multi‑Camera, Multi‑Device Phase Analysis Guide

This guide explains **end‑to‑end** how a real baseball event — a bat striking a ball and the ball thudding into the pitcher’s glove — can be analyzed using **multiple cameras and audio devices** to:

- align recordings without shared clocks,
- measure **relative phase and cycle offsets** between devices,
- interpret those offsets physically (time, distance),
- and test consistency across the whole recording set.

It synthesizes the earlier phase‑relation workflow, the adversarial consistency protocol, and the concrete bat‑to‑glove physics example.

---

## 1. The Physical Event (Ground Truth)

### 1.1 The two acoustic impulses
A single play produces **two dominant, impulsive sounds**:

1. **Bat crack**  
   - Very sharp onset  
   - Strong midrange energy (≈800–1500 Hz)  
   - Excellent for phase analysis  

2. **Glove thud**  
   - Lower energy, slightly broader spectrum  
   - Still phase‑trackable in midrange, but weaker  

These are **separate acoustic sources** in space and time.

---

## 2. What the Cameras and Devices Capture

Each camera / phone records:

- Video (with its own frame clock)
- Audio (with its own ADC clock)
- Unknown start time
- Unknown constant latency
- Possible drift

**No two devices are synchronized.**  
Absolute timestamps are unreliable.  
This is why **relative phase** is used instead.

---

## 3. Why Narrowband Phase Works Here

### 3.1 Choice of frequency band
We intentionally isolate a narrow midrange band, typically:

- **Center:** ~1000 Hz  
- **Bandwidth:** ~50–100 Hz (Q ≈ 10–20)

Reasons:
- Human‑scale wavelength (~0.34 m / ~1.1 ft)
- Stable mic phase response
- Transients “ring” cleanly after filtering
- Phase maps directly to distance intuitively

At 70°F:
- Speed of sound ≈ **344 m/s**
- Wavelength at 1 kHz ≈ **0.344 m (~1.13 ft)**

So:
- **1 cycle = 1 ms = ~1.13 ft of propagation**

---

## 4. Pre‑Processing Workflow (All Devices)

### Step 1 — Extract audio
- Export audio from every video
- Same sample rate (e.g., 48 kHz)
- Mono preferred

### Step 2 — Rough alignment
- Line up the **bat crack** visually
- Accuracy: within ~50–100 ms
- Purpose: get close enough for fine phase work

### Step 3 — Band‑pass filtering
- Apply narrow bandpass (e.g., 1000 Hz ±50 Hz)
- Render to new files
- Result: ringing quasi‑sinusoid per device

---

## 5. Phase Measurement Between Devices

### 5.1 Reference selection
Choose one track:
- Highest SNR
- Cleanest crack onset
- Likely closest mic

All others are measured **relative** to this reference.

### 5.2 Measuring phase / cycles
For each device pair:

- Measure **Δt** via GCC‑PHAT or cycle counting
- Convert:
  - Cycles = Δt × f
  - Phase = cycles × 360° (mod 360)

Example:
- 3.7 cycles @ 1 kHz  
→ 3.7 ms  
→ ~4.2 ft path difference

---

## 6. Building the Phase Relation Matrix

Create a matrix:
- Rows/columns = devices
- Entries = Δt, cycles, or phase

This matrix encodes **physical constraints**:
- A real event must embed consistently
- Fake or edited media creates contradictions

Triangle check:
Δt(A,B) + Δt(B,C) ≈ Δt(A,C)

Violations indicate drift, splice, or spoofing.

---

## 7. Interpreting the Bat Crack

For the **bat crack**:

- All devices hear the same impulse
- Phase offsets reflect:
  - different distances to home plate
  - constant device latency

Because the crack is sharp and loud:
- Coherence is high
- Phase jitter is low
- This is the **anchor event**

---

## 8. Interpreting the Glove Thud

The glove thud occurs later.

Each device:
- Measures a new Δt relative to its own crack time
- Phase analysis can be repeated for the thud

Crack → Thud elapsed time per device:
- Dominated by **ball flight time**
- Not sound propagation

This is why:
- The crack wavefront travels hundreds of feet
- The ball itself travels only ~60 ft

---

## 9. Connecting Cycles to Real Physics

Example assumptions:
- Distance bat → glove ≈ 60 ft (18.3 m)
- Ball speed ≈ 90 mph (40.2 m/s)
- Δt ≈ 0.455 s

At 1 kHz:
- Cycles elapsed ≈ **455**
- Sound distance in that time ≈ **156 m (~514 ft)**

This calibration explains why:
- Large cycle counts are normal over human‑scale actions
- Small **differences** in cycle count (few cycles) encode geometry

---

## 10. Multi‑Device Consistency Across Both Events

A valid recording set shows:

- Crack phase matrix: consistent
- Thud phase matrix: consistent
- Crack→Thud interval: stable across devices
- Multi‑band agreement (e.g., 1000 vs 1200 Hz)

Failures appear as:
- drifting phase (clock error)
- band disagreement (spoofing)
- clustering (replay or edit)

---

## 11. Adversarial & Reality Checks

Apply the adversarial protocol:

- Multi‑band confirmation
- Global residual minimization
- Outlier rejection
- Cluster detection

A real play:
- Fits one global geometry
- Degrades gracefully with noise
- Cannot be made consistent cheaply if faked

---

## 12. What This Ultimately Gives You

From unsynchronized consumer recordings, you can:

- Verify that all videos capture **the same play**
- Reject spliced or replayed clips
- Estimate relative mic positions
- Tie abstract phase numbers to **human‑scale distances**
- Build an acoustic truth record without clocks

The bat crack is not just a sound —  
it is a **shared physical constraint** written into every device.

---

## 13. Mental Model Summary

- **Sound does not carry timestamps**
- **Phase carries geometry**
- **Cycles are just distance in disguise**
- **Truth emerges from consistency, not precision**

This is why the bat‑to‑glove play is an ideal demonstration case.
