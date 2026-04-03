STATIONS_PROF_BALLOON_AIRCR_4doms - Multi-Platform Observations
=============================================================

**Category** : Technical  
**Objective** : Demonstrate I/O for stations, profilers, balloons, and aircraft observations

**Scientific Context & Specificity** :

STATIONS_PROF_BALLOON_AIRCR_4doms is a **technical demonstration case** for observation I/O. Its uniqueness:

- Tests **4 domain configurations** with observation networks
- Validates **observation extraction** from model output
- Demonstrates **multi-platform** data handling (stations, profilers, balloons, aircraft)

Unlike other technical cases:

- All other cases test **model physics**; this tests **I/O systems**
- Demonstrates **data assimilation prep** workflow
- Tests **observation operator** capabilities

Observation platforms:

- Surface stations (SYNOP, AWS)
- Wind profilers (U/V wind profiles)
- Radiosondes (balloons)
- Aircraft (AMDAR)

**Technical Specificities** :

Key I/O features tested:

- NETCDF output format
- Observation extraction routines
- Time interpolation
- Spatial interpolation

**Validation Targets** :

- Output format compliance
- Interpolation accuracy
- Complete metadata

**Execution** :

.. code-block:: bash

   cd integration_cases/...
   # Run simulation
   ./run_mesonh
   # Extract observations
   ./extract_obs

**Numerical Resources** :

- **Architecture** : Local or HPC
- **Processors** : 1-4
- **Memory** : < 1 GB
- **Runtime** : < 1 hour
