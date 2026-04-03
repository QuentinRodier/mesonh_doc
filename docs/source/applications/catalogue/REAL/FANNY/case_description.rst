FANNY - Mediterranean Flash Flood
=============================================================

**Category** : Realistic  
**Objective** : Simulate the September 2008 Mediterranean flash flood event

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 250 × 225 × 40
   * - Resolution
     - Dx=2500m, Dz=72m
   * - Simulation duration
     - 24 h
   * - Time step
     - 10 s
   * - Boundary conditions
     - OPEN (from AROME)
   * - Coriolis
     - Yes
   * - Advection
     - WENO5 + RKC4
   * - Turbulence
     - TKEL + 1D-BL89
   * - Surface
     - SURFEX (real terrain)
   * - Radiation
     - ECMW
   * - Microphysics
     - ICE3/LIMA
   * - Convection deep
     - KAFR

**Scientific Context & Specificity** :

FANNY is the **only Mediterranean flash flood case** in the catalog. Its uniqueness:

- Tests **deep convection** parameterization (KAFR)
- Uses **Mediterranean** realistic terrain
- Studies **orographic precipitation** mechanisms

Unlike other realistic cases:

- BOMEX/ARMCU are **idealized**; FANNY is **real event**
- Tests **convective system** life cycle
- Demonstrates **high-impact weather** modeling

The event:
- September 3, 2008 Mediterranean event
- Heavy precipitation over southeastern France
- Flash flooding in Gard region

**Technical Specificities** :

This case demonstrates Meso-NH's **deep convection** and **orographic precipitation** capabilities.

Key characteristics:

- AROME initialization and lateral boundaries
- KAFR convective scheme
- LIMA microphysics option

**Validation Targets** :

- Precipitation accumulation
- Convective system evolution
- Flash flood trigger

**Execution** :

.. code-block:: bash

   # Requires HPC
   cd integration_cases/...
   sbatch run_mesonh

**Numerical Resources** :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Nodes
     - 10
   * - Processors
     - 320
   * - Runtime
     - 4 hours
