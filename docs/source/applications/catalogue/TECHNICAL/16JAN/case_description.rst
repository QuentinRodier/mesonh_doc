16JAN - January 16th Grid-Nesting Case
=============================================================

**Category** : Technical  
**Objective** : Demonstrate two-way grid-nesting (parent + child domains)

**Scientific Context & Specificity** :

16JAN is a **technical demonstration case** for grid-nesting. Its uniqueness:

- Tests **two-way nesting** between parent and child
- Validates **AROME/ARPEGE** data initialization
- Demonstrates **convection-permitting** nesting workflow

Unlike other technical cases:

- GRIB tests **data input**; 16JAN tests **nesting coupling**
- DOUBLE_GRIDNESTING uses **three domains**; 16JAN uses **two domains**
- Demonstrates **operational** nesting configuration

Domain structure:

- Coarse domain (36 km): from ARPEGE
- Fine domain (9 km): from AROME

**Technical Specificities** :

This case demonstrates Meso-NH's **grid-nesting** capabilities.

Key characteristics:

- Two-way coupling (XWAY = 1. or 2.)
- Temporal nesting ratio (NDTRATIO)
- Lateral boundary relaxation

**Validation Targets** :

- Nesting interpolation
- Upward and downward coupling
- Conservation

**Execution** :

.. code-block:: bash

   cd integration_cases/...
   # Run coarse domain first
   ./run_coarse
   # Then fine domain
   ./run_fine

**Numerical Resources** :

.. list-table::
   :header-rows: 1
   :widths: 40 60

   * - Configuration
     - Resources
   * - Coarse (36km)
     - 4-16 processors
   * - Fine (9km)
     - 32-64 processors
