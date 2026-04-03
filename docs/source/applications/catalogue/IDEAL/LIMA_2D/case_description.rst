LIMA_2D - 2-Moment Microphysics
=============================================================

**Category** : Idealized · Academic (Microphysics)  
**Objective** : Test LIMA 2-moment microphysics scheme in 2D

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Type
     - 2D deep convection
   * - Microphysics
     - LIMA (2-moment)
   * - Turbulence
     - TKEL + 1D/3D

**Scientific Context & Specificity** :

LIMA_2D is a **validation case for LIMA** (Liquid Ice Multiple Aerosols) 2-moment microphysics. Its uniqueness:

- Tests **2-moment microphysics** (mass + number concentration)
- Uses **LIMA** scheme with prognostic droplet spectra
- Studies **aerosol effects** on clouds

Unlike other cases:

- BOMEX/ARMCU use **bulk** microphysics (ICE3); LIMA uses **2-moment**
- Tests **CCN activation** and **droplet spectral evolution**
- Validates **aerosol-cloud interactions**

**Technical Specificities** :

Key namelist sections:

.. code-block:: fortran

   ! LIMA 2-moment microphysics
   &NAM_PARAMn
   CCLOUD = 'LIMA',
   /
   &NAM_PARAM_LIMA
   NMOM_C = 2,                  ! 2-moment for cloud
   NMOM_R = 2,                  ! 2-moment for rain
   HPARAM_CCN = 'CPB',
   /

**Validation Targets** :

- Droplet spectra evolution
- CCN activation spectra
- Precipitation formation

**References** :

- Khairoutdinov, M., and Kogan, Y. (2000). "A New Cloud Physics Parameterization in a Large-Eddy Simulation Model." *Mon. Wea. Rev.*, 128, 229-243.
