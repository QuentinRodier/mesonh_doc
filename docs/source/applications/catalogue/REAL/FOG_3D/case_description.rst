FOG_3D - Paris Fog Event
=============================================================

**Category** : Realistic  
**Objective** : Simulate radiation fog formation over Paris (February 2009)

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 300 × 300 × 34
   * - Resolution
     - Dx=500m, Dz=0.25m (very fine near surface)
   * - Simulation duration
     - 12 h
   * - Time step
     - 4 s
   * - Boundary conditions
     - OPEN (from AROME)
   * - Coriolis
     - Yes
   * - Advection
     - CEN4TH + RKC4
   * - Turbulence
     - TKEL + 1D-BL89
   * - Surface
     - SURFEX + TEB
   * - Radiation
     - ECMW/ECRAD
   * - Microphysics
     - ICE3/LIMA
   * - Convection
     - None

**Scientific Context & Specificity** :

FOG_3D is the **only fog case** in the catalog. Its uniqueness:

- Tests **very high vertical resolution** near surface (0.25m)
- Uses **Paris** realistic terrain
- Studies **radiation fog** formation mechanism

Unlike other realistic cases:

- All other cases focus on **convective systems**; FOG focuses on **stable conditions**
- Tests **ECRAD radiation** scheme
- Demonstrates **urban fog** modeling

The case simulates:
- Nighttime radiative cooling
- Fog onset and evolution
- Urban impacts on visibility

**Technical Specificities** :

This case demonstrates Meso-NH's **fog modeling** with **very high resolution** near surface.

Key characteristics:

- Stretched vertical grid (0.25m near surface)
- AROME initialization
- ECRAD radiation scheme

**Validation Targets** :

- Fog onset timing
- Visibility reduction
- Fog depth and extent

**Execution** :

.. code-block:: bash

   cd integration_cases/...
   sbatch run_mesonh

**Numerical Resources** :

- **Architecture** : HPC required
- **Processors** : 128+
- **Memory** : ~8 GB
- **Runtime** : ~2-3 hours
