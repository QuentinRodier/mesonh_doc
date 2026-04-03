BIOMAIDIO - Marine Biogeochemistry (La Réunion)
=============================================================

**Category** : Realistic  
**Objective** : Simulate marine aerosol and biogeochemistry around La Réunion

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Location
     - La Réunion island
   * - Resolution
     - Dx=2-8km
   * - Duration
     - 6h
   * - Turbulence
     - TKEL + 1D-BL89
   * - Microphysics
     - LIMA
   * - Chemistry
     - ORILAM (aerosols)

**Scientific Context & Specificity** :

BIOMAIDIO is the **only marine biogeochemistry case** in the catalog. Its uniqueness:

- Tests **marine aerosol** parameterization (sea-salt, DMS)
- Uses **La Réunion** realistic location
- Studies **biogeochemical** emissions and impacts

Unlike other realistic cases:

- DUST focuses on **Saharan** dust; BIOMAIDIO focuses on **marine** aerosols
- Tests **ORILAM** aerosol scheme
- Demonstrates **marine-atmosphere** coupling

**Technical Specificities** :

Key characteristics:

- ORILAM aerosol scheme
- Sea-salt emissions
- DMS (dimethyl sulfide) chemistry

**Validation Targets** :

- Sea-salt concentration
- DMS oxidation products
- Aerosol optical depth

**References** :

- CHARMEX project: https://charmex.lce.hypert止

**Numerical Resources** :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Nodes
     - 1
   * - Processors
     - 64
   * - Runtime
     - 4h 30min
