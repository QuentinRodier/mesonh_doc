AZF_2M - Toulouse Industrial Explosion
=============================================================

**Category** : Realistic  
**Objective** : Simulate the AZF chemical plant explosion in Toulouse (September 21, 2001)

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 120 × 90 × 40
   * - Resolution
     - Dx=500m, Dz=72m
   * - Simulation duration
     - 1 h
   * - Time step
     - 2 s
   * - Boundary conditions
     - OPEN
   * - Coriolis
     - Yes
   * - Advection
     - CEN4TH + RKC4
   * - Turbulence
     - TKEL + 1D-BL89
   * - Surface
     - SURFEX (real terrain)
   * - Radiation
     - ECMW
   * - Microphysics
     - ICE3
   * - Convection shallow
     - EDKF

**Scientific Context & Specificity** :

AZF_2M is the **only industrial accident case** in the catalog. Its uniqueness:

- Tests **explosion dynamics** and **overpressure propagation**
- Uses **realistic terrain** from Toulouse region
- Studies **urban impacts** of industrial hazards

Unlike other realistic cases:

- All other cases model **natural phenomena**; AZF models **anthropogenic explosion**
- Tests **SURFEX coupling** with urban areas
- Demonstrates **emergency response** simulation capability

The event:
- AZF plant explosion (September 21, 2001)
- 31 casualties, significant urban damage
- Pressure wave propagation

**Technical Specificities** :

This case demonstrates Meso-NH's capability for **hazard assessment** and **urban impact modeling**.

Key characteristics:

- Realistic PGD with urban areas
- ECMW radiation coupling
- SURFEX surface schemes

**Validation Targets** :

- Overpressure distribution
- Damage patterns
- Timeline of pressure wave

**Execution** :

.. code-block:: bash

   # Requires HPC for full simulation
   # Initialization from IFS analysis
   cd integration_cases/...

**Numerical Resources** :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Nodes
     - 1
   * - Processors
     - 8
   * - Runtime
     - 2 hours

**References** :

- Documentation of the AZF accident: https://www.irsn.fr
