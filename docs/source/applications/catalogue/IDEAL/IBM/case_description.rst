IBM - Immersed Boundary Method
=============================================================

**Category** : Idealized · Applicative  
**Objective** : Simulate flow past complex geometries using the Immersed Boundary Method

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - Variable (60×400×10 to 1200×1200×150)
   * - Resolution
     - Dx=0.3-10m, Dz=0.3-10m
   * - Simulation duration
     - Variable (1250s to 100000s)
   * - Time step
     - 0.0175-2.5 s
   * - Boundary conditions
     - OPEN or WALL
   * - Coriolis
     - No
   * - Advection
     - WENO-K (5th order)
   * - Turbulence
     - TKEL + 3D-DELT/DEAR
   * - Surface
     - Ideal Flux (zero)
   * - Radiation
     - None
   * - Microphysics
     - None
   * - Convection
     - None
   * - IBM
     - Immersed Boundary Method

**Scientific Context & Specificity** :

IBM cases test the **Immersed Boundary Method** for flow past complex geometries. Their uniqueness:

- Tests **non-conforming grids** for obstacle modeling
- Uses **WENO-K** high-order advection for sharp gradients
- Studies **wall-bounded flows** and **obstacle wakes**

Available geometries:

- **CUBE** : Cube in a channel (validation)
- **CYLINDER** : Circular cylinder (Von Kármán vortex street)
- **ICIF_OBJ** : Industrial/civil engineering objects
- **MUST** : MUST project benchmark

Unlike other applicative cases:

- All other cases use **terrain-following** coordinates; IBM uses **Cartesian grid with IBM**
- Tests **high Reynolds number** flows past obstacles
- Requires **very fine resolution** near obstacles

**Technical Specificities** :

These cases demonstrate Meso-NH's **Immersed Boundary Method** capabilities.

Key namelist sections:

.. code-block:: fortran

   ! IBM activation
   &NAM_IBM_PARAMn
   LIBM = .TRUE.,                    ! Enable IBM
   LIBM_TROUBLE = .FALSE.,          ! Trouble shooting mode
   CIBM_ADV = 'LOWORD',            ! IBM advection
   XIBM_RUG = 6.24E-7,            ! Roughness [m]
   CIBM_FORC_BOUNT_V = 'WN3'      ! Body force method
   /

   ! WENO-K high-order advection
   &NAM_ADVn
   CUVW_ADV_SCHEME = 'WENO_K',    ! 5th order WENO
   NWENO_ORDER = 5,                ! 5th order
   LSPLIT_CFL = .TRUE.,           ! CFL-based splitting
   XSPLIT_CFL = 0.8,              ! CFL limit
   /

   ! Strict convergence
   &NAM_DYNn
   LRES = .TRUE.,                  ! Strict convergence
   XRES = 1.E-7,                 ! Convergence criterion
   NITR = 50,                     ! Max iterations
   /

   ! CYLINDER specific: WALL boundary
   &NAM_LBCn
   CLBCY = 2*"WALL",             ! WALL in Y
   /

**CUBE Configuration** :

- Domain: 640×160×41 grid points
- Resolution: 3.12 cm
- Duration: 1250 s
- Physics: Dry, no turbulence parameterization

**CYLINDER Configuration** :

- Domain: 60×400×10 grid points
- Resolution: 10 m
- Duration: 100 000 s
- Physics: Dry, viscosity enabled (XMU_V=8)

**MUST Configuration** :

- Domain: 1200×1200×40 grid points
- Resolution: 0.6 m / 0.3 m
- Duration: 150 s
- Physics: Dry, TKEL+DEAR turbulence

**Validation Targets** :

- Drag and lift coefficients
- Vortex shedding frequency
- Wake structure

**Execution** :

.. code-block:: bash

   # Requires HPC
   cd integration_cases/hpc/IBM/CUBE_FLUME_4
   sbatch run_mesonh

   cd integration_cases/hpc/IBM/CYLINDER
   sbatch run_mesonh

   cd integration_cases/hpc/IBM/MUST
   sbatch run_mesonh

**Numerical Resources** :

.. list-table::
   :header-rows: 1
   :widths: 40 60

   * - Configuration
     - Resources
   * - CUBE
     - 5 nodes, 480 processors, 24 hours
   * - CYLINDER
     - Check specific run script
   * - MUST
     - 15 nodes, 1600 processors, 3 hours

**References** :

- Mittal, R., and Iaccarino, G. (2005). "Immersed Boundary Methods." *Ann. Rev. Fluid Mech.*, 37, 239-261. https://doi.org/10.1146/annurev.fluid.37.082503.100959
- Gaitonde, D., and Visbal, M. (2001). "High-Order Schemes for Navier-Stokes Equations." *AIAA J.*, 39, 1770-1778.
