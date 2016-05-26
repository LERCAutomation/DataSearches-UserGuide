*******************
Setting up the tool
*******************

Before the Data Searches Tool will function, it needs to be installed and configured. It is recommended that the configuration is carried out first, although the steps are interchangeable for the ArcGIS implementation. 

.. index::
	single: Configuring the tool

Configuring the tool
====================

The configuration is stored in an XML file, and there are some differences in the contents of this file between the MapInfo and the ArcGIS implementations of the tool. Please ensure that you are using the correct XML file, examples of both of which can be found in the :doc:`appendix <../appendix/appendix>`. Settings are presented as nodes (beginning with a start node, e.g. ``<example>``, and finishing with an end note, e.g. ``<\example>``), with the value for the setting held between the ``<value>`` and ``<\value>`` node. 

The XML files can be edited in a text editor such as Notepad or Wordpad, or using a more feature rich XML editor such as as `Sublime Text <https://www.sublimetext.com/3>`_. The configuration file is split into two sections: a section containing general attributes of the searches, and a section that deals with the way each data layer should be handled. This structure is the same for both implementations of the tool. 

.. note::
	It is important that the structure of the file is maintained as it is presented in the :doc:`appendix <../appendix/appendix>`. Any changes to the structure may result in the Data Searches Tool not loading, or not working as expected.

Once editing has been completed and the edits have been saved it is recommended that the configuration file is opened using an internet browser such as Internet Explorer which will help highlight any editing errors – only if the structure of the file is valid will the whole file be displayed in the internet browser.

.. note::
	It is recommended that the configuration file is kept in a central (network) location, so that all data searches use the same setup. In case of the MapInfo implementation of the tool, it is essential that the configuration file is kept in the same folder as the compiled version of the tool.


Setup for ArcGIS
----------------

**General attributes**

The first section of the configuration file deals with a series of general attributes for the Data Searches Tool. These general nodes specify where files are kept, how output files should be named, and other overall settings. Details on these attributes and their expected values are shown in :numref:`tabArcGISGenAtt`. The table follows the order within which the attributes are found in the configuration file.

..note::
	The enquiry reference takes the form 'LERCName/Year/EnquiryNumber' (e.g. 'Example/2016/001'). Within the configuration file, it is possible to use all or parts of this reference for naming files and folders. The following options are available:
	``%ref%`` uses the full enquiry reference.
	``%shortref%`` uses the numeric part of the reference (e.g. '2016/001').
	``%subref%`` uses the Enquiry Number (e.g. '001').
	``%sitename%`` uses the name of the site (e.g. 'Example site').

.. _tabArcGISGenAtt:

.. table:: General attributes in the ArcGIS configuration file.

database 	The path to the Access database that contains the details of all search requests. This must be the full 			path including the ``.mdb`` extension.

+------------------------+------------------------------------------------------------+
| Attribute              |Description                                                 |            
+========================+============================================================+
| Database               || The path to the Access database that contains the details |
|                        || of all search requests. This must be the full path        |
|                        || including the ``.mdb`` extension.                         |
+------------------------+------------------------------------------------------------+
| RefColumn              || The name of the column, in the Enquiries table within the |
|                        || Access database, that contains the search reference.      |
+------------------------+------------------------------------------------------------+

+------------------------+----------------------------------------------------------+
| SiteColumn             |The name of the column, in the Enquiries table within the |
|                        |Access database, that contains the site name.             |
+------------------------+----------------------------------------------------------+
| RepChar                |The character(s) used to replace any special characters   |
|                        |in file or folder names. 'Special' characters are any of  |
|                        |the following: ``\, %,$, :, *, /, ?, <, >, |, ~, £, .``.  |
|                        |The replacement character can itself not be a special     |
|                        |character.                                                |
+------------------------+----------------------------------------------------------+
| LayerFolder            |The folder where layer files (``.lyr``) are kept. These   |
|                        |files are used to symbolise the GIS data layers that are  |
|                        |exported during processing.                               |
+------------------------+----------------------------------------------------------+
| SaveRootDir            |The folder within which all output folders will be        |
|                        |created.                                                  |
+------------------------|----------------------------------------------------------+
| SaveFolder             |The name of the folder that will be created for each      |
|                        |search. The keywords %ref%, %shortref%, %subref% and      |
|                        |%sitename% are allowed.                                   |
+------------------------+----------------------------------------------------------+
| GISFolder              |The name of the folder where all data generated by the    |
|                        |data searches tool will be stored. This folder will be    |
|                        |created in the ``SaveFolder``. The keywords %ref%,        |
|                        |%shortref%, %subref% and %sitename% are allowed.          |
+------------------------+----------------------------------------------------------+
| LogFileName            |The name of the log file that will be created during      |
|                        |processing. The keywords %ref%, %shortref%, %subref% and  |
|                        |%sitename% are allowed.                                   |
+------------------------+----------------------------------------------------------+
| DefaultClearLogFile    |Yes/No attribute, to set whether the check box for 'Clear |
|                        |Log File' on the interface should be set to checked       |
|                        |(``Yes``) or unchecked (``No``) by default.               |
+------------------------+----------------------------------------------------------+
| DefaultBufferSize      |The default buffer size that will appear in the interface |
|                        |when first loaded.                                        |
+------------------------+----------------------------------------------------------+
| BufferUnitOptions      |The options for buffer units that will be shown in the    |
|                        |interface. It is not recommended that these are changed.  |
|                        |Details of how any changes should be formatted are in     |
|                        |the comments for this attribute.                          |
+------------------------+----------------------------------------------------------+
| DefaultBufferUnit      |The buffer unit that should be shown by default in the    |
|                        |interface. This attribute is the index number of the unit |
|                        |in the dropdown list, with 1 being the first option.      |
+------------------------+----------------------------------------------------------+
| BufferLayerName        |The name of the layer file (kept in the ``LayerFolder``)  |
|                        |which will be used to symbolise the buffer layer. Must    |
|                        |include the ``.lyr`` extension.                           |
+------------------------+----------------------------------------------------------+
| SearchLayer            |The name of the data searches GIS layer in the interface. |
|                        |There may be either a single search layer (of either      |
|                        |points, polygons or lines) of this name, or there may be  |
|                        |multiple search layers present (e.g. one of each format), |
|                        |in which case their names should begin with the           |
|                        | ``SearchLayer`` name. See :numref:`figArcGISUI` for an   |
|                        |example.                                                  |
+------------------------+----------------------------------------------------------+


Setup for MapInfo
-----------------


Installing the tool (split MapInfo / ArcGIS)
============================================

ArcGIS
------
- Installing the add-in 
- Creating a menu bar (ArcGIS)
- Adding add-in to menu
- Configuring the add-in (first time)

MapInfo
-------
- Adding the tool
- Running the tool – different version
