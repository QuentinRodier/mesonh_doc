RECYCLING - LES Recycling Technique
=============================================================

**Category** : Idealized · Technical (LES)  
**Objective** : Demonstrate the recycling technique for LES initialization

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Type
     - LES with recycling
   * - Turbulence
     - Explicit (LES mode)
   * - Recycling
     - Lateral boundary recycling

**Scientific Context & Specificity** :

RECYCLING demonstrates the **lateral boundary recycling technique** for LES. Its uniqueness:

- Tests **periodic-like** behavior in finite domains
- Uses **recycling planes** to maintain turbulence
- Studies **inflow turbulence** generation

Unlike other cases:

- All other cases use **standard boundaries**; RECYCLING uses **recycling technique**
- Tests **turbulence inflow** methods
- Demonstrates **LES setup** workflow

**Technical Specificities** :

Key namelist sections:

.. code-block:: fortran

   ! Recycling configuration
   &NAM_RECYCL_PARAMn
   LRECYCL = .TRUE.,             ! Enable recycling
   LRECYCLW = .TRUE.,           ! West boundary
   XDRECYCLW = 4.,             ! Recycling distance [m]
   LRECYCLN = .FALSE.,
   /
   &NAM_MEAN
   LMEAN_FIELD = .TRUE.,        ! Mean field computation
   /

**Validation Targets** :

- Turbulence stationarity
- Energy spectra
- Mean profiles
