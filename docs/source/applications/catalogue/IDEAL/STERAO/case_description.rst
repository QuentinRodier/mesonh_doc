STERAO - STERAO-DC Lightning Discharge
=============================================================

**Category** : Idealized · Applicative  
**Objective** : Simulate a stratiform-to-convective transition with electrical discharges

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 160 × 160 × 50
   * - Resolution
     - Dx=1000m, Dz=77m
   * - Simulation duration
     - 3 h (10 800 s)
   * - Time step
     - 2.5 s
   * - Boundary conditions
     - OPEN (X), OPEN (Y)
   * - Coriolis
     - No
   * - Advection
     - CEN4TH + LEFR + PPM_01
   * - Turbulence
     - TKEL + 3D-DELT
   * - Surface
     - None
   * - Radiation
     - None
   * - Microphysics
     - ICE3 (warm rain)
   * - Electrification
     - ELE4
   * - Lightning
     - Flash detection and tracking

**Scientific Context & Specificity** :

STERAO is the **only lightning case** in the catalog. Its uniqueness:

- Tests **electrification and discharge** processes
- Uses **ELE4** non-inductive charging scheme
- Tracks **lightning flash geometry**

Unlike other applicative cases:

- SUPERCELL focuses on **dynamics**; STERAO focuses on **electrification**
- COPT81 is **2D**; STERAO is **3D**
- Tests **charging mechanisms** and **flash propagation**

The case simulates:
- Non-inductive charging (ice collisions)
- Electric field buildup
- Lightning flash detection

**Technical Specificities** :

This case demonstrates Meso-NH's **electrification and lightning** capabilities.

Key namelist sections:

.. code-block:: fortran

   ! Non-inductive charging (ELE4)
   &NAM_PARAMn
   CCLOUD = 'ICE3',
   CELEC = 'ELE4',               ! Non-inductive charging
   /

   ! Electric module configuration
   &NAM_ELEC
   LINDUCTIVE = .FALSE.,        ! Non-inductive only
   LELEC_FIELD = .TRUE.,         ! Electric field computation
   LFLASH_GEOM = .TRUE.,        ! Flash geometry tracking
   CNI_CHARGING = 'TAKAH',      ! Takahashi charging
   XLIM_NI_IS = 10.E-15,       ! Charge limits
   XLIM_NI_IG = 30.E-15,
   XLIM_NI_SG = 100.E-15,
   CLSOL = 'RICHA',             ! Soil model
   NLAPITR_ELEC = 4,            ! Relaxation iterations
   XETRIG = 200.E3,             ! Trigger threshold [V/m]
   XEBALANCE = 0.1,             ! Balance factor
   XDFRAC_ECLAIR = 2.3,         ! Flash fraction
   /

   ! Warm rain microphysics
   &NAM_PARAM_ICEn
   LRED = .TRUE.,
   CSUBG_AUCV_RC = 'NONE',
   LWARM = .TRUE.,               ! Warm rain process
   CPRISTINE_ICE = 'PLAT',
   /

   ! Series diagnostics
   &NAM_SERIES
   LSERIES = .TRUE.,
   /

**Validation Targets** :

- Electric field evolution
- Flash frequency and location
- Charge structure

**Execution** :

.. code-block:: bash

   # Requires HPC
   cd integration_cases/hpc/STERAO
   sbatch run_mesonh

**Numerical Resources** :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Nodes
     - 4
   * - Processors
     - 192
   * - Runtime
     - 4 hours

**References** :

- Helsdon, J. H., et al. (2001). "A Comparison of Charge Structure in Two Severe Thunderstorms." *J. Geophys. Res.*, 106, 1741-1756. https://doi.org/10.1029/2000JD900289
