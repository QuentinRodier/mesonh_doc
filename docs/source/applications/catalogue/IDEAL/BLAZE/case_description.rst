BLAZE - Wildfire Spread (ForeFire)
=============================================================

**Category** : Idealized · Applicative  
**Objective** : Simulate wildfire spread using the ForeFire coupling system

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 100 × 50 × 30
   * - Resolution
     - Dx=25m, Dz=10m
   * - Simulation duration
     - 10 min (600 s)
   * - Time step
     - 1 s
   * - Boundary conditions
     - OPEN (X), OPEN (Y)
   * - Coriolis
     - No
   * - Advection
     - WENO_K (3rd order) + RK53 + PPM_01
   * - Turbulence
     - None
   * - Surface
     - ISBA (vegetation)
   * - Radiation
     - None
   * - Microphysics
     - None
   * - Convection
     - None
   * - Fire module
     - ForeFire (2-way coupling)

**Scientific Context & Specificity** :

BLAZE is the **only wildfire case** in the catalog. Its uniqueness:

- Tests **ForeFire coupling** for fire spread simulation
- Uses **WENO-K advection** for sharp gradients
- Models **fire-atmosphere feedbacks**

Unlike other applicative cases:

- All other cases model **atmospheric processes**; BLAZE models **fire spread**
- Uses **ISBA surface scheme** with vegetation
- Demonstrates **2-way coupling** between fire and atmosphere

The case simulates:
- Fire front propagation
- Heat release to atmosphere
- Wind-driven fire spread

**Technical Specificities** :

This case demonstrates Meso-NH's **ForeFire coupling** for **wildfire modeling**.

Key namelist sections:

.. code-block:: fortran

   ! ForeFire coupling
   &NAM_FIREn
   LBLAZE = .TRUE.,                 ! Enable ForeFire
   CFIRE_CPL_MODE = '2WAYCPL',    ! 2-way coupling
   NREFINX = 5,                     ! Refinement in X
   NREFINY = 5,                     ! Refinement in Y
   XFLXCOEFTMP = 0.1,              ! Heat flux coefficient
   /

   ! ISBA surface with vegetation
   &NAM_PGD_SCHEMES
   CNATURE = 'ISBA',               ! Surface scheme
   /

   ! WENO-K advection for sharp gradients
   &NAM_ADVn
   CUVW_ADV_SCHEME = 'WENO_K',    ! WENO-K scheme
   NWENO_ORDER = 3,                ! 3rd order
   CTEMP_SCHEME = 'RK53',          ! RK53 for stability
   /

   ! OPEN boundaries for fire plume
   &NAM_LBCn
   CLBCX = 2*"OPEN",
   CLBCY = 2*"OPEN",
   /

   ! No physics - fire-driven dynamics
   &NAM_PARAMn
   CTURB = "NONE",
   CRAD = "NONE",
   CCLOUD = "NONE",
   /

**Available Variants** :

.. code-block:: bash

   # Different surface configurations
   integration_cases/local/BLAZE/01_flat_2WC/    # Flat with 2WC
   integration_cases/local/BLAZE/02_flat_A2F/    # Flat A2F
   integration_cases/local/BLAZE/03_flat_F2A/    # Flat F2A

**Validation Targets** :

- Fire front propagation speed
- Heat release rate
- Fire-atmosphere coupling strength

**Execution** :

.. code-block:: bash

   cd integration_cases/local/BLAZE/01_flat_2WC
   make clean && make
   ./run_BLAZE

**Numerical Resources** :

- **Architecture** : Local (single CPU)
- **Processors** : 1
- **Memory** : < 500 MB
- **Runtime** : < 5 minutes

**References** :

- Mandel, J., et al. (2011). "Coupled Atmosphere-Fire Wildland Fire Model." *Int. J. Wildland Fire*, 20, 194-204. https://doi.org/10.1071/WF09082
