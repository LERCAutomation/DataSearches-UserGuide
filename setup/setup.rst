*******************
Setting up the tool
*******************

.. index::
	single: Configuring the tool

Configuring the tool
====================

Before the Data Searches Tool will function, it needs to be installed and configured. It is recommended that the configuration is carried out first, although the steps are interchangeable for the ArcGIS implementation.

The configuration is stored in an XML file, and there are some differences in the contents of this file between the MapInfo and the ArcGIS implementations of the tool. Please ensure that you are using the correct XML file, examples of both of which can be found in the :doc:`appendix <../appendix/appendix>`. Settings are presented as nodes (beginning with a start node, e.g. ``<example>``, and finishing with an end note, e.g. ``<\example>``), with the value for the setting held between the ``<value>`` and ``<\value>`` node. 

The XML files can be edited in a text editor such as Notepad or Wordpad, or using a more feature rich XML editor such as as `Sublime Text <https://www.sublimetext.com/3>`_. The configuration file is split into two sections: a section containing general attributes of the searches, and a section that deals with the way each data layer should be handled. This structure is the same for both implementations of the tool. 

.. note::
	It is important that the structure of the file is maintained as it is presented in the :doc:`appendix <../appendix/appendix>`. Any changes to the structure may result in the Data Searches Tool not loading, or not working as expected.

Once editing has been completed and the edits have been saved it is recommended that the file is opened using an internet browser such as Internet Explorer which will help highlight any editing errors – only if the structure of the file is valid will the whole file be displayed in the internet browser.

Setup for ArcGIS
----------------



**General attributes**

The first section of the configuration file deals with a series of general attributes for the Data Searches Tool. These general nodes specify where files are kept, how output files should be named, and other overall settings. Details on these attributes are shown in :numref:`tabArcGISGenAtt`.

.. _tabArcGISGenAtt:

.. table:: General attributes in the ArcGIS configuration file.

+------------------------+----------------------------------------------------------+
| Attribute              |Description                                               |            
+========================+==========================================================+
| Database               |The path to the Access database that contains the details |
|                        |of all search requests.                                   |
+------------------------+----------------------------------------------------------+
| 

- Why this has to be done first
- All the options and what they need to look like (split MapInfo / ArcGIS)

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
