.. index::
	single: FAQ
	see: Frequently asked questions; FAQ

**************************
Frequently Asked Questions
**************************

This is a list of Frequently Asked Questions about the HLU Tool. Feel free to
suggest new entries!


**How do I get a copy of the tool?**

	This is a test it is a very quick test.
	The source code can be downloaded from `HabitatFramework/HLUTool <https://github.com/HabitatFramework/HLUTool>`_ and the latest installer setups for ArcGIS/MapInfo and MapInfo only can be downloaded from `HabitatFramework/HLUTool/Releases <https://github.com/HabitatFramework/HLUTool/releases>`_.

**Do I have to use IHS with the tool?**

	Yes, IHS is an integral part of the tool and data structure. It is likely that your existing habitat data can be translated into IHS and, once in IHS, it can easily be exported as IHS habitats, Broad habitats or Priority habitats.

**Why does the tool title bar show [READ ONLY]?**

	This shows that the data cannot currently be edited. This is either because your userid has not been added to the database or has been added incorrectly (see 'Lookup Tables' in the `HLUTool-TechnicalGuide <https://readthedocs.org/projects/hlutool-technicalguide/>`_ for details), or the active GIS layer is not in an active edit state. Once both of these conditions have been met click on the main window and the [READ ONLY] status should disappear.

**Can I use data that isn't snapped to OS MasterMap?**

	Technically you could but only by providing dummy, unique TOID values to every feature in your data. This is because the tool is designed to use the TOID to determine when a physical split or merge is to be performed and to manage the TOID_Fragment_IDs. Without dummy, unique TOIDs the tool would assume all the features in you data are fragments of the same 'blank' TOID which would heavily impact on performance. However, integrating habitat data with OS MasterMap also brings other benefits such as providing spatial accuracy to your data and providing a framework within which more recent or comprehensive habitat and land use data can be applied. See :ref:`habitat_framework` for more details.

**How do I convert my existing data into the required format?**

	The conversion of one or more existing habitat layers into a state that can be used with the HLU Tool is not simple, but the process brings all the benefits of having an OS MasterMap framework, and once completed the benefits of using the HLU Tool. There are up to 4 steps required to convert existing habitat layer(s) so that it can be used by the HLU Tool:

		1. Translate the habitat code(s) to IHS.
		2. Create an OS MasterMap framework for your regional extent and load with the IHS habitat data.
		3. Assign the OS MasterMap framework the required attributes to format them to match the required standards.
		4. Load the attribute data into the target relational database and save the spatial and minimum attribute data in a valid HLU GIS layer format.

	It is recommended that the conversion is performed by someone familiar with IHS and the OS MasterMap framework, expert in the configuration of the HLU Tool, experienced in advanced GIS geospatial processing, and ideally expert in SQL Server and developing data conversion routines. Enquiries can be made via the `ALERC forum <http://forum.lrcs.org.uk/viewforum.php?id=24>`_.

**Can I hide IHS habitats that don't occur in my region from the drop-down lists?**

	You can currently hide IHS habitats from the `Habitat` list on the IHS tab in the main window (see 'Lookup Tables' in the `HLUTool-TechnicalGuide <https://readthedocs.org/projects/hlutool-technicalguide/>`_ for details). There is also a planned change request to enable non-local IHS Habitats to be hidden from the `Habitat Type` list on the `Sources` tab in the main window.	

**Can several people use the tool at the same time?**

	Any number of users can use the tool for read-only access if they have a copy of the tool installed on their PC. Multiple users can also use the tool in edit mode but only within the limits of the database system and GIS application used by the tool. So the GIS layer and database would also have to be configured to support multiple users.

**Does the tool work with QGIS?**

	Currently only ArcGIS and MapInfo are supported with the tool. However, if funding was available the tool could be adapted to also support QGIS.

**How do I report a new bug or propose a change in the tool?**

	Please check the existing known issues and change requests on `HabitatFramework/HLUTool/Issues <https://github.com/HabitatFramework/HLUTool/issues>`_ before reporting/proposing new issues or changes. New issues or proposed changes can be posted on the `ALERC forum <http://forum.lrcs.org.uk/viewforum.php?id=24>`_

