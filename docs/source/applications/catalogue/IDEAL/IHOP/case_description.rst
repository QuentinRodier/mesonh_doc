IHOP - International H2O Project
=============================================================

**Category** : Idealized · Boundary Layer  
**Objective** : Study the atmospheric water cycle and nocturnal low-level jet dynamics

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 1 × 1 × 100
   * - Resolution
     - Dx=100m, Dz=40m
   * - Simulation duration
     - 7 h (25 200 s)
   * - Time step
     - 10 s
   * - Boundary conditions
     - CYCL (periodic)
   * - Coriolis
     - Yes (lat=36.56°N)
   * - Advection
     - CEN4TH + PPM_01
   * - Turbulence
     - TKEL + 1D-BL89 (RM17 available)
   * - Surface
     - Idealized Fluxes (H: 5→214 W/m²)
   * - Radiation
     - None
   * - Microphysics
     - REVE
   * - Shallow convection
     - EDKF

**Scientific Context & Specificity** :

IHOP is the **only case featuring a low-level jet (LLJ)** in this catalog. Its uniqueness:

- BOMEX/GABLS/ARMCU have **no jet structure**; IHOP explicitly models nocturnal LLJ
- FIRE has **no diurnal cycle**; IHOP captures the day-to-night transition
- IHOP includes **moisture advection** and **heterogeneous surface fluxes** (Lake Breeze)

The case simulates the IHOP-2002 field campaign (Kansas, June 2002) focusing on water vapor variability. Key features:

- Nocturnal LLJ peaking at ~1000 m after 18h UTC
- Morning lake breeze perturbation
- Moisture gradient evolution

**Technical Specificities** :

This case demonstrates Meso-NH's **moisture advection** capabilities and **variable surface forcing** with time-dependent fluxes.

Key namelist sections:

.. code-block:: fortran

   ! Time-varying surface fluxes (NAM_IDEAL_FLUX)
   &NAM_IDEAL_FLUX
   NFORCT = 2,
   NFORCF = 15,
   XTIMET(1) = 0., XTIMET(2) = 25200.,  ! Time array [s]
   XTIMEF(1) = 0., XTIMEF(2) = 1800., ... XTIMEF(15) = 25200.,
   XSFTH(1) = 5., XSFTH(7) = 126., ... XSFTH(15) = 214.,  ! Heat flux evolves
   XSFTQ(1) = 22., ... XSFTQ(15) = 179.,                    ! Moisture flux evolves
   CUSTARTYPE = 'Z0',
   XZ0 = 0.035,
   /

   ! Initial perturbation (hot bubble)
   &NAM_PERT_PRE
   CPERT_KIND = 'WH',              ! Warm bubble perturbation
   XAMPLIWH = 0.1,                 ! Amplitude [K]
   NKWH = 100,                     ! Vertical position
   /

   ! REVE microphysics for moisture
   &NAM_PARAMn
   CCLOUD = 'REVE',                ! REVE microphysics
   /

   ! Geostrophic forcing
   &NAM_FRC
   LGEOST_UV_FRC = .FALSE.,
   LTEND_THRV_FRC = .TRUE.,        ! Only virtual potential temp forcing
   LVERT_MOTION_FRC = .TRUE.,      ! Vertical motion forcing
   /

**Validation Targets** :

- LLJ strength and height
- Water vapor content evolution
- Turbulent kinetic energy profiles

**Execution** :

.. code-block:: bash

   # 1D version: local
   cd integration_cases/hpc/IHOP/1D
   ./run_prep_ideal_case
   ./run_mesonh

   # 3D version: requires HPC
   cd integration_cases/hpc/IHOP/3D
   sbatch run_mesonh

**Numerical Resources** :

.. list-table::
   :header-rows: 1
   :widths: 40 60

   * - Configuration
     - Resources
   * - IHOP_1D
     - Single CPU, < 1 GB RAM, ~5 min
   * - IHOP_3D (256×256×90)
     - 64 processors, ~2 GB RAM, ~2h

**References** :

- Weckwerth, T. M., et al. (2004). "An Overview of the International H2O Project (IHOP_2002) and Some Preliminary Highlights." *Bull. Amer. Meteor. Soc.*, 85, 253-277. https://doi.org/10.1175/BAMS-85-2-253
