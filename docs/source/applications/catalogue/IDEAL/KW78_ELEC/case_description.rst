KW78_ELEC - Kleinholtz 1978 Electrical Charging
=============================================================

**Category** : Idealized · Academic (Electrification)  
**Objective** : Simulate thunderstorm electrification using non-inductive charging

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Type
     - 2D thunderstorm with electrification
   * - Microphysics
     - ICE3 or LIMA
   * - Electrification
     - Non-inductive charging (ELE4)
   * - Lightning
     - Flash detection

**Scientific Context & Specificity** :

KW78_ELEC is based on the **Kleinholtz 1978** laboratory experiments on ice collision charging. Its uniqueness:

- Tests **non-inductive charging** mechanisms in thunderstorms
- Uses **ELE4** electrification scheme
- Studies **charge structure** and **lightning initiation**

Unlike other cases:

- STERAO is **3D**; KW78 is **2D**
- Tests **non-inductive charging** physics
- Validates **electrification parameterizations**

**Technical Specificities** :

Key namelist sections:

.. code-block:: fortran

   ! Electrification scheme
   &NAM_PARAMn
   CCLOUD = 'ICE3',
   CELEC = 'ELE4',
   /

   ! Electric module
   &NAM_ELEC
   LINDUCTIVE = .FALSE.,
   CNI_CHARGING = 'TAKAH',
   /

**Validation Targets** :

- Charge distribution
- Electric field profiles
- Lightning frequency

**References** :

- Takahashi, T. (1978). "Riming Electrification as a Charge Generation Mechanism in Thunderstorms." *J. Atmos. Sci.*, 35, 1536-1548.

**Numerical Resources** :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Value
   * - Nodes
     - 1
   * - Processors
     - 8
   * - Runtime
     - 2 hours
