.. index::
	single: Key Concepts

********
Concepts
********

.. index::
	single: MasterMap Framework
	see: Topographical identifier; TOID
	see: Fragment; TOID_Fragment_ID

.. _data_structure:

Data Components
===============

Due to the number and complexity of data attributes and the need to minimise data duplication and reduce data volumes the spatial data and attribute data are separated into separate components. The HLU Tool provides an interface that links the spatial and attribute data and presents them to the user as a single entity.

**Spatial Data**
The spatial data is stored in one or more GIS layers together with a minimal set of attributes that uniquely identifies and summarises each spatial feature. Separating the spatial data from the attribute data reduces the number of attributes required for the spatial layer which improves performance in the GIS application.

**Attribute Data**
The attribute data is stored in a relational database in a 'normalised' relational structure (i.e. groups of related attributes are divided into smaller, separate tables and relationships are defined between the tables). A normalised relational database enables the attributes to be retrieved and maintained in a very logical, and universal, way whilst simultaneously reducing the data storage requirements and improving the data structure and integrity.


.. _habitat_framework:

Habitat Framework
=================

Although most habitat surveys performed in the last 20 years are typically available as GIS layers, the spatial accuracy of the feature boundaries can be very variable. The quality will typically depend upon a range of factors, such as:

	* The quality of the original field survey maps and notes.
	* The scale and age of the base digital mapping.
	* The quality and age of any aerial photography layers.
	* The skill and patience of the GIS user digitising the data.

This variability can make it very difficult to combine habitat layers and to compare changes between surveys from different years. Moreover, unless the GIS user was very skilled or geospatial topology [2]_ was employed there will be overlaps and gaps between features which can bring problems when using the data in spatial or statistical queries.

.. [2] Geospatial topology is the arrangement for how point, line, and polygon features share geometry and is often used to define and enforce data integrity rules (e.g. no gaps should exist between polygons, there should be no overlapping features, etc).

One solution to these problems is to integrate all the habitat layers into a single framework based on Ordnance Survey's MasterMap dataset. MasterMap is the largest scale national mapping produced by the Ordnance Survey and provides highly detailed and seamless coverage.

All OS MasterMap features have a Topographic Identity or 'TOID' that uniquely identifies each object. OS MasterMap Topographic Area features also have a number of attributes (chiefly the Descriptive Group and Descriptive Term) that provide information about the real world object that the feature represents and these can provide basic habitat and land use information that can supplment any available habitat survey data.

Apart from the spatial representation of the features, the habitat framework only retains the TOID from OS MasterMap because all other attributes can be retrieved using this if necessary. Where OS MasterMap features need to be sub-divided into smaller units in order to represent habitat survey details that are not already shown these still retain the original TOID but are also assigned a fragment identifier so that each fragment can be uniquely identified.


.. _incid:

Incremental Identifier
======================

Every feature in the GIS layer, and associated attributes in the relational database, is assigned to an INCID (\ **Inc**\ remental **id**\ entifier). An INCID can be thought of as a logical grouping of features that share a common set of attributes and are spatially related (i.e. neighbouring or proximate) [3]_. Each INCID can relate to one or more features. Grouping features with common attributes in this way reduces the number of database records required and allows the features and their attributes to all be maintained together.

In order to amend the attributes for one or more features in a larger group of features (i.e. in the same INCID as other features) without updating the remaining features, the features must first be split into their own logical grouping - i.e. they must be assigned to a new INCID (see :ref:`logical_split` for more details.)

Similarly, features from different INCIDs that are actually related and should share the same common set of attributes can be merged into the same INCID (see :ref:`logical_merge` for more details.)

.. [3] Features in the same INCID do not have to be adjacent but it is recommended that they are at least spatially associated with one-another (e.g. they are within the same site or either side of the same road/railway).


.. raw:: latex

	\newpage

.. _priority_habitats:

Priority Habitats
=================

Some IHS Habitat and some multiplex codes (Formation, Management and Complex codes) are equivalent to, or more distinct than, priority habitats [4]_. When any such codes are selected in the main window :ref:`ihs_tab` the tool automatically adds the associated priority habitats to the 'Priority Habitats' section of the :ref:`details_tab`.

However, if priority habitat associated codes are changed or removed in the :ref:`ihs_tab` the tool does **not** automatically remove existing priority habitats from the 'Priority Habitats' section of the :ref:`details_tab`. Instead they are moved to the 'Potential Priority Habitats' section and the :ref:`determination_quality` is cleared.

.. note::
	Existing priority habitats that have been automatically moved to the 'Potential Priority Habitats' section but are no longer required must be deleted by the user (see :ref:`details_tab`.)

.. [4] Priority habitats are habitats identified as requiring action in the UK Biodiversity Action Plan (UK BAP) and continue to be regarded as conservation priorities in the UHS Post-2010 Biodiversity Framework.


.. _potential_priority_habitats:

Potential Priority Habitats
---------------------------

If a habitat area is close to, but does not currently meet, the definition of a priority habitat (but may do so with appropriate management or following habitat restoration work) then the appropriate priority habitat can be added to the 'Potential Priority Habitats' section of the :ref:`details_tab`.


.. _determination_quality:

Determination Quality
---------------------

Every priority habitat and potential priority habitat must be assigned a determination quality. This categorises the accuracy with which the priority habitat has been determined and can be very useful when there is not a direct translation between the IHS habitat or multiplex codes and the priority habitat, or when the original survey source(s) are not as spatially accurate as the OS MasterMap features in the framework and hence there is some uncertainty of the exact position of the priority habitat.

.. tabularcolumns:: |L|

.. table:: Determination Quality values

	+----------------------------------------------------------+
	|                  Determination Quality                   |
	+==========================================================+
	| Definitely is this habitat                               |
	+----------------------------------------------------------+
	| Habitat is in polygon, but not accurately mappable       |
	+----------------------------------------------------------+
	| Habitat probably in polygon, but not accurately mappable |
	+----------------------------------------------------------+
	| Probably is, but some uncertainty                        |
	+----------------------------------------------------------+
	| Not present but close to definition                      |
	+----------------------------------------------------------+


.. note::
	The Determination Quality 'Not present but close to definition' is only applicable for 'Potential Priority Habitats' and is the only Determination Quality available for 'Potential Priority Habitats'.


.. _interpretation_quality:

Interpretation Quality
----------------------

Every priority habitat and potential priority habitat must be assigned an interpretation quality. This is selected based on an assessment of the quality of the original habitat type and it's relationship between it and the priority habitat type and also the age of the original habitat source.

.. tabularcolumns:: |L|C|C|C|

.. table:: Interpretation Quality matrix for different survey types and ages

	+------------------------------------------+-----------------------------------------+
	|               Survey Type                | Age of Survey                           |
	|                                          +---------------+------------+------------+
	|                                          | < 5 years     | 5-10 years | > 10 years |
	+==========================================+===============+============+============+
	| NVC quadrat                              | High (1)      | Medium (2) | Medium (3) |
	+------------------------------------------+---------------+------------+------------+
	| NVC rapid                                | Medium (2)    | Medium (3) | Medium (4) |
	+------------------------------------------+---------------+------------+------------+
	| Phase 1 and target notes                 | Medium (3)    | Medium (4) | Low (5)    |
	+------------------------------------------+---------------+------------+------------+
	| Phase 1 map only                         | Low (5)       | Low (5)    | Low (6)    |
	+------------------------------------------+---------------+------------+------------+
	| ESA/ SSSI site description/ species list | Medium (3)    | Medium (3) | Medium (4) |
	+------------------------------------------+---------------+------------+------------+
	| Aerial Photo, Landcover                  | Low (5)       | Low (6)    | Low (7)    |
	+------------------------------------------+---------------+------------+------------+
	| Expert knowledge of site quality         | Medium (4)    | Medium (4) | Low (5)    |
	+------------------------------------------+---------------+------------+------------+


.. raw:: latex

	\newpage

.. _split:

Split Features
==============

Split features will perform two types of split depending upon the filter active in the tool. If one or more features from a single INCID are present in the current filter then the tool will perform a logical split. If two or more fragments from the same TOID and with the same TOID_Fragment_Id are present in the current filter then the tool will perform a physical split.

.. note::
	If two or more fragments from the same TOID and with the same TOID_Fragment_Id are selected in the GIS and **Get Map Selection** is clicked then the tool will recognise that the fragments must have been split by the user in the GIS layer and will **automatically** perform a physical split before displaying the attributes.

.. index::
	single: Split; Logical

.. _logical_split:

Logical Split
-------------

Logical split is used to create a new INCID in the database based upon a subset of features selected from a single INCID in the GIS layer. Logically splitting one or more features assigns them to a different INCID than the other features in the current INCID which then allows them to be updated independently of the remaining features in the original INCID.

For example, a group of adjacent permanent pasture features, each represented by a separate OS MasterMap feature, may be 'logically' grouped by being assigned to the same INCID because they share a common set of IHS codes, sources and other attributes. However, it may be discovered that one or more of the features are actually being managed differently to the remaining features. By logically splitting those features from the original INCID to form a new INCID those features can then be assigned a different IHS management code.

To display all the features in the INCID of a given feature:

* Select the feature of interest in the GIS layer.

	.. note::
		The selected features must all belong to the same INCID.

* Return to the HLU main window and click :guilabel:`Get Map Selection`.
* Click :guilabel:`Select Current INCID on Map`. All the features associated with the current INCID will be displayed as shown in the **left** part of the figure :ref:`figLSFD`.

.. _figLSFD:

.. figure:: figures/LogicalSplitDiagram.png
	:align: center

	Logical Split – Before (left) and After (right)


To perform a logical split:

* Select the subset of features to be split in the GIS layer as shown in the **right** part of the figure :ref:`figLSFD`.
* Return to the HLU main window and click :guilabel:`Get Map Selection`.
* Select one of the options in the 'Process' list.
* Click :guilabel:`Split Features`. A new INCID will be created and displayed as the current record.


.. raw:: latex

	\newpage

.. index::
	single: Split; Physical

.. _physical_split:

Physical Split
--------------

Physical split is use to create one or more new TOID fragments in the database based upon a single TOID that has already been split in the GIS layer. Physically splitting a feature into fragments allows the fragments to be updated independently of each other (once they have also been assigned to different INCIDs - see :ref:`logical_split`.)

For example, a woodland may appear in OS MasterMap as a single feature, but compartments within the woodland may be managed differently and/or may have different characteristics. By physically splitting the woodland feature along the compartment boundaries each compartment can then be assigned to it's own INCID (by performing a logical_split) so that they can be assigned different matrix, formation and management codes.

.. note::

	* Only one feature should be split in a single operation. Splitting multiple features will cause database synchronisation issues. 
	* If several features have been split, select the fragments for one original feature and split using the tool. Repeat this operation for the remaining features.
	* Ensure that the physical split is completed in the database prior to commencing any other operations such as 'Select by attributes …' to avoid database synchronisation issues.

ArcGIS
^^^^^^

To perform a physical split in ArGIS:

* On the 'Editor' toolbar (shown in the figure :ref:`figArcEMB`), click :guilabel:`Editor` and select :guilabel:`Start Editing`.

.. _figArcEMB:

.. figure:: figures/ArcGISEditMenuBar.png
	:align: center

	Edit Settings for Physical Split (ArcGIS)

* Select the feature to be split.
* On the 'Editor' toolbar, click :guilabel:`Cut Polygons Tool` draw a polyline through the feature to be split.

	.. tip::
		It is not necessary to **Save Edits** after splitting the feature in GIS because the changes will be saved automatically once the split has been completed with the tool.

* The feature will be split but still selected as shown in the figure :ref:`figArcSFD`. Return to the HLU GIS Tool and click :guilabel:`Get Map Selection`.

.. _figArcSFD:

.. figure:: figures/ArcGISSplitFeaturesDiagram.png
	:align: center

	Split Features (ArcGIS)

* Select one of the options in the 'Process' list.
* Click :guilabel:`Split Features`. The record will be updated and details added to the History tab for the INCID.


MapInfo
^^^^^^^

To perform a physical split in MapInfo:

* Set the Cosmetic layer as 'Editable' and draw the feature to split by.

.. tip::
	The Cosmetic layer should be used due to the time required for MapInfo to add a new feature to the full HLU layer.

* Set the HLU layer as 'Editable'.
* Select the feature to be split and go to Objects > Set Target.
* Select the polygon in the Cosmetic layer and go to Objects > Split.
* In the Data Disaggregation dialog ensure that 'Method' for all fields is set to 'Value' as shown in the figure :ref:`figMIDD`, then click :guilabel:`OK`.

.. _figMIDD:

.. figure:: figures/MapInfoDataDisaggregationDialog.png
	:align: center

	Data Disaggregation Dialog (MapInfo)

* The feature will be split but still selected as shown in the figure :ref:`figMISF`. Return to the HLU GIS Tool and click :guilabel:`Get Map Selection`.

.. _figMISF:

.. figure:: figures/MapInfoSplitFeaturesDiagram.png
	:align: center

	Split Features (MapInfo)

* Select one of the options in the 'Process' list.
* Click :guilabel:`Split Features`. The record will be updated and details added to the History tab for the INCID. The Cosmetic layer will be cleared.


.. _merge:

Merge Features
==============

Merge features will performs two types of merge depending upon the filter active in the tool. If two or more features from multiple INCIDs are present in the current filter then the tool will perform a logical merge. If two or more fragments from the same TOID and with different TOID_Fragment_Ids are present in the current filter then the tool will perform a physical merge.

.. index::
	single: Merge; Logical

.. _logical_merge:

Logical Merge
-------------

Logical merge combines all the features selected in the GIS into a single INCID chosen from from the selected features. This assigns the attributes from the chosen INCID to all the other selected features and logically groups the features into a single INCID so that they can be updated together in the future.

To perform a logical merge:

* Select the features to be merged and a feature from the INCID they are to be merged with in the GIS layer.
* Return to the HLU main window and click :guilabel:`Get Map Selection`.
* Select one of the options in the 'Process' list.
* Click :guilabel:`Merge Features`. A list of INCIDs will be displayed as shown in the figure :ref:`figLMD`.

.. _figLMD:

.. figure:: figures/LogicalMergeDialog.png
	:align: center

	Select INCID to Keep Dialog

* Click on the grey box to the left of the row to select an INCID. The associated feature will blink in the GIS window. Click :guilabel:`OK`.
* The selected features will be assigned to the selected INCID and details added to the History tab.
* If the merged features are fragments of the same TOID the user will be given the option to then perform a physical merge.

.. index::
	single: Merge; Physical

.. _physical_merge:

Physical Merge
--------------

Physical merge combines fragments of a single TOID into a single, larger, feature in the GIS layer. As the fragments must already belong to the same INCID there are no attribute updates but the boundaries between adjacent features will be removed.

To perform a physical merge:

* Select two or more fragments from one TOID in the GIS layer as shown in the **left** part of the figure :ref:`figPMD`.
* Return to the HLU main window and click :guilabel:`Get Map Selection`.
* Select one of the options in the 'Process' list.
* Click :guilabel:`Merge Features`. The features will be combined in the GIS layer as shown in the **right** part of the figure :ref:`figPMD`.

.. _figPMD:

.. figure:: figures/PhysicalMergeDiagram.png
	:align: center

	Physical Merge – Before (left) and After (right)


.. note::
	Only fragments belonging to the same TOID can be merged in a single operation. If fragments for several TOIDs need to be merged, the operation must be repeated for each TOID.



.. raw:: latex

	\newpage

.. index::
	single: Attribute Updates

.. _attribute_updates:

Attribute Updates
=================

Attribute Updates are the main mechanism for updating existing INCID details.

To update the attributes of an INCID:

* Ensure that the active HLU GIS layer is editable (for ArcGIS users click :guilabel:`Editor` on the Editor toolbar, select :guilabel:`Start Editing` and choose the active HLU layer, for MapInfo users set the active HLU layer as 'Editable').
* Select the feature or features to be updated.
* Click :guilabel:`Get Map Selection`.
* Make the required changes to the INCID attributes, ensuring that any fields highlighted as missing or in error are addressed.
* Click :guilabel:`Apply`. The INCID will be updated and details will be added to the History tab.


..note::
	The :guilabel:`Apply` button will only be displayed if:
		* The user is listed in the lut_user table.
		* The active GIS layer is in edit mode.
		* The user has made one or more changes to the current INCID.
		* There are no fields in error.

.. caution::
	If changes are made to an INCID and applied when only a subset of the TOIDs or fragments for that INCID are selected in GIS the user may be notified (depending upon their user Options) as shown in the figure :ref:`figAUWD`. See :ref:`interface_options` for more details.

.. _figAUWD:

.. figure:: figures/AttributeUpdateWarningDialog.png
	:align: center

	Attribute Update Warning Dialog

