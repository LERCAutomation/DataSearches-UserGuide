.. index::
   single: FAQ
   see: Frequently asked questions; FAQ

**************************
Frequently Asked Questions
**************************

General questions
=================

.. index::
   single: Downloads
   single: Profiles; Upgrading

**How do I get the tool?**

Download the appropriate compiled application and support files from the
`MapInfo releases <https://github.com/LERCAutomation/DataSearches-MapInfo/releases>`_.
Use profiles suitable for the current version; see the :ref:`profile
migration table <profile_migration>` for older naming settings.

.. index::
   single: ArcGIS Pro version

**Is there a version for another GIS application?**

A separate `ArcGIS Pro version <https://github.com/LERCAutomation/DataSearches-ArcPro>`_
is available with its own
`user guide <https://readthedocs.org/projects/datasearches-arcpro-userguide/>`_.
This guide describes the MapInfo version and its configuration.

.. index::
   single: Shared use
   single: Search table; Concurrent access

**Can several people use the tool at once?**

Each user can run it in their own MapInfo session. Source data layers are
queried, but the search-sites table is used temporarily during buffering and
can also be updated if configured. Coordinate access to shared search tables,
and avoid concurrent runs writing the same final output names. Fresh working
folders do not prevent final files or combined sites tables being overwritten.

.. index::
   single: QGIS

**Does the tool work with QGIS?**

No. Versions are available for MapInfo and ArcGIS Pro. The tool could be
adapted to support QGIS if funding were available.

Operating the tool
==================

.. index::
   single: Troubleshooting; Missing tables

**Why is a table missing from the form?**

Check that it is open in MapInfo and its :ref:`TableName <setting_tablename>`
matches the profile. It must also have a definition under ``MapTables``. Reopen the form after
opening the missing table. ``LoadWarning=No`` suppresses its warning, not the
requirement for the table to be open.

.. index::
   single: Troubleshooting; Hidden controls
   single: Search form; Hidden controls

**Why are some controls missing?**

Blank defaults hide optional controls. The tool then uses **No** or **None**
for mapping, retention, symbology, overwriting and combined sites choices.
Buffer defaults can also hide the size and units fields. Ask the profile
administrator to check the :ref:`form defaults <form_defaults>`, then reopen
the form.

.. index::
   single: Troubleshooting; Disabled site-name field

**Why can I not type a site name?**

With database lookup enabled the field is disabled. Click **Find** after
entering the reference. Correct names in the database, or use a profile without
lookup when manual entry is needed. See :ref:`Database <setting_database>`
and :ref:`RequireSiteName <requiresitename>` for the profile settings.

.. index::
   single: Troubleshooting; Replaced outputs

**Why is there only one set of results after searching twice?**

Outputs with matching names are replaced. Include ``%radius%`` in suitable
names or move the first set before rerunning. For combined sites results,
choose append if both sets are required; repeating the same selection can
create duplicates. See :ref:`the output-overwriting warning <OverwriteWarning>`.

.. index::
   single: Troubleshooting; Unexpected TAB files

**Why are TAB files present when I chose None or SHP?**

TAB files are retained for map display when **Add Selected Tables to Map**
is enabled and the layer permits retention. Buffer, search-feature and combined
sites tables have separate settings. See :ref:`output_formats`.

.. index::
   single: Troubleshooting; Missing outputs

**Why did a layer produce no output?**

Check the log for an empty selection, a count exceeding :ref:`RecMax
<setting_recmax>` or an error. Blank :ref:`Columns <setting_columns>` or
:ref:`Format <setting_format>` skips the tabular export;
:ref:`KeepLayer <setting_keeplayer>` set to No
prevents retained GIS output. Old files in the final folder do not establish
that the current run produced them.

.. index::
   single: Troubleshooting; Transfer failures

**What happens if a transfer fails?**

Mapping stops and untransferred files remain in that run's working folder.
Some may already be at the destination. A new run uses a fresh folder and
does not recover the earlier run automatically. Follow :ref:`transfer_recovery`.

.. index::
   single: Troubleshooting; Decimal buffer sizes
   single: Buffer; Decimal sizes

**Why does a small decimal radius behave like zero?**

The current buffer calculation tests the integer part of the size. Express
the same distance in smaller units, for example ``500 m`` instead of ``0.5 km``.
See :doc:`the running instructions <../execute/execute>` for other behaviour to check in existing profiles.

.. index::
   single: Troubleshooting; Log not updating

**Why is the final log not updating while the search runs?**

Messages are written to the temporary journal during processing and published
to the final log at the end, after any close-form prompt is answered. With
:ref:`WorkingDir <working_directory>`, look in the current working run folder;
otherwise look in the final GIS folder. See :ref:`run_logs` for filenames,
transfer behaviour and recovery if the final log cannot be written.

Tool issues
===========

.. index::
   pair: Bugs; Reporting
   single: Feature requests

**How do I report a bug or request a change?**

Check the existing
`MapInfo issues <https://github.com/LERCAutomation/DataSearches-MapInfo/issues>`_
first. Include:

* The Data Searches and MapInfo versions, including 32-bit or 64-bit architecture.
* The selected profile and relevant settings, with the search/layer definitions.
* Steps to reproduce the issue, the expected result and what actually happened.
* Relevant messages from the final log, temporary journal and any translator
  diagnostics; see :ref:`run_logs`.

Remove confidential data, credentials and identifying details from profiles,
logs and sample data before sharing them. For a feature request, describe the
workflow and the result you want.
