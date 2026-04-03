Reunion - Tropical Island Convection
=============================================================

**Category** : Idealized · Academic (Orography)  
**Objective** : Simulate tropical island convection over La Réunion

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Type
     - 3D with real orography (La Réunion)
   * - Resolution
     - Dx~1.5km
   * - Turbulence
     - TKEL + 1D-BL89
   * - Radiation
     - FIXE or ECMW
   * - Microphysics
     - Variable

**Scientific Context & Specificity** :

Reunion simulates **tropical island convection** over La Réunion volcano. Its uniqueness:

- Tests **realistic orography** from PGD file
- Uses **volcanic island** geometry (Piton de la Fournaise)
- Studies **orographic triggering** of convection

Unlike other cases:

- 2Drelief/3Drelief use **idealized** mountains; Reunion uses **real** orography
- Tests **island-scale** circulations
- Validates **orographic convection parameterization**

**Technical Specificities** :

Key characteristics:

- Real PGD from physiographic database
- Piton de la Fournaise volcano
- Trade wind environment

**Validation Targets** :

- Orographic precipitation patterns
- Island wake effects
- Cloud formation on slopes
