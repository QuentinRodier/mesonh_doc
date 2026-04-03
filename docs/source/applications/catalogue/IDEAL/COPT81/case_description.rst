COPT81 - COPT Case (Convective Organization)
=============================================================

**Category** : Idealized · Applicative  
**Objective** : Study convective organization and cold pool interactions in 2D

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 320 × 1 × 46
   * - Resolution
     - Dx=1250m, Dz=7.2m
   * - Simulation duration
     - 8 h (28 800 s)
   * - Time step
     - 10 s
   * - Boundary conditions
     - OPEN (X), CYCL (Y)
   * - Coriolis
     - No
   * - Advection
     - CEN4TH + RKC4 + PPM_01
   * - Turbulence
     - TKEL + 3D-DELT
   * - Surface
     - Idealized Fluxes (zero)
   * - Radiation
     - None
   * - Microphysics
     - ICE3
   * - Convection
     - Implicit (self-generated)

**Scientific Context & Specificity** :

COPT81 simulates **convective self-organization** in 2D. Its uniqueness:

- Tests **cold pool dynamics** and **convective outflow interactions**
- Uses **zero surface fluxes** (isolated system)
- Studies **convective cell merging** and **gust front propagation**

Unlike other applicative cases:

- SUPERCELL simulates **3D supercell**; COPT81 simulates **2D convective lines**
- BOMEX/ARMCU have **external forcing**; COPT81 has **self-generated convection**
- Tests **CARTESIAN budget** diagnostics (NBUMOD, XBULEN)

The case simulates a quasi-steady convective system with:
- Multiple updrafts/downdrafts
- Cold pool generation
- Gravity wave emission

**Technical Specificities** :

This case demonstrates Meso-NH's **cold pool dynamics** capabilities and **CARTESIAN budget** diagnostics.

Key namelist sections:

.. code-block:: fortran

   ! Zero surface fluxes (isolated system)
   &NAM_IDEAL_FLUX
   XSFTH(:) = 0.,              ! No surface heat flux
   XSFTQ(:) = 0.,              ! No surface moisture flux
   /

   ! CARTESIAN budget diagnostics
   &NAM_BUDGET
   CBUTYPE = 'CART',           ! Cartesian budget
   XBULEN = 3600.,            ! Budget averaging length [s]
   XBUWRI = 3600.,            ! Budget output frequency [s]
   NBUKL = 1, NBUKH = 46,    ! Vertical extent
   NBUIL = 1, NBUIH = 320,    ! Horizontal extent
   /

   ! 3D turbulence with explicit time scheme
   &NAM_TURBn
   XIMPL = 0.,                ! Explicit turbulence
   CTURBDIM = "3DIM",
   CTURBLEN = "DELT",
   /

   ! OPEN boundary with phase speed
   &NAM_LBCn
   CLBCX = 2*"OPEN",          ! OPEN in X
   XCPHASE_PBL = 20.,         ! Phase speed for gravity waves
   /

**Validation Targets** :

- Cold pool propagation speed
- Convective mass flux evolution
- Budget terms (advection, diffusion, source/sink)

**Execution** :

.. code-block:: bash

   cd integration_cases/local/COPT81/COPT81_CART
   make clean && make
   ./run_COPT81_CART

**Numerical Resources** :

- **Architecture** : Local (single CPU)
- **Processors** : 1
- **Memory** : < 500 MB
- **Runtime** : < 15 minutes
