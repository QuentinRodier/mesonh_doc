CYCLONE - Tropical Cyclone
=============================================================

**Category** : Realistic (Semi-Idealized)  
**Objective** : Simulate tropical cyclone structure and dynamics

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 240 × 240 × 70
   * - Resolution
     - Dx=4000m, Dz=25m
   * - Simulation duration
     - 48 h
   * - Time step
     - 5 s
   * - Boundary conditions
     - OPEN (idealized)
   * - Coriolis
     - Yes
   * - Advection
     - CEN4TH + RKC4
   * - Turbulence
     - TKEL + 1D-BL89
   * - Surface
     - SURFEX (ocean)
   * - Radiation
     - ECMW
   * - Microphysics
     - ICE3
   * - Convection
     - KAFR

**Scientific Context & Specificity** :

CYCLONE is the **only tropical cyclone case** in the catalog. Its uniqueness:

- Tests **axisymmetric vortex** dynamics
- Uses **semi-idealized** configuration (realistic physics, idealized BC)
- Studies **cyclone structure** and **intensity changes**

Unlike other realistic cases:

- All other cases use **real data** initialization; CYCLONE uses **idealized vortex**
- Tests **ocean coupling** effects
- Demonstrates **hurricane-scale** modeling

The case simulates:
- Mature tropical cyclone
- Eyewall dynamics
- Spiral rainbands

**Technical Specificities** :

This case demonstrates Meso-NH's **tropical cyclone** modeling capabilities.

Key characteristics:

- Initial vortex from analytical formulation
- OPEN boundaries with relaxation
- KAFR convection scheme

**Validation Targets** :

- Minimum central pressure
- Maximum wind speed
- Eye/eyewall structure

**Execution** :

.. code-block:: bash

   # Semi-idealized setup
   cd integration_cases/...
   sbatch run_mesonh

**Numerical Resources** :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Nodes
     - 24
   * - Processors
     - 768
   * - Runtime
     - 4 hours
