COLD_BUBBLE - Non-Hydrostatic Cold Pool
=============================================================

**Category** : Idealized · Academic  
**Objective** : Validate non-hydrostatic dynamics and cold pool evolution

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 1024 × 1 × 128
   * - Resolution
     - Dx=50m, Dz=50m (uniform)
   * - Simulation duration
     - 15 min (900 s)
   * - Time step
     - 0.5 s (very small for stability)
   * - Boundary conditions
     - CYCL (X), CYCL (Y)
   * - Coriolis
     - No
   * - Advection
     - CEN4TH + LEFR + PPM_01
   * - Turbulence
     - None
   * - Surface
     - None
   * - Radiation
     - None
   * - Microphysics
     - None
   * - Convection
     - None

**Scientific Context & Specificity** :

COLD_BUBBLE is the **highest-resolution dynamical test case** in the catalog. Its uniqueness:

- Tests **non-hydrostatic** dynamics (CRESI solver)
- Uses **very fine resolution** (50m grid) to resolve small-scale motions
- Simulates **cold pool genesis** from initial thermodynamic perturbation

Unlike other academic cases:

- HYDRO tests **hydrostatic** waves; COLD_BUBBLE tests **non-hydrostatic** buoyancy-driven flows
- 2Drelief/3Drelief have **orographic forcing**; COLD_BUBBLE has **thermodynamic perturbation**
- This is the **fastest evolving** case (15 min simulation)

The case simulates the evolution of a cold bubble:
- Initial perturbation: Δθ = -16.2 K
- Bubble radius: XRADX=4000m, XRADZ=2000m
- Center at z = 3000m

**Technical Specificities** :

This case demonstrates Meso-NH's **non-hydrostatic** capabilities with **high resolution** and **viscosity**.

Key namelist sections:

.. code-block:: fortran

   ! Non-hydrostatic pressure solver (CRESI)
   &NAM_DYNn
   CPRESOPT = 'CRESI',           ! Non-hydrostatic solver
   NITR = 4,                     ! Number of iterations
   /

   ! Cold temperature perturbation
   &NAM_PERT_PRE
   CPERT_KIND = 'TH',            ! Temperature perturbation
   XAMPLITH = -16.2,            ! Amplitude [K] (negative = cold)
   XCENTERZ = 3000.,             ! Bubble center height [m]
   XRADX = 4000.,               ! Horizontal radius [m]
   XRADZ = 2000.,               ! Vertical radius [m]
   /

   ! Very high resolution uniform grid
   &NAM_VER_GRID
   YZGRID_TYPE = 'FUNCTN',
   ZDZGRD = 50.,                ! Uniform 50m vertical spacing
   ZDZTOP = 50.,
   LTHINSHELL = .TRUE.,         ! Thin shell correction
   /

   ! Physical viscosity
   &NAM_VISC
   LVISC = .TRUE.,               ! Enable viscosity
   LVISC_TH = .TRUE.,            ! Viscosity for theta
   LVISC_UVW = .TRUE.,           ! Viscosity for momentum
   XMU_V = 20.,                  ! Dynamic viscosity [m²/s]
   XPRANDTL = 1.,                ! Prandtl number
   /

   ! Small time step for stability
   &NAM_DYNn
   XTSTEP = 0.5,                ! 0.5 second time step
   /

   ! No physics - pure dynamics
   &NAM_PARAMn
   CTURB = "NONE",
   CRAD = "NONE",
   CCLOUD = "NONE",
   /

**Validation Targets** :

- Cold pool descent velocity
- Gravity wave generation
- Numerical stability at high resolution

**Execution** :

.. code-block:: bash

   cd integration_cases/local/COLD_BUBBLE
   make clean && make
   ./run_COLD_BUBBLE

**Numerical Resources** :

.. list-table::
   :header-rows: 1
   :widths: 40 60

   * - Configuration
     - Resources
   * - 2D (1024×1×128)
     - Single CPU, < 500 MB RAM, ~5 min
   * - Notes
     - Requires small time step (0.5s) for CFL stability

**References** :

- Straka, J. M., et al. (1993). "Numerical Solutions of a Nonhydrostatic Deep-Atmospheric Internal Gravity Wave." *Monthly Weather Review*, 121, 761-772. https://doi.org/10.1175/1520-0493(1993)121<0761:NSOAND>2.0.CO;2
