SNOW_BLOW - Blowing Snow (3D)
=============================================================

**Category** : Idealized · Applicative  
**Objective** : Simulate 3D blowing snow plumes over complex terrain

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 60 × 60 × 70
   * - Resolution
     - Dx=50m, Dz=10m
   * - Simulation duration
     - 3 h (10 800 s)
   * - Time step
     - 1.5 s
   * - Boundary conditions
     - OPEN (X), OPEN (Y)
   * - Coriolis
     - No
   * - Advection
     - CEN4TH + RKC4
   * - Turbulence
     - TKEL + 3D-DEAR
   * - Surface
     - ISBA (snow)
   * - Radiation
     - FIXE (fixed)
   * - Microphysics
     - ICE3
   * - Convection
     - None

**Scientific Context & Specificity** :

SNOW_BLOW extends the 1D BLOWSNOW case to **3D with topography**. Its uniqueness:

- Tests **3D snow plume** formation
- Uses **realistic terrain** with ISBA
- Studies **topographic effects** on snow drift

Unlike other applicative cases:

- BLOWSNOW is **1D column**; SNOW_BLOW is **3D with terrain**
- FIRE focuses on **fire spread**; SNOW_BLOW focuses on **snow transport**
- Tests **3D turbulence** effects on particles

The case simulates:
- Snow accumulation patterns
- Drifting snow dunes
- Wind-snow interactions

**Technical Specificities** :

This case demonstrates Meso-NH's **3D blowing snow** capabilities with **terrain coupling**.

Key namelist sections:

.. code-block:: fortran

   ! ISBA snow surface scheme
   &NAM_PGD_SCHEMES
   CNATURE = 'ISBA',
   /

   ! Fixed radiation (simplified)
   &NAM_PARAMn
   CRAD = 'FIXE',               ! Fixed radiation
   CCLOUD = 'ICE3',            ! Ice microphysics
   /

   ! 3D turbulence with DEAR
   &NAM_TURBn
   CTURBDIM = "3DIM",
   CTURBLEN = "DEAR",
   XIMPL = 1.,
   /

   ! OPEN boundaries
   &NAM_LBCn
   CLBCX = 2*"OPEN",
   CLBCY = 2*"OPEN",
   /

   ! Horizontal relaxation at boundaries
   &NAM_DYNn
   LHORELAX_UVWTH = .TRUE.,
   LVE_RELAX = .TRUE.,
   /

**Validation Targets** :

- Snow accumulation patterns
- Plume structure
- Erosion/deposition rates

**Execution** :

.. code-block:: bash

   cd integration_cases/local/SNOW_BLOW
   ./run_mesonh

**Numerical Resources** :

- **Architecture** : Local or HPC
- **Processors** : 4-16
- **Memory** : ~1 GB
- **Runtime** : ~30 minutes
