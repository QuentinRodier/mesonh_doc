GABLS1 - GEWEX Atmospheric Boundary Layer Study
=============================================================

**Category** : Idealized · Boundary Layer (Stable)  
**Objective** : Validate turbulence parameterizations under stable atmospheric conditions

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 1 × 1 × 155
   * - Resolution
     - Dx=2m, Dz=2m (very high)
   * - Simulation duration
     - 9 h (32 400 s)
   * - Time step
     - 10 s
   * - Boundary conditions
     - CYCL (periodic)
   * - Coriolis
     - Yes (f=1.03×10⁻⁴ s⁻¹)
   * - Advection
     - CEN4TH + PPM_01
   * - Turbulence
     - TKEL + 1D-BL89 (RM17 available)
   * - Surface
     - TSZ0 (fixed surface temperature)
   * - Radiation
     - None
   * - Microphysics
     - Disabled (dry air)
   * - Convection
     - Disabled

**Scientific Context & Specificity** :

GABLS1 is the **only stable boundary layer case** in this catalog. Its uniqueness:

- BOMEX/ARMCU/FIRE model **convective** BL; GABLS models **stable** BL
- GABLS has **no moisture or clouds**; other cases include hydrometeors
- GABLS uses **very high resolution** (2m) to capture small-scale structures

The case represents the "hard problem" of stable boundary layer turbulence:

- Intermittent turbulence
- Gravity waves
- Low-level jets
- Weak vertical mixing

This is a **GEWEX/GCSS reference case** for model intercomparison, specifically designed to expose weaknesses in turbulence schemes under stable conditions.

**Technical Specificities** :

This case demonstrates Meso-NH's capability to simulate **stable boundary layers** with **very high vertical resolution** and **TSZ0 surface scheme**.

Key namelist sections:

.. code-block:: fortran

   ! High vertical resolution grid
   &NAM_VER_GRID
   NKMAX = 155,
   ZDZGRD = 2.,                   ! 2m vertical spacing
   ZDZTOP = 2.,
   ZZMAX_STRGRD = 500.,           ! Stretching starts at 500m
   ZSTRGRD = 0.,
   /

   ! Dry air (no moisture)
   &NAM_CONFn
   LUSERV = .FALSE.,              ! No water vapor
   /

   ! Fixed surface temperature (TSZ0)
   &NAM_CONF_PRE
   CIDEAL = 'RSOU',               ! Radio sounding initialization
   /

   ! Geostrophic forcing only (no surface fluxes)
   &NAM_FRC
   LGEOST_UV_FRC = .TRUE.,        ! Geostrophic wind forcing
   /

   ! Long time scale for turbulence (stable conditions)
   &NAM_TURBn
   CTURBLEN = 'BL89',
   XIMPL = 1.,                    ! Fully implicit
   LRMC01 = .TRUE.,               ! Redelsorder-Machenhauer correction
   /

   ! No microphysics, no convection
   &NAM_PARAMn
   CCLOUD = 'NONE',
   CDCONV = 'NONE',
   /

**Validation Targets** :

- Wind speed profile (nocturnal jet)
- Temperature profile
- Turbulent length scales

**Execution** :

.. code-block:: bash

   # HPC recommended (tall vertical domain)
   cd integration_cases/hpc/GABLS1/1D
   sbatch run_prep_ideal_case
   sbatch run_mesonh

**Numerical Resources** :

.. list-table::
   :header-rows: 1
   :widths: 40 60

   * - Configuration
     - Resources
   * - GABLS1_1D
     - Single CPU, < 1 GB RAM, ~10 min
   * - GABLS1_3D (100×100×155)
     - 128 processors, ~4 GB RAM, ~1h

**References** :

- Cuxart, J., et al. (2006). "Single-Column Model Intercomparison for a Stably Stratified Atmospheric Boundary Layer." *Bound.-Layer Meteor.*, 118, 273-303. https://doi.org/10.1007/s10546-005-3780-1
- Beare, R. J., et al. (2006). "Intercomparison of Large-Eddy Simulations of the Stable Boundary Layer." *Bound.-Layer Meteor.*, 118, 247-272. https://doi.org/10.1007/s10546-005-3788-4
