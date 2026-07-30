Pico Case - Model Description
The Pico Case is a parametric, two-piece protective enclosure designed using box-primitive geometry. It consists of a Base and a Lid that snap/interlock together using custom rail and latch mechanics.
The script generates two watertight 3D files (pico_case_base.stl and pico_case_lid.stl) pre-aligned in their closed, assembled position for seamless import into 3D CAD software like Tinkercad.
1. Physical Specifications & Dimensions
Width (
W
W
): 150.0 mm
Depth (
D
D
): 130.0 mm
Base Height (
H
H
): 40.0 mm
Lid Wall Height (
L
H
LH
): 25.0 mm
Main Wall Thickness (
T
T
): 3.0 mm
Retaining Collar Thickness (
C
C
): 1.5 mm
Assembly State:
Total combined height in the closed state offset: 65.0 mm.
Lid is flipped 
180
∘
180 
∘
 
 and aligned directly on top of the base.
2. Key Design Features
A. Base Shell (pico_case_base.stl)
Ventilation Grille (Left Wall):
Features bottom (
Z
=
0
–
8
 mm
Z=0–8 mm
) and top (
Z
=
34
–
40
 mm
Z=34–40 mm
) framing.
Includes 10 vertical airflow slats spaced at 10 mm intervals (running along 
Y
=
15
 mm
Y=15 mm
 to 
115
 mm
115 mm
).
USB-C / Power Delivery (PD) Port Cutout (Back Wall):
Located at X: 
15
–
31
 mm
15–31 mm
, Z: 
15
–
19
 mm
15–19 mm
.
Built-in chamfered entry bevels on both sides of the cutout for smooth cable clearance.
Upper Retaining Collar:
A 
1.5
 mm
1.5 mm
 thin inner perimeter wall that extends from 
Z
=
35
 mm
Z=35 mm
 to 
44
 mm
44 mm
 to register and align the lid during closure.
Male Locking Rails (Left & Right Sides):
Stepped cam-and-groove side teeth (
Z
=
40.5
–
43.0
 mm
Z=40.5–43.0 mm
) designed to slide into mating tracks inside the lid.
Internal Snap Systems:
Snap System #1 (Corner Hook): A rigid corner post (
6
×
6
 mm
6×6 mm
) paired with a stepped retention hook pillar.
Snap System #2 (Flex Arm Latch): A flexible retention arm (
12
 mm
12 mm
 long) with a locking wedge, chamfered top, and structural gussets for strength.
B. Lid Shell (pico_case_lid.stl)
Cover Shell: A 
3
 mm
3 mm
 top plate with 
25
 mm
25 mm
 side walls.
Female Alignment Grooves:
Recessed tracks running along the internal side walls (
Z
=
21.5
–
24.5
 mm
Z=21.5–24.5 mm
).
Includes lead-in funnels and stepped deep grooves designed to securely clip over the base's male locking rails.
3. Advanced CAD & Mesh Features
Watertight Manifold Union (manifold3d):
Unlike simple shape aggregation, the script uses the manifold engine via trimesh to perform true Boolean operations (UNION). This melts all individual primitive boxes into one solid shell per part, eliminating coincident faces, duplicate internal planes, or rendering gaps in Tinkercad.
Tinkercad Gap Bridging ("Weld Boxes"):
Small 
0.2
 mm
0.2 mm
 clearance gaps present in raw physical printing tolerances (such as the gap between the retaining collar and outer wall) are filled with explicit "weld" primitives. This guarantees that Tinkercad treats the structure as a single fused body without "floating" disconnected shapes.
Pre-Aligned Assembly:
The lid coordinates are transformed mathematically (
180
∘
180 
∘
 
 rotation around 
X
X
, offset by 
Y
=
+
130
 mm
Y=+130 mm
, 
Z
=
+
65
 mm
Z=+65 mm
) so both parts import into Tinkercad already snapped together in the locked position.
