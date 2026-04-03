OCEAN_LES - Ocean Large-Eddy Simulation
=============================================================

**Category** : Idealized · Applicative  
**Objective** : Simulate ocean-atmosphere boundary layer coupling

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 128 × 128 × 100
   * - Resolution
     - Dx=125m, Dz=20m
   * - Simulation duration
     - 24 h (86 400 s)
   * - Time step
     - 30 s (run1), 10 s (run2)
   * - Boundary conditions
     - CYCL (X), CYCL (Y)
   * - Coriolis
     - Yes
   * - Advection
     - CEN4TH + RKC4
   * - Turbulence
     - TKEL + 1D-DELT
   * - Surface
     - SEAFLUX
   * - Radiation
     - None
   * - Microphysics
     - None (dry)
   * - Convection
     - None
   * - Ocean coupling
     - LHE (Liquid Water/Energy)

**Scientific Context & Specificity** :

OCEAN_LES is the **only ocean coupling case** in the catalog. Its uniqueness:

- Tests **ocean-atmosphere coupling** (LHE equations)
- Uses **deep ocean** parameterization
- Studies **oceanic mixed layer** dynamics

Unlike other applicative cases:

- FIRE uses **flux-specified** surface; OCEAN_LES uses **full coupling**
- All other cases are **atmospheric**; OCEAN_LES includes **ocean dynamics**
- Tests **Coriolis effects** on ocean circulation

The case simulates:
- Oceanic mixed layer evolution
- Wind-driven stirring
- Ocean-atmosphere momentum exchange

**Technical Specificities** :

This case demonstrates Meso-NH's **ocean coupling** capabilities using the **LHE equation system**.

Key namelist sections:

.. code-block:: fortran

   ! Ocean coupling
   &NAM_CONF
   CEQNSYS = 'LHE',              ! Ocean coupling equations
   /

   ! Deep ocean parameterization
   &NAM_FRC
   LDEEPOC = .TRUE.,             ! Enable deep ocean
   XCENTX_OC = 8000.,           ! Ocean center X [m]
   XCENTY_OC = 8000.,           ! Ocean center Y [m]
   XRADX_OC = 4000.,            ! Ocean radius X [m]
   XRADY_OC = 4000.,            ! Ocean radius Y [m]
   /

   ! Dry air (ocean simulation)
   &NAM_CONFn
   LUSERV = .FALSE.,
   LUSERC = .FALSE.,
   LUSERR = .FALSE.,
   /

   ! Periodic boundaries (ocean basin)
   &NAM_LBCn
   CLBCX = 2*"CYCL",
   CLBCY = 2*"CYCL",
   XCPHASE = 0.,
   /

   ! 1D turbulence (oceanic)
   &NAM_TURBn
   CTURBDIM = "1DIM",
   CTURBLEN = "DELT",
   XIMPL = 0.,
   LRMC01 = .FALSE.,
   /

**Validation Targets** :

- Ocean mixed layer depth
- Velocity profiles
- Temperature evolution

**Execution** :

.. code-block:: bash

   # Requires HPC
   cd integration_cases/hpc/OCEAN_LES/002_run1
   # Available: run1 (coarse), run2 (fine)
   sbatch run_mesonh

**Numerical Resources** :

.. list-table::
   :header-rows: 1
   :widths: 40 60

   * - Configuration
     - Resources
   * - OCEAN_LES run1
     - 64 processors, ~4 GB RAM, ~6h
   * - OCEAN_LES run2
     - 128 processors, ~8 GB RAM, ~6h

**References** :

- McWilliams, J. C. (1996). "Modeling the Ocean General Circulation." *Ann. Rev. Fluid Mech.*, 28, 215-248. https://doi.org/10.1146/annurev.fluid.28.1.215
