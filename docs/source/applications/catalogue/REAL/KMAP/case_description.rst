KMAP - K產品 MAP (Korea)
=============================================================

**Category** : Realistic  
**Objective** : Convection-permitting simulation over East Asia

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Location
     - East Asia (Korea)
   * - Resolution
     - Dx=2-32km (3 nests)
   * - Duration
     - 12h
   * - Turbulence
     - TKEL + 1D-BL89
   * - Microphysics
     - ICE3
   * - Convection
     - KAFR (deep)
   * - Radiation
     - ECRAD

**Scientific Context & Specificity** :

KMAP is a **convection-permitting** case for East Asia. Its uniqueness:

- Tests **convection-permitting** resolution (2km)
- Uses **Korean** location and IFS data
- Studies **mesoscale convective systems**

Unlike other realistic cases:

- All other cases focus on **Europe**; KMAP focuses on **East Asia**
- Tests **ECRAD radiation** scheme
- Demonstrates **multi-scale** nesting (32→8→2km)

**Technical Specificities** :

Key characteristics:

- Triple nesting (32km → 8km → 2km)
- IFS initialization
- ECRAD radiation

**Validation Targets** :

- Convective initiation
- Precipitation patterns
- Cloud structure

**References** :

- KMAP project documentation
