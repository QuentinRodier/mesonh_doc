DOUBLE_GRIDNESTING - Multi-Domain Grid Nesting
=============================================================

**Category** : Technical  
**Objective** : Demonstrate two-way grid-nesting with two child domains

**Scientific Context & Specificity** :

DOUBLE_GRIDNESTING is a **technical demonstration case** for multi-domain coupling. Its uniqueness:

- Tests **two-way nesting** with **two child domains**
- Validates **interpolation** between parent and children
- Demonstrates **complex nesting** workflows

Unlike other technical cases:

- 16JAN uses **2 domains** (1 parent + 1 child); DOUBLE_GRIDNESTING uses **3 domains** (1 parent + 2 children)
- GRIB tests **data input**; DOUBLE_GRIDNESTING tests **domain coupling**
- Demonstrates **large-eddy** to **convection-permitting** nesting

Domain structure:

- Domain 1 (coarse): ~9 km resolution
- Domain 2 (medium): ~3 km resolution
- Domain 3 (fine): ~1 km resolution

**Technical Specificities** :

Key namelist sections:

.. code-block:: fortran

   ! Grid nesting configuration
   &NAM_NESTING
   NDAD(1) = 0,                 ! Domain 1: parent (no dad)
   NDAD(2) = 1,                 ! Domain 2: child of 1
   NDAD(3) = 1,                 ! Domain 3: child of 1 (not 2)
   NDTRATIO(1) = 3,            ! Ratio 1→2: 3
   NDTRATIO(2) = 3,            ! Ratio 1→3: 3
   XWAY(1) = 1.,               ! Two-way coupling
   XWAY(2) = 1.,
   /

**Validation Targets** :

- Nesting interpolation quality
- Two-way feedback strength
- Conservation properties

**Execution** :

.. code-block:: bash

   cd integration_cases/...
   # Run parent first, then children
   ./run_parent
   ./run_child1
   ./run_child2

**Numerical Resources** :

.. list-table::
   :header-rows: 1
   :widths: 40 60

   * - Configuration
     - Resources
   * - All domains
     - 64+ processors total
   * - Memory
     - ~8-16 GB total

**References** :

- Meso-NH documentation: Grid-nesting chapter
