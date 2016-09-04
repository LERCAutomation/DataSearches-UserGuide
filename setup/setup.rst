*******************
Setting up the tool
*******************

Before the Data Searches tool will function, it needs to be installed and configured. It is recommended that the configuration is carried out first, although the steps are interchangeable for the ArcGIS implementation. 

.. index::
	single: Configuring the tool

Configuring the tool
====================

The configuration is stored in an XML file called 'DataSearches.xml', and there are some differences in the contents of this file between the MapInfo and the ArcGIS implementations of the tool. Please ensure that you are using the correct XML file, examples of both of which can be found in the :doc:`Appendix <../appendix/appendix>`. Attributes and settings are presented as nodes (beginning with a start node, e.g. ``<example>``, and finishing with an end note, e.g. ``<\example>``), with the value for the setting held between the ``<value>`` and ``<\value>`` tag. 

.. caution:: 
	The name of the configuration file must be 'DataSearches.xml'. The tool will not load if a different name is used.

The XML file can be edited in a text editor such as Notepad or Wordpad, or using a more feature rich XML editor such as as `Sublime Text <https://www.sublimetext.com/3>`_. The configuration file is split into two sections:

_`General attributes`
	General and default attributes for the tool.

_`Data layers`
	Deals with the way each data layer should be handled. This structure is the same for both implementations of the tool.

.. caution::
	It is important that the structure of the file is maintained as it is presented in the :doc:`Appendix <../appendix/appendix>`. Any changes to the structure may result in the Data Searches tool not loading, or not working as expected.

Once editing has been completed and the edits have been saved, it is recommended that the configuration file is opened using an internet browser such as Internet Explorer which will help highlight any editing errors – only if the structure of the file is valid will the whole file be displayed in the internet browser.

.. note::
	It is recommended that the configuration file is kept in a central (network) location, so that all users use the same configuration. Additionally, in case of the MapInfo implementation of the tool, it is essential that the configuration file is kept in the same folder as the compiled version of the tool.


.. index::
	single: Special characters in XML

.. raw:: latex

   \newpage

Special characters in XML
-------------------------

The characters ``&``, ``<`` and ``>`` are not valid within values and, so in order to be used, must be **escaped** with XML entities as follows:

<
	This must be escaped with ``&lt;`` entity, since it is assumed to be the beginning of a tag. For example, ``RecYear &lt; 2010``

>
	This should be escaped with ``&gt;`` entity. It is not mandatory -- it depends on the context -- but it is strongly advised to escape it. For example, ``RecYear &gt; 1980``

&
	This must be escaped with ``&amp;`` entity, since it is assumed to be the beginning of a entity reference. For example, ``TaxonGroup = 'Invertebrates - Dragonflies &amp; Damselflies'``


.. index::
	single: Setup; ArcGIS


Setup for ArcGIS
----------------

.. index::
	single: General attributes; ArcGIS


General attributes for ArcGIS
*****************************

The first section of the configuration file deals with a series of general attributes for the Data Searches tool. These general nodes specify where files are kept, how output files should be named and other overall settings. Details on these attributes (and their typical values where known) are given below. The list follows the order within which the attributes are found in the configuration file. This version of the configuration details is valid for the ArcGIS version 1.2.1 of the Data Searches tool.

.. note::
	The enquiry reference takes the form 'LERCName/Year/EnquiryNumber' (e.g. 'XYBRC/2016/001'). Within the configuration file, it is possible to use all or parts of this reference for naming files and folders. The following options are available:

	- ``%ref%`` uses the full enquiry reference.
	- ``%shortref%`` uses the numeric part of the reference (e.g. '2016/001').
	- ``%subref%`` uses the Enquiry Number (e.g. '001').
	- ``%sitename%`` uses the name of the site (e.g. 'Example site').


Database
	The path to the Access database that contains the details of all search requests. This must be the full path including the ``.mdb`` extension. The database must have a table called 'Enquiries' that contains, at the very least, the search reference and the site name.

RefColumn
	The name of the column in the Enquiries table within the Access database that contains the search reference. The name must be given without any brackets. The search reference must follow the format 'LERCName/Year/EnquiryNumber'.

SiteColumn
	The name of the column in the Enquiries table within the Access database, that contains the site name. The name must be given without any brackets.

RepChar
	The character(s) used to replace any special characters in file or folder names. 'Special' characters are any of the following: ``\, %,$, :, *, /, ?, <, >, |, ~, £, .``. The replacement character can itself not be a special character.

_`LayerFolder`
	The folder where layer files (``.lyr``) are kept. These files are used to symbolise the GIS data layers that are exported during processing.

SaveRootDir
	The folder within which all output folders will be created.
 
SaveFolder
	The name of the folder that will be created for each search. The keywords ``%ref%``, ``%shortref%``, ``%subref%``and ``%sitename%`` are allowed.

GISFolder
	The name of the folder where all data generated by the Data Searches tool will be stored. This folder will be created in the SaveFolder. The keywords ``%ref%``, ``%shortref%``, ``%subref%`` and ``%sitename%`` are allowed.

LogFileName
	The name of the log file that will be created during processing. The keywords ``%ref%``, ``%shortref%``, ``%subref%``and ``%sitename%`` are allowed.

DefaultClearLogFile
	Yes/No attribute, defining whether the check box for 'Clear Log File?' on the interface should be set to checked (``Yes``) or unchecked (``No``) when the form is opened.

DefaultBufferSize
	The default buffer size that will appear in the 'Buffer Size' text box when the form is opened.

BufferUnitOptions
	The options for buffer units that will be shown in the 'Buffer Unit' drop-down list. It is not recommended that these are changed. However, details of how any changes should be formatted are in the comments for this attribute within the XML file.

DefaultBufferUnit
	The buffer unit that should be shown by default in the 'Buffer Unit' drop-down list. This attribute is the index number of the unit in the drop-down list, with 1 being the first option.

BufferLayerName
	The name of the layer file (kept in the `LayerFolder`_) which will be used to symbolise the buffer layer. Must include the ``.lyr`` extension.

SearchLayer
	The name of the data searches GIS layer in the interface. There may be either a single search layer (of either points, polygons or lines) of this name, or there may be multiple search layers present (e.g. one of each format) in which case their names should begin with the SearchLayer entry. See :numref:`figArcGISUI` for an example. In the case of this example, the entry for this node was ``SearchSites`` and the `SearchLayerExtensions`_ entry (see next attribute) was ``_point;_poly;_line``. 

_`SearchLayerExtensions`
	If multiple search layers are used, this node should contain a list of the extensions for each layer, delimited by semicolons (e.g. in the example used above, the entry was ``_point;_poly;_line``). If only a single layer is used this attribute should be left blank.

SearchColumn
	The name of the column in the search layer(s) that holds the search reference.

AggregateColumns
	A list, delimited by semicolons, of the fields in the search layer that should be used to dissolve the buffer during processing. This attribute can be used in cases where the search sites are multi-part features which may create a number of overlapping buffers rather than one continuous one.

AddSelectedLayersOptions
	The options that should be shown in the 'Add Selected layers to Map' drop-down list. These options should not be changed.

DefaultAddSelectedLayers
	The default option for adding the selected layers that should be shown when the form opens. This attribute is the index number of the item in the 'Add Selected Layers to Map' drop-down list, with 1 being the first option. If no value is entered the list box will be hidden and no layers will be added to the map.

OverwriteLabelOptions
	The options that should be shown in the 'Overwrite Map Labels' drop-down list. These options should not be changed.

DefaultOverwriteLabels
	The default option for the 'Overwrite Map Labels' drop-down that should be shown when the form opens. This attribute is the index number of the item in the drop-down list, with 1 being the first option. If no value is entered the list box will be hidden and labels will not be overwritten.

CombinedSitesTableOptions
	The options that should be shown in the 'Create Combined Sites Table' drop-down list. These options should not be changed.

DefaultCombinedSitesTable
	The default option for the 'Create Combined Sites Table' drop-down that should be shown when the form opens. This attribute is the index number of the item in the drop-down list, with 1 being the first option. If no value is entered the list box will be hidden and no combined sites table will be created.

CombinedSitesTable
	This section defines the combined sites table. It has the following entries:

	Columns
		A comma-delimited list of the column headings that the combined sites table should have.
	Suffix
		An entry of what the suffix of the file name should be. The name of the combined sites table is given by ``subref_Suffix.Format``, e.g. ``001_sites.csv`` where the suffix is ``sites`` and the format is ``csv``. The use of the ``subref`` keyword is predefined in this case and cannot be changed.
	Format
		The format that the combined sites table should have. Choose from ``csv`` or ``txt``.


.. index::
	single: Map layer attributes; ArcGIS

Map layer attributes for ArcGIS
*******************************

All map layer attributes are found within the ``<MapLayers>`` node. For each data layer that can be included in the searches, a new child node is created that has the name of the layer (e.g. ``<Sites_-_SSSIs>``). This name is name of the layer as it will be shown in the tool menu, and can be different from the layer name as it is shown in the ArcGIS table of contents (which will be set in a subsequent child node). A simple example of a map layer definition with limited attributes is shown in :numref:`figXMLExampleArcGIS`. 

.. tip::
	If you wish to display spaces in any layer names in the tool menu use an underscore (``_``) for each space in the node name for the layer. XML does not allow spaces in node names, but the tool will translate these underscores into spaces when the form is opened.

.. _figXMLExampleArcGIS:

.. figure:: figures/DataLayerXMLExampleArcGIS.png
	:align: center

	Simplified example of data layer attributes configuration (ArcGIS)

The attributes that are required for each map layer are as follows:

LayerName
	The name of the layer as it is shown in the GIS interface. Characters that cannot be included in the layer name are ``/`` and ``&`` as they will cause the tool to fail. The characters ``-``, ``_``, ``+`` and ``\`` are permitted.

Prefix
	The prefix will be used to start the name of any GIS layer that is exported from this data layer during the search. The naming followed for exported GIS layers is ``Prefix_subref.shp``, e.g. ``SSSIs_001.shp``. The use of the ``subref`` keyword in this case is predefined and cannot be changed.

Suffix
	The suffix will be used to finish the name of any tabular file that is exported from this data layer during the search. The naming followed for exported tabular data is ``subref_Suffix.Format``, e.g. ``0001_SSSIs.csv``. The use of the ``subref`` keyword in this case is predefined and cannot be changed.

Columns
	A comma-separated list of columns that should be included in the tabular data exported from this data layer during the search. The column names are case sensitive and should match the column names in the source layer. Distance and Radius columns may be included by adding the keywords 'Distance' and 'Radius'. If results from any aggregate functions are to be included, they should follow the naming convention that ArcGIS employs for statistics fields, as follows:

	- Column names are up to 10 characters long and are case sensitive.
	- Statistics column names are made up of the statistic requested (e.g. COUNT, SUM, MEAN, FIRST, etc.), the underscore character (``_``), and the name of the column to which the statistic applies (e.g. ``COUNT_Year``). Names longer than 10 characters are abbreviated. 
	- If, due to abbreviation, two output columns would be given the same name, ArcGIS will automatically add a count of ``_1`` to the column name. Where the column name is nine or ten characters long, it will replace the last one or two characters of the second column with ``_1``, always ensuring the length of the column name does not exceed ten characters. 
	- Numbering for any subsequent columns with the same name will follow this format adding one to each column number until this number reaches 9. Any subsequent columns will be numbered ``_10``, ``_11`` etc, so adding or replacing up to three rather than two characters in the column name. Again in all cases the new column name will be ten characters long or less.

	.. tip::
		If you are unsure what the output column names will be from an aggregation operation, run the Dissolve tool (this resides in the ArcGIS toolbox, under Data Management Tools => Generalisation) on a sample of your data, and include the statistics columns with the relevant statistic types as you intend to use them in the Data Searches tool. The output will contain the column names as they will be generated by the Data Searches tool, since it uses the same process.


_`GroupColumns`
	A comma-separated list of the name(s) of any column(s) that should be used for grouping the outputs from the search on this layer. The column names are case sensitive and should match the column names in the source layer.

_`StatisticsColumns`
	If `GroupColumns`_ are specified, statistics may be requested from any columns in the input layer. The format of this attribute is as follows: ``ColumnName1;STATISTIC$ColumnName2;STATISTIC``, e.g. ``Area;SUM$Year;COUNT``. Note that in order to be included in the tabular output, the output columns for these statistics must be included in the Columns list as described above.

OrderColumns
	A comma-separated list of columns by which the results should be ordered in the tabular output for this layer. The order of this list overrides any order in the `GroupColumns`_ attribute.

Criteria
	Selection criteria that should be used on the data layer during the search. These can be used to, for example, suppress confidential records, report on particular species only, or only include records after a certain date. The criteria take the form ``ColumnName Operand Value`` and may include ``AND`` and ``OR`` statements and similar. String values should be enclosed in single quotes. An example might be ``Name = 'myName' AND Year > 2010``. Only records that match the criteria will be exported.

	.. note::
		Any clause specified here must adhere to ArcGIS SQL syntax as the clause will be run within ArcGIS.

_`IncludeDistance`
	A Yes/No attribute that defines whether the distance of each feature in the data layer to the search location will be measured during the process. The results can be added to the tabular output by using the keyword 'Distance' in the Columns list.

_`IncludeRadius`
	A Yes/No attribute that defines whether the buffer radius that was used will be available for inclusion to the tabular output during the process. The results can be added to the tabular output by using the keyword 'Radius' in the Columns list. 

KeyColumn
	The name of the column containing the unique identifier for this data layer.

Format
	The format of tabular output exported from this data layer during a search. Options are ``csv`` and ``txt``. If ``txt`` is selected as a format no column names will be included in the output. They are included for ``csv`` output.

KeepLayer
	A Yes/No attribute that defines whether a GIS data layer should be kept of the features selected in this map layer during the search. If ``No`` is entered all geographical data generated for this data layer during the process will be deleted. If ``Yes`` is entered, a data layer will be created that follows the naming convention ``Prefix_subref.shp``. The use of the ``subref`` keyword in this case is predefined and cannot be changed. 

	.. note:: 
		If no features are selected in a data layer during a search, no new data layer will be created even if the KeepLayer attribute is set to ``Yes``.

_`LayerFileName`
	The name of the layer file (``.lyr``) that should be used to symbolise any GIS output from this data layer. The layer file should be present in the `LayerFolder`_ specified in the general attributes. This name is case sensitive. If no value is entered the system will use the default symbology assigned during processing.

OverwriteLabels
	A Yes/No attribute that specifies whether the labels in this data layer can be overwritten for any GIS output. If the attribute is set to ``No``, labels will not be overwritten even if requested by the user through the 'Overwrite Map Labels' options on the form.

LabelColumn
	The name of the column in this data layer that contains the labels. If this entry has a column name that does not exist in the data layer, the tool will create this label column when necessary even if OverwriteLabels is set to ``No``. In this case, the features will be automatically numbered and numbering will follow the rule that is selected by the user through the 'Overwrite Map Labels' options on the form. If this attribute is left blank, no labels will be created or displayed for this layer even when requested by the user. 

LabelClause
	An ArcGIS clause that defines the format, font type, font size and colour of the labels for this layer. The format of this clause is as follows: ``Font:FontName$Size:FontSize$Red:PercentRed$Green:PercentGreen`` ``$Blue:PercentBlue$Type:PlacementType``, where the ``Type`` is the ArcGIS label placement type with the following options:  NoRestrictions, OnePerName, OnePerPart or OnePerShape. An example would be ``Font:Arial$Size:10$Red:0$Green:0$Blue:0$Type:NoRestrictions``. If no clause is filled in these default settings are applied (Arial, size 10, black, each polygon in a multi-part polygon is labelled).

CombinedSitesColumns
	A comma-separated list of column names to be included in the combined sites table. If this entry is left blank the data layer will not be included in the combined sites table. A number of special cases apply to this attribute:

	- Any entry surrounded by double quotes (e.g. ``"Protected sites"``) will be included in the combined sites table 'as is'. So, in the case of this example, each row that is added to the combined sites table from this data layer will have the entry 'Protected sites' in one of the columns. This feature is useful in distinguishing which data layer each row in the combined sites table originates from. 

	- If `IncludeDistance`_ is set to ``yes``, the keyword ``Distance`` can be included as a column name. The tool will automatically include the calculated distance of each feature to the point of interest in the combined sites table. Similarly the keyword ``Radius`` can be included if `IncludeRadius`_ is set to ``yes``. This will then add the buffer radius that was used for each entry in the table.

	.. note:: 
		The column headings of the combined sites table follow the 'Columns' entry under the CombinedSitesTable attribute in the general attributes. It is important to ensure that the CombinedSitesColumns are given in the same order as expected by this attribute.

_`CombinedSitesGroupColumns`
	A comma-separated list of column names by which the output from this data layer should be grouped before inclusion in the combined sites table. 

_`CombinedSitesStatisticsColumns`
	If any aggregation is applied for this data layer (through the `CombinedSitesGroupColumns`_ attribute), statistics may be included in the combined sites table in the same way as described for `StatisticsColumns`_.

_`CombinedSitesOrderByColumns`
	A comma-separated list of column names by which the output of this layer should be ordered before inclusion in the combined sites table. This entry overrides any ordering created by the `CombinedSitesGroupColumns`_ attribute.

.. caution::
	All entries in the configuration file are **case sensitive**. Most common errors in the setting up of the tool are caused by using the incorrect case for entries.


.. raw:: latex

   \newpage

.. index::
	single: Setup; MapInfo

Setup for MapInfo
-----------------

.. index::
	single: General attributes; MapInfo

General attributes for MapInfo
******************************

The first section of the configuration file deals with a series of general attributes for the Data Searches tool. These general nodes specify where files are kept, how output files should be named and other overall settings. Details on these attributes (and their typical values where known) are given below. The list follows the order within which the attributes are found in the configuration file. This version of the configuration details is valid for the MapInfo version 1.2.1 of the Data Searches tool.

.. note::
	The enquiry reference takes the form 'LERCName/Year/EnquiryNumber' (e.g. 'XYBRC/2016/001'). Within the configuration file, it is possible to use all or parts of this reference for naming files and folders. The following options are available:

	- ``%ref%`` uses the full enquiry reference.
	- ``%shortref%`` uses the numeric part of the reference (e.g. '2016/001').
	- ``%subref%`` uses the Enquiry Number (e.g. '001').
	- ``%sitename%`` uses the name of the site (e.g. 'Example site').


_`ToolTitle`
	The title to use for the program in the MapInfo Tools menu.

Database
	The path to the Access database that contains the details of all search requests. This must be the full path including the ``.mdb`` extension. The database must have a table called 'Enquiries' that contains, at the very least, the search reference and the site name.

EnquiriesDir
	The folder where a temporary table will be created by MapInfo when querying the Access database.

RefColumn
	The name of the column in the Enquiries table within the Access database that contains the search reference. The name must be given without any brackets. The search reference must follow the format 'LERCName/Year/EnquiryNumber'.

SiteColumn
	The name of the column in the Enquiries table within the Access database, that contains the site name. The name must be given without any brackets.

RepChar
	The character(s) used to replace any special characters in file or folder names. 'Special' characters are any of the following: ``\, %,$, :, *, /, ?, <, >, |, ~, £, .``. The replacement character can itself not be a special character.

SaveRootDir
	The folder within which all output folders will be created.
 
SaveFolder
	The name of the folder that will be created for each search. The keywords ``%ref%``, ``%shortref%``, ``%subref%``and ``%sitename%`` are allowed.

GISFolder
	The name of the folder where all data generated by the Data Searches tool will be stored. This folder will be created in the SaveFolder. The keywords ``%ref%``, ``%shortref%``, ``%subref%`` and ``%sitename%`` are allowed.

LogFileName
	The name of the log file that will be created during processing. The keywords ``%ref%``, ``%shortref%``, ``%subref%``and ``%sitename%`` are allowed.

DefaultBufferSize
	The default buffer size that will appear in the 'Buffer Size' text box when the form is opened.

BufferUnitOptions
	The options for buffer units that will be shown in the 'Buffer Unit' drop-down list. It is not recommended that these are changed. However, details of how any changes should be formatted are in the comments for this attribute within the XML file.

DefaultBufferUnit
	The buffer unit that should be shown by default in the 'Buffer Unit' drop-down list. This attribute is the index number of the unit in the drop-down list, with 1 being the first option.

BufferSymbology
	The symbology to be applied to the buffered search area.

RecMax
	The maximum number of records what will be extracted in any one map layer. This is a simple measure to avoid exceeding MapInfo's standard 4Gb file size.

SearchTable
	The name of the GIS layer containing the data search point, line or polygon.

SearchColumn
	The name of the column in the search table that holds the search reference.

AggregateColumns
	A list, delimited by commas, of the fields in the search layer that should be used to dissolve the buffer during processing. This attribute can be used in cases where the search sites are multi-part features which may create a number of overlapping buffers rather than one continuous one.

AddSelectedTablesOptions
	The options that should be shown in the 'Add Selected layers to Map' drop-down list. These options should not be changed.

DefaultAddSelectedTables
	The default option for adding the selected layers that should be shown when the form opens. This attribute is the index number of the item in the 'Add Selected Layers to Map' drop-down list, with 1 being the first option. If no value is entered the list box will be hidden and no layers will be added to the map.

OverwriteLabelOptions
	The options that should be shown in the 'Overwrite Map Labels' drop-down list. These options should not be changed.

DefaultOverwriteLabels
	The default option for the 'Overwrite Map Labels' drop-down that should be shown when the form opens. This attribute is the index number of the item in the drop-down list, with 1 being the first option. If no value is entered the list box will be hidden and labels will not be overwritten.

CombinedSitesOptions
	The options that should be shown in the 'Create Combined Sites Table' drop-down list. These options should not be changed.

DefaultCombinedSitesTable
	The default option for the 'Create Combined Sites Table' drop-down that should be shown when the form opens. This attribute is the index number of the item in the drop-down list, with 1 being the first option. If no value is entered the list box will be hidden and no combined sites table will be created.

CombinedSitesTable
	This section defines the combined sites table. It has the following entries:

	TableName
		The name of the temporary GIS layer that will be created when generating the combines sites table.
	Columns
		A comma-delimited list of the column headings, and their data types/lengths, that the combined sites table should have.
	Suffix
		An entry of what the suffix of the file name should be. The name of the combined sites table is given by ``subref_Suffix.Format``, e.g. ``001_sites.csv`` where the suffix is ``sites`` and the format is ``csv``. The use of the ``subref`` keyword is predefined in this case and cannot be changed.
	Format
		The format that the combined sites table should have. Choose from ``csv`` or ``txt``.


.. index::
	single: Map layer attributes; MapInfo

Map layer attributes for MapInfo
********************************

All map layer attributes are found within the ``<MapTables>`` node. For each data layer that can be included in the searches, a new child node is created that has a descriptive name for the layer (e.g. ``<Sites_-_SSSIs>``). This name is name of the layer as it will be shown in the tool interface, and can be different from the layer name as it is known in the active MapInfo workspace (which will be set in a subsequent child node). A simple example of a map layer definition with limited attributes is shown in :numref:`figXMLExampleMapInfo`. 

.. tip::
	If you wish to display spaces in any layer names in the tool menu use an underscore (``_``) for each space in the node name for the layer. XML does not allow spaces in node names, but the tool will translate these underscores into spaces when the form is opened.

.. _figXMLExampleMapInfo:

.. figure:: figures/DataLayerXMLExampleMapInfo.png
	:align: center

	Simplified example of data layer attributes configuration (MapInfo)

The attributes that are required for each map layer are as follows:

TableName
	The name of the layer as it is known in the active workspace.

Prefix
	The prefix will be used to start the name of any GIS layer that is exported from this data layer during the search. The naming followed for exported GIS layers is ``Prefix_subref.shp``, e.g. ``SSSIs_001.shp``. The use of the ``subref`` keyword in this case is predefined and cannot be changed.

Suffix
	The suffix will be used to finish the name of any tabular file that is exported from this data layer during the search. The naming followed for exported tabular data is ``subref_Suffix.Format``, e.g. ``0001_SSSIs.csv``. The use of the ``subref`` keyword in this case is predefined and cannot be changed.

Columns
	A comma-separated list of columns that should be included in the tabular data exported from this data layer during the search. The column names (not case sensitive) should match the column names in the source layer.

	.. note::
		A radius column (the radius of the search buffer) may be included by adding the keyword '%Radius%'. If any aggregate functions are included a name should be provided for the columns (e.g. 'COUNT(*) "RecCount"').

_`SelectCriteria`
	Selection criteria that should be used on the data layer during the search. These can be used to, for example, suppress confidential records, report on particular species only, or only include records after a certain date. The criteria take the form ``ColumnName Operand Value`` and may include ``AND`` and ``OR`` statements and similar. String values should be enclosed in double quotes. An example might be ``Name = "myName" AND Year > 2010``. Only records that match the criteria will be selected.

	.. note::
		Any clause specified here must adhere to MapInfo SQL syntax as the clause will be run within MapInfo.

ExportCriteria
	Additional criteria that will be applied **after** records have been selected using the `SelectCriteria`_ but **before** they are exported to a tabular output. Typically this is used to group and order records using the ``Group By`` and ``Order By`` clauses. Examples might be ``Group By SSSI_Name Order By SSSI_Name`` and ``Order By SORTORDER, LATIN_NAME``.

KeyColumn
	The name of the column containing the unique identifier for this data layer.

Format
	The format of tabular output exported from this data layer during a search. Options are ``csv`` and ``txt``. If ``txt`` is selected as a format no column names will be included in the output. They are included for ``csv`` output.

KeepLayer
	A Yes/No attribute that defines whether a GIS data layer should be kept of the features selected in this map layer during the search. If ``No`` is entered all geographical data generated for this data layer during the process will be deleted. If ``Yes`` is entered, a data layer will be created that follows the naming convention ``Prefix_subref.tab``. The use of the ``subref`` keyword in this case is predefined and cannot be changed. 

	.. note::
		If no features are selected in a data layer during a search, no new data layer will be created even if the KeepLayer attribute is set to ``Yes``

OverwriteLabels
	A Yes/No attribute that specifies whether the labels in this data layer can be overwritten for any GIS output. If the attribute is set to ``No``, labels will not be overwritten even if requested by the user through the 'Overwrite Map Labels' options on the form.

LabelColumn
	The name of the column in this data layer that contains the labels. If this entry has a column name that does not exist in the data layer the tool will create this label column. In this case, the features will be automatically numbered and numbering will follow the rule that is selected by the user through the 'Overwrite Map Labels' options on the form. If this attribute is left blank, no labels will be created or displayed for this layer even when requested by the user. 

_`LabelClause`
	A MapBasic clause that controls the labelling options, including expression used to construct the labels, the line call-out style, font type/size, label position and offset, overlap rules, duplicate controls and visibility. An example would be ``Font ("Arial",256,10,16711680,16777215) With Name Auto On``. If no clause is provided no labels will appear.

	.. note::
		For more information on how to set label clauses lookup the MapBasic **Set Map statement** instruction in the MapBasic Reference guide for your current version of MapInfo, available at `MapBasic product documentation <http://www.pbinsight.com/support/product-documentation/details/mapinfo-mapbasic>`_.

CombinedSitesColumns
	A comma-separated list of column names to be included in the combined sites table. If this entry is left blank the data layer will not be included in the combined sites table. A number of special cases apply to this attribute:

	- Any entry surrounded by double quotes (e.g. ``"SSSI"``) will be included in the combined sites table 'as is'. So, in the case of this example, each row that is added to the combined sites table from this data layer will have the entry 'SSSI' in the relevant column. This feature is useful in distinguishing which data layer each row in the combined sites table originates from. 

	- An entry of ``%Radius%`` means the search area radius size (e.g. '2km') that was used will be added to each row in the combined sites table for this data layer.

	.. note:: 
		The column headings of the combined sites table follow the 'Columns' entry under the CombinedSitesTable attribute in the general attributes. It is important to ensure that the CombinedSitesColumns are given in the same order as expected by this attribute.

CombinedSitesCriteria
	SQL criteria that will be applied **after** records have been selected using the `SelectCriteria`_ but **before** they are added to a combined sites table. Typically this is used to group and order records using the ``Group By`` and ``Order By`` clauses. An example might be ``Group By SiteDetails, Map_Label Order By SiteDetails, Map_Label``.

.. caution::
	All entries in the configuration file are **case sensitive**. Most common errors in the setting up of the tool are caused by using the incorrect case for entries.


.. raw:: latex

   \newpage

.. index::
	single: Installation

Installing the tool
===================

.. index::
	single: Installation; ArcGIS

Installing in ArcGIS
--------------------

Installing the tool in ArcGIS is straightforward. There are a few different ways it can be installed:

Installation through Windows Explorer
*************************************

Open Windows Explorer and double-click on the ESRI Add-in file for the data searches tool (:numref:`figInstallTool`).

.. _figInstallTool:

.. figure:: figures/AddInInstall.png
	:align: center

	Installing the Data Searches tool from Windows Explorer

.. raw:: latex

   \newpage

Installation will begin after confirming you wish to install the tool on the dialog that appears (:numref:`figConfirmInstall`).

.. _figConfirmInstall:

.. figure:: figures/AddInConfirmInstall.png
	:align: center

	Installation begins after clicking 'Install Add-in'


Once it is installed, it will become available to add to the ArcGIS interface as a button (see `CustomisingToolbarsArcGIS`_).

.. note::
	In order for this process to work all running ArcMap sessions must be closed. The tool will not install or install incorrectly if there are copies of ArcMap running.

.. raw:: latex

   \newpage

Installation from within ArcMap
*******************************

Firstly, open the Add-In Manager through the Customize menu (:numref:`figOpenAddInManager`).

.. _figOpenAddInManager:

.. figure:: figures/StartAddInManager.png
	:align: center

	Starting the ArcGIS Add-In Manager

.. raw:: latex

   \newpage

If the Data Searches tool is not shown, use the **Options** tab to add the folder where the tool is kept (:numref:`figAddInOptions`). The security options should be set to the lowest setting as the tool is not digitally signed.

.. _figAddInOptions:

.. figure:: figures/AddInOptions.png
	:align: center

	The 'Options' tab in the ArcGIS Add-In Manager

Once the tool shows in the Add-In Manager (:numref:`figAddInManager`), it is available to add to the ArcGIS interface as a button (see `CustomisingToolbarsArcGIS`_).

.. _figAddInManager:

.. figure:: figures/AddInManager.png
	:align: center

	The ArcGIS Add-In Manager showing the Data Searches tool


.. raw:: latex

   \newpage

.. _CustomisingToolbarsArcGIS:

Customising toolbars
********************

In order to add the Data Searches tool to the user interface, it needs to be added to a toolbar. It is recommended that this is done inside a document that has already been loaded with all the data layers that are required for the tool to run. The tool should then be saved with this document (see `Fundamentals of Saving your Customizations <http://desktop.arcgis.com/en/arcmap/10.3/guide-books/customizing-the-ui/fundamentals-of-saving-your-customizations.htm>`_ for an explanation of how customisations are stored within ArcGIS).

.. _figCustomizeMode:

.. figure:: figures/CustomizeMode.png
	:align: center

	Starting Customize Mode in ArcGIS


Customising toolbars is done through the Customize dialog, which can be started either through the Add-In Manager (by clicking **Customize**, see :numref:`figAddInManager`), or through choosing the 'Customize Mode...' option in the Customize Menu (:numref:`figCustomizeMode`).

.. raw:: latex

   \newpage

Once this dialog is open, ensure that the check box 'Create new toolbars and menus in the document' is checked in the **Options** tab (:numref:`figCustomizeOptions`).

.. _figCustomizeOptions:

.. figure:: figures/CustomizeAnnotated.png
	:align: center

	Customising the document in ArcGIS


.. raw:: latex

   \newpage

It is recommended that the button for the Data Searches tool is added to a new toolbar. Toolbars are created through the **Toolbars** tab in the Customize dialog, as shown in figures :numref:`figCustomizeToolbars` and :numref:`figNameToolbar`.

.. _figCustomizeToolbars:

.. figure:: figures/CustomizeToolbarsAnnotated.png
	:align: center

	Adding a new toolbar in ArcGIS

.. _figNameToolbar:

.. figure:: figures/NameNewToolbar.png
	:align: center

	Naming the new toolbar in ArcGIS


.. raw:: latex

   \newpage

Once a new toolbar is created and named, it is automatically added to the ArcMap interface as well as to the Customize dialog (:numref:`figNewToolbar`. In this case the toolbar was named 'TestToolbar'). 

.. _figNewToolbar:

.. figure:: figures/NewToolbarAddedAnnotated.png
	:align: center

	New toolbar added to the ArcGIS Interface


.. raw:: latex

   \newpage

As a final step the Data Searches tool is added to the toolbar. This is done from the **Command** tab in the Customize dialog (:numref:`figAddInCommands`). Click on **Add-In Controls** and the Data Searches tool will be shown in the right-hand panel.

.. _figAddInCommands:

.. figure:: figures/AddInCommandsAnnotated.png
	:align: center

	Finding the Data Searches tool in the add-in commands


.. raw:: latex

   \newpage

To add the tool to the toolbar, simply drag and drop it onto it (:numref:`figDragDropTool`). Close the Customize dialog and **save the document**. The Data Searches tool is now ready for its final configuration and first use.

.. _figDragDropTool:

.. figure:: figures/DragAndDropTool.png
	:align: center

	Adding the Data Searches tool to the new toolbar

.. raw:: latex

   \newpage

In order to function, the tool needs to know the location of the XML configuration file. The first time the tool is run, or whenever the configuration file is moved, a dialog will appear asking for the folder containing the XML file (:numref:`figFirstStart`). Navigate to the folder where the XML file is kept and click **OK**. If the XML file is present and its structure is correct, the Data Searches form will be shown. Even if the tool is not run at this time, the location of the configuration file will be stored for future use.

.. _figFirstStart:

.. figure:: figures/FirstStart.png
	:align: center

	Locating the configuration file folder


.. raw:: latex

   \newpage

.. index::
	single: Installation; MapInfo

Installing in MapInfo
---------------------

To install the tool in MapInfo, make sure that the configuration of the XML file as described above is complete, that the XML file is in the same directory as the tool MapBasic application (.MBX). Then, open `Tool Manager` in MapInfo by selecting :kbd:`Tools --> Tool Manager...` in the menu bar (:numref:`figToolManager`). 

.. _figToolManager:

.. figure:: figures/ToolManager.png
	:align: center

	The Tool Manager in MapInfo 12 or earlier


.. raw:: latex

   \newpage

In the `Tool Manager` dialog, click **Add Tool...**, then locate the tool using the browse button :kbd:`...` on the `Add Tool` dialog (:numref:`figAddTool`). Enter a name in the **Title** box (e.g. 'DataSearches'), and a description if desired. Then click **Ok** to close the `Add Tool` dialog.

.. _figAddTool:

.. figure:: figures/AddToolDialog.png
	:align: center

	Adding a tool in Tool Manager


.. raw:: latex

   \newpage

The tool will now show in the `Tool Manager` dialog (:numref:`figToolAdded`) and the **Loaded** box will be checked. To load the tool automatically whenever MapInfo is started check the **AutoLoad** box.  Then click **Ok** to close the `Tool Manager` dialog.

.. _figToolAdded:

.. figure:: figures/DataSearchesLoaded.png
	:align: center

	The Data Searches tool is loaded

The tool will now appear as a new entry in the `Tools` menu (:numref:`figToolMenu`).

.. _figToolMenu:

.. figure:: figures/DataSearchesToolMenu.png
	:align: center

	The Data Searches tool menu

.. note::
	The name that will appear in the `Tools` menu is dependent on the `ToolTitle`_ value in the configuration file, **not** the name given when adding the tool using the Tool Manager.

.. tip::
	It is recommended that a MapInfo Workspace is created that contains all the required GIS layers to run the tool. Once this workspace has been set up and the tool has been configured and installed, running the Data Searches tool becomes a simple process.

