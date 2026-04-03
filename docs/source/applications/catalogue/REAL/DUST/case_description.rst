DUST - Saharan Dust Event
=============================================================

**Category** : Realistic  
**Objective** : Simulate Saharan dust transport and radiative effects

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 30 × 30 × 30
   * - Resolution
     - Dx=30000m, Dz=100m
   * - Simulation duration
     - 72 h
   * - Time step
     - 120 s
   * - Boundary conditions
     - OPEN (from IFS)
   * - Coriolis
     - Yes
   * - Advection
     - WENO5 + RKC4
   * - Turbulence
     - TKEL + 1D-BL89
   * - Surface
     - SURFEX
   * - Radiation
     - ECMW
   * - Microphysics
     - ICE3
   * - Convection
     - KAFR

**Scientific Context & Specificity** :

DUST is the **only dust/aerosol case** in the catalog. Its uniqueness:

- Tests **aerosol transport** parameterization
- Uses **Saharan** realistic surface
- Studies **dust-radiation** feedbacks

Unlike other realistic cases:

- All other cases focus on **hydrometeors**; DUST focuses on **aerosols**
- Tests **ORILAM** aerosol scheme
- Demonstrates **dust plume** modeling

The case simulates:
- Saharan dust emission
- Long-range transport
- Radiative impacts

**Technical Specificities** :

This case demonstrates Meso-NH's **aerosol modeling** with **ORILAM** coupling.

Key characteristics:

- ORILAM aerosol scheme
- Dust emission from SURFEX
- ECMW radiation coupling

**Validation Targets** :

- Dust optical depth
- Surface concentration
- Radiative forcing

**Execution** :

.. code-block:: bash

   cd integration_cases/...
   sbatch run_mesonh

**Numerical Resources** :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Nodes
     - 1
   * - Processors
     - 16
   * - Runtime
     - 10 hours
