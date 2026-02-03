
# Acoustic Witness Cloud
## Multi-Device Event Verification via Audio Phase Geometry

---

## What This Repository Demonstrates

This project shows how multiple **unsynchronized consumer devices** can jointly verify the timing and spatial consistency of real-world acoustic events using **physics-based constraints**, even when:

- device clocks are inaccurate,
- GPS is unavailable or spoofed,
- audio contains noise, echoes, or reverberation.

**Core idea:**  
> Phase is locally ambiguous, but globally constrained.

---

## Physical Basis (Shared Across All Examples)

### Speed of Sound

\[
c \approx 343 \,\text{m/s} \approx 1125 \,\text{ft/s}
\]

### Midrange Audio Wavelength

For a representative frequency \( f \approx 1000 \,\text{Hz} \):

\[
\lambda = \frac{c}{f} \approx 0.343 \,\text{m} \approx 1.13 \,\text{ft}
\]

### Phase–Distance Relationship

A measured phase difference \( \phi \in [0,2\pi) \) corresponds to:

\[
d = \left(n + \frac{\phi}{2\pi}\right)\lambda, \quad n \in \mathbb{Z}
\]

This is the **phase wrapping problem**:  
each device measures phase accurately but cannot determine the integer cycle count \( n \).

---

## Why Multiple Devices Matter

For three devices \( A, B, C \), relative arrival times must satisfy:

\[
\Delta t_{AB} + \Delta t_{BC} \approx \Delta t_{AC}
\]

Translated to distance:

\[
d_{AB} + d_{BC} \approx d_{AC}
\]

Incorrect cycle counts violate these constraints.  
Only **one integer assignment across all devices** produces a physically consistent geometry.

---

## Example 1: Bat Crack → Glove Thud (Minimal Reverb)

**File:**  
`bat_crack_to_glove_multidevice_phase_guide.md`

### Scenario

- Event 1: Bat strikes ball (“crack”)
- Event 2: Ball reaches glove (“thud”)
- Multiple phones record both events
- No shared clock

### Measured Quantities

For device \( i \):

- Phase at crack: \( \phi_{i,c} \)
- Phase at thud: \( \phi_{i,g} \)

Time difference per device:

\[
\Delta t_i =
\left(n_i + \frac{\phi_{i,g} - \phi_{i,c}}{2\pi}\right)\frac{1}{f}
\]

### Constraint Across Devices

For any two devices \( i, j \):

\[
\Delta t_i - \Delta t_j =
\frac{d_{i,g} - d_{i,c} - (d_{j,g} - d_{j,c})}{c}
\]

All devices must agree on the **same ball flight time**.

### Result

- Wrong integer cycle assignments fail cross-device consistency
- One solution satisfies all constraints
- Absolute timing emerges without synchronized clocks

This is the **clean reference case**.

---

## Example 2: Sports Stadium (Moderate Reverb, Large Scale)

**File:**  
`Sports Stadium Audio Analysis.txt`

### Differences from Example 1

- Distances up to \( \sim 100 \,\text{m} \)
- Crowd noise and PA echoes
- Multiple candidate transients

### Early-Arrival Principle

Direct path arrives before reflections:

\[
t_{\text{direct}} < t_{\text{reflected}}
\]

Phase coherence is strongest in the **first arrival window**.

### Multi-Device Distance Constraints

For devices \( A, B, C \) observing the same event:

\[
|d_A - d_B| \le c \cdot |\Delta t_{AB}|
\]

Triangle inequality must hold:

\[
d_{AB} \le d_{AC} + d_{BC}
\]

### What Breaks

- Late echoes violate triangle closure
- Edited audio introduces inconsistent delays

### Result

Despite noise, **global geometry still closes**.  
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

Instead of a single impulse:

- Extract repeated impulsive micro-events (snare hits, claps)
- Solve for consistency across many events

For event \( k \):

\[
d_{i,k} =
\left(n_{i,k} + \frac{\phi_{i,k}}{2\pi}\right)\lambda
\]

Require geometry to be stable:

\[
d_{i,k} - d_{j,k} \approx d_{i,k+1} - d_{j,k+1}
\]

### Interpretation

The room geometry is fixed.  
Cycle assignments that imply “moving walls” are invalid.

### Result

Accuracy degrades, but fabricated or edited audio fails quickly.

---

## Sound Source Localization (When Device Locations Are Known)

If device positions \( (x_i, y_i, z_i) \) are known, the sound source position  
\( (x_s, y_s, z_s) \) and emission time \( t_0 \) can be solved.

For each device:

\[
d_i = c (t_i - t_0)
\]

and simultaneously:

\[
d_i =
\left(N_i + \frac{\phi_i}{2\pi}\right)\lambda
\]

This yields a system of equations:

\[
\sqrt{(x_i - x_s)^2 + (y_i - y_s)^2 + (z_i - z_s)^2}
= d_i
\]

With enough devices:

- integer cycle counts \( N_i \) are forced to a single solution,
- the sound **origin location** is determined,
- the **total distance traveled** by the wave is known,
- and the **emission time** \( t_0 \) emerges automatically.

This works because only one geometry satisfies **all cycles, all distances, and all devices simultaneously**.

---

## Summary Insight

A single recording cannot tell you the truth.  
A network of recordings must agree with physics.

**Truth is the solution that survives every constraint.**

