BLOWSNOW_c1b1D - Blowing Snow (1D Column)
=============================================================

**Category** : Idealized · Applicative  
**Objective** : Simulate blowing snow saltation and suspension

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 1 × 1 × 70
   * - Resolution
     - Dx=10000m, Dz=6m
   * - Simulation duration
     - 20 min (1 200 s)
   * - Time step
     - 0.5 s
   * - Boundary conditions
     - CYCL (X), CYCL (Y)
   * - Coriolis
     - No
   * - Advection
     - CEN4TH (implicit)
   * - Turbulence
     - TKEL + 1D-BL89
   * - Surface
     - ISBA (snow)
   * - Radiation
     - None
   * - Microphysics
     - None
   * - Snow transport
     - Saltation + suspension

**Scientific Context & Specificity** :

BLOWSNOW_c1b1D is the **only snow transport case** in 1D. Its uniqueness:

- Tests **snow saltation and suspension** physics
- Uses **ISBA snow** surface scheme
- Studies **particle-to-fluid coupling**

Unlike other applicative cases:

- All other cases model **atmospheric processes**; BLOWSNOW models **snow transport**
- Uses **1D turbulence** for column simulation
- Tests **surface-atmosphere coupling** with snow

The case simulates:
- Snow particle trajectories
- Saltation layer dynamics
- Suspension in turbulent flow

**Technical Specificities** :

This case demonstrates Meso-NH's **snow transport** capabilities using **ISBA snow scheme**.

Key namelist sections:

.. code-block:: fortran

   ! ISBA snow surface scheme
   &NAM_PGD_SCHEMES
   CNATURE = 'ISBA',
   /

   ! 1D turbulence (column)
   &NAM_TURBn
   CTURBDIM = "1DIM",
   CTURBLEN = "BL89",
   XIMPL = 1.,
   /

   ! Implicit advection (stability)
   &NAM_ADVn
   CUVW_ADV_SCHEME = 'CEN4TH',
   /

   ! Short time step (fast dynamics)
   &NAM_DYNn
   XTSTEP = 0.5,               ! 0.5 second time step
   /

   ! Periodic boundaries
   &NAM_LBCn
   CLBCX = 2*"CYCL",
   CLBCY = 2*"CYCL",
   /

**Validation Targets** :

- Snow flux profiles
- Saltation height
- Suspension fraction

**Execution** :

.. code-block:: bash

   cd integration_cases/local/BLOWSNOW_c1b1D
   ./run_mesonh

**Numerical Resources** :

- **Architecture** : Local (single CPU)
- **Processors** : 1
- **Memory** : < 100 MB
- **Runtime** : < 1 minute

**References** :

- Pomeroy, J. W., and Gray, D. M. (1995). "Snowcover Accumulation, Relocation and Management." *Nat. Hydrol. Res. Inst. Sci. Rep.*, 7, 85-92.
