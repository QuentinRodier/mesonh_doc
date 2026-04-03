2Drelief - 2D Bell-Shaped Mountain
=============================================================

**Category** : Idealized · Academic  
**Objective** : Validate orographic flow dynamics and gravity wave generation over a 2D mountain

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 256 × 1 × 48
   * - Resolution
     - Dx=5km, Dz=40m (stretching above 5km)
   * - Simulation duration
     - 3 h (10 800 s)
   * - Time step
     - 60 s
   * - Boundary conditions
     - OPEN (X), CYCL (Y)
   * - Coriolis
     - No
   * - Advection
     - CEN4TH + RKC4 + PPM_01
   * - Turbulence
     - TKEL + 3D-DELT
   * - Surface
     - None
   * - Radiation
     - None
   * - Microphysics
     - None
   * - Convection
     - None

**Scientific Context & Specificity** :

2Drelief is the **simplest orographic test case** in the catalog. Its uniqueness:

- Tests **pure dynamics** without moisture, radiation, or complex physics
- Validates **mountain wave generation** and **gravity wave drag**
- Uses **bell-shaped (BELL) topography** with XHMAX=500m, XAX=10km

Unlike other academic cases:

- COLD_BUBBLE tests **thermodynamic perturbations**; 2Drelief tests **orographic forcing**
- HYDRO tests **wave propagation**; 2Drelief tests **mountain-induced flows**

The case simulates airflow over a 2D bell-shaped mountain with:
- Constant wind profile (10 m/s)
- Stable stratification (N≈0.02 s⁻¹)
- Dry conditions

**Technical Specificities** :

This case demonstrates Meso-NH's **orographic flow** capabilities with **OPEN boundary conditions** in the flow-perpendicular direction.

Key namelist sections:

.. code-block:: fortran

   ! Bell-shaped mountain topography
   &NAM_CONF_PRE
   CZS = 'BELL',                 ! Bell-shaped mountain
   XHMAX = 500.,                ! Mountain height [m]
   XAX = 10000.,                ! Mountain half-width [m]
   /

   ! OPEN boundary conditions (outflow)
   &NAM_LBCn
   CLBCX = 2*"OPEN",            ! OPEN in X (flow-perpendicular)
   CLBCY = 2*"CYCL",            ! CYCL in Y (flow-parallel)
   XCPHASE = 20.,               ! Phase speed for gravity waves
   /

   ! 3D turbulence with DELT length scale
   &NAM_TURBn
   CTURBDIM = "3DIM",
   CTURBLEN = "DELT",
   LTURB_FLX = .TRUE.,
   LTURB_DIAG = .TRUE.,
   /

   ! Numerical diffusion for stability
   &NAM_DYNn
   XT4DIFU = 1500.,             ! 4th order numerical diffusion
   LNUMDIFU = .TRUE.,
   /

**Validation Targets** :

- Mountain wave amplitude and wavelength
- Vertical velocity perturbations
- Pressure perturbation patterns

**Execution** :

.. code-block:: bash

   cd integration_cases/local/2Drelief
   make clean && make
   ./run_2Drelief

**Numerical Resources** :

- **Architecture** : Local (single CPU)
- **Processors** : 1
- **Memory** : < 500 MB
- **Runtime** : < 5 minutes
