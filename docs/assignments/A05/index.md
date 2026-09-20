# A5 – Bracket Design

## Objective

Design a bracket that holds a horizontal force applied symmetrically by a polyester strap,
using the concept design in Appendix B. The bracket is split into five features, A through E,
and each one is sized twice: once so it will not yield, and once so it will not deflect more
than 0.005 in. The larger of the two dimensions is the one that gets used.

The reaction from one feature becomes the applied load of the next, so the five analyses
have to be done in order rather than independently.

## Design requirements

| Requirement | Value | Where it came from |
|---|---|---|
| Applied load, F | 700 lbf | Chosen inside the 500 < F < 800 lbf range |
| Load per side, P | 350 lbf | Bracket is symmetric, so the load splits evenly |
| Safety factor, SF | 4 | Assignment |
| Maximum deflection | 0.005 in per feature | Assignment |
| Material | ASTM A36 steel | One of the three allowed metals |
| Yield strength, Sy | 36,000 psi | Machinery's Handbook |
| Modulus, E | 29 × 10⁶ psi | Machinery's Handbook |
| Allowable stress | 9,000 psi | Sy / SF |
| T-beam fit dimensions | a = 0.498, b = 0.9992, c = 1.499 in | Figure 1 |
| Direct shear | Neglected | Assignment |

## Material selection

I picked ASTM A36 structural steel. The strap load is a real working load on a bracket that
clamps onto a rigid T beam, and A36 is the cheapest, most available structural steel for
something bolted or welded into a frame. Aluminium would have meant thicker sections for the
same deflection limit, and titanium is not worth the cost for a strap bracket.

![Load per side and allowable stress](img/a5-hand-a-01.jpg)

## Analyze

The load path is what drives the whole assignment. The 700 lbf splits in half by symmetry, so
each side carries 350 lbf. Feature A carries that 350 lbf as a cantilever and hands its
reaction to Feature B. Feature B passes the same 350 lbf into Feature C, which is simply
supported, so each of its end reactions is only 175 lbf. That 175 lbf is what Feature D
carries, and D passes it to Feature E.

Appendix D gives the models for the first three features: A is a cantilever beam, B is an
axially loaded bar, and C is a simply supported beam with a concentrated load at the centre.
D and E follow from the same reasoning — D is another axial member and E is a cantilever.

## Feature A – circular cantilever

Feature A is the cylinder the strap wraps around. It is fixed where it meets Feature B and
carries the 350 lbf half-load at its free end. I chose L_A = 1.50 in.

### Known and unknown variables

Known: P = 350 lbf, L_A = 1.50 in, Sy = 36,000 psi, SF = 4, σ_allow = 9,000 psi, E = 29 × 10⁶ psi,
δ_max = 0.005 in. Unknown: the minimum diameter d_A.

### Assumptions

Feature A behaves as a cantilever beam fixed where it meets Feature B, with the 350 lbf
half-load acting at the free end. The cross section is circular and uniform along the length.
Loading is static and the material stays elastic. Bending stress controls the design and
direct shear failure is neglected, as the assignment allows. For the stiffness analysis,
small-deflection beam theory applies, shear deflection is negligible, and the maximum
deflection occurs at the free end.

### Free-body diagram

![Feature A free-body diagram](img/a5-hand-a-02.jpg)

### Stress analysis

![Equilibrium and the bending stress relation](img/a5-hand-a-03.jpg)

![Numerical solution for the diameter](img/a5-hand-a-04.jpg)

### Stiffness analysis

![Feature A free-body diagram, stiffness](img/a5-hand-a-05.jpg)

![Cantilever deflection solved for the required diameter](img/a5-hand-a-06.jpg)

![Numerical solution](img/a5-hand-a-07.jpg)

### Decision

Stress needs 0.841 in and stiffness needs 0.485 in, so stress governs. Rounding up to a
standard size gives d_A = 0.875 in.

![Checks on the selected diameter](img/a5-hand-a-08.jpg)

## Feature B – axially loaded bar

Appendix D says to treat Feature B as an axially loaded bar. The 350 lbf reaction from
Feature A goes straight into it. I chose L_B = 1.25 in and a width of 1.00 in, leaving the
thickness as the unknown.

### Known and unknown variables

![Known values](img/a5-hand-b-01.jpg)

### Assumptions

Feature B is an axially loaded rectangular bar with the load centred, so there is no bending.
The cross section is uniform and the stress is uniform across it. Direct shear failure is
neglected. For the stiffness analysis the material stays elastic and shear deformation is
negligible.

### Free-body diagram

![Feature B free-body diagram](img/a5-hand-b-02.jpg)

### Stress analysis

![Axial stress solved for the thickness](img/a5-hand-b-03.jpg)

![Numerical solution](img/a5-hand-b-04.jpg)

### Stiffness analysis

![Known values for the stiffness analysis](img/a5-hand-b-05.jpg)

![Axial deflection solved for the area](img/a5-hand-b-06.jpg)

![Numerical solution](img/a5-hand-b-07.jpg)

### Decision

Stress needs 0.0389 in, stiffness needs 0.0030 in, so stress governs. Both are far too thin
to machine or handle, so I used a practical t_B = 0.375 in.

![Checks on the selected thickness](img/a5-hand-b-08.jpg)

## Feature C – simply supported beam

Appendix D says to treat Feature C as a simply supported beam with a concentrated load at the
centre. This is the lower arm of the jaw. The 350 lbf from Feature B lands at mid-span and the
two ends react with 175 lbf each. I chose L_C = 2.50 in and b_C = 1.00 in.

### Free-body diagram

![Feature C free-body diagram](img/a5-hand-c-01.jpg)

### Known and unknown variables

![Known values](img/a5-hand-c-02.jpg)

### Assumptions

Feature C is simply supported at both ends with the concentrated load at mid-span. The cross
section is rectangular and uniform. Bending controls and direct shear failure is neglected.
The supports are frictionless and carry no moment. For the stiffness analysis the maximum
deflection occurs at mid-span and shear deflection is negligible.

### Stress analysis

![Equilibrium, maximum moment and the bending stress relation](img/a5-hand-c-03.jpg)

![Numerical solution for the height](img/a5-hand-c-04.jpg)

### Stiffness analysis

![Deflection solved for the required second moment of area](img/a5-hand-c-05.jpg)

![Numerical solution](img/a5-hand-c-06.jpg)

### Decision

Stress needs 0.382 in and stiffness needs 0.211 in, so stress governs. Rounding up gives
h_C = 0.500 in.

![Checks on the selected section](img/a5-hand-c-07.jpg)

## Feature D – axially loaded bar

Feature D is the vertical back of the jaw. It carries the reaction from one end of Feature C
up into Feature E, so it is modelled the same way as Feature B. Its height is set by the
1.499 in T-beam opening, so L_D = 1.50 in, with a 1.00 in width.

### Known and unknown variables

Known: P_D = 175 lbf, L_D = 1.50 in, w_D = 1.00 in, σ_allow = 9,000 psi, E = 29 × 10⁶ psi,
δ_max = 0.005 in. Unknown: the minimum thickness t_D.

### Assumptions

Feature D is modelled as an axially loaded rectangular member with the load centred, so
bending is neglected in this simplified model. The cross section is uniform and direct shear
failure is neglected. The load carried is a single end reaction from Feature C, 175 lbf, not
the full 350 lbf.

### Free-body diagram

![Feature D free-body diagram](img/a5-hand-d-01.jpg)

### Stress analysis

![Axial stress solved for the thickness](img/a5-hand-d-02.jpg)

![Numerical solution](img/a5-hand-d-03.jpg)

### Stiffness analysis

![Axial deflection solved for the area](img/a5-hand-d-04.jpg)

![Numerical solution](img/a5-hand-d-05.jpg)

### Decision

Stress needs 0.0194 in and stiffness needs 0.0018 in, so stress governs. Both are
impractically thin, so I used the same practical section as Feature B, t_D = 0.375 in.

![Checks on the selected thickness](img/a5-hand-d-06.jpg)

## Feature E – rectangular cantilever

Feature E is the upper arm of the jaw, the last feature before the bracket meets the T beam.
It is a cantilever fixed at Feature D with the 175 lbf at its free end. Its length is set by
the 0.9992 in reach over the flange, so L_E = 1.00 in, with b_E = 1.00 in.

### Known and unknown variables

![Known values](img/a5-hand-e-01.jpg)

### Assumptions

Feature E behaves as a cantilever fixed at Feature D with the load at the free end. The cross
section is rectangular and uniform and the material stays elastic. Direct shear failure is
neglected. For the stiffness analysis, small-deflection beam theory applies, shear deflection
is negligible, and the maximum deflection occurs at the free end.

### Free-body diagram

![Feature E free-body diagram](img/a5-hand-e-02.jpg)

### Stress analysis

![Equilibrium and the bending stress relation](img/a5-hand-e-03.jpg)

![Numerical solution for the height](img/a5-hand-e-04.jpg)

### Stiffness analysis

![Known values for the stiffness analysis](img/a5-hand-e-05.jpg)

![Cantilever deflection solved for the required height](img/a5-hand-e-06.jpg)

![Numerical solution](img/a5-hand-e-07.jpg)

### Decision

Stress needs 0.342 in and stiffness needs 0.169 in, so stress governs. Rounding up gives
h_E = 0.375 in.

![Checks on the selected section](img/a5-hand-e-08.jpg)

## Overall stress and stiffness comparison

| Feature | Model | Stress minimum | Stiffness minimum | Selected | Governing |
|---|---|---|---|---|---|
| A | Circular cantilever | d = 0.841 in | d = 0.485 in | Ø0.875 in | Stress |
| B | Axial bar | t = 0.0389 in | t = 0.0030 in | 0.375 in | Stress |
| C | Simply supported | h = 0.382 in | h = 0.211 in | 0.500 in | Stress |
| D | Axial bar | t = 0.0194 in | t = 0.0018 in | 0.375 in | Stress |
| E | Rectangular cantilever | h = 0.342 in | h = 0.169 in | 0.375 in | Stress |

Stress governs every feature. On the two axial members it is not even close — Feature B needs
0.0389 in for stress against 0.0030 in for stiffness, about thirteen times more.

## CAD Model

I built the model feature by feature so that each solid in the tree lines up with one of the
five analyses, rather than sketching the whole bracket at once.

### CAD Step 1 – Feature A

The cylinder, Ø0.875 in by 1.50 in long, sketched on the Right plane and extruded.

![Feature A in SOLIDWORKS](img/a5-cad-01-featureA.png)

### CAD Step 2 – Feature B

The vertical plate the cylinder is fixed to, 1.00 × 1.25 × 0.375 in.

![Feature B in SOLIDWORKS](img/a5-cad-02-featureB.png)

### CAD Step 3 – Feature C

The lower arm of the jaw, 2.50 in span by 0.500 in deep, 1.00 in wide.

![Feature C in SOLIDWORKS](img/a5-cad-03-featureC.png)

### CAD Step 4 – Feature D

The vertical back, 0.375 in thick and 2.374 in tall, which sets the 1.499 in jaw opening.

![Feature D in SOLIDWORKS](img/a5-cad-04-featureD.png)

### CAD Step 5 – Feature E

The upper arm, 1.00 in long by 0.375 in deep, closing the jaw over the T-beam flange.

![Feature E in SOLIDWORKS](img/a5-cad-05-featureE.png)

### Final dimensions

| Feature | Final size |
|---|---|
| A – cylinder | Ø0.875 in × 1.50 in long |
| B – vertical plate | 1.00 wide × 1.25 tall × 0.375 thick |
| C – lower arm | 2.50 long × 0.500 tall × 1.00 wide |
| D – vertical back | 0.375 thick × 2.374 tall × 1.00 wide |
| E – upper arm | 1.00 long × 0.375 tall × 1.00 wide |
| Jaw opening | 1.499 in, matching dimension c of the T beam |

The model reports a volume of 3.5579 in³. Adding the five features by hand and subtracting the
two overlaps where D meets C and E gives 3.5578 in³, so the geometry is what I intended.

## Multiview Drawings

## Decide

### Final stress and stiffness check

| Feature | Max stress | Allowable | Deflection | Allowed | Result |
|---|---|---|---|---|---|
| A | 7,982 psi | 9,000 psi | 0.00047 in | 0.005 in | PASS |
| B | 933 psi | 9,000 psi | 0.00004 in | 0.005 in | PASS |
| C | 5,250 psi | 9,000 psi | 0.00038 in | 0.005 in | PASS |
| D | 467 psi | 9,000 psi | 0.00002 in | 0.005 in | PASS |
| E | 7,466 psi | 9,000 psi | 0.00046 in | 0.005 in | PASS |

Every feature passes both requirements. Feature E is the closest to its limit at 7,466 psi
against 9,000 psi allowable, which makes it the critical feature in the design.

## Mistakes and changes

The two axial members came out absurdly thin. Feature B only needed 0.0389 in of thickness to
survive 350 lbf and Feature D only needed 0.0194 in. Those numbers are correct, but a bracket
built from 0.02 in steel is not something you could handle, drill or weld. I kept the
calculated minimums as the analytical result and then set both to 0.375 in, which is what
actually gets modelled. The calculation tells you the floor, not the answer.

I also mislabelled a decimal in the Feature C deflection check, writing 0.0038 in where the
arithmetic gives 0.00038 in. It passes either way, but it is the kind of slip that would
matter if the number had been close to the limit.

## Lessons learned

### Governing failure mode

Stress governed all five features, and by a wide margin on the axial members — Feature B
needed 0.0389 in for stress against 0.0030 in for stiffness, roughly thirteen times more.
Feature E was the closest to its limit at 7,466 psi against the 9,000 psi allowable.

This is the reverse of what happened in A3 and A4. With steel at 29 × 10⁶ psi, the 0.005 in
deflection limit is easy to satisfy, so the 9,000 psi allowable is what actually sizes the
bracket. The governing requirement is a property of the material as much as the geometry.

### Error propagation

Feature C is where the load path halves. Its two end reactions are 175 lbf each, not the full
350 lbf, and that 175 lbf is what Features D and E get sized on. If I had carried the 350 lbf
straight through, D and E would have been sized for twice their real load. Summing the
vertical forces on the Feature C free-body diagram before moving on is what caught it.

### Assumption sensitivity

The assignment allows direct shear failure to be neglected. If shear mattered, the thin axial
members are the ones that would change — Feature B carries 350 lbf across 0.375 in², and a
shear check against roughly 0.577 × 9,000 = 5,200 psi would have to be added.

The material choice is the bigger one. 6061-T6 aluminium has about a third of the modulus and
two thirds of the allowable stress, so the same bracket in aluminium would be governed by
stiffness in at least some features instead of by stress, and the answer to "which requirement
controls this design" would flip.

## Time log

## Appendix – reference material

- Machinery's Handbook, ANSI/ASME Standard Limits and Fits, pp. 646–660
- Machinery's Handbook, beam deflection and section modulus tables

## CAD file download

Below I have provided the file for my bracket design:

[Click here to download A5_Bracket.SLDPRT](A5_Bracket.SLDPRT) — the part as modelled, with
ASTM A36 steel applied and all five features in the tree.
