BOMEX - Barbados Oceanographic and Meteorological Experiment
=============================================================

**Category** : Idealized · Boundary Layer  
**Objective** : Validate turbulence and shallow convection schemes in marine conditions

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 1 × 1 × 75
   * - Horizontal resolution
     - 40 km × 40 km
   * - Vertical resolution
     - 40 m (manual grid)
   * - Simulation duration
     - 8 h (28 800 s)
   * - Time step
     - 120 s
   * - Boundary conditions
     - CYCL (periodic)
   * - Coriolis
     - Yes (lat=15°N)
   * - Advection
     - CEN4TH + RKC4
   * - Turbulence
     - TKEL + 1D-BL89
   * - Surface
     - Idealized Fluxes (H=9.2 W/m², LE=6.2×10⁻⁵ kg/m²/s)
   * - Radiation
     - None
   * - Microphysics
     - ICE3 (3-class)
   * - Shallow convection
     - EDKF

**Scientific Context & Specificity** :

BOMEX is the **gold-standard reference case** for marine boundary layer modeling. Unlike other cases:

- GABLS focuses on **stable** conditions; BOMEX focuses on **convective** conditions
- ARMCU uses **continental** fluxes; BOMEX uses **oceanic** fluxes with weak latent heat
- FIRE models **stratocumulus**; BOMEX models **shallow cumulus**

The case represents near-equilibrium conditions with quasi-constant surface fluxes and steady geostrophic forcing (-8.75 m/s). It tests whether models correctly simulate:

- Cumulus cloud fraction (~10-15%)
- Liquid water content profiles
- Boundary layer height (~1500 m)
- Turbulent flux profiles

**Technical Specificities** :

This case demonstrates Meso-NH's capability to run **idealized 1D simulations with surface flux forcing** and **shallow convection parameterization**.

Key namelist sections:

.. code-block:: fortran

   ! Surface flux forcing (NAM_IDEAL_FLUX)
   &NAM_IDEAL_FLUX
   XSFTH(1) = 9.2031331377508980,  ! Surface heat flux [W/m²]
   XSFTQ(1) = 6.1601E-5,            ! Surface moisture flux [kg/m²/s]
   XZ0 = 0.035,                     ! Roughness length [m]
   CUSTARTYPE = 'USTAR',            ! u* based formulation
   XUSTAR(1) = 0.28,               ! Friction velocity [m/s]
   /

   ! Shallow convection (EDKF)
   &NAM_PARAMn
   CSCONV = 'EDKF',                 ! EDKF shallow convection
   /
   &NAM_PARAM_MFSHALLn
   CMF_UPDRAFT = 'EDKF',
   CMF_CLOUD = 'DIRE',
   LMF_FLX = .TRUE.,
   /

   ! Geostrophic forcing (NAM_FRC)
   &NAM_FRC
   LGEOST_UV_FRC = .TRUE.,
   LTEND_THRV_FRC = .TRUE.,
   lvert_motion_frc = .TRUE.,
   XRELAX_HEIGHT_FRC = 2600.,
   /

**Validation Targets** :

- θ_l, q_t, and wind vertical profiles
- Buoyancy flux profiles
- Cloud base height and top

**Execution** :

.. code-block:: bash

   cd integration_cases/local/BOMEX
   make clean && make
   ./run_BOMEX

**Outputs** :

- ``BOMEX_00100.nc`` : Initial state after PREP_IDEAL
- ``BOMEX_1D.nc`` : Meso-NH output
- Post-processing: ``plot_BOMEX.py``

**Numerical Resources** :

- **Architecture** : Local (single CPU sufficient)
- **Processors** : 1
- **Memory** : < 500 MB
- **Runtime** : < 5 minutes

**References** :

- Siebesma, A. P., et al. (2003). "A Large Eddy Simulation Intercomparison Study of Shallow Cumulus Convection." *J. Atmos. Sci.*, 60, 1201-1219. https://doi.org/10.1175/1520-0469(2003)60<1201:ALESIS>2.0.CO;2
- Holland, J. Z., and Rasmusson, E. M. (1973). "Measurements of the atmospheric mass, energy, and momentum budgets over a 500-kilometer square of tropical ocean." *Mon. Wea. Rev.*, 101, 44-55. https://doi.org/10.1175/1520-0493(1973)101<0044:MOTAME>2.3.CO;2

:download:`BOMEX.pdf <BOMEX.pdf>`
