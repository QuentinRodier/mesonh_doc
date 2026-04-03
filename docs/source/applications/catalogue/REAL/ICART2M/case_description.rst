ICART2M - Intensive Cloud And Radiation Testbed
=============================================================

**Category** : Realistic  
**Objective** : Cloud and radiation interactions over land

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Location
     - Southwestern France
   * - Resolution
     - Dx=2.5-15km
   * - Duration
     - 3h
   * - Turbulence
     - TKEL + 1D-BL89
   * - Microphysics
     - ICE3
   * - Convection
     - EDKF (shallow), KAFR (deep)
   * - Radiation
     - ECMW

**Scientific Context & Specificity** :

ICART2M is a **cloud-radiation testbed** case. Its uniqueness:

- Tests **cloud-radiation** interactions
- Uses **Southwest France** configuration
- Studies **boundary layer** cloud processes

Unlike other realistic cases:

- FOG focuses on **fog**; ICART focuses on **boundary layer clouds**
- Tests **ECMW radiation** coupling
- Demonstrates **continental** cloud modeling

**Technical Specificities** :

Key characteristics:

- IFS initialization
- Multi-resolution nesting (15km → 2.5km)
- ECMW radiation scheme

**Validation Targets** :

- Cloud fraction evolution
- Radiative fluxes
- Cloud optical properties

**References** :

- ICART campaign documentation

**Numerical Resources** :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Nodes
     - 1
   * - Processors
     - 4
   * - Runtime
     - 1 hour
