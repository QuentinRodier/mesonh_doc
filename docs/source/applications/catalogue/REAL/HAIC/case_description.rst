HAIC - High Altitude Ice Clouds (Guyana)
=============================================================

**Category** : Realistic  
**Objective** : Simulate deep convection and ice clouds over Guyana

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 360 × 250 × 70
   * - Resolution
     - Dx=2500m, Dz=30m
   * - Simulation duration
     - 24 h
   * - Time step
     - 10 s
   * - Boundary conditions
     - OPEN (from AROME)
   * - Coriolis
     - Yes
   * - Advection
     - CEN4TH + RKC4
   * - Turbulence
     - TKEL + 1D-BL89
   * - Surface
     - SURFEX
   * - Radiation
     - ECMW/ECRAD
   * - Microphysics
     - ICE3/LIMA
   * - Convection shallow
     - EDKF

**Scientific Context & Specificity** :

HAIC is the **only Guyana/South America case** in the catalog. Its uniqueness:

- Tests **tropical deep convection** parameterization
- Uses **Guyana** realistic terrain
- Studies **high ice clouds** and cirrus anvils

Unlike other realistic cases:

- All other cases focus on **European** weather; HAIC focuses on **tropical** convection
- Tests **ECRAD radiation** coupling
- Demonstrates **tropical meteorology** modeling

The case simulates:
- Tropical convective systems
- Ice cloud anvils
- Mesoscale organization

**Technical Specificities** :

This case demonstrates Meso-NH's **tropical convection** modeling capabilities.

Key characteristics:

- AROME initialization
- ECRAD radiation scheme
- EDKF shallow convection

**Validation Targets** :

- Convective onset time
- Cloud top heights
- Precipitation patterns

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
     - 8
   * - Processors
     - 1024
   * - Runtime
     - 5 hours
