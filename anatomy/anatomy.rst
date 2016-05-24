************************
Anatomy of a data search
************************

.. index::
	single: Detailed process description

Detailed process description
============================

The process of a typical data search can be broken down into a number of distinct steps that are described here. In the next section the way that the Data Searches Tool carries out these steps is explained.

Entering a search location
--------------------------

Before any search can be carried out, the point, line or polygon describing the location that the search is centred on has to be entered into the GIS system. Typically this would be held in a single data layer, with some associated attributes such as the search reference or the name of the search site.

Buffering the search site
-------------------------

Once the search location is entered into the GIS system, it can be used as input into a buffering tool. The user chooses the radius within which the search will be carried out, and buffers the search location using this search radius. The output from this operation is saved as a new GIS data layer.

Selecting the relevant data layers
----------------------------------

Using the buffer layer created in the previous step, each of the data layers describing the presence of protected sites and/or species is selected one by one.

Exporting the results
---------------------

The selected features are exported in the format required by the user. This can include both GIS data layers to allow mapping and visualisation, and tabular data for reporting purposes. Labels may be added to the GIS data at this point to aid in the identification of individual sites on any maps that are created. Other columns may need to be added or removed from the tabular data at this point to create the exact output the user requires. If a summary table of the results is needed for the search report, the user has to create this by hand from the exported tables using a spreadsheet or word processing package.

Repeating the process
---------------------

For statutory reasons the search radius may vary between (for example) protected sites and protected species. In this case the search has to be repeated with a new buffer layer.

.. index::
	single: The Data Searches Tool

The Data Searches Tool
======================

There are four parts to the Data Searches Tool that work together to automate the process described above:
1. An Access database that contains details about search requests, including a unique search reference number.
#. One or more GIS layers that describe the locations of the searches, using the same unique search reference number to identify each search request.
#. An XML file that specifies how the searches are set up and what data should be exported for each data layer
#. The Data Searches Tool interface.

The Data Searches Tool is used within a GIS environment and requires all the required data layers to be preloaded in the GIS. 

Tool workflow
-------------

The Data Searches Tool requires minimum user input in order to carry out its processes once it is configured. The workflow is as follows:
1. The user enters the unique search reference. At this point, the tool retrieves the site name for this search from the Access database.
#. If the search reference exists but no name was found, the user may enter the site name.
#. The user specifies which data layers to search. Only layers that are present in the GIS are made available at this point.
#. A buffer size is entered and the units for this buffer are specified.
#. The user chooses whether to add any selected GIS layers to the map, and whether (and how) this new data should be labelled. 
#. Finally, the user selects whether a table combining all the results should be created during the process, and whether the log file should be cleared before the process starts. 
#. Once the user clicks 'OK' the process starts.

In essence, the process that the tool follows is identical to the manual search described above. 
1. Firstly the search reference is located in the the data layer(s) containing the search location.
#. The location is buffered using the specified radius, resulting in a new data layer that is saved in the output folder.
#. Selections are made on all data layers specified by the user using this buffer layer.
#. The resulting selections are exported to the output folder as specified in the configuration file. At this point, columns may be automatically added, removed or changed, labels may be added to the output and summary data can be calculated. Output can be saved as tabular data only, or as both tabular and GIS data.
#. If required the output is also added to a summary 'combined sites' table to aid reporting.
#. GIS data is added to the map as detailed by the user. Layers are symbolised as specified in the configuration file, and labels are added if requested.
#. During the process the tool reports its progress to a log file and when the process finishes this log file is displayed, allowing the user to assess the success of the data search. The log file is kept with the other output in the output directory.


- Worked example of outputs

