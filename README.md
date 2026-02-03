
# Acoustic Witness Cloud
## Multi-Device Event Verification via Audio Phase Geometry

![image](https://github.com/user-attachments/assets/25e2ec32-d726-4c35-882b-7b68a316318a)

![image](https://github.com/user-attachments/assets/6e7c7b3f-81eb-4b90-98c2-631e5c45f902)

---

## What This Repository Demonstrates

This project shows how multiple **unsynchronized consumer devices** (phones, cameras, recorders) can jointly verify the timing and spatial consistency of real-world acoustic events using **physics-based constraints**, even when:

- Device clocks are inaccurate or drifting  
- GPS is unavailable, jammed, or spoofed  
- Audio contains noise, echoes, or reverberation  

**Core idea:**

> **Phase is locally ambiguous, but globally constrained.**

A single recording is never enough.  
Multiple recordings must agree with physics.

---

## Physical Basis (Shared Across All Examples)

### Speed of Sound

At room temperature:

```
c ≈ 343 meters/second ≈ 1125 feet/second
```

### Midrange Audio Wavelength

For a representative audio frequency of approximately 1 kHz:

```
f ≈ 1000 Hz
λ = c / f ≈ 0.343 meters ≈ 1.13 feet
```

This wavelength is short enough to give fine spatial resolution,  
yet long enough to remain stable across consumer microphones.

---

### Phase–Distance Relationship

Each device measures **phase**, not distance.

A measured phase value φ (between 0 and 2π) corresponds to:

```
distance = (integer_cycles + fractional_phase) × wavelength

d = ( n + φ / 2π ) × λ
```
where:

- `φ` is the measured phase
- `n` is an unknown integer cycle count
- `λ` is the wavelength

This is the **phase wrapping problem**:

> Phase can be measured precisely,  
> but the total number of cycles traveled is initially unknown.

---

## Why Multiple Devices Matter

With three devices A, B, and C, relative arrival times must be consistent.

In time form:

```
Δt_AB + Δt_BC ≈ Δt_AC
```

In distance form:

```
d_AB + d_BC ≈ d_AC
```

Incorrect integer cycle choices violate these relationships.

**Only one assignment of integer cycles across all devices produces a valid physical geometry.**

This is how ambiguity collapses into truth.

---

## Example 1: Bat Crack → Glove Thud (Minimal Reverb)

**File:**  
`bat_crack_to_glove_multidevice_phase_guide.md`

### Scenario

- Event 1: Bat strikes ball (“crack”)
- Event 2: Ball reaches glove (“thud”)
- Multiple phones record both events
- Devices are not time-synchronized

### What Each Device Measures

For device *i*:

- Phase at crack: φᵢ,c
- Phase at thud: φᵢ,g

The time difference between events for that device is:

```
Δt_i = ( n_i + (φᵢ,g − φᵢ,c) / 2π ) × (1 / f)
```

Each device has its own unknown integer cycle count `n_i`.

---

### Cross-Device Constraint

For any two devices *i* and *j*:

```
Δt_i − Δt_j =
( (dᵢ,glove − dᵢ,crack) − (dⱼ,glove − dⱼ,crack) ) / c
```

All devices must agree on the **same ball flight time**.

### Result

- Wrong cycle counts fail consistency checks
- One configuration satisfies all constraints
- Absolute timing emerges without shared clocks

This is the **clean reference case**.

---

## Example 2: Sports Stadium (Moderate Reverb, Large Scale)

**File:**  
`Sports Stadium Audio Analysis.txt`

### Differences from Example 1

- Distances up to ~100 meters
- Crowd noise and PA system echoes
- Multiple candidate acoustic transients

### Early-Arrival Principle

The direct sound path always arrives before reflections:

```
t_direct < t_reflected
```

Phase coherence is strongest during this first arrival window.

---

### Multi-Device Distance Constraints

For devices A, B, and C observing the same event:

```
| d_A − d_B | ≤ c × | Δt_AB |
```

Triangle inequality must hold:

```
d_AB ≤ d_AC + d_BC
```

### What Breaks

- Late echoes violate triangle closure
- Edited or replayed audio introduces inconsistent delays

### Result

Even in noisy environments, **global geometry still closes**.  
False positives fail residual checks.

---

## Example 3: Concert Venue (Heavy Reverb, Dense Noise)

**File:**  
`Concert Audio Analysis.txt`

### Why This Is Hard

- Continuous sound field
- Strong reverberation
- Overlapping frequency content

### Strategy Shift

Instead of relying on a single impulse:

- Extract repeated impulsive micro-events (snare hits, claps)
- Enforce consistency across many events

For event *k* and device *i*:

```
dᵢ,k = ( nᵢ,k + φᵢ,k / 2π ) × λ
```

Require geometry stability:

```
dᵢ,k − dⱼ,k ≈ dᵢ,k+1 − dⱼ,k+1
```

### Interpretation

The room does not move.  
Cycle assignments implying “moving walls” are invalid.

### Result

Precision degrades, but fabricated or edited audio fails quickly.

---

## Sound Source Localization (Known Device Positions)

If device positions are known:

```
Device i at (xᵢ, yᵢ, zᵢ)
Sound source at (x_s, y_s, z_s)
```

Distance traveled by the sound wave:

```
dᵢ = c × ( tᵢ − t₀ )
```

Also from phase measurement:

```
dᵢ = ( Nᵢ + φᵢ / 2π ) × λ
```

Geometric constraint:

```
sqrt( (xᵢ − x_s)² + (yᵢ − y_s)² + (zᵢ − z_s)² ) = dᵢ
```

With enough devices:

- Integer cycle counts become fixed
- Sound origin location is solved
- Total travel distance is known
- Emission time emerges automatically

Only **one solution** satisfies all devices, all cycles, and all distances.

---

## Summary Insight

A single recording cannot tell you the truth.

A **network of recordings constrained by physics** can.

> **Truth is the solution that survives every constraint.**
