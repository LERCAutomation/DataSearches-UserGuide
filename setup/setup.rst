*******************
Setting up the tool
*******************

This chapter describes Data Searches for MapInfo version |release|. Configure
the tool before making it available to users, and back up existing profiles
when upgrading.

.. index::
   single: Administrators; Installation and upgrades
   single: Upgrading the tool
   pair: Profiles; Backups

.. _administrator_checklist:

Administrator checklist
=======================

Use this checklist when preparing an installation or upgrading an existing one.

1. **Back up the installation and profiles.** Keep a copy of the current
   application, launch file, profiles and support files before replacing them.
   Read the :ref:`change_log` for changes since the installed version.
#. **Install the matching application and support files.** Use the compiled
   application supplied for the MapInfo version and its 32-bit or 64-bit edition.
   Keep the launch file, profiles and supplied icons together, and load the
   application using Tool Manager or the Tools window as described below.
#. **Check the configuration.** Review source and search-table names, reference
   and label columns, output paths and form defaults against :ref:`configuration`.
   Use the :ref:`profile migration table <profile_migration>` for older
   settings. Preserve XML node names, case and positional option order.
#. **Check access and optional components.** Users need access to source data
   and writable search tables and output folders. Check working-folder access
   and separation from final output when using ``WorkingDir``. If enabled,
   check the Access database, drivers and writable ``EnquiriesDir``, Universal
   Translator for SHP output, and any formatting script and its dependencies.
   Avoid concurrent searches writing the same final output names.
#. **Validate a representative search.** Use a separate test output folder.
   Check the log for errors, skipped layers and counts, then compare exported
   fields, filenames, retained GIS data, label values and map display with the
   request. Test lookup, working-folder transfer, SHP conversion, formatting
   scripts and combined sites append or overwrite where the installation uses
   them. Check an empty selection too; existing output files can remain.
#. **Prepare the routine workflow.** Save a workspace containing the required
   search and source tables. Give users the appropriate profile, output
   location and :ref:`quick_start` instructions once validation is complete.

.. index::
   single: Profiles; Migrating older settings
   single: Prefix
   single: Suffix

.. _profile_migration:

Migrating older profiles
------------------------

The current tool does not read the old naming settings below. Check the
:ref:`example_xml` when upgrading, and test the resulting filenames.

.. list-table:: Naming-setting replacements
   :header-rows: 1
   :widths: 28 28 44

   * - Location and old setting
     - Current setting
     - What to supply
   * - MapTables layer: ``Prefix``
     - :ref:`GISOutputName <setting_gisoutputname>`
     - Complete GIS base name, without extension.
   * - MapTables layer: ``Suffix``
     - :ref:`TableOutputName <setting_tableoutputname>`
     - Complete tabular-export base name, without extension.
   * - CombinedSitesTable: ``Suffix``
     - ``TableOutputName`` within :ref:`CombinedSitesTable <setting_combinedsitestable>`
     - Complete combined-sites export base name, without extension.

The reference is not added automatically. For example, use
``SSSIs_%subref%_%radius%`` as ``GISOutputName`` and
``%subref%_SSSIs_%radius%`` as the layer's ``TableOutputName``. With reference
``001`` and a 1 km buffer, these produce ``SSSIs_001_1km.tab`` and
``001_SSSIs_1km.csv`` when TAB and CSV outputs are enabled. Use
``%subref%_sites`` for the combined-sites export to produce ``001_sites.csv``.
The retained combined TAB name is configured separately by its ``TableName``.

.. index::
   single: Installation
   single: MapInfo; Loading the tool
   single: Tool Manager
   single: AutoLoad

Installing the tool
===================

Use the compiled application supplied for your MapInfo version and its 32-bit
or 64-bit edition. Copy the application and its supplied support files to the
installation folder. Keep ``DataSearches.xml``, the profile XML files and the
supplied ribbon icons with the application. Source files alone are not a
runnable installation.

Load the application using MapInfo's **Tool Manager** or **Tools** window.
In the classic interface, choose **Tools --> Tool Manager**, select **Add Tool**,
browse to the application and enter a title. Select **Loaded** to load it now
and **AutoLoad** to load it whenever MapInfo starts. Ribbon editions have
equivalent tool-management controls with a different layout.
:numref:`figAddTool` identifies the adding and loading steps.

.. _figAddTool:

.. figure:: figures/AddToolDialog.png
   :align: center

   Adding and loading the Data Searches application in MapInfo

The classic interface adds a **Data Searches** menu under **Tools**, with
**Run**, **About** and **Exit** commands. The 64-bit ribbon interface adds a
button in the **Home** tab's **Tools** group, illustrated in
:numref:`figLaunchRibbon`. Its title comes from :ref:`ToolTitle <setting_tooltitle>`
in the launch configuration.

.. tip::
   Save a workspace containing the search-sites table and all source tables
   required by the profiles. Open these before opening the search form, and
   include the search-sites table in a map window.

.. index::
   single: Requirements
   pair: Folders; Permissions
   single: Search table; Write access

Requirements and folder access
------------------------------

Users need access to the installation, source data and final output folders.
The search-sites table must be writable: MapInfo uses it temporarily during
buffer creation and commits pending edits before that step. Save or discard
other edits before running the tool.

Database lookup needs a readable Access database, a writable ``EnquiriesDir``
and suitable database drivers. If ``WorkingDir`` is configured, it must be
writable and Windows ``robocopy.exe`` must be available. SHP output requires
the Universal Translator configured by ``UTPath`` and ``UTCommand``. An optional
export ``Macro`` requires Windows Script Host and any software used by the script.

.. index::
   single: Configuring the tool
   single: XML; Profiles
   pair: XML; Configuration
   single: Profiles; Creating and choosing
   single: DataSearches.xml
   single: DefaultProfile.xml
   single: DefaultProfile
   single: ToolTitle

.. _configuration:

Configuring the tool
====================

.. _setting_tooltitle:

Keep both parts of the configuration alongside the compiled application:

* ``DataSearches.xml`` is the launch configuration. Its ``DataSearches`` node
  contains ``ToolTitle`` and ``DefaultProfile``.
* A profile, usually ``DefaultProfile.xml``, contains the general settings and
  ``MapTables`` definitions under its own ``DataSearches`` node.

.. _setting_defaultprofile:

One profile is used automatically. With several XML files other than
``DataSearches.xml``, the tool asks the user to choose. Keep unrelated XML files
out of the application folder. ``DefaultProfile`` sets the initially selected
file; include ``.xml``. If blank, the default is ``DefaultProfile.xml``.

.. caution::
   Keep the launch file name ``DataSearches.xml``. The tool excludes it from
   the profile list, so a separate profile is required. Preserve node names
   and their case.

Edit XML in a text or XML editor. A setting normally has the form
``<Example><value>setting</value></Example>``. Closing tags use a forward slash.
Check the XML for well-formedness after editing; valid XML can still contain
incorrect paths, table names or SQL. The appendix provides
:ref:`downloadable examples <example_xml>`.

.. index::
   pair: XML; Special characters

Special characters in XML
-------------------------

Within values, escape ``<`` as ``&lt;`` and ``&`` as ``&amp;``. Escaping ``>``
as ``&gt;`` is also good practice. For example::

   <SelectCriteria>
       <value>Year &gt; 2010 And Status &lt;&gt; "Confidential"</value>
   </SelectCriteria>

The XML reader restores these characters before passing the expression to
MapInfo. Double quotes within element text do not need escaping.

.. index::
   single: XML; Variables
   pair: File names; Variables
   single: Variables; Search details

.. _naming_variables:

Naming variables
----------------

These variables work in ``SaveFolder``, ``GISFolder``, ``LogFileName``,
``BufferSaveName``, ``SearchFeatureName``, ``GroupLayerName``, each layer's
``GISOutputName`` and ``TableOutputName``, and the combined sites
``TableOutputName``. Use the lower-case spellings shown.

.. list-table::
   :header-rows: 1
   :widths: 26 74

   * - Variable
     - Meaning
   * - ``%ref%``
     - Full search reference entered on the form.
   * - ``%shortref%``
     - Numeric part of the reference, with separators processed for names.
   * - ``%subref%``
     - Final part of the processed numeric reference.
   * - ``%sitename%``
     - Site name entered or retrieved from the database.
   * - ``%organisation%``
     - Organisation retrieved using ``OrgColumn``.
   * - ``%partner%``
     - Partner retrieved using ``PartnerColumn``.
   * - ``%radius%``
     - Buffer size and unit abbreviation; decimal points become underscores
       in names, for example ``1_5km``.

The reference variables depend on :ref:`RepChar <setting_repchar>`.
For ``XYBRC/2026/001``, the current processing gives:

.. list-table:: Reference-variable examples
   :header-rows: 1
   :widths: 34 33 33

   * - RepChar
     - %shortref%
     - %subref%
   * - Space, as in the appendix profile
     - ``2026_001``
     - ``2026_001``
   * - Underscore (``_``)
     - ``2026_001``
     - ``001``
   * - Blank
     - ``2026001``
     - ``2026001``

The tool converts spaces to underscores before looking for the final
``RepChar`` separator. With a space replacement, that separator is no longer
present, so ``%subref%`` keeps the whole processed reference. Check your own
reference patterns before changing an existing profile. The worked example's
reference ``001`` gives ``001`` for both variables with all three settings.

Special characters are replaced and spaces in GIS table names become underscores.
Specify complete output names; a reference is not added automatically.
Variables are not expanded in ``WorkingDir`` or ``SaveRootDir``.

.. index::
   single: Profiles; General settings

General profile settings
========================

.. index::
   pair: Access database; Configuration
   single: Search table; Configuration

Database and search tables
--------------------------

.. index::
   single: Debug
   single: Log files; Diagnostic messages

.. _setting_debug:

Debug
   ``Yes`` adds diagnostic messages to the log.

.. index::
   single: Database

.. _setting_database:

Database
   Full Access database path, including its extension. Leave blank to run
   without lookup and enter the site name manually.

.. index::
   single: EnquiriesDir
   single: EnquiriesTable

.. _setting_enquiriesdir:

EnquiriesDir
   Writable folder for the Access table's ``Enquiries.tab`` registration.

.. _setting_enquiriestable:

EnquiriesTable
   Table inside the Access database, for example ``Enquiries``.

.. index::
   single: RefColumn
   single: Search reference; Configuration

.. _setting_refcolumn:

RefColumn
   Reference column used in both the Access table and ``SearchTable``. Use
   the same column name in both. Text references support MapInfo ``LIKE`` patterns.

.. index::
   single: SiteColumn
   single: OrgColumn
   single: PartnerColumn

.. _setting_sitecolumn:

.. _setting_orgcolumn:

.. _setting_partnercolumn:

SiteColumn, OrgColumn, PartnerColumn
   Access columns holding the site name, requester organisation and partner.
   Leave unused names blank. The optional search-table update uses these names too.

.. index::
   single: RadiusColumn

.. _setting_radiuscolumn:

RadiusColumn
   Search-table column intended to receive the buffer size and units during
   an optional update. It does not retrieve a radius from Access. Leave blank
   if unused.

.. index::
   single: RequireSiteName
   single: Site name; Required or optional

.. _requiresitename:

.. _setting_requiresitename:

RequireSiteName
   ``Yes`` requires a site name; ``No`` permits a blank. With lookup enabled,
   the site-name control is disabled and **Find** retrieves the name. Without
   lookup the field is editable.

.. index::
   single: SearchTable

.. _setting_searchtable:

SearchTable
   Open MapInfo table containing the search locations. One profile uses one
   search table; several matching features can be selected. Its reference
   column is ``RefColumn``. ``SearchColumn`` is not read by the current tool.

.. index::
   single: AggregateColumns
   single: Buffer; Preserving attributes

.. _setting_aggregatecolumns:

AggregateColumns
   MapBasic ``Data`` assignments used when creating the buffer, for example
   ``EnquiryRef=EnquiryRef, SiteName=SiteName``. Preserve fields needed by
   buffer-based export expressions. This is not just a list of field names.

.. index::
   single: UpdateTable
   single: Search table; Updating attributes

.. _setting_updatetable:

UpdateTable
   Controls the optional attempt to update search-table attributes from lookup
   values and the radius. Set explicitly to ``No`` unless this operation has
   been checked for your installation; see :doc:`the running instructions <../execute/execute>`. It does
   not make the table read-only during buffering.

.. index::
   pair: Outputs; Folders
   single: Log files; Configuration

Output folders and logging
--------------------------

.. index::
   single: RepChar
   single: File names; Special characters

.. _setting_repchar:

RepChar
   Replacement for special characters in generated names. A space is allowed.
   Choose a character suitable for Windows file names and MapInfo table names.

.. index::
   single: SaveRootDir
   single: SaveFolder
   single: GISFolder

.. _setting_saverootdir:

SaveRootDir
   Full final output root, such as ``D:\DataSearches\Reports`` or a UNC path.

.. _setting_savefolder:

SaveFolder
   Request folder beneath the root. Supports :ref:`naming_variables`.
   Leave blank to use the root directly.

.. _setting_gisfolder:

GISFolder
   Output folder beneath the request folder. Supports naming variables.
   Leave blank to use the request folder directly.

.. index::
   single: WorkingDir
   pair: Folders; Working storage
   single: Robocopy

.. _working_directory:

.. _setting_workingdir:

WorkingDir
   Optional working root, preferably local when final outputs are on a network.
   Each run creates a fresh subfolder beneath it. Interrupted runs are retained
   and are neither cleared nor included in later runs. Leave blank or omit
   this setting to process directly in the final GIS folder. The working run
   folder and final folder must not overlap.

   After processing, saved tables are committed and closed and Robocopy moves
   the current run's files to the final GIS folder before results are mapped.
   Matching outputs are replaced; unrelated destination files are retained.
   For an append, the existing combined sites table is copied into the fresh
   working folder first.

   A failed move stops mapping and retains untransferred files. A partial move
   can leave files in both locations. The log identifies both folders. See
   :ref:`transfer_recovery` before retrying.

.. index::
   single: LogFileName
   single: Log files; Temporary journal

.. _setting_logfilename:

LogFileName
   Final log name, including an extension such as ``.log``. Supports naming
   variables. A temporary journal adds ``_tmp`` before the extension.

.. index::
   single: DefaultClearLogFile

.. _setting_defaultclearlogfile:

DefaultClearLogFile
   ``Yes`` initially checks **Clear log file?**; ``No`` appends to the final
   log. This setting does not control output overwriting.

.. index::
   single: Buffer; Configuration
   single: Search features; Configuration

Buffer and search-feature settings
----------------------------------

.. index::
   single: DefaultBufferSize

.. _setting_defaultbuffersize:

DefaultBufferSize
   Initial buffer size. Blank or zero hides the size control and uses zero.
   See :doc:`the running instructions <../execute/execute>` before configuring radii below one unit.

.. index::
   single: BufferUnitOptions
   single: DefaultBufferUnit

.. _setting_bufferunitoptions:

BufferUnitOptions
   Display-name and MapInfo-unit pairs separated by ``$``, with ``;`` between
   each name and abbreviation, for example ``Metres;m$Kilometres;km$``.

.. _setting_defaultbufferunit:

DefaultBufferUnit
   One-based position in ``BufferUnitOptions``. Blank hides the control; the
   code then uses position 3 internally, so retain a valid third option.

.. index::
   single: KeepBufferArea
   single: KeepSearchFeature

.. _setting_keepbufferarea:

.. _setting_keepsearchfeature:

KeepBufferArea, KeepSearchFeature
   ``Yes`` retains the buffer or selected search features as TAB files and adds
   them to map windows. ``No`` removes the corresponding temporary table.
   These are separate from the data-layer retention and mapping choices.

.. index::
   single: BufferSaveName
   single: SearchFeatureName

.. _setting_buffersavename:

.. _setting_searchfeaturename:

BufferSaveName, SearchFeatureName
   Retained table names without extensions. Supports naming variables.

.. index::
   single: BufferSymbology
   single: SearchAreaSymbology
   single: Symbology; Buffer and search features

.. _setting_buffersymbology:

.. _setting_searchareasymbology:

BufferSymbology, SearchAreaSymbology
   MapBasic global display styles for the buffer and search-feature layers,
   applied for **Layers only** or **Layers and tables**. Follow the example
   profile's syntax.

.. _setting_buffer:

.. _setting_searcharea:

Buffer, SearchArea
   Optional sections with ``Symbology`` rules for saved object styles. Each
   ``Symbol`` rule has ``Clause`` (filter, or blank for all), ``Object``
   (``Region``, ``Line`` or ``Point``), and the appropriate ``Pen`` and ``Brush``,
   ``Pen``, or ``Symbol`` values. Each value uses a ``value`` child element.
   Rules apply to saved buffer and search-feature objects for **Layers and tables**.

.. index::
   single: CoordinateSystem
   single: Coordinate systems

.. _coordinate_system:

.. _setting_coordinatesystem:

CoordinateSystem
   Existing profiles may contain this setting. The current source reads it
   but does not apply a coordinate-system command. Configure source tables
   appropriately rather than relying on this setting to reproject output.

.. index::
   single: RecMax
   pair: Selection; Record limit

.. _setting_recmax:

RecMax
   Maximum spatially selected record count for each layer. Exceeding it skips
   the whole layer and logs the reason; it does not truncate the selection.
   Set a positive limit suited to your data and MapInfo's table-size limits.

.. index::
   pair: Profiles; Form defaults
   single: Map display; Configuration

.. _form_defaults:

Form defaults and map display
-----------------------------

Options are positional. Keep their order as shown; changing the wording does
not change the behaviour assigned to each position. Defaults are one-based.

.. index::
   single: AddSelectedTablesOptions
   single: DefaultAddSelectedTables

.. _setting_addselectedtablesoptions:

.. _setting_defaultaddselectedtables:

AddSelectedTablesOptions, DefaultAddSelectedTables
   ``No;Yes - Without labels;Yes - With labels``. Blank default hides the
   control and uses **No**.

.. index::
   single: KeepSelectedTablesOptions
   single: DefaultKeepSelectedTables

.. _setting_keepselectedtablesoptions:

.. _setting_defaultkeepselectedtables:

KeepSelectedTablesOptions, DefaultKeepSelectedTables
   ``None;TAB;SHP;BOTH``. Blank default hides the control and uses **None**.
   The layer also needs ``KeepLayer=Yes``. Requesting map display retains its
   TAB file even for **None** or **SHP**.

.. index::
   single: ApplySymbologyOptions
   single: DefaultApplySymbology

.. _setting_applysymbologyoptions:

.. _setting_defaultapplysymbology:

ApplySymbologyOptions, DefaultApplySymbology
   ``None;Layers only;Layers and tables``. Blank default hides the control
   and uses **None**. Layer styles affect displayed results; table styles
   affect saved buffer and search-feature objects.

.. index::
   single: GroupLayerName
   single: Map display; Results group

.. _setting_grouplayername:

GroupLayerName
   Results group name in map windows. Supports naming variables.

.. index::
   single: OverwriteLabelOptions
   single: DefaultOverwriteLabels

.. _setting_overwritelabeloptions:

.. _setting_defaultoverwritelabels:

OverwriteLabelOptions, DefaultOverwriteLabels
   ``No;Yes - Reset Each Layer;Yes - Reset Each Group;Yes - Do Not Reset``.
   Blank default hides the control and uses **No**. Numbering also affects
   output attributes, subject to each layer's ``OverwriteLabels`` setting.

.. index::
   single: CombinedSitesOptions
   single: DefaultCombinedSitesTable

.. _setting_combinedsitesoptions:

.. _setting_defaultcombinedsitestable:

CombinedSitesOptions, DefaultCombinedSitesTable
   ``None;Append to existing table;Overwrite existing table``. Blank default
   hides the control and uses **None**. Configure a separate ``WorkingDir``
   before appending to an existing table; see :doc:`the running instructions <../execute/execute>`.

.. index::
   single: CombinedSitesTable
   single: Combined sites table; Configuration

.. _setting_combinedsitestable:

CombinedSitesTable
   Defines the combined sites TAB table and its tabular export:

   TableName
      Internal TAB name, without extension, for example ``Sites``. Keep it
      distinct from source and other output table names.
   Columns
      Ordered MapBasic column definitions with types and lengths, for example
      ``Site_Type Char(20), Site_Name Char(100), Map_Label Char(10)``.
   TableOutputName
      Export base name, supporting naming variables, for example ``%subref%_sites``.
      The former ``Suffix`` setting is not read.
   Format
      ``csv``, ``txt`` or ``dbf``. CSV has headings; TXT is comma-delimited
      without headings. The TAB table is retained for future appends.

.. index::
   single: UTPath
   single: UTCommand
   pair: Shapefiles; Universal Translator

.. _setting_utpath:

.. _setting_utcommand:

UTPath, UTCommand
   Folder and executable of the installed Universal Translator for SHP output,
   for example the MapInfo ``UT`` folder and ``Fme.exe``. Older installations
   may use ``Imut.exe``. Conversion errors are logged.

.. index::
   single: Map layer attributes
   pair: Profiles; Map layer settings
   single: MapTables

.. _map_layer_settings:

Map layer settings
==================

Each child of ``MapTables`` defines a search. ``Sites_-_SSSIs`` appears as
**Sites - SSSIs**: underscores become spaces. The part before a hyphen supplies
the logical group for label numbering. Several definitions can use the same
source table with different filters. The :ref:`downloadable profile
<example_xml>` shows the current XML structure for one definition.


.. index::
   single: TableName

.. _setting_tablename:

TableName
   Source table name as it is open in MapInfo, without path or extension.

.. index::
   single: GISOutputName

.. _setting_gisoutputname:

GISOutputName
   GIS file base name for TAB and SHP output. Supports naming variables.
   The former ``Prefix`` setting is not read.

.. index::
   single: TableOutputName

.. _setting_tableoutputname:

TableOutputName
   Tabular export base name without extension. Supports naming variables.
   The former ``Suffix`` setting is not read.

.. index::
   single: Columns
   single: Tabular exports; Columns

.. _setting_columns:

Columns
   Comma-separated MapInfo SQL expressions for export, including source fields,
   calculated expressions, aggregates with aliases and :ref:`export_expressions`.
   Blank ``Columns`` or ``Format`` skips tabular export without preventing
   GIS or combined sites output.

.. index::
   single: SelectCriteria
   pair: Selection; Filters

.. _setting_selectcriteria:

SelectCriteria
   Optional condition applied with the spatial selection, for example
   ``Year > 2010 And Confidential <> "Y"``. Omit any leading ``Where`` or
   ``And``: the tool adds ``And (...)``. Escape XML special characters.

.. index::
   single: ExportCriteria
   single: Tabular exports; Grouping and sorting

.. _setting_exportcriteria:

ExportCriteria
   Extra SQL after the export spatial condition, commonly
   ``Group By ... Order By ...``. Further filters must begin with ``And``.

.. index::
   single: KeyColumn
   single: Labels; Ordering by key

.. _setting_keycolumn:

KeyColumn
   Optional source column for ordering and assigning consistent label numbers
   to records sharing a key. Numeric keys are supported.

.. index::
   single: Format
   single: CSV files
   single: TXT files
   single: DBF files
   single: Tabular exports; Formats

.. _setting_format:

Format
   ``csv``, ``txt`` or ``dbf``. CSV has column headings; TXT is comma-delimited
   without headings. Exports use the WindowsLatin1 character set.

.. index::
   single: Macro
   pair: Tabular exports; Formatting scripts
   single: XLSX files

.. _setting_macro:

Macro
   Optional full path to a Windows Script Host script run after export. It
   receives the working folder, exported file name and expected XLSX file name
   as three arguments. A non-zero exit or missing XLSX is reported. Leave blank
   if no script is required.

.. index::
   single: KeepLayer

.. _setting_keeplayer:

KeepLayer
   ``Yes`` allows GIS retention and mapping; ``No`` removes GIS output after
   tabular export and combined sites processing. Formats follow **Keep Selected
   Tables**. Empty or over-limit selections do not produce new outputs.

.. index::
   single: LoadWarning

.. _setting_loadwarning:

LoadWarning
   ``No`` suppresses warnings for a source table that is not open. It remains
   excluded from the form.

.. index::
   single: PreselectLayer
   single: Tables; Preselection

.. _setting_preselectlayer:

PreselectLayer
   ``Yes`` highlights this definition on opening the form. Users can change it.

.. index::
   single: OverwriteLabels

.. _setting_overwritelabels:

OverwriteLabels
   ``Yes`` allows the form's overwrite option to number the output label column.
   ``No`` preserves existing values. Changes affect output, not source data.

.. index::
   single: LabelColumn
   single: LabelClause
   single: Labels; Configuration

.. _setting_labelcolumn:

LabelColumn
   Column used for labels; it must exist or be successfully created in output.
   For sequential numbers, use ``OverwriteLabels=Yes`` and an overwrite option.
   Do not rely on a missing column being numbered when overwriting is disabled.

.. _setting_labelclause:

LabelClause
   MapBasic label clause, for example
   ``Font ("Arial",0,10,0) With Map_Label Auto On``. When blank and a valid
   ``LabelColumn`` exists, the current tool uses ``With LabelColumn``. Use an
   explicit clause to control appearance and visibility.

.. index::
   single: Symbology; Data layers

.. _setting_symbology:

Symbology
   Global display style applied when the output is mapped and symbology is
   enabled, for example
   ``Global Pen (2,2,16711680) Global Brush (1,16777215,16777215)``.
   This is a single ``value``, unlike the ``Buffer`` and ``SearchArea`` rules.

.. index::
   single: CombinedSitesColumns
   single: CombinedSitesCriteria

.. _setting_combinedsitescolumns:

CombinedSitesColumns
   Expressions inserted into ``CombinedSitesTable``. Their count, order and
   types must match its ``Columns``. Blank excludes this layer. Quoted text
   can identify the source, for example ``"SSSI", SiteName, Map_Label``.

.. _setting_combinedsitescriteria:

CombinedSitesCriteria
   Extra SQL for combined sites selection, commonly ``Group By ...`` or
   ``Order By ...``. Start additional filters with ``And``. This is independent
   of ``ExportCriteria``.

.. note::
   Historical comments mention ``OutputType``, but the current profile reader
   does not read it. Selected GIS features are copied in full when they
   intersect the buffer; that setting does not clip their geometry. Overlap
   expressions can report intersecting areas.

.. index::
   pair: Tabular exports; Expressions
   single: Measurements; Area and length
   single: Overlap; Area and length
   single: Variables; Measurements

.. _export_expressions:

Export expressions and measurements
===================================

``Columns`` and ``CombinedSitesColumns`` accept the lower-case search variables
listed under :ref:`naming_variables`. Variables become quoted values: do not
quote the variable itself. Supply aliases where needed, for example
``%radius% "Radius"`` or ``%ref% "SearchRef"``. Radius values here retain their
decimal point, for example ``1.5km``.

.. list-table::
   :header-rows: 1
   :widths: 28 72

   * - Expression
     - Result
   * - ``%overlap%`` or ``%overlaparea%``
     - Selected source-feature area overlapping the buffer, in hectares.
   * - ``%searcharea%``
     - Buffer/search area, in hectares.
   * - ``%searchlen%``
     - Buffer/search object length, in metres.
   * - ``%inputarea%``
     - Full selected data-layer feature area, in hectares.
   * - ``%inputlen%``
     - Selected data-layer feature length, in metres.
   * - ``%searchlayer%``
     - Buffer table name, for attribute expressions such as
       ``%searchlayer%.EnquiryRef "SearchRef"``.

For overlap length, use ``%overlapLen%`` in ``Columns`` and ``%overlaplen%`` in
``CombinedSitesColumns``; the spellings differ in the current code. Measurements
depend on geometry type. The ``input`` expressions refer to selected data-layer
features, not the original search-site polygon.

During ordinary export expressions the selected data table is ``Select_Table``
and the buffer is ``Buffer_Area``. Qualify ambiguous field names. Preserve any
buffer attributes needed by expressions through ``AggregateColumns``.

.. caution::
   Keep XML nodes and variables exactly as shown. Check profiles with
   representative data, empty selections, repeated runs and combined sites
   appends before making them available to users.
