FIRE - Marine Stratocumulus
=============================================================

**Category** : Idealized · Boundary Layer (Marine)  
**Objective** : Model marine stratocumulus and turbulence-radiation-microphysics interactions

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 1 × 1 × 120
   * - Resolution
     - Dx=2500m, Dz=10m
   * - Simulation duration
     - 25 h (90 000 s)
   * - Time step
     - 120 s
   * - Boundary conditions
     - CYCL (periodic)
   * - Coriolis
     - Yes
   * - Advection
     - CEN4TH + RKC4
   * - Turbulence
     - TKEL + 1D-BL89
   * - Surface
     - SEAFLUX (oceanic fluxes)
   * - Radiation
     - ECMWF or ECRAD
   * - Microphysics
     - KHKO, LIMA, or LIMA_MALA
   * - Shallow convection
     - EDKF

**Scientific Context & Specificity** :

FIRE is the **most physically comprehensive case**, combining:

- **Radiation** (unique among BL cases) : Day-night cycle with cloud-radiation feedbacks
- **SEAFLUX** : Interactive ocean-atmosphere coupling
- **Advanced microphysics** : LIMA (2-moment) vs KHKO (bulk)

Unique features vs other cases:

- BOMEX has **no radiation**; FIRE has full radiation scheme
- GABLS has **no moisture**; FIRE has full microphysics chain
- ARMCU has **continental** fluxes; FIRE has **marine** fluxes

The case simulates the FIRST ISCCP REGIONAL EXPERIMENT (Pacific coast, California), featuring:

- **Night** : Thick stratocumulus deck (>90% coverage)
- **Day** : Progressive fragmentation, cumulus beneath

This case tests the **turbulence-radiation-microphysics triad**, critical for climate modeling.

**Technical Specificities** :

This case demonstrates Meso-NH's **full physics suite** including **radiation**, **SEAFLUX**, and **advanced microphysics**.

Key namelist sections:

.. code-block:: fortran

   ! Radiation scheme (ECMWF or ECRAD)
   &NAM_PARAMn
   CRAD = 'ECMWF',                ! ECMWF radiation OR 'ECRAD'
   /
   &NAM_PARAM_RADn
   XDTRAD = 360.,                 ! Radiation time step [s]
   CLW = 'MORC',                  ! Cloud liquid water property
   CAER = 'SURF',                 ! Aerosol from surface
   CEFRADL = '2MOM',              ! 2-moment effective radius
   COPWLW = 'SAVI',               ! Longwave property
   COPWSW = 'FOUQ',               ! Shortwave property
   /

   ! Ocean-atmosphere coupling (SEAFLUX)
   &NAM_SEAFLUXn
   CSEA_FLUX = 'DIRECT',          ! Direct flux computation
   CSEA_ALB = 'TA96',             ! Taylor albedo scheme
   /

   ! Advanced microphysics (LIMA - 2-moment)
   &NAM_PARAMn
   CCLOUD = 'LIMA',               ! 2-moment microphysics
   /
   &NAM_PARAM_C2R2
   HPARAM_CCN = 'CPB',            ! CCN parameterization
   XCHEN = 0.173E+09,            ! CCN concentration [m^-3]
   XKHEN = 1.403,                 ! HEN parameters
   LRAIN = .FALSE.,
   LSEDC = .FALSE.,
   /

   ! 3D advection schemes for WENO variant
   &NAM_ADVn
   CUVW_ADV_SCHEME = 'WENO5',    ! 3D: WENO5 for sharp gradients
   /

**Available Variants** :

.. code-block:: bash

   # Local 1D versions
   integration_cases/local/FIRE_1D/KHKO/          # Bulk microphysics
   integration_cases/local/FIRE_1D/LIMA/           # 2-moment microphysics
   integration_cases/local/FIRE_1D/LIMA_MALA/      # LIMA + aerosol
   integration_cases/local/FIRE_1D/LIMA_ECRAD/     # LIMA + ECRAD radiation
   integration_cases/local/FIRE_1D/ECMW/           # ECMW radiation

   # HPC 3D versions
   integration_cases/hpc/FIRE/WENO5/               # 3D WENO5
   integration_cases/hpc/FIRE/CEN4TH_RKC4/        # 3D CEN4TH

**Validation Targets** :

- Stratocumulus cloud fraction and liquid water path
- Cloud-radiation interaction
- Surface flux evolution

**Numerical Resources** :

.. list-table::
   :header-rows: 1
   :widths: 40 60

   * - Configuration
     - Resources
   * - FIRE_1D (any variant)
     - Single CPU, < 1 GB RAM, ~30 min
   * - FIRE_3D (CEN4TH_RKC4_LIMA_ECRAD)
     - 4 nodes, 256 processors, 3 hours

**References** :

- Stevens, B., et al. (2003). "On the Structure of the Marine Boundary Layer." *Quart. J. Roy. Meteor. Soc.*, 129, 919-943. https://doi.org/10.1256/qj.02.202
- Moeng, C.-H., et al. (1996). "Simulation of a Stratocumulus-Topped PBL." *J. Atmos. Sci.*, 53, 3685-3706. https://doi.org/10.1175/1520-0469(1996)053<3685:SOASTP>2.0.CO;2
