.. index::
	single: Running the tool

****************
Running the tool
****************

The operation of the Data Searches tool is explained in this section. While the interface is similar between the ArcGIS and MapInfo implementations of the tool, there are some differences. These are pointed out where relevant throughout this document.

As discussed in the :doc:`Setting up the tool <../setup/setup>` section, the Data Searches tool is operated from a GIS project file within which the data required to run the tool is already loaded. It also relies on an optional Access database with details about the searches, and a configuration document. Therefore, before running the tool, ensure the following conditions are met:

- A GIS document has been created which contains both the search sites layer(s) and the data layers describing protected sites and species that will be queried, as required. 
- Where applicable, an Access database exists that contains the relevant information about the searches, in the correct tables and formats.
- The search sites layer(s) have a column that contains the unique reference for each search, and this reference has the correct format.
- The XML configuration document has been set up correctly, both for general settings and for each individual layer that will be queried. It is named correctly. For ArcGIS, both the launch configuration and a profile configuration have been set up.
- The Data Searches tool has been installed and set up.

.. seealso::
	Please refer to the :doc:`setup <../setup/setup>` section for further information about any of these requirements.


.. raw:: latex

   \newpage

.. index::
	single: Opening the form

Opening the form
================

To open the Data Searches tool in ArcGIS, click on the **Data Searches tool** button (:numref:`figLaunchArcGIS`).

.. _figLaunchArcGIS:

.. figure:: figures/LaunchSearchesToolArcGIS.png
	:align: center

	Launching the Data Searches tool (ArcGIS)


To open the Data Searches tool in MapInfo, select **Tools... -> Data Extractor** in the `Tools` menu (:numref:`figLaunchMapInfo`).

.. _figLaunchMapInfo:

.. figure:: figures/LaunchSearchesToolMapInfo.png
	:align: center

	Launching the Data Searches tool (MapInfo)


.. raw:: latex

   \newpage

In ArcGIS, if more than one profile is found and the launch configuration is set up to allow the user to choose, a menu will appear asking the user to choose an XML profile (:numref:`figChooseXML`).

.. _figChooseXML:

.. figure:: figures/ChooseXMLFile.png
	:align: center

	Choosing an XML profile in ArcGIS


If there are any structural issues with the XML document, the tool will display a message with the error it has encountered, and not load any further. If any of the map layers that are listed in the configuration document are not present in the active ArcGIS document or MapInfo workspace, a warning will be shown (:numref:`figLaunchWarningArcGIS`). The layers that are missing will not be loaded into the form and so cannot be included in the search process.

.. _figLaunchWarningArcGIS:

.. figure:: figures/LaunchWarningArcGIS.png
	:align: center

	Warning message displayed for any data layers not loaded


.. raw:: latex

   \newpage

Provided that the XML document is otherwise correct, the form will display (:numref:`figDisplayFormArcGIS`), using the settings given in the XML file for the defaults.

.. _figDisplayformArcGIS:

.. figure:: figures/DisplayFormArcGIS.png
	:align: center

	The form displaying the available data layers (ArcGIS)


.. note::
	The MapInfo version of the form has an additional button after the `Search Reference` field (:numref:`figSearchRefButtonMapInfo`) to retrieve the Site Name.

	.. _figSearchRefButtonMapInfo:

	.. figure:: figures/SearchReferenceButtonMapInfo.png
		:align: center

		The additional search reference button (MapInfo)


.. raw:: latex

   \newpage

.. index::
	single: Using the form

Using the form
==============

Enter the search reference in the **Search Reference** box. If the search reference exists in the linked Access database, the site name will be displayed in the Site Name box (:numref:`figSearchRefKnownArcGIS`). The search reference is case insensitive.

.. _figSearchRefKnownArcGIS:

.. figure:: figures/SearchReferenceKnownArcGIS.png
	:align: center

	Site name displays automatically if the search reference is found


If the search reference does not exist, but you are certain the search reference exists in the search layer(s), enter the site name manually (:numref:`figSearchRefUnknownArcGIS`). If the site does not have a name and the attribute :ref:`RequireSiteName <requiresitename>` in the XML profile is set to No, the site name can be left blank.

.. _figsearchRefUnknownArcGIS:

.. figure:: figures/SearchReferenceUnknownArcGIS.png
	:align: center

	Site name can be filled in manually if the search reference is not found


.. note::
	The MapInfo version of the form has an additional button **Find** after the `Search Reference` field (:numref:`figSearchRefButtonMapInfo`). This button must be clicked to check if the search reference exists in the linked Access database and display the site name in the `Site Name` box.


.. raw:: latex

   \newpage

Now select the data layers you wish to include in the search in the 'Layers to Search' list (ArcGIS) or 'MapInfo Tables' list (MapInfo). Use the :kbd:`Ctrl` key to select individual layers, or the :kbd:`Shift` key to select a range of layers. Selected layers will appear highlighted, layers that will not be included remain unselected (:numref:`figSelectLayersArcGIS`).

.. _figSelectLayersArcGIS:

.. figure:: figures/SelectLayersArcGIS.png
	:align: center

	Select the layers to include in the search


Next, select the buffer size and units in the Buffer Size and Buffer Units boxes (:numref:`figBufferSettingsArcGIS`). The buffer size box accepts decimal points. A buffer size of zero (0) is acceptable, however in ArcGIS the tool will create a buffer polygon of 0.01 metres if a zero buffer size is specified, in order for the buffer layer to be symbolised correctly.

.. _figBufferSettingsArcGIS:

.. figure:: figures/BufferSettingsArcGIS.png
	:align: center

	Select the buffer size and units you wish the search to use.

.. raw:: latex

   \newpage

Decide whether you wish to add the results of the search to the screen and select the relevant option in the 'Add Selected Layers to Map' drop-down box. There are three options (:numref:`figLayerSettingsArcGIS`):

.. _figLayerSettingsArcGIS:

.. figure:: figures/AddLayerSettingsArcGIS.png
	:align: center

	Select how results should be added to the map, if at all

- **No** ... Layers will not be added to the map.
- **Yes - Without labels** ... Layers will be added to the map but will not be labelled.
- **Yes - With labels** ... Layers will be added to the map and will be labelled.

When either of the 'Yes' options is selected, layers will be added to the map in accordance with the settings that are given for each map layer in the configuration document. 

.. note:: 
	If the KeepLayer attribute is set to ``No`` for an individual layer, it will not be added to the map even if the user selects a 'Yes' option in the drop-down list.

.. raw:: latex

   \newpage

If you have selected 'Yes - With labels', select how labels should be added in the 'Overwrite Map Labels' drop-down box (:numref:`figLabelSettingsArcGIS`). If you have made a different selection in the 'Add Selected Layers to Map' drop-down box, any settings in the 'Overwrite Map Labels' will be ignored. There are three options: 

.. _figLabelSettingsArcGIS:

.. figure:: figures/LabelSettingsArcGIS.png
	:align: center

	Select how labels should be added to the map, if at all

- **No** ... Existing map labels will not be overwritten. However, new map labels will be created if the map label column given in the configuration document doesn't exist.
- **Yes - Reset Each Layer** ... Labels will be numbered from 1 and increase by 1 for each feature. For each new layer the label number will be reset to 1.
- **Yes - Reset Each Group** ...  Labels will be numbered from 1 and increase by 1 for each feature in a layer group. For the first layer in each new layer group the label number will be reset to 1.
- **Yes - Do Not Reset** ... Labels will be numbered from 1 and increase by 1 for each feature, but the counter will increase incrementally for all the layers (i.e. it will not reset to 1 at the start of each layer).

.. note:: 
	A 'layer group' is defined by the inclusion of a hyphen in the layer definition. The part of the layer definition before the hyphen is treated as the group name (see the :ref:`note <group>` on group layers).

.. note::
	Map layers will be labelled in accordance with the settings that are given for each map layer in the configuration document. These settings can override the above options in the following circumstances:

	- If no 'LabelColumn' is given in the configuration file, the map layer will not be labelled in any circumstance.
	- If the 'OverwriteLabels' attribute is set to ``No``, the labels for this map layer will not be overwritten even if requested by the user.


.. note::
	If no default values have been given in the XML file for 'DefaultAddSelectedLayers', 'DefaultOverwriteLabels' or 'DefaultCombinedSitesTable', the drop-downs relating to these options will **not show on the form**. In this case, no layers will be added, no labels overwritten, and no combined sites table created, respectively.


.. raw:: latex

   \newpage

Decide how the combined sites table should be created by selecting the relevant option in the 'Create Combined Sites Table' drop-down box. There are three options (:numref:`figCombinedSitesArcGIS`):

.. _figCombinedSitesArcGIS:

.. figure:: figures/CreateCombinedSitesArcGIS.png
	:align: center

	Select how the combined sites table should be created

- **None** ... No combined sites table will be created. Any existing combined sites table for this search reference will be retained.
- **Append to existing table** ... Records will be appended to the combined sites table (if it already exists), otherwise a new combined sites table will be created.
- **Overwrite existing table** ... Records will be saved to a new combined sites table. If a combined sites table already exists it will be deleted first.


.. raw:: latex

   \newpage

Finally, select whether the log file should be cleared before the process runs by checking or unchecking the 'Clear Log File' check-box (:numref:`figClearLogFileArcGIS`).

.. _figClearLogFileArcGIS:

.. figure:: figures/ClearLogFileArcGIS.png
	:align: center

	Select option for clearing the log file


Click **OK** for the search process to start.


While the Data Searches tool is running the search, the map interface will become inactive (in ArcGIS the screen will show 'Paused'). Once the process is finished the interface will reactivate.

When the search is finished, a message box will appear (:numref:`figFinishedArcGIS`). If you would like to rerun the search (for example, for different data layers, or for a different buffer size), choose to keep the form open and it will retain the information as it was entered for the last search.

.. _figFinishedArcGIS:

.. figure:: figures/FinishedArcGIS.png
	:align: center

	Prompt to close the form when the search process completes


.. raw:: latex

   \newpage

Once you have made your choice, the log file will be shown using Notepad (:numref:`figLogFileArcGIS`). Using this you can review whether the search was carried out as expected. When you are finished, close the log file. It has already been saved in the analysis folder for future reference.

.. _figLogFileArcGIS:

.. figure:: figures/LogFileArcGIS.png
	:align: center

	Example log file shown for review


You can now repeat the search process using a different search radius with different data layers, or for a different search request, as required.

.. _OverwriteWarning:

.. caution:: 
	If you rerun the search process using the **same search reference**, for example with a different buffer size, it is possible that some outputs will overwritten, or duplicated, as follows:

	- Output tables and GIS layers will be overwritten if the same map layer is included in a second search. Only one copy of each output table and / or GIS layer can be saved for the same search reference.
	
	- The combined sites table will be overwritten if **Overwrite existing table** is selected in the 'Create Combined Sites Table' option.

	- Combined sites records will be duplicated if the same map layer is included in a second search and if **Append to existing table** is selected in the 'Create Combined Sites Table' option.


.. raw:: latex

   \newpage

.. index::
	single: Search results

Search results
==============

When the search is finished, any exported data tables, saved GIS layers, the buffer GIS layer, and the log file are all saved in the 'GISFolder' specified in the XML document. Any saved GIS layers resulting from the search are also added to the map interface (if requested).

.. note::
	Only results for those layers for which features were found within the search radius are saved and added to the map.


.. raw:: latex

   \newpage

.. index::
	single: Search results; ArcGIS

Search results in ArcGIS
------------------------

In ArcGIS, search results are added to the current document as follows:

- If 'Yes' is selected in the 'Add Selected Layers to Map' search option, each saved GIS layer (where 'Yes' is selected in the 'KeepLayer' attribute in the configuration) is added to a new group layer. The name of the group layer follows the 'GroupLayerName', with any special characters replaced with the 'RepChar' as specified in the XML document (e.g. '2016/001' becomes '2016 001').

- If either 'Yes - with labels' or 'Yes - without labels' are selected in the 'Add Selected Layers to Map' search option and, if a layer file name is specified in the 'LayerFileName' attribute in the configuration for a saved layer, symbology is applied to that layer using the specified layer file.

- If 'Yes - with labels' is selected in the 'Add Selected Layers to Map' search option and, if a column name is specified in the 'LabelColumn' attribute in the configuration for a saved layer, labels are applied to that layer (as specified in the configuration using the 'LabelClause' attribute).

- A buffer GIS layer, created during the search, will be added to the new group layer and symbology will be applied using the appropriate layer file (as specified in the configuration using the 'BufferLayerName' general attribute).

- Unless the buffer radius specified is zero, the map will zoom to the extent of the buffer layer that was created during the search.

An example of how the results will appear in ArcGIS is shown in :numref:`figResultsArcGIS`.

.. _figResultsArcGIS:

.. figure:: figures/ResultsArcGIS.png
	:align: center

	Example results from search process (ArcGIS)


.. raw:: latex

   \newpage

.. index::
	single: Search results; MapInfo

Search results in MapInfo
-------------------------

In MapInfo, search results are added to the active workspace as follows:

- If 'Yes' is selected in the 'Add Selected Layers to Map' search option, each saved GIS layers (where 'Yes' is selected in the 'KeepLayer' attribute in the configuration) is added to **all** map windows that contain the relevant source layer. This means that if there are multiple map windows open in the workspace containing the same source layer the saved GIS layer will be added to each of those map windows.

- If 'Yes - with labels' is selected in the 'Add Selected Layers to Map' search option and, if a column name is specified in the 'LabelColumn' attribute in the configuration for a saved layer, labels are applied to that layer (as specified in the configuration using the 'LabelClause' attribute).

- A buffer GIS layer, created during the search, will be added to **all** map windows.

- The map will zoom to the extent of the buffer layer that was created during the search.

An example of how the results will appear in MapInfo is shown in :numref:`figResultsMapInfo`.

.. _figResultsMapInfo:

.. figure:: figures/ResultsMapInfo.png
	:align: center

	Example results from search process (MapInfo)
