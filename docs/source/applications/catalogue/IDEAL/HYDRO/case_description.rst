HYDRO - Hydrostatic Wave Propagation
=============================================================

**Category** : Idealized · Academic  
**Objective** : Test the hydrostatic dynamical core and PPM advection schemes

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 90 × 1 × 121
   * - Resolution
     - Dx=2km, Dz=250m
   * - Simulation duration
     - 4.2 h (15 000 s)
   * - Time step
     - 10 s
   * - Boundary conditions
     - CYCL (X), CYCL (Y)
   * - Coriolis
     - No
   * - Advection
     - CEN4TH + RKC4 + PPM_00 (tested)
   * - Turbulence
     - None
   * - Surface
     - None
   * - Radiation
     - None
   * - Microphysics
     - None (dry air)
   * - Convection
     - None

**Scientific Context & Specificity** :

HYDRO is a **pure dynamical core test case** for validating **hydrostatic wave propagation**. Its uniqueness:

- Tests **PPM (Piecewise Parabolic Method)** advection schemes
- No physics at all - pure dynamics
- Tests the **anelastic approximation** (CEQNSYS='DUR')

Unlike other academic cases:

- COLD_BUBBLE tests **non-hydrostatic** dynamics; HYDRO tests **hydrostatic**
- 2Drelief/3Drelief have **orography**; HYDRO has flat terrain
- Tests **CGRAD pressure solver** with Richardson iteration (NITR=4)

The case simulates wave propagation in a 2D domain with:
- Constant stratification
- Zero initial wind
- Periodic boundaries

**Technical Specificities** :

This case demonstrates Meso-NH's **hydrostatic dynamical core** and **PPM advection** capabilities.

Key namelist sections:

.. code-block:: fortran

   ! Hydrostatic pressure solver with Richardson iteration
   &NAM_DYNn
   CPRESOPT = 'CGRAD',           ! CGRAD = Richardson method
   NITR = 4,                     ! Number of iterations
   XRELAX = 1.0,                 ! Relaxation factor
   /

   ! Pure dry dynamics (all hydrometeors disabled)
   &NAM_CONFn
   LUSERV = .FALSE.,             ! No water vapor
   LUSERC = .FALSE.,             ! No cloud water
   LUSERR = .FALSE.,             ! No rain
   LUSERI = .FALSE.,             ! No ice
   LUSERS = .FALSE.,             ! No snow
   LUSERG = .FALSE.,             ! No graupel
   LUSERG = .FALSE.,             ! No hail
   /

   ! PPM advection schemes
   &NAM_ADVn
   CUVW_ADV_SCHEME = 'CEN4TH',   ! 4th order for momentum
   CMET_ADV_SCHEME = 'PPM_00',   ! PPM for meteorological vars
   CSV_ADV_SCHEME = 'PPM_00',    ! PPM for scalars
   /

   ! No physics
   &NAM_PARAMn
   CTURB = "NONE",
   CRAD = "NONE",
   CCLOUD = "NONE",
   CDCONV = "NONE",
   /

   ! Vertical relaxation at top
   &NAM_DYNn
   LVE_RELAX = .TRUE.,          ! Vertical relaxation
   XRIMKMAX = 0.0004,            ! Relaxation coefficient
   XALKTOP = 0.01,               ! Rayleigh damping
   /

**Validation Targets** :

- Hydrostatic balance maintenance
- Wave propagation speed
- PPM scheme conservation properties

**Execution** :

.. code-block:: bash

   cd integration_cases/local/HYDRO
   make clean && make
   ./run_HYDRO

**Numerical Resources** :

- **Architecture** : Local (single CPU)
- **Processors** : 1
- **Memory** : < 200 MB
- **Runtime** : < 5 minutes
