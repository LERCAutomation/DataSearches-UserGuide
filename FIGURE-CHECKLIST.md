# MapInfo figure checklist: eight PNGs to create

The guide has been consolidated to **12 figure placements: eight replacement
PNGs and four existing classic MapInfo installation figures**. Main-form and
results images are each included once and referenced from the other chapters.

Save the eight new images in `D:\GitHub\DataSearches-UserGuide` using the
exact paths below. Replace the existing placeholder files in place. Some
placeholders still show the old interface; those image contents have not been
changed by the documentation edits.

Use Data Searches v1.4.47, fictional or anonymised data, and one consistent
example search. Capture at a readable scale. The guide does not fix image
dimensions, so choose enough resolution for labels and annotations to remain
legible at normal page width.

## Required files

| File, relative to the guide folder | Subject | Used in |
| --- | --- | --- |
| `execute/figures/DisplayForm.png` | Annotated main form | Used once in Running the tool and referenced from Introduction and Anatomy. |
| `anatomy/figures/InterfaceAnnotated.png` | Prepared workspace | Anatomy: the prepared workspace. |
| `setup/figures/DataLayerXMLExample.png` | Current XML definition | Setup: map layer settings. |
| `execute/figures/LaunchSearchesTool.png` | Ribbon launch | Running the tool: opening the form. Classic-menu users are referred to the existing setup image. |
| `execute/figures/ChooseXMLFile.png` | Profile chooser | Running the tool: choosing a profile. |
| `anatomy/figures/OutputFolderAnnotated.png` | Final output folder | Anatomy: output files. |
| `execute/figures/Results.png` | Annotated results | Used once in Running the tool and referenced from Introduction and Anatomy. |
| `execute/figures/LogFile.png` | Current run log | Running the tool: reviewing a completed search. |

## Capture details

### Annotated main form

`execute/figures/DisplayForm.png`

Show the full v1.4.47 form with Search Ref, Find and Site Name; several table definitions highlighted; buffer size and units; Add Selected Tables to Map; Keep Selected Tables; Apply Symbology to Tables; Overwrite Map Labels; Create Combined Sites Table; Clear log file?; and Ok. Use numbered callouts or short annotations, leaving text readable. Use a profile with nonblank optional defaults so every main control is visible. A successful lookup and representative selected options give the image useful context.

### Prepared workspace

`anatomy/figures/InterfaceAnnotated.png`

Show MapInfo before processing, with the search-sites table, source tables and search geometry. Annotate the map and layer list.

### Current XML definition

`setup/figures/DataLayerXMLExample.png`

Show one annotated MapTables definition with TableName, GISOutputName, TableOutputName and value elements. Use the current appendix profile; do not use the obsolete Prefix/Suffix structure.

### Ribbon launch

`execute/figures/LaunchSearchesTool.png`

Show the Data Searches button in the Home tab / Tools group of the current MapInfo ribbon.

### Profile chooser

`execute/figures/ChooseXMLFile.png`

Show the Please Choose a Profile dialog, preferably with its list open and at least two valid profiles available. This dialog appears only when multiple profiles exist.

### Final output folder

`anatomy/figures/OutputFolderAnnotated.png`

Show the completed search folder in File Explorer. Annotate tabular exports, TAB companion files, any SHP file sets, combined sites output and log. Keep the complete file sets visible where practical.

### Annotated results

`execute/figures/Results.png`

Show the completed MapInfo map and layer list. Identify the results group, retained data layers, map labels, original search feature and buffer. Use a profile that retains and displays these items.

### Current run log

`execute/figures/LogFile.png`

Show a completed v1.4.47 run log in Notepad, including version/profile, selected options, record counts and completion. Enable WorkingDir if you want the capture to illustrate working/final folder paths and transfer messages too.

## Existing figures retained

These four classic MapInfo installation screenshots can remain. You do not
need to recreate them for this refresh:

| File | Purpose |
| --- | --- |
| `setup/figures/ToolManager.png` | Classic Tool Manager. |
| `setup/figures/AddToolDialog.png` | Add Tool dialog. |
| `setup/figures/DataSearchesLoaded.png` | Loaded and AutoLoad settings. |
| `setup/figures/DataSearchesToolMenu.png` | Classic Data Searches menu commands; also referenced from Running the tool. |

## Figures no longer required

The separate introduction form, workflow form, Find crop, successful lookup,
manual entry, table selection, buffer controls, dropdowns and clear-log
checkbox images have been removed from the guide. The main-form image and
the existing written instructions cover these topics.

The missing-table warning and completion-prompt screenshots have also been
removed; the instructions explain what to do. One results image replaces
the separate overview, older MapInfo and current-interface results figures.

The tabular-output, combined-sites-table and overview-log figures previously
in published section 3.3.2 remain removed. One current log figure is retained
in Running the tool.

Unused image files have been removed. The repository retains only the 12
referenced figure PNGs and the logo/favicon used by the build configuration.
Create only the eight replacement images listed above. Do not recreate the
old add-in installation or toolbar-customisation screenshots.

## Before publication

- Replace the eight files above and check that their contents match the captions.
- Review the annotated form and results at normal page width in HTML and PDF.
- Check that example names, reference, radius and output files are consistent.
- Rebuild the guide after replacing the PNGs. Figure numbers are generated automatically.
- The editorial comment in `preface/preface.rst` and this work list may be removed after the refresh.
