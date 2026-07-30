
---

# Pico Case - Model Description

The **Pico Case** is a parametric, two-piece protective enclosure designed using box-primitive geometry. It consists of a **Base** and a **Lid** that snap/interlock together using custom rail and latch mechanics. 

The script generates two watertight 3D files (`pico_case_base.stl` and `pico_case_lid.stl`) pre-aligned in their closed, assembled position for seamless import into 3D CAD software like Tinkercad.

---

## 1. Physical Specifications & Dimensions

* **Width ($W$):** 150.0 mm
* **Depth ($D$):** 130.0 mm
* **Base Height ($H$):** 40.0 mm
* **Lid Wall Height ($LH$):** 25.0 mm
* **Main Wall Thickness ($T$):** 3.0 mm
* **Retaining Collar Thickness ($C$):** 1.5 mm
* **Assembly State:** 
  * Total combined height in the closed state offset: **65.0 mm**.
  * Lid is flipped $180^\circ$ and aligned directly on top of the base.

---

## 2. Key Design Features

### A. Base Shell (`pico_case_base.stl`)
1. **Ventilation Grille (Left Wall):**
   * Features bottom ($Z=0\text{--}8\text{ mm}$) and top ($Z=34\text{--}40\text{ mm}$) framing.
   * Includes **10 vertical airflow slats** spaced at 10 mm intervals (running along $Y=15\text{ mm}$ to $115\text{ mm}$).
2. **USB-C / Power Delivery (PD) Port Cutout (Back Wall):**
   * Located at X: $15\text{--}31\text{ mm}$, Z: $15\text{--}19\text{ mm}$.
   * Built-in **chamfered entry bevels** on both sides of the cutout for smooth cable clearance.
3. **Upper Retaining Collar:**
   * A $1.5\text{ mm}$ thin inner perimeter wall that extends from $Z=35\text{ mm}$ to $44\text{ mm}$ to register and align the lid during closure.
4. **Male Locking Rails (Left & Right Sides):**
   * Stepped **cam-and-groove side teeth** ($Z=40.5\text{--}43.0\text{ mm}$) designed to slide into mating tracks inside the lid.
5. **Internal Snap Systems:**
   * **Snap System #1 (Corner Hook):** A rigid corner post ($6\times 6\text{ mm}$) paired with a stepped retention hook pillar.
   * **Snap System #2 (Flex Arm Latch):** A flexible retention arm ($12\text{ mm}$ long) with a locking wedge, chamfered top, and structural gussets for strength.

### B. Lid Shell (`pico_case_lid.stl`)
1. **Cover Shell:** A $3\text{ mm}$ top plate with $25\text{ mm}$ side walls.
2. **Female Alignment Grooves:**
   * Recessed tracks running along the internal side walls ($Z=21.5\text{--}24.5\text{ mm}$).
   * Includes lead-in funnels and stepped deep grooves designed to securely clip over the base's male locking rails.

---

## 3. Advanced CAD & Mesh Features

* **Watertight Manifold Union (`manifold3d`):** 
  Unlike simple shape aggregation, the script uses the `manifold` engine via `trimesh` to perform true Boolean operations (`UNION`). This melts all individual primitive boxes into **one solid shell per part**, eliminating coincident faces, duplicate internal planes, or rendering gaps in Tinkercad.
* **Tinkercad Gap Bridging ("Weld Boxes"):**
  Small $0.2\text{ mm}$ clearance gaps present in raw physical printing tolerances (such as the gap between the retaining collar and outer wall) are filled with explicit "weld" primitives. This guarantees that Tinkercad treats the structure as a single fused body without "floating" disconnected shapes.
* **Pre-Aligned Assembly:**
  The lid coordinates are transformed mathematically ($180^\circ$ rotation around $X$, offset by $Y=+130\text{ mm}$, $Z=+65\text{ mm}$) so both parts import into Tinkercad already snapped together in the locked position.

---
