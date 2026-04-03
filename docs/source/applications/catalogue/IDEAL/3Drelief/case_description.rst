3Drelief - 3D Bell-Shaped Mountain
=============================================================

**Category** : Idealized · Academic  
**Objective** : Validate 3D orographic flow dynamics and cross-flow propagation

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 128 × 96 × 72
   * - Resolution
     - Dx=2km, Dz=250m
   * - Simulation duration
     - 2.8 h (10 000 s)
   * - Time step
     - 80 s
   * - Boundary conditions
     - OPEN (X), OPEN (Y)
   * - Coriolis
     - No
   * - Advection
     - CEN4TH + RKC4 + PPM_01
   * - Turbulence
     - None
   * - Surface
     - None
   * - Radiation
     - None
   * - Microphysics
     - None (dry air)
   * - Convection
     - None

**Scientific Context & Specificity** :

3Drelief extends the 2D mountain case to **three dimensions**. Its uniqueness:

- Tests **3D flow dynamics** vs 2Drelief's 2D simplification
- Uses **horizontal relaxation** at lateral boundaries (NRIMX=6, NRIMY=3)
- Tests **OPEN boundary conditions** in both horizontal directions

Unlike other cases:

- 2Drelief has **periodic** boundary in Y; 3Drelief has **OPEN** boundaries
- HYDRO tests **pure wave propagation**; 3Drelief tests **orographic 3D effects**
- No turbulence or physics - pure dynamical core test

The case simulates airflow over a 3D bell-shaped mountain with:
- Constant wind profile
- Stable stratification
- Dry conditions (LUSERV=.FALSE.)

**Technical Specificities** :

This case demonstrates Meso-NH's **3D orographic flow** capabilities with **OPEN boundary conditions** and **horizontal relaxation**.

Key namelist sections:

.. code-block:: fortran

   ! 3D configuration with horizontal relaxation
   &NAM_DYNn
   LHORELAX_UVWTH = .TRUE.,      ! Horizontal relaxation on U,V,W,TH
   LHORELAX_RV = .FALSE.,
   LVE_RELAX = .TRUE.,           ! Vertical relaxation at top
   NRIMX = 6,                    ! Relaxation points in X
   NRIMY = 3,                    ! Relaxation points in Y
   XRIMKMAX = 0.001666,          ! Relaxation coefficient
   /

   ! OPEN boundaries in both directions
   &NAM_LBCn
   CLBCX = 2*"OPEN",            ! OPEN in X
   CLBCY = 2*"OPEN",            ! OPEN in Y
   /

   ! No moisture (dry air)
   &NAM_CONFn
   LUSERV = .FALSE.,             ! Dry simulation
   /

   ! No physics - pure dynamics
   &NAM_PARAMn
   CTURB = "NONE",
   CRAD = "NONE",
   CCLOUD = "NONE",
   /

   ! No numerical diffusion (clean dynamics)
   &NAM_DYN
   LNUMDIFU = .FALSE.,          ! No numerical diffusion
   /

**Validation Targets** :

- 3D mountain wave structure
- Lateral boundary reflections (should be minimal)
- Vertical velocity patterns

**Execution** :

.. code-block:: bash

   cd integration_cases/local/3Drelief
   make clean && make
   ./run_3Drelief

**Numerical Resources** :

- **Architecture** : Local or HPC
- **Processors** : 4-16 (parallel)
- **Memory** : ~1 GB
- **Runtime** : < 10 minutes
