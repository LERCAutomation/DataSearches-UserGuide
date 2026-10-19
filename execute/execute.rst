****************
Running the tool
****************

For a routine search, follow :doc:`../quickstart/quickstart`. This chapter
explains the form options and results in more detail.

Before opening the form, load the workspace containing the configured
search-sites table and the source data tables. Ensure the chosen profile and
output locations are available. If lookup is enabled, the Access database
must also be available. See :doc:`../setup/setup` for configuration details.

.. index::
   single: Running the tool
   single: Search form; Opening
   single: Profiles; Choosing

Opening the form
================

In the classic interface, select **Tools --> Data Searches --> Run Data Searches**.
In the 64-bit ribbon interface, click **Data Searches** in the **Home** tab's
**Tools** group. The title may differ if ``ToolTitle`` has been customised.
:numref:`figLaunchRibbon` shows the ribbon button.

.. _figLaunchRibbon:

.. figure:: figures/LaunchSearchesTool.png
   :align: center

   Launching Data Searches from the MapInfo ribbon

If several profiles are available, choose the required one. With one profile,
it is selected automatically. The profile controls the available tables and
the initial form settings. A source table that is not open is omitted from
the list, with a warning unless its ``LoadWarning`` is ``No``. The search-sites
table itself must be open or the form will not load.

If a configured source table is missing, open it in MapInfo and reopen the
search form.

:numref:`figDisplayForm` identifies the controls used in the following steps.
The profile can hide optional controls; the illustrated profile shows them all.

.. _figDisplayForm:

.. figure:: figures/DisplayForm.png
   :align: center

   Annotated Data Searches form: reference, tables, buffer and output options


Using the form
==============

.. index::
   single: Search reference; Entering
   pair: Site name; Lookup
   single: Access database; Finding an enquiry
   single: Search reference; Wildcards

Search reference and site name
------------------------------

Enter the reference in **Search Ref**. With Access lookup enabled, click
**Find** to retrieve the site name, organisation and partner. The site-name
field is disabled in this mode; correct a missing or incorrect name in the
database, or use an administrator-prepared profile without lookup. Without
lookup, type the site name manually. The site name can be blank when
:ref:`RequireSiteName <requiresitename>` is ``No``.

The reference, **Find** button and site-name field are identified in
:numref:`figDisplayForm`.


The reference must identify the required features in the configured search
table. Text references use MapInfo ``LIKE`` matching and can contain wildcard
patterns. A pattern can select several search features; Access lookup uses
the first matching enquiry. Use a full reference for a single request.

.. index::
   single: Tables; Selecting
   single: Buffer; Size and units
   single: Radius; Buffer size
   single: Units; Buffer
   single: Buffer; Zero radius

Selecting tables and the buffer
-------------------------------

Highlight the definitions to process in **MapInfo Tables**. Use **Ctrl** for
individual selections or **Shift** for a range. Preselected definitions can
be deselected. At least one table must be selected.


Choose **Buffer Size** and **Buffer Units**. Zero uses the selected search
geometry without expanding it, including point or line geometry. Decimal
values can be entered, but the current buffer calculation treats values below
one unit as zero; use smaller units to express such a distance, for example
``500 m`` rather than ``0.5 km``. Blank or zero buffer defaults may hide these
controls. See :numref:`figDisplayForm` for the table list and buffer controls.

.. index::
   pair: Map display; Adding results
   single: Add Selected Tables to Map

Adding results to maps
----------------------

**Add Selected Tables to Map** has these choices:

* **No**: do not add the selected data-layer outputs to maps.
* **Yes - Without labels**: add the retained outputs without requesting labels.
* **Yes - With labels**: add the outputs using each layer's label settings.


A definition with ``KeepLayer=No`` is not mapped. These choices do not control
the buffer and original search-feature layers: their own ``KeepBufferArea``
and ``KeepSearchFeature`` settings control retention and display.

.. index::
   pair: GIS files; Retention
   single: Keep Selected Tables
   single: TAB files
   single: Shapefiles; Retention

Keeping GIS files
-----------------

**Keep Selected Tables** controls the saved GIS formats for definitions whose
``KeepLayer`` is ``Yes``:

* **None**: no retained GIS file, unless a TAB file is needed for map display.
* **TAB**: keep MapInfo TAB files and their associated files.
* **SHP**: create shapefiles using the configured Universal Translator.
* **BOTH**: keep TAB files and create shapefiles.


Map display retains a TAB file even when **None** or **SHP** is chosen.
Tabular exports and the combined sites table are controlled separately.
Keep all companion files together when moving TAB tables or shapefiles.
See :ref:`output_formats` for the interaction with mapping and other exports.

.. index::
   pair: Symbology; Applying styles
   single: Apply Symbology to Tables

Applying symbology
------------------

**Apply Symbology to Tables** has three choices:

* **None**: do not apply configured symbology.
* **Layers only**: apply configured global display styles to mapped results,
  including retained buffer and search-feature layers.
* **Layers and tables**: also apply the profile's object-style rules to the
  saved buffer and search-feature tables.


The table-style rules apply to the buffer and search-feature sections. A data
layer's own ``Symbology`` value controls its display in map windows.

.. index::
   pair: Labels; Numbering
   single: Overwrite Map Labels
   single: Labels; Reset limitations

.. _label_numbering:

Labels
------

**Overwrite Map Labels** controls numbering in the selected output tables:

* **No**: retain existing label values.
* **Yes - Reset Each Layer**: restart numbering for each layer.
* **Yes - Reset Each Group**: request numbering by the group name before the
  hyphen in a layer definition; see the current limitation below.
* **Yes - Do Not Reset**: continue numbering across layers.


Each layer must allow overwriting and define a suitable ``LabelColumn``.
Numbering can also be used in tabular exports and the combined sites table;
it is not restricted to runs that display map labels. To display those values,
choose **Yes - With labels** under **Add Selected Tables to Map**.

.. note::
   The current implementation starts a reset sequence at 2 and does not reset
   the group counter as intended when changing groups. Use **Reset Each Layer**
   or **Do Not Reset** where predictable sequences are required, and check the
   generated values.

.. index::
   pair: Combined sites table; Appending and overwriting
   single: Create Combined Sites Table
   single: Log files; Clearing or appending

Combined sites table and log
----------------------------

**Create Combined Sites Table** offers:

* **None**: do not create or update it; existing output remains.
* **Append to existing table**: add rows to the existing TAB table, or create
  one if none exists. Only definitions with ``CombinedSitesColumns`` contribute.
* **Overwrite existing table**: create a fresh table, replacing the previous one.


Use a configured working root when appending: the current append operation
attempts a folder copy even when working storage is disabled.

Check **Clear log file?** to replace the previous final log, or leave it
unchecked to append this run's messages. It does not change output retention
or overwriting. Controls with blank profile defaults may be hidden, using
the initial **No** or **None** choice.


.. index::
   single: Searches; Starting and finishing
   single: Log files; Checking results

Starting and finishing a search
===============================

Click **Ok** to start. Wait for processing and any file transfer to finish.
The tool selects matching search features, creates the buffer, processes the
selected definitions and generates the configured outputs.

If a :ref:`working folder <working_directory>` is configured, outputs are
created in a fresh run folder and then moved to the final GIS folder before
map display. Otherwise processing writes directly to the final folder. Local
working storage does not remove the requirement for access to the final folder.

When prompted **Do you wish to close the form?**, choose **No** to retain the
current selections for another run. The final log opens in Notepad. Check it
for errors, skipped layers, selection counts, export counts and transfer
messages before using the results. A completion message does not establish
that every layer, formatting script or shapefile conversion succeeded.

See :ref:`run_logs` for log timing, examples and diagnostics.

.. index::
   pair: Outputs; Overwriting
   single: Combined sites table; Duplicate records

.. _OverwriteWarning:

.. caution::
   Reusing output names can replace files from a previous run. Names depend
   on the profile, not just the search reference. Include ``%radius%`` in
   output names or move earlier results if both searches must be kept.

   Appending the same layer again can duplicate combined sites records.
   Overwrite replaces the combined table; append does not remove duplicates.
   A layer producing no new output does not clear older files with that name.

.. index::
   single: Search results
   single: Selection; Whole features
   single: Map display; Results group

Search results
==============

Final outputs are stored beneath ``SaveRootDir``, then ``SaveFolder`` and
``GISFolder`` where those are non-blank. Depending on the profile and choices,
they include CSV, TXT or DBF exports, TAB and/or SHP data, retained search and
buffer tables, the combined sites TAB table and export, optional formatted
XLSX files, and logs.

Spatial selection copies whole data features that intersect the buffer; it
does not clip their geometry. Export expressions can calculate overlap areas.
If a selection is empty or exceeds ``RecMax``, the layer is skipped and logged.

Mapped output is added to each map window containing its source layer. If
none contains it, the tool attempts to use the active map window. Results are
placed in the configured group. Retained buffer and search-feature layers
are added separately, and the map view is adjusted to the buffer extent.

:numref:`figResults` identifies the results group, output layers, labels and
retained search and buffer features in MapInfo.

.. _figResults:

.. figure:: figures/Results.png
   :align: center

   Annotated MapInfo search results and retained search geometry

.. index::
   single: Output formats; Quick reference
   single: KeepLayer; Output-format interaction
   single: TAB files; Mapping and retention
   single: Combined sites table; Output formats

.. _output_formats:

Output format reference
=======================

For a selected data-layer definition with :ref:`KeepLayer <setting_keeplayer>`
set to ``Yes``, these choices apply after successful processing:

.. list-table:: Retained data-layer GIS files
   :header-rows: 1
   :widths: 24 38 38

   * - Keep Selected Tables
     - Add Selected Tables to Map: No
     - Either Yes mapping choice
   * - None
     - No retained data-layer GIS file.
     - TAB retained for map display.
   * - TAB
     - TAB retained.
     - TAB retained and mapped.
   * - SHP
     - SHP created; TAB removed.
     - SHP created and TAB retained for map display.
   * - BOTH
     - TAB retained and SHP created.
     - TAB retained and mapped; SHP created.

``KeepLayer=No`` prevents retained GIS output and mapping for that data-layer
definition. It does not prevent its tabular export or contribution to combined
sites. SHP creation requires a working Universal Translator configuration;
check the log for conversion failures.

.. list-table:: Outputs controlled separately
   :header-rows: 1
   :widths: 25 75

   * - Output
     - Controls and behaviour
   * - Layer CSV, TXT or DBF
     - :ref:`Columns <setting_columns>` and :ref:`Format <setting_format>`.
       Blank Columns or Format skips this export. CSV has headings; TXT is
       comma-delimited without headings. GIS-retention choices do not select
       the tabular format.
   * - Combined sites
     - **Create Combined Sites Table**, :ref:`CombinedSitesTable
       <setting_combinedsitestable>` and each layer's
       :ref:`CombinedSitesColumns <setting_combinedsitescolumns>`. Creates or
       updates a retained TAB table and exports it as CSV, TXT or DBF. Append
       and overwrite are independent of **Keep Selected Tables**.
   * - Buffer and original search features
     - :ref:`KeepBufferArea <setting_keepbufferarea>` and
       :ref:`KeepSearchFeature <setting_keepsearchfeature>`. Each Yes setting
       retains its own TAB table and adds it to map windows independently
       of the data-layer mapping and retention choices.
   * - Formatted XLSX
     - An optional :ref:`Macro <setting_macro>` runs after layer export and
       is expected to create the XLSX file. Script errors or a missing XLSX
       are reported in the log.

Empty selections or selections exceeding :ref:`RecMax <setting_recmax>` skip
the layer. Skipped outputs do not clear files left by an earlier run. Keep TAB
and SHP companion files together when copying or delivering GIS outputs.

.. index::
   pair: Log files; Temporary journal
   single: Log files; Publication timing
   single: Log files; Recovery
   single: Debug; Diagnostics
   single: Universal Translator; Diagnostic files

.. _run_logs:

Run logs and diagnostics
========================

The final log is named by :ref:`LogFileName <setting_logfilename>` and saved
in the final GIS output folder. Messages accumulate in memory and are also
appended to a temporary journal during processing. The final log is updated
when processing finishes or a handled stop reaches the reporting stage,
after you answer any close-form prompt. It then opens in Notepad. Use the
journal to inspect progress while the tool is running.

.. list-table:: Log locations
   :header-rows: 1
   :widths: 30 70

   * - File
     - Location and purpose
   * - Final log
     - Final folder beneath SaveRootDir, SaveFolder and GISFolder. Contains
       published run messages. **Clear log file?** deletes the previous final
       log at the start; unchecked, new messages append at the end.
   * - Temporary journal with WorkingDir
     - The fresh working run folder during processing. A successful output
       transfer moves it to the final folder; a partial transfer may leave it
       in either location. Check the recorded paths.
   * - Temporary journal without WorkingDir
     - The final GIS folder, alongside the final log. The journal is appended
       to and can contain more than one run; use timestamps and run headings.

The journal inserts ``_tmp`` before the final log's extension, or appends
``_tmp`` if it has no extension. For the worked example, the names are
``Data_Search_001.log`` and ``Data_Search_001_tmp.log``. The journal may remain
after the final log has been written; its presence alone does not indicate
failure.

Check the whole final log for the reference, profile, buffer, selected options,
record counts, skipped layers, export/script failures and transfer messages.
The following excerpt is illustrative: timestamps and intervening messages
are omitted, and 25 is an example count, not a recorded test result.

.. code-block:: text

   Processing search '001' ...
   Buffer size = '1km'
   25 records selected.
   Process completed!

A completion message does not establish that every output succeeded. Set
:ref:`Debug <setting_debug>` to ``Yes`` in a diagnostic profile for additional
messages. SHP conversion can also create ``TabToShp_<userid>_MUT.log`` and a
corresponding ``.fme`` mapping file in the processing folder. With WorkingDir,
these move with the run's files when transfer succeeds. Review the translator
log when conversion fails, and retain relevant diagnostics for a bug report.

If the final log cannot be written, the tool reports its path and the temporary
journal path and retains pending messages in memory. Restore access and retry
while the tool remains open. A new search is prevented while pending messages
cannot be written. If necessary, copy the temporary journal before closing
MapInfo; messages held only in memory do not survive closing the application.

.. index::
   pair: Errors; Recovery
   single: Transfers; Failures
   single: Working storage; Interrupted runs
   single: Log files; Recovering messages

.. _transfer_recovery:

Interrupted runs and transfer failures
======================================

From version 1.4.47, each working run is kept separate. Starting again uses a fresh
folder; it does not resume, clear or move the failed run's files.

If a move fails, mapping stops. Record the source and destination shown in
the log and check both: some files may have moved successfully. Robocopy
retries failures three times with a two-second delay; an exit code of 8 or
higher, or failure to launch it, is treated as a transfer failure.

Restore access to the destination or release file locks, then decide whether
to recover the retained files or rerun the search. Close affected tables before
manual recovery, and move complete TAB or SHP file sets together. Check the
combined sites table before choosing append again after a partial transfer.
Keep failed-run folders until recovery is complete; remove them manually only
when their contents are no longer needed.

For temporary journals and final-log recovery, see :ref:`run_logs`.
