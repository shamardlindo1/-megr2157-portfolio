# A4 – Motor Mount

## Objective

Design a mount for a brushed 24 V DC gear motor with a 99.5:1 planetary gearbox, bolted
to rigid wall A. The mount is made of two features: Feature 1 carries the motor, Feature 2
bolts to the wall. Both are sized first for yield strength and then for a maximum
deflection of 0.30 mm at the free end, with a safety factor of 3 on a 300 N shaft load.
The motor's own weight is neglected. The finished design is modelled parametrically in
SOLIDWORKS with clearance holes for the shaft and the bolts.

## Design requirements

| Requirement | Value | Where it came from |
|---|---|---|
| Applied load, P | 300 N | Assignment, Figure 1 |
| Safety factor, n | 3 | Assignment |
| Maximum deflection | 0.30 mm | Assignment |
| Motor shaft | Ø6 mm, 18 mm long | Appendix A |
| Motor mounting holes | 4 × M3 on a Ø22 mm bolt circle | Appendix A |
| Motor body | Ø28 mm | Appendix A |
| Bolt clearance holes | Ø3.4 mm | Assignment |
| Material | ABS, PETG or PLA | Assignment |

## Material selection

I chose PETG. All three allowed materials are printable thermoplastics, but PETG is
tougher than PLA and less prone to warping than ABS, which matters for a bracket that
carries a real load and has thin sections around the bolt holes.

Published PETG properties vary with print settings, so I used conservative lower-bound
values rather than the best numbers I could find:

![PETG properties used](img/hand-f1-01.jpg)

With the required safety factor of 3, the allowable stress is

![Allowable stress](img/hand-f1-02.jpg)

These are the values I entered into the custom PETG material in SOLIDWORKS, so the model
and the hand calculations use the same numbers.

![PETG material properties](img/material-1.jpg)

![PETG material properties, continued](img/material-2.jpg)

## Feature 1 – motor plate

### Known and unknown variables

![Known variables](img/hand-f1-03.jpg)

![Unknown variables](img/hand-f1-04.jpg)

Why 45 mm wide: the motor body is Ø28 mm and the bolt circle is Ø22 mm, so the plate has
to be at least ~36 mm across to leave material outside the bolt holes. 45 mm gives about
8 mm of material past the motor body on each side.

Why 40 mm long: the motor has to sit clear of the wall plate. 40 mm puts the motor centre
far enough out that the Ø28 mm body does not foul the vertical plate, without making the
cantilever any longer than it needs to be — and every extra millimetre of length costs
deflection as the cube.

### Assumptions

Feature 1 is treated as a rectangular cantilever beam, fixed where it meets Feature 2,
with zero deflection and zero slope at that end, exactly as the assignment directs. The
300 N motor load is modelled as a point load at the motor centre. The motor's weight is
neglected. The safety factor of 3 is taken to cover the material removed by the shaft
opening and the bolt holes, so the beam is analysed as a solid rectangular section.

### Free-body diagram

![Feature 1 free-body diagram](img/fbd-feature1.jpg)

Summing forces vertically gives the reaction at the fixed end equal to the applied load.
Taking moments about the fixed end gives the maximum bending moment, which occurs there:

![Reaction, maximum moment and the bending stress relation](img/hand-f1-05.jpg)

### Stress analysis, solved symbolically

Setting the maximum bending stress equal to the allowable stress and solving for the
thickness:

![Thickness required by stress](img/hand-f1-06.jpg)

### Deflection analysis, solved symbolically

For a cantilever with a point load at the free end:

![Cantilever deflection](img/hand-f1-07.jpg)

Solving for the required second moment of area:

![Required second moment of area](img/hand-f1-11.jpg)

and for a rectangular section:

![Thickness required by deflection](img/hand-f1-12.jpg)

### Numerical solution

![Numerical solution for the thickness](img/hand-f1-08.jpg)

Deflection governs, not stress. Rounding up to a practical dimension:

![Selected thickness](img/hand-f1-09.jpg)

### Checks on the selected section

![Checks on the selected section](img/hand-f1-10.jpg)

## Feature 2 – wall plate

### Known and unknown variables

![Known variables](img/hand-f2-01.jpg)

![Unknown variables](img/hand-f2-02.jpg)

### Assumptions

Feature 2 is approximated as a rectangular cantilever fixed at the wall. The wall itself
is rigid and the bolts hold the plate against it without slipping, so the plate can be
treated as built in. The connection between the two features transfers both the 300 N
force and the bending moment that force creates about the corner — that transferred
moment is the load case that actually sizes this plate.

### Free-body diagram

![Feature 2 free-body diagram](img/fbd-feature2.jpg)

### Stress analysis, solved symbolically

Both the force and the transferred moment bend the wall plate, and the worst section is
at the wall:

![Maximum moment, bending stress and the thickness required by stress](img/hand-f2-05.jpg)

### Shear analysis

A thin plate can fail in transverse shear before it fails in bending, so this is checked
as well. For a rectangular section:

![Transverse shear stress](img/hand-f2-06.jpg)

The allowable shear stress is estimated from the von Mises criterion:

![Allowable shear stress](img/hand-f2-03.jpg)

### Deflection analysis, solved symbolically

The two loads are superposed — a point force at the free end plus an applied end moment:

![Deflection by superposition](img/hand-f2-04.jpg)

Solving for the required second moment of area:

![Required second moment of area and thickness](img/hand-f2-07.jpg)

### Numerical solution

![Numerical solution for the wall plate thickness](img/hand-f2-08.jpg)

Deflection governs again. Rounding up:

![Selected thickness](img/hand-f2-09.jpg)

### Checks on the selected section

![Checks on the selected section](img/hand-f2-10.jpg)

Note how small the shear stress is — 0.455 MPa against 8.66 MPa allowable. Shear was never
going to size this plate, but checking it is what tells you that bending is the real
problem rather than assuming it.

## Sketch

Hand sketch of the mount in isometric with the dimensions that drive the model. The two
plate thicknesses, 15 mm and 22 mm, come straight out of the deflection calculations
above; the 80 mm length, 45 mm width and 60 mm height follow from those two plus the
40 mm motor stand-off. Hole sizes and spacings are from Appendix A.

![Isometric sketch of the motor mount](img/sketch-isometric.jpg)

## CAD Model (Parametric)

### Global variables and equations

The whole model is driven from the design inputs rather than from typed dimensions.

Driving variables:

    "P" = 300            applied load, N
    "n" = 3              safety factor
    "E" = 2000           PETG modulus, MPa
    "Sy" = 45            PETG yield, MPa
    "delta_max" = 0.3    deflection limit, mm
    "b" = 45             bracket width, mm
    "L1" = 40            motor centre from the corner, mm
    "Lp" = 58            motor plate length past the corner, mm
    "H" = 45             wall plate height, mm
    "d_bolt" = 3.4       bolt clearance, mm
    "d_shaft" = 8        shaft clearance, mm

Driven equations:

    "sigma_allow" = "Sy" / "n"
    "I_req1" = "P" * "L1"^3 / ( 3 * "E" * "delta_max" )
    "h1"     = int( ( 12 * "I_req1" / "b" )^(1/3) ) + 1
    "M_tr"   = "P" * "L1"
    "I_req2" = ( "P" * "H"^3 / 3 + "M_tr" * "H"^2 / 2 ) / ( "E" * "delta_max" )
    "t2"     = int( ( 12 * "I_req2" / "b" )^(1/3) ) + 1
    "L_total" = "t2" + "Lp"
    "H_total" = "H" + "h1"

![Global variables in the Equations dialog](img/equations-1.jpg)

![Global variables, continued](img/equations-2.jpg)

Geometry driven by those variables:

    "D1@Sketch1" = "t2"        ->  22 mm
    "D2@Sketch1" = "H_total"   ->  60 mm
    "D1@Sketch2" = "L_total"   ->  80 mm
    "D2@Sketch2" = "h1"        ->  15 mm

![The dimensions driven by the variables](img/equations-driven.jpg)

The two plate thicknesses are never typed in. `h1` and `t2` are solved from the deflection
requirement and then rounded up to the next whole millimetre by `int(...) + 1`, which is
the same rounding I did by hand. Change the load to 400 N, or the span to 50 mm, and the
bracket re-sizes itself.

One thing to watch: SOLIDWORKS equations do not carry units, they just do arithmetic on
numbers. The document has to be in MMGS so a bare 22 is read as 22 mm. I set that before
building anything.

![Motor mount, isometric](img/cad-model.jpg)

### Features on the model

| Feature | Size | Why |
|---|---|---|
| Motor plate | 80 × 45 × 15 mm | Feature 1 analysis, 58 mm of reach past the corner |
| Wall plate | 22 × 45 × 60 mm | Feature 2 analysis |
| Shaft clearance | Ø8 mm | Ø6 mm shaft plus clearance |
| Motor bolt holes | 4 × Ø3.4 mm on a Ø22 mm bolt circle | M3 clearance, matches Appendix A |
| Wall bolt holes | 4 × Ø3.4 mm, 30 mm apart | M3 clearance into wall A |
| Corner rib | 20 × 20 × 10 mm triangle | Deflection-minimising feature |

### Feature to minimise deflection

The triangular rib at the inside corner is the deflection-minimising feature. Both plates
pass the 0.30 mm limit on their own, but the beam model treats the corner as perfectly
built in, and a real L-bracket does not behave that way — the corner opens up under load
and adds deflection the hand calculation never sees. The rib carries load straight across
that corner in compression instead of relying on the bend, which is the cheapest stiffness
available. It cost about 2,000 mm³ of material.

## Mistakes and changes

The first extrusion silently produced nothing. I had set the end condition to mid-plane,
which the model rebuilt without complaint but with zero volume, so the feature tree showed
sketches and no solid. Switching to a two-directional blind extrusion of 22.5 mm each way
gave the same symmetric result and actually built. The clue was the mass properties
reporting zero, not anything visible on screen.

I also pasted the PETG material into the existing MEGR2156 library and then renamed the
category to "Plastics", which moved the two steels from A2 into a category called Plastics
as well. I put that back.

## Results

| Quantity | Feature 1 | Feature 2 | Limit |
|---|---|---|---|
| Span | 40 mm | 45 mm | — |
| Section | 45 × 15 mm | 45 × 22 mm | — |
| Required I | 10,666.7 mm⁴ | 35,437.5 mm⁴ | — |
| Actual I | 12,656.3 mm⁴ | 39,930 mm⁴ | — |
| Max bending stress | 7.11 MPa | 7.02 MPa | 15 MPa |
| Max shear stress | — | 0.455 MPa | 8.66 MPa |
| Deflection | 0.2528 mm | 0.2662 mm | 0.30 mm |
| Factor of safety | 6.3 | 6.4 | 3 |

Both features are governed by deflection, not strength. The stresses land around 7 MPa
against 15 MPa allowable, so the mount is roughly twice as strong as it needs to be while
only just meeting the stiffness requirement. That is the same pattern as A3 — with a
material this compliant, the 0.30 mm limit runs out of room long before the material
yields, and sizing on stress alone would have produced a bracket far too floppy to use.

## Lessons learned

The load that sizes a part is not always the load you were handed. Feature 1 takes a
300 N force and that is the whole story. Feature 2 takes the same 300 N, but it also
takes the 12,000 N·mm moment that force creates about the corner, and that moment is
almost half of the 25,500 N·mm the wall plate actually sees. If I had carried only the
force across the joint I would have sized the wall plate for roughly half the load and
called it done. Drawing the second free-body diagram properly, with the transferred
moment on it, is what caught that.

Deflection governed both features again, the same as A3, but this time I expected it and
sized on stiffness first instead of working out the strength answer and then being
surprised. With PETG at 2,000 MPa the 0.30 mm limit runs out long before 15 MPa does, and
both plates ended up around 7 MPa — roughly twice as strong as they need to be. That is
not waste so much as what a stiffness requirement costs you in a compliant material.

The last one is just to check my own work instead of assuming it is right. I made
mistakes all the way through this assignment — a moment written in N·m when it should
have been N·mm, an arithmetic slip in one of the required-I numbers, and an extrusion
that silently built nothing because the end condition was wrong. None of those announced
themselves. The units error looked fine until I compared it against the stress that came
out of it, and the empty extrusion only showed up when I pulled the mass properties and
saw zero volume. Going back over every step and fixing what I found is what turned a
draft full of small errors into something I would hand in.

## Time log

This assignment took me three days from start to finish.

## Appendix – motor mount research

Commercial L-bracket motor mounts I looked at before settling on the geometry:

- [Pololu steel L-bracket for NEMA 23 stepper motors](https://www.pololu.com/product/2258)
- [Pololu stamped aluminium L-bracket for NEMA 17 stepper motors](https://www.pololu.com/product/2266)
- [Phidgets NEMA 17 motor mounting bracket](https://www.phidgets.com/?prodid=357)
- [ZYLtech NEMA 17 stepper motor L-mount bracket](https://www.zyltech.com/nema-17-stepper-motor-bracket-l-mount/)
- [StepperOnline motor bracket range](https://www.omc-stepperonline.com/motor-bracket)
- [NEMA 17 L-bracket model on GrabCAD](https://grabcad.com/library/nema-17-l-bracket-1)

Two things from that survey fed into my design. Almost every commercial bracket is a
simple L with the motor face plate and the mounting plate at right angles, which is what
Appendix B shows and what the beam equations suit. And the sheet-metal ones are far
thinner than my 15 and 22 mm plates, because steel and aluminium are one to two orders of
magnitude stiffer than PETG — the thickness here is entirely a consequence of the material
the assignment restricted us to.

## CAD file download

Below I have provided the file for my motor mount design:

[Click here to download A4_Motor_Mount.SLDPRT](A4_Motor_Mount.SLDPRT) — the part with the
global variables and equations still live, so both plate thicknesses re-solve if you change
the load, the span or the material.
