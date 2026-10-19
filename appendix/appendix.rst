********
Appendix
********

.. index::
   single: Appendix; Change Log
   single: Change Log
   single: Releases; History

.. _change_log:

Change Log
==========

This history covers the MapInfo tool through version |release|. It was
reconstructed from ``DataSearches.mb`` version comments, historical source,
and the `GitHub commits <https://github.com/LERCAutomation/DataSearches-MapInfo/commits/master/>`_
and `tags <https://github.com/LERCAutomation/DataSearches-MapInfo/tags>`_.
Entries describe the changes recorded at the time; the setup chapter describes
the settings used by the current version.

Dates in code comments take precedence over commit or tag dates. Where only
a revision month is recorded, no release day has been inferred. Version 1.4.46
spans the July and September 2026 revision comments. Versions 1.4.40 and
1.4.43 have no separately recorded dates. Version 1.4.47 includes the latest
source changes. Older numbers such as 1.40 and 1.31 are shown in the later
three-part form, 1.4.0 and 1.3.1.

**1.4.47**
(October 2026)

Safer working folders, file transfers and failure recovery.

    * **Changed:** Each search uses a fresh subfolder under ``WorkingDir``. Interrupted runs are retained and excluded from later runs.
    * **Improved:** Working and final output folders are checked for overlap, and their paths are recorded in the log.
    * **Improved:** Saved working tables are committed and closed before transfer. Matching destination outputs are replaced while unrelated files are retained.
    * **Fixed:** Failed or partial transfers retain untransferred files and stop the mapping stage. Logging follows the temporary journal if it has already moved.
    * **Fixed:** Messages are retained in memory if the final log cannot be written, and must be written before another search starts.
    * **Improved:** External-process failures are detected more reliably, including failures to launch the Universal Translator.

**1.4.46**
(September 2026)

Introduced working storage for output processing and improved file handling.

    * **New:** Optional ``WorkingDir`` creates outputs in temporary storage before moving them to the final output folder, reducing output traffic to network storage.
    * **Improved:** Added retries and error handling around table opening, saving and combined sites processing.
    * **Improved:** Checked external script results and expected XLSX output, and improved temporary and final logging.
    * **Fixed:** Mapping distinguishes deliberately omitted GIS outputs from expected outputs that are missing.

**1.4.45**
(August 2025)

Configurable symbology application.

    * **New:** Added choices to apply no symbology, layer display styles only, or layer and table styles.

**1.4.44**
(August 2025)

Further file-access improvements.

    * **Improved:** Reduced errors during file-access operations.

**1.4.43**
(August 2025)

Broader file-access error handling.

    * **Improved:** Extended error handling across file-access operations.

**1.4.42**
(April 2025)

More reliable logging.

    * **Improved:** Improved error handling when writing the log file.

**1.4.41**
(December 2021)

Wildcard search references.

    * **New:** Allowed search references to contain wildcard characters.

**1.4.40**
(December 2021)

Additional search attributes in exports.

    * **New:** Allowed search-area columns in exported files and the combined sites table.
    * **Changed:** Increased the widths of the form and table list.

**1.4.39**
(September 2021)

Saved search and buffer styles.

    * **New:** Added object symbology for search-area and buffer features.

**1.4.38**
(March 2021)

More flexible export column names.

    * **Changed:** Stopped assigning default output column names to search variables, allowing explicit aliases.

**1.4.37**
(March 2021)

Search variables and output corrections.

    * **New:** Allowed search variables in exported files and combined sites records.
    * **Fixed:** Corrected area outputs in the combined sites table.
    * **Changed:** Hid buffer controls when their defaults were blank and removed spaces from references used in table names.

**1.4.36**
(29th January 2021)

Additional area measurements.

    * **New:** Added search/buffer area and input-feature area expressions for exports and combined sites records.

**1.4.35**
(24th July 2020)

Empty combined sites output.

    * **Changed:** Added removal of an empty combined sites output table.

**1.4.34**
(15th December 2019)

Repeated runs from the same form.

    * **Fixed:** Corrected a problem when running another search without closing the tool.

**1.4.33**
(31st October 2019)

Map display and export corrections.

    * **Fixed:** Corrected unintended labels with a blank label clause, handling when no map window was open, combined sites export errors and grouping of local output tables.

**1.4.32**
(30th August 2019)

Map labels.

    * **Fixed:** Corrected map labels not being added.

**1.4.31**
(5th August 2019)

Shapefile translation.

    * **Fixed:** Handled a missing Universal Translator mapping file.

**1.4.30**
(1st August 2019)

64-bit profile support and output folders.

    * **New:** Enabled XML profiles in the 64-bit tool.
    * **Improved:** Created missing output paths and added funding details to the About box.

**1.4.29**
(2nd July 2019)

Choice of configuration profile.

    * **New:** Allowed users to select the XML profile to use.

**1.4.28**
(27th February 2019)

GIS output formats.

    * **New:** Added choices to keep TAB files, SHP files or both.

**1.4.27**
(22nd October 2018)

64-bit interface.

    * **New:** Added tool buttons for 64-bit MapInfo Pro.

**1.4.26**
(4th October 2018)

Partner details and logging.

    * **New:** Added ``%partner%`` naming variables and optional updates of partner details in the search layer.
    * **Improved:** Recorded the selected options in the log.

**1.4.25**
(21st September 2018)

Buffer creation.

    * **Changed:** Returned to using the search layer rather than the cosmetic layer to create buffers.

**1.4.24**
(30th July 2018)

Layer styles and additional profile options.

    * **New:** Added output-layer symbology, numeric keys, default log clearing, search-feature naming and search-radius variables.
    * **New:** Recorded coordinate-system setup and Copy/Clip/Overlap/Intersect output options in the version comments; see the current :ref:`coordinate-system <coordinate_system>` and :ref:`map-layer settings <map_layer_settings>` for their supported behaviour.
    * **Changed:** Revised label resetting by layer/group and allowed optional radius updates in the search layer.

**1.4.23**
(9th March 2018)

Zero-radius searches.

    * **New:** Allowed a zero buffer for point and line search sites.

**1.4.22**
(20th February 2018)

Long table names.

    * **Fixed:** Corrected handling when local file names were too long.

**1.4.21**
(24th January 2018)

Clearer configuration names.

    * **Changed:** Renamed XML nodes to make their purpose clearer and align naming across tool versions.

**1.4.20**
(15th June 2017)

Naming variables and optional site names.

    * **New:** Allowed variables in output name prefixes and suffixes and made site names configurable as required or optional.

**1.4.19**
(17th May 2017)

Optional updates and retained search geometry.

    * **New:** Added options to retain search and buffer areas and run a formatting macro/script.
    * **Changed:** Made site-name and organisation updates optional and removed hard-coded column names.

**1.4.18**
(15th March 2017)

Selection error handling.

    * **Improved:** Handled errors when selecting objects for export.

**1.4.17**
(3rd January 2017)

Search-layer attributes.

    * **New:** Added updates of site name and organisation in the search layer.

**1.4.16**
(15th November 2016)

Group-layer handling.

    * **Fixed:** Corrected a subscript-out-of-range error involving a group layer.

**1.4.15**
(2nd November 2016)

Missing group layers.

    * **Fixed:** Corrected a problem when a group layer was not added to a map window.

**1.4.14**
(1st November 2016)

Buffer creation.

    * **Changed:** Used the cosmetic layer to create the search buffer. This was subsequently reversed in version 1.4.25.

**1.4.13**
(24th October 2016)

Layer defaults and label controls.

    * **New:** Added layer preselection, per-layer label resetting and suppression of missing-layer warnings.
    * **Changed:** Hid the search layer before searching.

**1.4.12**
(20th October 2016)

Decimal buffer sizes.

    * **Fixed:** Corrected a problem with decimal buffer values.

**1.4.11**
(16th August 2016)

Layer grouping and overlap areas.

    * **New:** Added map-window grouping, overlap-area expressions and retained search features with configured symbology.
    * **Changed:** Removed the requirement to include ``Where`` in selection criteria.

**1.4.10**
(14th August 2016)

Search-table validation.

    * **Improved:** Checked that the search-sites table was open.

**1.4.9**
(14th July 2016)

Multiple tool instances.

    * **New:** Allowed separate instances to use different titles in the Tools menu.

**1.4.8**
(27th June 2016)

Radius values and combined sites handling.

    * **New:** Allowed the search radius in exports and combined sites records, and added append/overwrite choices for the combined table.

**1.4.7**
(30th May 2016)

Display names and version numbering.

    * **Changed:** Converted underscores to spaces in displayed layer names and introduced three-part version numbers.
    * **New:** Added a configuration attribute for saved GIS layer prefixes.

**1.4.6**
(5th May 2016)

CSV headings.

    * **New:** Included column titles in CSV exports.

**1.4.5**
(11th April 2016)

Lookup controls and optional form fields.

    * **New:** Added the site-name lookup button.
    * **Changed:** Hid controls when their default values were blank.

**1.4.4**
(24th March 2016)

Separate selection and export criteria.

    * **New:** Split SQL criteria into selection and export stages and logged separate counts.
    * **Changed:** Removed GIS layers that were not needed for map display.

**1.4.3**
(14th March 2016)

Tabular export formats.

    * **New:** Added CSV, DBF and TXT output choices.

**1.4.2**
(9th March 2016)

End-of-run controls.

    * **New:** Added a choice to keep the form open and displayed the log using Notepad.

**1.4.1**
(17th January 2016)

Missing-table reporting.

    * **Improved:** Counted source tables that were not already open in MapInfo.

**1.4.0**
(19th October 2015)

Expanded search and reporting workflow.

    * **New:** Added site-name lookup or entry, selectable buffer units, retained and labelled map results, sequential labels and combined sites reporting.
    * **New:** Added naming variables and configurable buffer symbology.

**1.3.1**
(April 2013)

Earliest recorded MapInfo release.

    * **New:** Listed configured MapInfo layers and extracted selected data within a radius of a search location.
    * **Changed:** The source was first uploaded to GitHub in January 2015; its own revision comment dates this version to April 2013.

.. raw:: latex

   \newpage

.. index::
   single: Example XML files
   pair: XML; Examples
   single: Profiles; Examples

.. _example_xml:

Example XML files
=================

These examples use the current MapInfo configuration structure. Replace the
paths and table/column names with those used by your organisation. The example
search table ``SearchSites`` must contain ``EnquiryRef`` and ``SiteName``;
the data table ``SSSIs`` must contain ``SiteRef`` and ``SiteName``. Its label
column can be created in the output when numbering is enabled.

The default example runs without Access lookup or a formatting script and
keeps TAB results. Its working root is deliberately blank, so processing writes
directly to the final folder. To enable local working storage, set
``WorkingDir`` to a writable root separate from the final output path.
Profiles are installation-specific: validate them with representative data
before use.

.. index::
   single: DataSearches.xml; Example

Launch configuration
--------------------

Save as :download:`DataSearches.xml <examples/DataSearches.xml>` beside the application.

.. literalinclude:: examples/DataSearches.xml
   :language: xml

.. index::
   single: DefaultProfile.xml; Example

Profile configuration
---------------------

Save as :download:`DefaultProfile.xml <examples/DefaultProfile.xml>` in the same folder.
The example makes the main choices visible. A blank optional default hides
its control; a value of 1 selects the first choice and keeps it visible.

.. literalinclude:: examples/DefaultProfile.xml
   :language: xml

.. raw:: latex

   \newpage

.. index::
   single: GNU Free Documentation License

GNU Free Documentation License
==============================

::

                    GNU Free Documentation License
                     Version 1.3, 3 November 2008
    
    
     Copyright (C) 2000, 2001, 2002, 2007, 2008 Free Software Foundation, Inc.
         <http://fsf.org/>
     Everyone is permitted to copy and distribute verbatim copies
     of this license document, but changing it is not allowed.
    
    0. PREAMBLE
    
    The purpose of this License is to make a manual, textbook, or other
    functional and useful document "free" in the sense of freedom: to
    assure everyone the effective freedom to copy and redistribute it,
    with or without modifying it, either commercially or noncommercially.
    Secondarily, this License preserves for the author and publisher a way
    to get credit for their work, while not being considered responsible
    for modifications made by others.
    
    This License is a kind of "copyleft", which means that derivative
    works of the document must themselves be free in the same sense.  It
    complements the GNU General Public License, which is a copyleft
    license designed for free software.
    
    We have designed this License in order to use it for manuals for free
    software, because free software needs free documentation: a free
    program should come with manuals providing the same freedoms that the
    software does.  But this License is not limited to software manuals;
    it can be used for any textual work, regardless of subject matter or
    whether it is published as a printed book.  We recommend this License
    principally for works whose purpose is instruction or reference.
    
    
    1. APPLICABILITY AND DEFINITIONS
    
    This License applies to any manual or other work, in any medium, that
    contains a notice placed by the copyright holder saying it can be
    distributed under the terms of this License.  Such a notice grants a
    world-wide, royalty-free license, unlimited in duration, to use that
    work under the conditions stated herein.  The "Document", below,
    refers to any such manual or work.  Any member of the public is a
    licensee, and is addressed as "you".  You accept the license if you
    copy, modify or distribute the work in a way requiring permission
    under copyright law.
    
    A "Modified Version" of the Document means any work containing the
    Document or a portion of it, either copied verbatim, or with
    modifications and/or translated into another language.
    
    A "Secondary Section" is a named appendix or a front-matter section of
    the Document that deals exclusively with the relationship of the
    publishers or authors of the Document to the Document's overall
    subject (or to related matters) and contains nothing that could fall
    directly within that overall subject.  (Thus, if the Document is in
    part a textbook of mathematics, a Secondary Section may not explain
    any mathematics.)  The relationship could be a matter of historical
    connection with the subject or with related matters, or of legal,
    commercial, philosophical, ethical or political position regarding
    them.
    
    The "Invariant Sections" are certain Secondary Sections whose titles
    are designated, as being those of Invariant Sections, in the notice
    that says that the Document is released under this License.  If a
    section does not fit the above definition of Secondary then it is not
    allowed to be designated as Invariant.  The Document may contain zero
    Invariant Sections.  If the Document does not identify any Invariant
    Sections then there are none.
    
    The "Cover Texts" are certain short passages of text that are listed,
    as Front-Cover Texts or Back-Cover Texts, in the notice that says that
    the Document is released under this License.  A Front-Cover Text may
    be at most 5 words, and a Back-Cover Text may be at most 25 words.
    
    A "Transparent" copy of the Document means a machine-readable copy,
    represented in a format whose specification is available to the
    general public, that is suitable for revising the document
    straightforwardly with generic text editors or (for images composed of
    pixels) generic paint programs or (for drawings) some widely available
    drawing editor, and that is suitable for input to text formatters or
    for automatic translation to a variety of formats suitable for input
    to text formatters.  A copy made in an otherwise Transparent file
    format whose markup, or absence of markup, has been arranged to thwart
    or discourage subsequent modification by readers is not Transparent.
    An image format is not Transparent if used for any substantial amount
    of text.  A copy that is not "Transparent" is called "Opaque".
    
    Examples of suitable formats for Transparent copies include plain
    ASCII without markup, Texinfo input format, LaTeX input format, SGML
    or XML using a publicly available DTD, and standard-conforming simple
    HTML, PostScript or PDF designed for human modification.  Examples of
    transparent image formats include PNG, XCF and JPG.  Opaque formats
    include proprietary formats that can be read and edited only by
    proprietary word processors, SGML or XML for which the DTD and/or
    processing tools are not generally available, and the
    machine-generated HTML, PostScript or PDF produced by some word
    processors for output purposes only.
    
    The "Title Page" means, for a printed book, the title page itself,
    plus such following pages as are needed to hold, legibly, the material
    this License requires to appear in the title page.  For works in
    formats which do not have any title page as such, "Title Page" means
    the text near the most prominent appearance of the work's title,
    preceding the beginning of the body of the text.
    
    The "publisher" means any person or entity that distributes copies of
    the Document to the public.
    
    A section "Entitled XYZ" means a named subunit of the Document whose
    title either is precisely XYZ or contains XYZ in parentheses following
    text that translates XYZ in another language.  (Here XYZ stands for a
    specific section name mentioned below, such as "Acknowledgements",
    "Dedications", "Endorsements", or "History".)  To "Preserve the Title"
    of such a section when you modify the Document means that it remains a
    section "Entitled XYZ" according to this definition.
    
    The Document may include Warranty Disclaimers next to the notice which
    states that this License applies to the Document.  These Warranty
    Disclaimers are considered to be included by reference in this
    License, but only as regards disclaiming warranties: any other
    implication that these Warranty Disclaimers may have is void and has
    no effect on the meaning of this License.
    
    2. VERBATIM COPYING
    
    You may copy and distribute the Document in any medium, either
    commercially or noncommercially, provided that this License, the
    copyright notices, and the license notice saying this License applies
    to the Document are reproduced in all copies, and that you add no
    other conditions whatsoever to those of this License.  You may not use
    technical measures to obstruct or control the reading or further
    copying of the copies you make or distribute.  However, you may accept
    compensation in exchange for copies.  If you distribute a large enough
    number of copies you must also follow the conditions in section 3.
    
    You may also lend copies, under the same conditions stated above, and
    you may publicly display copies.
    
    
    3. COPYING IN QUANTITY
    
    If you publish printed copies (or copies in media that commonly have
    printed covers) of the Document, numbering more than 100, and the
    Document's license notice requires Cover Texts, you must enclose the
    copies in covers that carry, clearly and legibly, all these Cover
    Texts: Front-Cover Texts on the front cover, and Back-Cover Texts on
    the back cover.  Both covers must also clearly and legibly identify
    you as the publisher of these copies.  The front cover must present
    the full title with all words of the title equally prominent and
    visible.  You may add other material on the covers in addition.
    Copying with changes limited to the covers, as long as they preserve
    the title of the Document and satisfy these conditions, can be treated
    as verbatim copying in other respects.
    
    If the required texts for either cover are too voluminous to fit
    legibly, you should put the first ones listed (as many as fit
    reasonably) on the actual cover, and continue the rest onto adjacent
    pages.
    
    If you publish or distribute Opaque copies of the Document numbering
    more than 100, you must either include a machine-readable Transparent
    copy along with each Opaque copy, or state in or with each Opaque copy
    a computer-network location from which the general network-using
    public has access to download using public-standard network protocols
    a complete Transparent copy of the Document, free of added material.
    If you use the latter option, you must take reasonably prudent steps,
    when you begin distribution of Opaque copies in quantity, to ensure
    that this Transparent copy will remain thus accessible at the stated
    location until at least one year after the last time you distribute an
    Opaque copy (directly or through your agents or retailers) of that
    edition to the public.
    
    It is requested, but not required, that you contact the authors of the
    Document well before redistributing any large number of copies, to
    give them a chance to provide you with an updated version of the
    Document.
    
    
    4. MODIFICATIONS
    
    You may copy and distribute a Modified Version of the Document under
    the conditions of sections 2 and 3 above, provided that you release
    the Modified Version under precisely this License, with the Modified
    Version filling the role of the Document, thus licensing distribution
    and modification of the Modified Version to whoever possesses a copy
    of it.  In addition, you must do these things in the Modified Version:
    
    A. Use in the Title Page (and on the covers, if any) a title distinct
       from that of the Document, and from those of previous versions
       (which should, if there were any, be listed in the History section
       of the Document).  You may use the same title as a previous version
       if the original publisher of that version gives permission.
    B. List on the Title Page, as authors, one or more persons or entities
       responsible for authorship of the modifications in the Modified
       Version, together with at least five of the principal authors of the
       Document (all of its principal authors, if it has fewer than five),
       unless they release you from this requirement.
    C. State on the Title page the name of the publisher of the
       Modified Version, as the publisher.
    D. Preserve all the copyright notices of the Document.
    E. Add an appropriate copyright notice for your modifications
       adjacent to the other copyright notices.
    F. Include, immediately after the copyright notices, a license notice
       giving the public permission to use the Modified Version under the
       terms of this License, in the form shown in the Addendum below.
    G. Preserve in that license notice the full lists of Invariant Sections
       and required Cover Texts given in the Document's license notice.
    H. Include an unaltered copy of this License.
    I. Preserve the section Entitled "History", Preserve its Title, and add
       to it an item stating at least the title, year, new authors, and
       publisher of the Modified Version as given on the Title Page.  If
       there is no section Entitled "History" in the Document, create one
       stating the title, year, authors, and publisher of the Document as
       given on its Title Page, then add an item describing the Modified
       Version as stated in the previous sentence.
    J. Preserve the network location, if any, given in the Document for
       public access to a Transparent copy of the Document, and likewise
       the network locations given in the Document for previous versions
       it was based on.  These may be placed in the "History" section.
       You may omit a network location for a work that was published at
       least four years before the Document itself, or if the original
       publisher of the version it refers to gives permission.
    K. For any section Entitled "Acknowledgements" or "Dedications",
       Preserve the Title of the section, and preserve in the section all
       the substance and tone of each of the contributor acknowledgements
       and/or dedications given therein.
    L. Preserve all the Invariant Sections of the Document,
       unaltered in their text and in their titles.  Section numbers
       or the equivalent are not considered part of the section titles.
    M. Delete any section Entitled "Endorsements".  Such a section
       may not be included in the Modified Version.
    N. Do not retitle any existing section to be Entitled "Endorsements"
       or to conflict in title with any Invariant Section.
    O. Preserve any Warranty Disclaimers.
    
    If the Modified Version includes new front-matter sections or
    appendices that qualify as Secondary Sections and contain no material
    copied from the Document, you may at your option designate some or all
    of these sections as invariant.  To do this, add their titles to the
    list of Invariant Sections in the Modified Version's license notice.
    These titles must be distinct from any other section titles.
    
    You may add a section Entitled "Endorsements", provided it contains
    nothing but endorsements of your Modified Version by various
    parties--for example, statements of peer review or that the text has
    been approved by an organization as the authoritative definition of a
    standard.
    
    You may add a passage of up to five words as a Front-Cover Text, and a
    passage of up to 25 words as a Back-Cover Text, to the end of the list
    of Cover Texts in the Modified Version.  Only one passage of
    Front-Cover Text and one of Back-Cover Text may be added by (or
    through arrangements made by) any one entity.  If the Document already
    includes a cover text for the same cover, previously added by you or
    by arrangement made by the same entity you are acting on behalf of,
    you may not add another; but you may replace the old one, on explicit
    permission from the previous publisher that added the old one.
    
    The author(s) and publisher(s) of the Document do not by this License
    give permission to use their names for publicity for or to assert or
    imply endorsement of any Modified Version.
    
    
    5. COMBINING DOCUMENTS
    
    You may combine the Document with other documents released under this
    License, under the terms defined in section 4 above for modified
    versions, provided that you include in the combination all of the
    Invariant Sections of all of the original documents, unmodified, and
    list them all as Invariant Sections of your combined work in its
    license notice, and that you preserve all their Warranty Disclaimers.
    
    The combined work need only contain one copy of this License, and
    multiple identical Invariant Sections may be replaced with a single
    copy.  If there are multiple Invariant Sections with the same name but
    different contents, make the title of each such section unique by
    adding at the end of it, in parentheses, the name of the original
    author or publisher of that section if known, or else a unique number.
    Make the same adjustment to the section titles in the list of
    Invariant Sections in the license notice of the combined work.
    
    In the combination, you must combine any sections Entitled "History"
    in the various original documents, forming one section Entitled
    "History"; likewise combine any sections Entitled "Acknowledgements",
    and any sections Entitled "Dedications".  You must delete all sections
    Entitled "Endorsements".
    
    
    6. COLLECTIONS OF DOCUMENTS
    
    You may make a collection consisting of the Document and other
    documents released under this License, and replace the individual
    copies of this License in the various documents with a single copy
    that is included in the collection, provided that you follow the rules
    of this License for verbatim copying of each of the documents in all
    other respects.
    
    You may extract a single document from such a collection, and
    distribute it individually under this License, provided you insert a
    copy of this License into the extracted document, and follow this
    License in all other respects regarding verbatim copying of that
    document.
    
    
    7. AGGREGATION WITH INDEPENDENT WORKS
    
    A compilation of the Document or its derivatives with other separate
    and independent documents or works, in or on a volume of a storage or
    distribution medium, is called an "aggregate" if the copyright
    resulting from the compilation is not used to limit the legal rights
    of the compilation's users beyond what the individual works permit.
    When the Document is included in an aggregate, this License does not
    apply to the other works in the aggregate which are not themselves
    derivative works of the Document.
    
    If the Cover Text requirement of section 3 is applicable to these
    copies of the Document, then if the Document is less than one half of
    the entire aggregate, the Document's Cover Texts may be placed on
    covers that bracket the Document within the aggregate, or the
    electronic equivalent of covers if the Document is in electronic form.
    Otherwise they must appear on printed covers that bracket the whole
    aggregate.
    
    
    8. TRANSLATION
    
    Translation is considered a kind of modification, so you may
    distribute translations of the Document under the terms of section 4.
    Replacing Invariant Sections with translations requires special
    permission from their copyright holders, but you may include
    translations of some or all Invariant Sections in addition to the
    original versions of these Invariant Sections.  You may include a
    translation of this License, and all the license notices in the
    Document, and any Warranty Disclaimers, provided that you also include
    the original English version of this License and the original versions
    of those notices and disclaimers.  In case of a disagreement between
    the translation and the original version of this License or a notice
    or disclaimer, the original version will prevail.
    
    If a section in the Document is Entitled "Acknowledgements",
    "Dedications", or "History", the requirement (section 4) to Preserve
    its Title (section 1) will typically require changing the actual
    title.
    
    
    9. TERMINATION
    
    You may not copy, modify, sublicense, or distribute the Document
    except as expressly provided under this License.  Any attempt
    otherwise to copy, modify, sublicense, or distribute it is void, and
    will automatically terminate your rights under this License.
    
    However, if you cease all violation of this License, then your license
    from a particular copyright holder is reinstated (a) provisionally,
    unless and until the copyright holder explicitly and finally
    terminates your license, and (b) permanently, if the copyright holder
    fails to notify you of the violation by some reasonable means prior to
    60 days after the cessation.
    
    Moreover, your license from a particular copyright holder is
    reinstated permanently if the copyright holder notifies you of the
    violation by some reasonable means, this is the first time you have
    received notice of violation of this License (for any work) from that
    copyright holder, and you cure the violation prior to 30 days after
    your receipt of the notice.
    
    Termination of your rights under this section does not terminate the
    licenses of parties who have received copies or rights from you under
    this License.  If your rights have been terminated and not permanently
    reinstated, receipt of a copy of some or all of the same material does
    not give you any rights to use it.
    
    
    10. FUTURE REVISIONS OF THIS LICENSE
    
    The Free Software Foundation may publish new, revised versions of the
    GNU Free Documentation License from time to time.  Such new versions
    will be similar in spirit to the present version, but may differ in
    detail to address new problems or concerns.  See
    http://www.gnu.org/copyleft/.
    
    Each version of the License is given a distinguishing version number.
    If the Document specifies that a particular numbered version of this
    License "or any later version" applies to it, you have the option of
    following the terms and conditions either of that specified version or
    of any later version that has been published (not as a draft) by the
    Free Software Foundation.  If the Document does not specify a version
    number of this License, you may choose any version ever published (not
    as a draft) by the Free Software Foundation.  If the Document
    specifies that a proxy can decide which future versions of this
    License can be used, that proxy's public statement of acceptance of a
    version permanently authorizes you to choose that version for the
    Document.
    
    11. RELICENSING
    
    "Massive Multiauthor Collaboration Site" (or "MMC Site") means any
    World Wide Web server that publishes copyrightable works and also
    provides prominent facilities for anybody to edit those works.  A
    public wiki that anybody can edit is an example of such a server.  A
    "Massive Multiauthor Collaboration" (or "MMC") contained in the site
    means any set of copyrightable works thus published on the MMC site.
    
    "CC-BY-SA" means the Creative Commons Attribution-Share Alike 3.0 
    license published by Creative Commons Corporation, a not-for-profit 
    corporation with a principal place of business in San Francisco, 
    California, as well as future copyleft versions of that license 
    published by that same organization.
    
    "Incorporate" means to publish or republish a Document, in whole or in 
    part, as part of another Document.
    
    An MMC is "eligible for relicensing" if it is licensed under this 
    License, and if all works that were first published under this License 
    somewhere other than this MMC, and subsequently incorporated in whole or 
    in part into the MMC, (1) had no cover texts or invariant sections, and 
    (2) were thus incorporated prior to November 1, 2008.
    
    The operator of an MMC Site may republish an MMC contained in the site
    under CC-BY-SA on the same site at any time before August 1, 2009,
    provided the MMC is eligible for relicensing.
    
    
    ADDENDUM: How to use this License for your documents
    
    To use this License in a document you have written, include a copy of
    the License in the document and put the following copyright and
    license notices just after the title page:
    
        Copyright (c)  YEAR  YOUR NAME.
        Permission is granted to copy, distribute and/or modify this document
        under the terms of the GNU Free Documentation License, Version 1.3
        or any later version published by the Free Software Foundation;
        with no Invariant Sections, no Front-Cover Texts, and no Back-Cover Texts.
        A copy of the license is included in the section entitled "GNU
        Free Documentation License".
    
    If you have Invariant Sections, Front-Cover Texts and Back-Cover Texts,
    replace the "with...Texts." line with this:
    
        with the Invariant Sections being LIST THEIR TITLES, with the
        Front-Cover Texts being LIST, and with the Back-Cover Texts being LIST.
    
    If you have Invariant Sections without Cover Texts, or some other
    combination of the three, merge those two alternatives to suit the
    situation.
    
    If your document contains nontrivial examples of program code, we
    recommend releasing these examples in parallel under your choice of
    free software license, such as the GNU General Public License,
    to permit their use in free software.

