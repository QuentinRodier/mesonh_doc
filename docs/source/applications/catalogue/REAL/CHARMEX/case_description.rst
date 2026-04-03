CHARMEX - Chemistry and Mediterranean EXperiment
=============================================================

**Category** : Realistic  
**Objective** : Simulate Mediterranean chemistry with biogenic emissions

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Location
     - Mediterranean basin
   * - Resolution
     - Dx=50km
   * - Duration
     - 12h
   * - Turbulence
     - TKEL + 1D-BL89
   * - Microphysics
     - LIMA
   * - Convection
     - KAFR (deep)
   * - Chemistry
     - REPROCIS (isoprene, BVOC)

**Scientific Context & Specificity** :

CHARMEX is the **only Mediterranean chemistry case** in the catalog. Its uniqueness:

- Tests **biogenic VOC** emissions (isoprene, monoterpenes)
- Uses **Mediterranean** realistic configuration
- Studies **photochemical** pollution events

Unlike other realistic cases:

- DUST focuses on **mineral dust**; CHARMEX focuses on **biogenic** chemistry
- Tests **REPROCIS** gas-phase chemistry
- Demonstrates **Mediterranean** specific chemistry

**Technical Specificities** :

Key characteristics:

- REPROCIS chemistry scheme
- MEGAN biogenic emissions
- ECRAD radiation coupling

**Validation Targets** :

- Ozone episodes
- Isoprene concentrations
- SOA formation

**References** :

- CHARMEX project documentation: https://charmex.lce.hypert止

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
     - 3h 20min
