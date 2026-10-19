***********
Quick start
***********

Use these steps for routine searches after an administrator has installed the
tool and prepared a workspace and profile. For installation or upgrades, use
the :ref:`administrator_checklist`. You do not need to edit XML for routine use.
The :doc:`../execute/execute` chapter explains individual options in detail.

.. index::
   single: Quick start
   single: Searches; Routine workflow
   single: Workspace; Opening

.. _quick_start:

Run a routine search
====================

1. **Open the prepared workspace.** Check that the search-sites table and
   required source layers are open, and that the request's location and
   reference are present in the search-sites table. Save or discard pending
   edits before running the tool.
#. **Open the tool and choose a profile.** Use **Tools --> Data Searches -->
   Run Data Searches** in the classic interface, or **Data Searches** in the
   **Home** tab's **Tools** group. Choose the profile for the request if
   prompted; a single profile is selected automatically.
#. **Enter the request and select layers.** Enter **Search Ref** and click
   **Find** if lookup is enabled, or type **Site Name** manually. Select the
   required definitions in **MapInfo Tables**; use **Ctrl** for individual
   selections or **Shift** for a range. Check **Buffer Size** and **Buffer Units**.
#. **Check the options.** Confirm map display, retained GIS format, symbology,
   label numbering and combined sites output. Some controls may be hidden by
   the profile. Check **Clear log file?** only if the previous log can be
   replaced. See :ref:`output_formats` for format choices.
   Reusing output names can replace earlier results; appending to
   combined sites can duplicate records.
#. **Run the search.** Click **Ok** and wait for processing and any transfer
   to finish. At the close-form prompt, choose **No** if you want to retain
   the selections for another search.
#. **Review the log and outputs.** In the log opened in Notepad, check the
   reference, profile, radius, counts, skipped layers and errors. Check the
   saved files and map against the request before using the results. For
   transfer problems, follow :ref:`transfer_recovery`.

:numref:`figDisplayForm` identifies the form controls; :numref:`figResults`
shows the mapped outputs.

.. index::
   single: Worked example
   pair: Searches; Worked example
   single: Outputs; Example filenames

.. _worked_example:

Worked example: a 1 km sites search
===================================

This illustrative search uses the :ref:`appendix profile <example_xml>`.
An administrator must adapt its paths and prepare the example data first:
an open ``SearchSites`` table with a text ``EnquiryRef`` of ``001`` and a
``SiteName`` column, and an open ``SSSIs`` table with ``SiteRef`` and
``SiteName`` columns. Include SSSI polygons intersecting the search buffer.
The example data and workspace are not supplied with this guide.

Choose ``DefaultProfile.xml`` if prompted. Enter **Search Ref** ``001`` and
**Site Name** ``Example Meadow`` manually; the appendix profile does not use
Access lookup. Select **Sites - SSSIs**, set **Buffer Size** to ``1`` and
**Buffer Units** to **Kilometres**, and use these options:

.. list-table::
   :header-rows: 1
   :widths: 50 50

   * - Control
     - Choice
   * - Add Selected Tables to Map
     - Yes - With labels
   * - Keep Selected Tables
     - TAB
   * - Apply Symbology to Tables
     - Layers only
   * - Overwrite Map Labels
     - Yes - Reset Each Layer
   * - Create Combined Sites Table
     - Overwrite existing table
   * - Clear log file?
     - Checked for this fresh example run

Use a fresh example output folder, then click **Ok**. With the appendix paths
unchanged, outputs are written directly to ``D:\DataSearches\Reports\001\GIS``.
After a successful run with matching features, expect:

.. list-table::
   :header-rows: 1
   :widths: 50 50

   * - File
     - Contents
   * - ``SSSIs_001_1km.tab``
     - Retained SSSI features and label values.
   * - ``001_SSSIs_1km.csv``
     - Site reference, name, label, radius and overlap area.
   * - ``Buffer_001_1km.tab`` and ``SearchArea_001_1km.tab``
     - Search buffer and original selected search feature.
   * - ``Sites.tab`` and ``001_sites.csv``
     - Combined sites table and its CSV export.
   * - ``Data_Search_001.log``
     - Processing messages and counts for the run.

Keep each TAB file with its companion files. No shapefiles or XLSX files are
requested by these choices. The map should show the retained search geometry,
buffer and SSSI results, with data results in the ``001_Example_Meadow`` group.
Check the log and CSV against the selected features; counts and overlap areas
depend on the prepared data. Check label values too: the current reset
sequence starts at 2, as explained under :ref:`label numbering <label_numbering>`.

Use :numref:`figOutputFolder` to help identify the output files, and
:ref:`run_logs` for the final log, temporary journal and diagnostic messages.
