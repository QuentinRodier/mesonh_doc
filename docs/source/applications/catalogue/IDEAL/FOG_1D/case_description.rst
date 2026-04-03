FOG_1D - Radiation Fog (1D Column)
=============================================================

**Category** : Idealized · Boundary Layer (Fog)  
**Objective** : Simulate radiation fog formation in 1D column

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Dimensions (X×Y×Z)
     - 1 × 1 × variable
   * - Resolution
     - Dx=variable, Dz=variable (fine near surface)
   * - Simulation duration
     - ~12-24h
   * - Turbulence
     - TKEL + 1D-BL89
   * - Radiation
     - ECMW or ECRAD
   * - Microphysics
     - ICE3/LIMA

**Scientific Context & Specificity** :

FOG_1D is the **1D counterpart to FOG_3D**. Its uniqueness:

- Tests **radiation fog** physics in simple 1D setup
- Uses **high vertical resolution** near surface
- Studies **fog onset** and **stratus-to-fog transition**

Unlike other cases:

- FOG_3D is **3D** with realistic terrain; FOG_1D is **column**
- BOMEX/ARMCU focus on **convective** BL; FOG focuses on **stable** conditions
- Tests **radiation cooling** effects

**Technical Specificities** :

Key characteristics:

- Stretched vertical grid (fine near surface)
- ECMW/ECRAD radiation
- ICE3 or LIMA microphysics

**Validation Targets** :

- Fog liquid water content
- Visibility reduction
- Surface temperature evolution

**References** :

- Duynkerke, P. G. (1991). "Radiation Fog: A Comparison of Model Results with Observations." *Bound.-Layer Meteor.*, 54, 221-246.
