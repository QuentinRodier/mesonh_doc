ARMCU - ARM Continental Cumulus
=============================================================

**Category** : Idealized · Boundary Layer (Continental)  
**Objective** : Model the continental diurnal cycle with shallow convection

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 1 × 1 × 100
   * - Resolution
     - Dx=40km, Dz=40m
   * - Simulation duration
     - 15 h (54 000 s)
   * - Time step
     - 100 s
   * - Boundary conditions
     - CYCL (periodic)
   * - Coriolis
     - Yes
   * - Advection
     - CEN4TH + RKC4
   * - Turbulence
     - TKEL + 1D-BL89
   * - Surface
     - Idealized Fluxes (diurnal cycle, H: -30→140→-10 W/m²)
   * - Radiation
     - None
   * - Microphysics
     - ICE3
   * - Shallow convection
     - EDKF

**Scientific Context & Specificity** :

ARMCU is the **continental counterpart to BOMEX**. Key differences:

- BOMEX has **oceanic** surface fluxes (weak, quasi-constant); ARMCU has **strong diurnal cycle**
- FIRE models **stratiform** clouds; ARMCU models **cumulus** development
- ARMCU includes **conditional sampling** diagnostics (CONDSAMP)

The case simulates ARM SGP observations (Southern Great Plains, USA) with characteristic phases:

1. **Night** : Stable conditions, negative heat flux (-30 W/m²)
2. **Morning** : First cumulus appearance (~10h UTC)
3. **Afternoon** : Peak convection (H=140 W/m²), shallow cumulus development
4. **Evening** : Progressive dissipation

**Technical Specificities** :

This case demonstrates Meso-NH's **continental boundary layer** modeling with **strong diurnal forcing** and **conditional sampling diagnostics**.

Key namelist sections:

.. code-block:: fortran

   ! Strong diurnal cycle surface forcing
   &NAM_IDEAL_FLUX
   NFORCT = 2,
   NFORCF = 31,                   ! 31 time points for smooth diurnal cycle
   XTIMET(1) = 0., XTIMET(2) = 54000.,
   XSFTH(1) = -30.,              ! Night: negative flux
   XSFTH(7) = 60., ... XSFTH(13) = 130.,   ! Morning ramp-up
   XSFTH(14) = 140.,             ! Peak at midday
   XSFTH(21) = 100., ... XSFTH(26) = -10., ! Evening decline
   XSFTQ(1) = 2.0E-6, ... XSFTQ(16) = 2.0E-4,  ! Moisture evolves
   /

   ! Conditional sampling diagnostics
   &NAM_CONDSAMP
   LCONDSAMP = .TRUE.,            ! Enable conditional sampling
   NCONDSAMP = 3,                 ! Number of sample categories
   /

   ! ICE3 microphysics (continental)
   &NAM_PARAMn
   CCLOUD = 'ICE3',               ! 3-class ice microphysics
   CSCONV = 'EDKF',               ! Shallow convection
   /

   ! LRMC01 for stable conditions
   &NAM_TURBn
   LRMC01 = .TRUE.,               ! Redelsorder-Machenhauer correction
   /

**Conditional Sampling** : The CONDSAMP variant provides cloud-resolving diagnostics (updraft/downdraft statistics).

**Validation Targets** :

- Diurnal evolution of cloud fraction
- Boundary layer height cycle
- Shallow cumulus mass flux profiles

**Execution** :

.. code-block:: bash

   cd integration_cases/local/ARMCU_1D_CONDSAMP
   make clean && make
   ./run_ARMCU

**Numerical Resources** :

- **Architecture** : Local (single CPU)
- **Processors** : 1
- **Memory** : < 500 MB
- **Runtime** : < 10 minutes

**References** :

- Xu, K.-M., and Randall, D. A. (1996). "A Semi-Empirical Cloudiness Parameterization for Use in Climate Models." *J. Atmos. Sci.*, 53, 3084-3102. https://doi.org/10.1175/1520-0469(1996)053<3084:ASCPFU>2.0.CO;2
