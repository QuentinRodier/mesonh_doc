PANAME - Paris Metropolitan Area
=============================================================

**Category** : Realistic  
**Objective** : Simulate summer urban climate over Paris with TEB urban canopy

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 400 × 400 × 68
   * - Resolution
     - Dx=300m, Dz=4m
   * - Simulation duration
     - 24 h
   * - Time step
     - 5 s (1.7s fine)
   * - Boundary conditions
     - OPEN (from AROME)
   * - Coriolis
     - Yes
   * - Advection
     - WENO3 + RKC4
   * - Turbulence
     - TKEL + 1D/3D-HM21
   * - Surface
     - SURFEX + TEB
   * - Radiation
     - ECMW
   * - Microphysics
     - ICE3
   * - Convection shallow
     - EDKF

**Scientific Context & Specificity** :

PANAME is the **only urban climate case** in the catalog. Its uniqueness:

- Tests **TEB (Town Energy Balance)** urban canopy model
- Uses **Paris metropolitan** realistic terrain
- Studies **urban heat island** and **pollution dispersion**

Unlike other realistic cases:

- All other cases have **rural or ocean** surfaces; PANAME has **urban** surface
- Tests **TEB coupling** with atmospheric model
- Demonstrates **metropolitan-scale** modeling capability

The case simulates:
- Summer conditions over Paris
- Urban heat island effect
- Boundary layer evolution

**Technical Specificities** :

This case demonstrates Meso-NH's **urban climate modeling** with **TEB** urban canopy.

Key characteristics:

- Multi-resolution nesting (300m → 100m possible)
- TEB urban parameterization
- AROME lateral boundaries

**Validation Targets** :

- Urban heat island intensity
- Temperature distribution
- Wind channeling in streets

**Execution** :

.. code-block:: bash

   # Requires HPC
   # AROME initialization
   cd integration_cases/...
   sbatch run_mesonh

**Numerical Resources** :

.. list-table::
   :header-rows: 1
   :widths: 40 60

   * - Configuration
     - Resources
   * - PANAME 300m
     - 256 processors, ~20 GB RAM
   * - PANAME 100m
     - 512+ processors, ~40 GB RAM

**References** :

- Masson, V. (2000). "A Physically-Based Scheme for the Urban Energy Budget in Atmospheric Models." *Bound.-Layer Meteor.*, 94, 357-397. https://doi.org/10.1023/A:1002463829265
