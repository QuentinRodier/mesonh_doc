EOLIENNE - Wind Turbine Wakes
=============================================================

**Category** : Idealized · Applicative  
**Objective** : Simulate wind turbine wakes and power production

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - Variable (450×120×80 to 2250×600×168)
   * - Resolution
     - Dx=10-50m, Dz=10m
   * - Simulation duration
     - Variable (6-3600 s)
   * - Time step
     - 1-5 s
   * - Boundary conditions
     - CYCL (all)
   * - Coriolis
     - Yes
   * - Advection
     - CEN4TH + RKC4 + PPM_01
   * - Turbulence
     - TKEL + 3D-DEAR/HM21
   * - Surface
     - SEAFLUX (ocean) or ISBA (land)
   * - Radiation
     - None
   * - Microphysics
     - None
   * - Convection
     - None
   * - Wind turbine
     - Actuator Disc / ALM / ADR

**Scientific Context & Specificity** :

EOLIENNE is the **only wind energy case** in the catalog. Its uniqueness:

- Tests **wind turbine parameterizations** (ADNR, ALM, ADR)
- Uses **actuator disc** or **actuator line** methods
- Studies **wake interactions** and **power production**

Unlike other applicative cases:

- All other cases model **atmospheric processes**; EOLIENNE models **wind turbine physics**
- Tests **different turbine parameterizations** (ADNR vs ALM vs ADR)
- Can simulate **single or multiple turbines**

The case simulates:
- Turbine wake recovery
- Power production estimation
- Wake turbulence enhancement

**Technical Specificities** :

This case demonstrates Meso-NH's **wind turbine modeling** capabilities with multiple parameterizations.

Key namelist sections:

.. code-block:: fortran

   ! Actuator Disc (ADNR)
   &NAM_EOL
   LMAIN_EOL = .TRUE.,            ! Enable wind turbine
   CMETH_EOL = 'ADNR',           ! Actuator Disc method
   /
   &NAM_EOL_ADNR
   CFARM_CSVDATA = 'data_farm.csv',    ! Farm data
   CTURBINE_CSVDATA = 'data_turbine.csv',  ! Turbine data
   CINTERP = 'CLS',               ! Velocity interpolation
   /

   ! Actuator Line (ALM) - alternative
   CMETH_EOL = 'ALM',            ! Actuator Line Method
   /

   ! Actuator Disk with Rotation (ADR) - alternative
   CMETH_EOL = 'ADR',            ! Actuator Disk with Rotation
   /

   ! Sea surface fluxes
   &NAM_SEAFLUXn
   CSEA_FLUX = 'DIRECT',
   CSEA_ALB = 'TA96',
   /

   ! Geostrophic forcing
   &NAM_FRC
   LGEOST_UV_FRC = .TRUE.,
   LTEND_THRV_FRC = .TRUE.,
   LVERT_MOTION_FRC = .TRUE.,
   /

   ! 3D turbulence
   &NAM_TURBn
   CTURBDIM = "3DIM",
   CTURBLEN = "DEAR",
   XIMPL = 1.,
   LTURB_FLX = .TRUE.,
   LTURB_DIAG = .TRUE.,
   /

**Available Variants** :

.. code-block:: bash

   # ADNR (Actuator Disc)
   integration_cases/local/EOLIENNE_FAST/ADNR/
   integration_cases/hpc/EOLIENNE/ADNR/

   # ALM (Actuator Line)
   integration_cases/local/EOLIENNE_FAST/ALM/
   integration_cases/hpc/EOLIENNE/ALM/

   # ADR (Actuator Disk with Rotation)
   integration_cases/hpc/EOLIENNE/ADR/

   # Single or multiple turbines
   # 01-1WT: Single turbine
   # 02-1WT_and_Nest: Single with nest
   # 03-2WT: Two turbines

**Validation Targets** :

- Wake deficit and recovery
- Power production
- Turbulence intensity increase

**Execution** :

.. code-block:: bash

   # Local fast version
   cd integration_cases/local/EOLIENNE_FAST/ADNR
   ./run_mesonh

   # HPC full version
   cd integration_cases/hpc/EOLIENNE/ADNR/01-1WT
   sbatch run_mesonh

**Numerical Resources** :

.. list-table::
   :header-rows: 1
   :widths: 40 60

   * - Configuration
     - Resources
   * - EOLIENNE_FAST (450×120×80)
     - 16 processors, ~2 GB RAM, ~30 min
   * - EOLIENNE_HPC ADR (2250×600×168)
     - 2 nodes, 256 processors, 30 min

**References** :

- Sorensen, J. N., and Shen, W. Z. (2002). "Numerical Modeling of Wind Turbine Wakes." *J. Fluids Eng.*, 124, 393-399. https://doi.org/10.1115/1.1471361
