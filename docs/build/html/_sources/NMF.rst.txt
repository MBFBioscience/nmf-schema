Neuromorphological File Specification
=====================================


Version 1.0.0 [1]_


1. Definitions
--------------


1. Research Resource Identifier (RRID): a persistent and unique identifier for referencing a research resource.


2. Introduction to the Neuromorphological File Format
------------------------------------------------------


This specification describes the elements of the neuromorphological data file. The structures represented have been continually developed for over 30 years, balancing accurate 3D representation of microscopic structures with the efficiency for reading, writing, storing, and rendering the reconstruction data. The neuromorphological file format balances structure with flexibility by storing each modeled object as a unique data element, and providing mechanisms for grouping any number and type of data elements. File-level metadata is stored that provides detail on the sample origin to ensure no important source information is separated from the corresponding data. Each structure implemented has had a strong influence from top neuroscientists to maintain a meaningful model and provide the necessary analysis options for that entity. The file specification will continue to be updated as needed to define added or modified data elements.


3. Neuromorphological File Contents
------------------------------------
The neuromorphological file format is an Extensible Markup Language (XML) 1.0 (Fifth Edition) format and includes two organizational aspects, elements, and attributes [1]. These aspects are detailed in the neuromorphological file specification provided by The World Wide Web Consortium (WC3). All neuromorphological data files have a header section that includes the file's introductory content followed by any traced data elements. Traced data elements are representations of a diverse range of neuromorphological structures found in microscopy image data.
::    

	<?xml version="1.0" encoding="ISO-8859-1"?>
	<mbf version= 4.0 appname="ApplicationName" appversion="YYYY.V.M" apprrid="SCR_xxxxx" insrrid="SCR_xxxxx">
	  <description></description>
	  <filefacts></filefacts>
	  <sparcdata></sparcdata>
	  <property name="TimePointManager"></property>
	  <images></images>
	  <thumbnail cols="64" rows="64"></thumbnail>
	
	  TRACING DATA
	
	</mbf>
	
*Figure 1 A Neuromorphological data file.  The header elements are displayed in blue. All MBF tracing data is a nested element of the <mbf> element and is represented above with the comment, TRACING DATA.*


3.1 Coordinate Space 
^^^^^^^^^^^^^^^^^^^^
The coordinate space for all neuromorphological data files is a three-dimensional space and all coordinates and measurements are in micrometer units (µm). The origin point of the coordinate system is (0, 0, and 0).


.. image:: 1.png
    :width: 900px
    :align: center
    :height: 400px
    :alt: alternate text

*Figure 2 demonstrates the 3D coordinate space with an origin point of (0, 0, and 0). The gray planes represent a 3D image volume with an image location coordinate, coord: (x, y, and z). Note the direction of the Z-axis. The most positive image plane of the 3D volume is image plane 1. The following image planes are in the same X and Y location, but their z location changes incrementally based on the z scaling. The units of this coordinate space are in micrometers (µm).*


4. Header Elements 
-------------------
The first line of all neuromorphological data files is always the XML declaration element. It contains two attributes, version and encoding, that define the structure and storage units of the neuromorphological file format.
::

    <?xml version="1.0" encoding="ISO-8859-1"?>

*Figure 3 The XML document declaration element, attributes, and values as they apear in the segmentation data file.*


*Table 1 The XML declaration element, attributes, and descriptions for all fields.*


The remainder of the data file is embedded within the <mbf> element, including file header information and the elements that comprise the tracing data used to model neuronal morphology and surrounding anatomies. The closing </mbf> is the last line of all neuromorphological data files.
::

    <mbf version= 4.0 appname="ApplicationName" appversion="YYYY.V.M" apprrid="SCR_xxxxx" insrrid="SCR_xxxxx">
	 ⋮
	</mbf>

*Figure 4 The <mbf> element, attributes, and values as they apear in the segmentation data file. The appversion for all MBF Bioscience software is reported with the year, version, and minor version (YYYY.V.M). The virtical elipses between the attributes of the <mbf> elements  and the </mbf> end tag is used as shorthand to indicate there are additional child elements of the <mbf> element that are not detailed in this figure.*


The following attributes reside directly within the <mbf> element:


*Table 2 The <mbf> element, attributes, and descriptions for all fields.*


The remaining portion of the header information is described in detail below. File header information includes necessary metadata that helps to describe the data included in the neuromorphological file.



4.1 <description>
^^^^^^^^^^^^^^^^^


The <description> element is a string of user optional text describing the contents of the data file. The format of the text is character data indicated by the CDATA section, used to differentiate the text block from markup.
::

    <description><![CDATA[Example description of image segmentation file]]></description>

*Figure 5 The <description> element contains the CDATA start section <![CDATA[ and CDATA end section ]] to indicate a large string of text that is not a data element.*


4.2 <filefacts>
^^^^^^^^^^^^^^^


The <filefacts> element stores sequentially ordered serial Z sections for the data file that correspond to physically or virtually sectioned histologic tissue. If no sections have been created for a data file, the only child element of the <filefacts> is the <sectionmanager>. In this case, the values of the <sectionmanager> attributes indicate there have been no sections created and the child element should be disregarded.
::

    <filefacts>
	  <sectionmanager currentsection="" sectioninterval="0" startingsection="0"/>
	</filefacts>

*Figure 6 displays the <filefacts> of a data file with no sections. Note the current section has no value, the sectioninterval value is “0”, and the startingsection value is “0”.*


If serial Z sections have been created for the data file, this child element contains meaningful parameters about the sections. Child <section> elements for each Z section are stored in the <filefacts> element.
::

    <filefacts>
	   <section sid="S1" name="Section N0" top="z.zz" cutthickness="n.nn" mountedthickness="n.nn"/>
	   <section sid="S2" name="Section N1" top="z.zz" cutthickness="n.nn" mountedthickness="n.nn"/>
	   <section sid="S3" name="Section N2" top="z.zz" cutthickness="n.nn" mountedthickness="n.nn"/>
	   <sectionmanager currentsection="Section Nx" sectioninterval="i" startingsection="N0"/>
	</filefacts>

*Figure 7 The <filefacts> of a data file with serial sections. Each section in the data file has a corresponding <section> element. The attributes of the <sectionmanager> element are now significant values.*


All child elements and attributes of the <filefacts> are defined in Table 3. 

*Table 3 The <filefacts> element, its child elements, attributes, and descriptions for all fields.*


4.3 <sparcdata>
^^^^^^^^^^^^^^^
The <sparcdata> element stores additional subject and annotation metadata. This information allows neuromorphological data files to be queried by species, subject ID, sex, age, and organ of the image sample origin. 

MBF products interface with an external database, Scicrunch that maintains lists of anatomical terms separated by organ, species, and atlas/parcellation scheme. Each anatomy term is associated with a unique identifier and is approved by a team of anatomical experts. The <sparcdata> element informs the species, subject, sex, and age of the image sample segmented along with the exact anatomical list used to segment the image.  
::

    <sparcdata>
	  <subject species="http://purl.obolibrary.org/obo/NCBITaxon_XXXXXX" subjectid="SUBJECT_001" sex="Male" age="14 Weeks"/>
	  <atlas organ="Brain" label="Allen Mouse Brain Atlas Terminology" rootid="http://purl.org/sig/ont/fma/fmaXXXX"/>
	</sparcdata>

*Figure 8 A neuromorphological data file related to a microscopy image sample from a 14-week old male mouse brain delineated using anatomical terminology from the Allen Mouse Brain Atlas [3]. The species and atlas rootid provide URL links to the term lists origin.*

The <sparcdata> child elements and their attributes are detailed in Table 4.

*Table 4 The <sparcdata> element, its child elements, attributes, and descriptions for all fields.*

4.4 <property name="TimePointManager">
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


The <property> element named “TimePointManager” will always be present in the neuromorphological data files, however, it is not used at this time. The element can be disregarded.


4.5 <images>
^^^^^^^^^^^^


Raw image data is not saved within neuromorphological data files, rather they are linked with a file location and name and other information about the image.

The <images> element in the header can contain one or many <image> elements enabling the neuromorphological data file to be associated with any number of source images. The images can be either 2D (a single image plane) or 3D (multiple image planes from a single file or multiple files). Image data can be combined in several ways inside the neuromorphological data file. The simplest is the single 3D or 2D image file. See an example in Figure 9. 
::

    <images>
	  <image>
	    <filename>\\FilePath\ImageName</filename><channels merge="no">
		<channel id="red" source="none"/>
		  <channel id="green" source="none"/>
		  <channel id="blue" source="none"/>
		</channels>
		<scale x="x.xxx" y="y.yyy"/>
		<coord x="x.xxx" y="y.yyy" z="z.zzz"/>
		<zspacing z="z.zzz" slices="n"/>
	  </image>
	</images>


*Figure 9 An <images> element with only one image associated with the data file.*

Within each <image> element, five nested elements provide details pertaining to that image(s).

*Table 5 The <image> element, its child elements, attributes, and descriptions for all fields.*

A neuromorphological data file with multiple, distinct images associated to the same file may include many <image> child elements in the <images> element. Each image will have its own set of child elements and attributes.
::

    <images>
	  <image>
	    <filename>\\FilePath\Image[1]</filename>
	    <channels merge="no"></channels>
		<scale/>
	    <coord/>
		<zspacing/>
	  </image>
	  <image>
	    <filename>\\FilePath\Image[2]</filename>
	    <channels merge="no"></channels>
		<scale/>
	    <coord/>
	    <zspacing/>
	  </image>
	</images>

*Figure 10 An <images> element with multiple distinct images associated with the same data file. Note there are two separate <image> child elements within the <images> element. For concicity, the attributes of each child elements of each <image> have been excluded from the figure, but follow the same structure as see in Figure 9.*

A 3D volume can be made up of many 2D image planes. These volumes are recorded within the neuromorphological data file with one <image> child element and an ordered list of <filename> children elements pointing to the location and file name for each image plane. Each 2D image plane is sequentially loaded from the list into a 3D image volume. The scale is consistent for every image plane. The <coord> reports the X, Y, and Z coordinates of the upper, left-hand corner of the first image plane. The distance between image planes and the number of slices is kept constant for the entire image volume.
::

    <images>
	  <image>
	    <filename>FilePath\Image[1]</filename>
		<filename>FilePath\Image[2]</filename>
		<filename>FilePath\Image[3]</filename>
		<filename>FilePath\Image[4]</filename>
		⋮
		<filename>FilePath\Image[N]</filename>
		<channels merge="no"></channels>
		<scale/>
		<coord/>
		<zspacing z="z.zzz" slices="N"/>
	  </image>
	</images>

*Figure 11 A data file with many 2D image planes that make up a 3D image volume. The file path and image name for each 2D image are reported sequentially in the same <image> child element. In the <zspacing> element, the distance between each 2D image is reported, z=“z.zz”. The number of 2D image planes that construct the 3D volume will equal the total number of slices=”N”. Other image elements have been shortened to emphasize the important differences in this image organization. The <channels>, <scale>, and <coord> attributes are still included in these data files.*

A multi-channel microscopy image can be generated by merging 2 or 3 source images that make up the image color channels. If the images are merged to create a multi-channel image, the <channels> merge attribute will have a value of “yes”. There will always be three <filename> elements that sequentially correspond to the <channel> elements (i.e. <filename>1 will always correspond to the red <channel> element). The <channel> id attribute reports the pseudocolor of the color channel (red, green, or blue). The source attribute defines the image channel number from the source image starting at 0. If no image is selected for a <channel> element, the <filename> will remain but no image path or name is reported and the <channel> source value will equal “none”.
::

    <images>
	  <image>
	    <filename>FilePath\Image[1]</filename>
	    <filename>FilePath\Image[2]</filename>
	    <filename>FilePath\Image[1]</filename>
	    <channels merge="yes">
	      <channel id="red" source="0"/>
	      <channel id="green" source="2"/>
	      <channel id="blue" source="1"/>
	    </channels>
	    <scale/>
	    <coord/>
	    <zspacing/>
	  </image>
	</images>

*Figure 12 A data file with multiple images merged into one multi-channel image. The first channel of Image[1], source=”0”, is displayed in MBF Bioscience software as red. The third channel of Image[2], source=”2”, is displayed in MBF Bioscience software as green. The second channel of Image[1], source”1”, is displayed in MBF Bioscience software as blue.*


4.6 <thumbnail>
^^^^^^^^^^^^^^^


The <thumbnail> element stores data to create a small graphical (64x64) representation of the tracing data. Each of the 64 <thumbnail-line> elements represent one row in the thumbnail. The 64 pixels in each row are represented with a 3-byte hexadecimal (RRGGBB) alphanumeric character.
::

    <thumbnail cols="64" rows="64">
	  <thumbnail-line>0xRR1GG1BB1RR2GG2BB2...RR64GG64BB64</thumbnail-line>
	  <thumbnail-line></thumbnail-line>
	  ⋮
	</thumbnail>

*Figure 13 The <thumbnail> element, child elements, attributes, and values as they apear in the segmentation data file. The cols and rows attributes define the pixel dimentions of the 2D traced data thumbnail. A <thumbnail-line> child elements is present for every row of the <thumbnail>, but it is abbriviated here for concision. There are RRGGBB characters for each column of the data file. In the figure, the subscript numbers indicate the column number for the character.*


5.Trace Data
------------


The traced data elements include all data models of neuromorphological structures and additional image annotations. A data file will not necessarily contain all traced data elements. Typically a data file will include more than one of a single traced element in a data file. For example, there may be many contours of the same contour type and/or of a different contour type depending on what has been segmented. Figure 14 demonstrates the general organization of all trace data elements with a neuromorphological data file.
::


	<?xml version="1.0" encoding="ISO-8859-1"?>
	<mbf ...>
	  HEADER ELEMENTS
	  <contour></contour>
	  <marker></marker>
	  <arrow></arrow>
	  <tree>
	    <spine></spine>
	    <varicosity></varicosity>
	  </tree>
	  <vessel></vessel>
	  <text></text>
	  <scalebar></scalebar>
	</mbf>

*Figure 14 Demonstrates the organization of all traced data elements in the Neuromorphological file format. All traced data and header elements are child elements of  the <mbf> element. The <spine> and <varicosity> elements are child elements of the <tree>. The order and number of these elements within the parent <tree> may vary. The header elements are represented with the HEADER ELEMENTS comment and do not actually appear this way in the data file. They have been abbreviated to focus attention on the traced data elements.*


5.1 Common Components
^^^^^^^^^^^^^^^^^^^^^


5.1.1 Color
###########


The color attribute is seen in many neuromorphological file elements. It uses a 3-byte hexadecimal (RRGGBB) alphanumeric character to represent the color of traced structures.

5.1.2 <point>
#############


The nested element <point> is included in several elements of the neuromorphological  file format to denote a point at a distinct X, Y, and Z location with a 3D micrometer coordinate space. The <point> element also includes a diameter value indicating the thickness at that point. These coordinates are represented using the corresponding x, y, z, and d attributes and are always in micrometer units.
::

    <point x="x.xx" y="y.yy" z="z.zz" d="d.dd"/>

*Figure 15 The <point> element, attributes, and values as they apear in the segmentation data file.*


5.1.3 <property name="Channel">
###############################


The “Channel” <property> indicates the image color channel used to trace an object. If a detection is performed on only one of the image color channels, then that image channel is reported for the detected data element. If the detection is performed on two or more color channels, the <property name= “Channel”> element will not be written for that structure. If the image is monochrome, the <property name= “Channel”> element will not be written for any structure. Child elements are expected to be detected in the same color channel as their parent structure. For example, a <branch>, <spine>, or <varicosity> is expected to be detected in the same color channel as the associated <tree>.
::
    
	Line#  Neuromorphological Data File
	[0]    <property name="Channel">
	[1]    <n>1</n>
	[2]    <n>0</n>
	[3]    <c>#RRGGBB</c></property>

*Figure 16 The <property name=”Channel” > element, attributes, and values. The line numbers and return spaces present in the figure above were added for clarity and do not exist in the data file structure. The line numbers correspond with the numbered values in Table 6. The “Channel” values actually appear as a string.*

*Table 6 The <property name=”Channel”> element, values, and descriptions for all fields.*


5.1.4 <property name="Set">
###########################


The <property> named “Set” can be found in any trace data element. The <property> is used to name and group one or many trace data elements. These elements can either be the same type (ex. just <tree> elements) or different types (ex. <marker>, <tree>, and <contour> elements). A set has one value that is a text string indicating the name of that set. An element can be associated with multiple “Set” properties.
::


	<contour name="Soma 1" color="#FFFF00" closed="true" shape="Contour">
	  <property name="GUID"></property>
	  <property name="FillDensity"></property>
	  <property name="Set"><s>EXAMPLE SET NAME</s></property>
	  <point .../>
	</contour>


*Figure 17 An example of the  “Set”  <property> and its text string value, <s>EXAMPLE SET NAME</s>. In this example, the <contour> element “Soma 1” has been placed into a set called EXAMPLE SET NAME. The <contour> includes the child  element <property name=”Set”> and the unique set name to indicate it belongs to the group of trace elements.*


5.2 <marker>
^^^^^^^^^^^^


5.3 Punctum
^^^^^^^^^^^


5.4 <contour>
^^^^^^^^^^^^^


5.5 Neurons
^^^^^^^^^^^


5.5.1 <tree>
############


5.5.2 Somas and Cell Bodies
###########################


5.6 Vascular Networks
^^^^^^^^^^^^^^^^^^^^^

5.6.1 <vessel>
##############


5.7 Annotations
^^^^^^^^^^^^^^^

5.7.1 <arrow>
#############


5.7.2 <text>
############


5.7.3 <scalebar>
################


6. References
-------------

.. [1] The version number given here is for the neuromorphological file specification and is independent of the version number for the Neuromophological file format and any MBF Bioscience Software. The date after the version number is the last modification date of this document.

