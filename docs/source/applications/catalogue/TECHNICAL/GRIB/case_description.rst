GRIB - GRIB Data Interpolation
=============================================================

**Category** : Technical  
**Objective** : Test GRIB file reading and horizontal interpolation from IFS/AROME data

**Scientific Context & Specificity** :

GRIB is a **technical demonstration case** for data input. Its uniqueness:

- Tests **GRIB file reading** capabilities
- Validates **horizontal interpolation** from coarse to fine grid
- Demonstrates **PREP_IDEA** with external data

Unlike other technical cases:

- 16JAN tests **grid-nesting**; GRIB tests **data input pipeline**
- DOUBLE_GRIDNESTING tests **multi-domain coupling**; GRIB tests **data assimilation prep**
- Demonstrates **operational workflow** for real-case initialization

This case validates:
- GRIB API functionality
- Interpolation schemes (bilinear, bicubic)
- Vertical interpolation methods

**Technical Specificities** :

Key validation points:

- GRIB format support (GRIB1/GRIB2)
- Horizontal interpolation accuracy
- Vertical level mapping
- Missing value handling

**Execution** :

.. code-block:: bash

   cd integration_cases/...
   # Read GRIB and interpolate to Meso-NH grid
   ./run_prep_grib

**Numerical Resources** :

- **Architecture** : Local
- **Processors** : 1
- **Memory** : < 1 GB
- **Runtime** : < 5 minutes

**References** :

- ECMWF: https://confluence.ecmwf.int/display/UDOCK/GRIB+API+functions
