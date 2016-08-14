************************
Anatomy of a data search
************************

.. index::
	single: Data search process

This section describes how a typical data search might be carried out manually, and how the Data Searches tool automates this process. Please note that the examples used in this illustration are purely fictional and do not represent a real-world scenario. 

Data search process
===================

The process of a typical data search can be broken down into a number of distinct steps that are described here. In the next section the way that the Data Searches tool carries out these steps is explained.

Entering a search location
	Before any search can be carried out, the point, line or polygon describing the location that the search is centred on has to be entered into the GIS system. Typically this would be held in a single data layer, with some associated attributes such as the search reference or the name of the search site.

Buffering the search site
	Once the search location is entered into the GIS system, it can be used as input into a buffering tool. The user chooses the radius within which the search will be carried out, and buffers the search location using this search radius. The output from this operation is saved as a new GIS data layer.

Selecting the relevant data layers
	Using the buffer layer created in the previous step, each of the data layers describing the presence of protected sites and/or species is selected one by one.

Exporting the results
	The selected features are exported in the format required by the user. This can include both GIS data layers to allow mapping and visualisation, and tabular data for reporting purposes. Labels may be added to the GIS data at this point to aid in the identification of individual sites on any maps that are created. Other columns may need to be added or removed from the tabular data at this point to create the exact output the user requires. If a summary table of the results is needed for the search report, the user has to create this by hand from the exported tables using a spreadsheet or word processing package.

Repeating the process
	For statutory reasons the search radius may vary between (for example) protected sites and protected species. In this case the search needs to be repeated with a new buffer layer.

.. raw:: latex

   \newpage

.. index::
	single: Tool overview

The Data Searches tool
======================

There are four component parts to the Data Searches tool that work together to automate the process described above:

1. An Access database that contains details about search requests, including a unique search reference number.
#. One or more GIS layers that describe the locations of the searches, using the same unique search reference number to identify each search request.
#. An XML configuration file that specifies how the searches are set up and what data should be exported for each data layer.
#. The Data Searches tool itself.

The Data Searches tool is used within a GIS environment and requires all the required data layers to be preloaded in the GIS (see :numref:`figArcGISUI`). 

.. _figArcGISUI:

.. figure:: figures/InterfaceArcGISAnnotated.png
	:align: center

	Example of an ArcGIS document configured for the Data Searches tool

.. raw:: latex

   \newpage

Tool workflow
-------------

The Data Searches tool requires minimum user input in order to carry out its processes once it is configured. The simple workflow is as follows (see :numref:`figUIAnn`):

1. The user enters the unique search reference. At this point, the tool retrieves the site name for this search from the Access database.
#. If no name was found, the user may enter the site name manually.
#. The user specifies which data layers to search. Only layers that are loaded in the GIS are made available at this point.
#. A buffer size is entered and the units for this buffer are specified.
#. The user chooses whether to add any selected GIS layers to the map, and whether (and how) this new data should be labelled. 
#. Finally, the user selects whether a table combining all the results should be created during the process, and whether the log file should be cleared before the process starts. 
#. Once the user clicks :kbd:`OK` the process starts.

.. _figUIAnn:

.. figure:: figures/MenuExampleAnnotated.png
	:align: center

	The Data Searches tool workflow


.. raw:: latex

   \newpage

In essence, the process that the tool follows is identical to the manual search process described above. 

1. Firstly the search reference is located in the the data layer(s) containing the search location.
#. The location is buffered using the specified radius, resulting in a new data layer that is saved in the output folder.
#. Selections are made on all data layers specified by the user using this buffer layer.
#. The resulting selections are exported to the output folder as specified in the configuration file. At this point, columns may be automatically added, removed or changed, labels may be added to the output and summary data can be calculated. Output can be saved as tabular data only, or as both tabular and GIS data.
#. If required the output is also added to a summary 'combined sites' table to aid reporting.
#. GIS data is added to the map as detailed by the user. Layers are symbolised as specified in the configuration file, and labels are added if requested.
#. During the process the tool reports its progress to a log file and when the process finishes this log file is displayed, allowing the user to assess the success of the data search. The log file is kept with the other output in the output directory.


.. raw:: latex

   \newpage

.. index::
	single: Tool outputs

Tool outputs
============

Below is a selection of outputs generated from an example data search using the search options shown in figures :numref:`figArcGISUI` and :numref:`figUIAnn`. These examples were generated using the ArcGIS tool - the outputs from the MapInfo tool have a slightly different format. The tabular data, however, is the same for both implementations of the tool [Andy you might want to include the visuals from the MapInfo implementation].

When the process finishes, the GIS output is presented within the GIS interface (:numref:`figArcOutputAnn`). Note the output layers are presented in a logical format and their names refer back to the search reference number. The symbology of the layers is customised, as is the labelling applied to each output layer. The buffer that was used for the analysis is also included in the output. Only layers for which a feature was found within the search radius will be included in the output.

.. _figArcOutputAnn:

.. figure:: figures/ExampleOutputArcGISAnnotated.png
	:align: center

	Example of GIS output from the Data Searches tool (ArcGIS)


.. raw:: latex

   \newpage

Output folder
-------------

All the GIS and tabular outputs from the tool are stored in a user defined folder (:numref:`figOutputFolder`). These outputs may include a combination of GIS layers, the buffer layer that was used, tabular layers in different formats, a combined sites table, and the log file.

.. _figOutputFolder:

.. figure:: figures/OutputFolderAnnotated.png
	:align: center

	Example of the Data Searches tool output folder


.. raw:: latex

   \newpage

Output files
------------

GIS layers can be produced, either as an aid to generating maps for the data search or for sending to the requestor. A GIS layer will also be created containing the buffered search area used for the search - this search area can be based on an input GIS layer containing either points, lines or polygons.

Tabular outputs are also produced in a text based format (.csv or .txt) and can include the radius of the search area and / or the distance of each feature to the search area (:numref:`figTabularOutput`). It is also possible to create summary statistics for any column during the process, which will be included in the tabular output.

.. _figTabularOutput:

.. figure:: figures/ExampleTabularOutput.png
	:align: center

	Example of tabular output from the Data Searches tool

A combined sites table can also be produced (see :numref:`figCombinedSites`). This table contains a summary of the all sites that are found within the search area. This output is highly customisable and it is easy to exclude or include layers in this table, and choose what data columns to include, as required. Any summary statistics generated for each layer can be included in this table.

.. _figCombinedSites:

.. figure:: figures/CombinedSitesTableExample.png
	:align: center

	Example of a combined sites table


.. raw:: latex

   \newpage

Finally, the log file details each step that was taken during the process, and gives some feedback about the outcomes of the steps. This includes reporting on the input for the search, the number of features that were selected in each data layer, and which data layers did not return any features (:numref:`figLogFileExample`).

.. _figLogFileExample:

.. figure:: figures/LogFileExample.png
	:align: center

	Example of a Data Searches tool log file


The following chapters, :doc:`setting up the tool <../setup/setup>` and :doc:`running the tool <../execute/execute>`, will guide you through setting up and operating the tool in such a way that these tool outputs meet the exact requirements of data searches within your organisation.