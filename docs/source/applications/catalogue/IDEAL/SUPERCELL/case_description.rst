SUPERCELL - Supercell Thunderstorm
=============================================================

**Category** : Idealized · Applicative  
**Objective** : Simulate a supercell thunderstorm with full microphysics

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 600 × 600 × 89
   * - Resolution
     - Dx=500m, Dz=10.9m
   * - Simulation duration
     - 3 h (10 800 s)
   * - Time step
     - 2 s
   * - Boundary conditions
     - OPEN (X), OPEN (Y)
   * - Coriolis
     - No
   * - Advection
     - CEN4TH + RKC4 + PPM_01
   * - Turbulence
     - TKEL + 3D-DEAR
   * - Surface
     - None
   * - Radiation
     - None
   * - Microphysics
     - ICE4/LIMA (6-class)
   * - Convection
     - Explicit (no parameterization)

**Scientific Context & Specificity** :

SUPERCELL is the **most complex convective case** in the catalog. Its uniqueness:

- Tests **3D supercell dynamics** with mesocyclone
- Uses **full 6-class microphysics** (ICE4 or LIMA)
- Requires **very high resolution** (500m) for storm structure

Unlike other applicative cases:

- COPT81 is **2D**; SUPERCELL is **3D** with storm-relative flow
- STERAO focuses on **electrification**; SUPERCELL focuses on **dynamics**
- Requires **HPC resources** due to domain size

The case simulates a supercell with:
- Rotating updraft (mesocyclone)
- Hook echo
- Hail production
- Storm splitting

**Technical Specificities** :

This case demonstrates Meso-NH's **supercell simulation** capabilities with **advanced microphysics**.

Key namelist sections:

.. code-block:: fortran

   ! Full microphysics (ICE4 or LIMA)
   &NAM_PARAMn
   CCLOUD = 'ICE4',             ! 6-class ice microphysics
   /
   &NAM_PARAM_ICEn
   CSUBG_AUCV_RC = 'CLFR',    ! Subgrid cloud fraction
   LRED = .TRUE.,              ! Ice sublimation
   LSEDIC = .TRUE.,            ! Ice sedimentation
   /

   ! LIMA microphysics (2-moment, alternative)
   &NAM_PARAM_LIMA
   NMOM_C = 1, NMOM_R = 1,    ! 1-moment for cloud, rain
   NMOM_I = 1, NMOM_S = 1,    ! 1-moment for ice, snow
   NMOM_G = 1, NMOM_H = 1,    ! 1-moment for graupel, hail
   LKESSLERAC = .TRUE.,        ! Kessler autoconversion
   LAERO_MASS = .FALSE.,       ! No aerosol mass
   /

   ! 3D turbulence with DEAR scheme
   &NAM_TURBn
   CTURBDIM = "3DIM",
   CTURBLEN = "DEAR",
   XIMPL = 1.,
   LTURB_DIAG = .FALSE.,
   LTURB_FLX = .FALSE.,
   /

   ! Time-splitting for microphysics
   LPTSPLIT = .TRUE.,          ! Enable time-splitting
   NMAXITER = 1,               ! Max iterations
   /

**Validation Targets** :

- Mesocyclone structure
- Reflectivity patterns (hook echo)
- Hail accumulation
- Updraft velocity peaks

**Execution** :

.. code-block:: bash

   # Requires HPC
   cd integration_cases/hpc/SUPERCELL
   # Available versions: ICE4, LIMA111111, LIMA222110, LIMA222222_JW_CIBU
   sbatch run_mesonh

**Numerical Resources** :

.. list-table::
   :header-rows: 1
   :widths: 40 60

   * - Configuration
     - Resources
   * - SUPERCELL (600×600×89)
     - 20 nodes, 2560 processors, 2 hours

**References** :

- Klemp, J. B. (1987). "Dynamics of Two-Dimensional Supercell Thunderstorms." *J. Atmos. Sci.*, 44, 1359-1386. https://doi.org/10.1175/1520-0469(1987)044<1359:DOTST>2.0.CO;2
