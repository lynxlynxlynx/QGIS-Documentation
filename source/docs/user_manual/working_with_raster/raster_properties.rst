.. comment out this disclaimer (by putting '.. ' in front of it) if file is uptodate with release

|updatedisclaimer|

Raster Properties Dialog
=========================

To view and set the properties for a raster layer, double click
on the layer name in the map legend or right click on the layer name and choose
:guilabel:`Properties` from the context menu: 

This will open the :guilabel:`Raster Layer Properties` dialog, (see figure_raster_1_).

There are several tabs on the dialog:
   - :guilabel:`Style`
   - :guilabel:`Transparency`
   - :guilabel:`Colormap`
   - :guilabel:`General`
   - :guilabel:`Metadata`
   - :guilabel:`Pyramids`
   - :guilabel:`Histogram`


.. _figure_raster_1:

.. only:: html

   **Figure Raster 1:**

.. figure:: /static/user_manual/working_with_raster/rasterPropertiesDialog.png
   :align: center
   :width: 40em

   Raster Layers Properties Dialog |nix|

.. index:: Symbology, Single_Band_Raster, Three_Band_Color_Raster, Multi_Band_Raster	

.. _label_symbology:

Style Tab
----------

QGIS can render raster layers in two different ways: 
   1. Single band - one band of the image will be rendered as gray or in 
      pseudocolor or a freak out.
   2. Three band color - three bands from the image will be rendered, each
      band representing the red, green or blue component that will be used to create
      a color image.


Within both render types you can invert the color output using the
|checkbox| :guilabel:`Invert color map` checkbox.

**Single Band Rendering**

This selection offers you two possibilites to choose. At first you can
select which band you like to use for rendering (if the dataset has more than
one band).

The second option offers a selection of available colortables for rendering.

The following settings are available through the dropdownbox
:guilabel:`color map: Grayscale` |selectstring|, where grayscale is 
the default setting.

.. index:: Pseudocolor, Freak_out

Also available are:
   - :guilabel:`Pseudocolor`
   - :guilabel:`Freak Out`
   - :guilabel:`Colormap`


When selecting the entry :guilabel:`Colormap` |selectstring|, the tab :guilabel:`Colormap` becomes available. For more information see :ref:`label_colormaptab`.

QGIS can restrict the data displayed to only show cells whose values are
within a given number of standard deviations of the mean for the
layer. 

This is useful when you have one or two cells with abnormally high values in 
a raster grid that are having a negative impact on the rendering of the raster. 
This option is only available for pseudocolor and freak out images.

**Three band color**


This selection offers you a wide range of options to modify the appearance
of your rasterlayer. For example you could switch color-bands from the
standard RGB-order to something else.

Also scaling of colors are available.

.. tip:: **Viewing a Single Band of a Multiband Raster**

   If you want to view a single band (for example Red) of a multiband
   image, you might think you would set the Green and Blue bands to 
   "Not Set". But this is not the correct way. To display the Red band,
   set the image type to grayscale, then select Red as the band to use for Gray.

.. index:: Contrast_enhancement

**Contrast enhancement**


.. note::  
   when adding GRASS rasters the option *Contrast enhancement* will be 
   always set to automatically to *stretch to min max* regardless if 
   the Quantum GIS general options this is set to another value.

.. index:: Transparency

Transparency Tab
-----------------

QGIS has the ability to display each raster layer at varying transparency
levels. Use the transparency slider to indicate to what extent the underlying 
layers (if any) should be visible though the current raster layer. 
This is very useful, if you like to overlay more than one rasterlayer, e.g. a 
shaded relief-map overlayed by a classified rastermap. 
This will make the look of the map more three dimensional.

Additionally you can enter a rastervalue, which should be treated as
*NODATA*. This can be done manually or with the 
|mActionContextHelp| :sup:`Add values from display` icon.

An even more flexible way to customize the transparency can be done in the
:guilabel:`Custom transparency options` section.
The transparency of every pixel can be set in this tab.

As an example we want to set the water of our example rasterfile
:file:`landcover.tif` to a transparency of 20 %. The following steps
are neccessary:


#. Load the rasterfile :file:`landcover`.
#. Open the :guilabel:`Properties` dialog by double-clicking on the raster 
   filename in the legend or by right-clicking and choosing :menuselection:`Properties` 
   from the popup menu.
#. Select the :guilabel:`Transparency` tab
#. Click the |mActionNewAttribute| :sup:`Add values manually`
   button. A new row will appear in the pixel-list.
#. Enter the raster-value (we use 0 here) and adjust the transparency to 20 %.
#. Press the **[Apply]** button and have a look at the map.


You can repeat the steps 4 and 5 to adjust
more values with custom transparency.

As you can see this is quite easy to set custom transparency, but it can be
quite a lot of work. Therefore you can use the button 
|mActionFileSave| :sup:`Export to file` to save your transparency-list to a file. 
The button |mActionFolder| :sup:`Import from file` loads your transparency-settings 
and applies them to the current rasterlayer.


.. _label_colormaptab:

Colormap
---------

.. index:: Colormap

The :guilabel:`Colormap` tab is only available, when you have selected a
single-band-rendering within the :guilabel:`Style` tab 
(see :ref:`label_symbology`).

.. index:: Color_interpolation, Discrete

Three ways of color interpolation are available:
   1. :guilabel:`Discrete`
   2. :guilabel:`Linear`
   3. :guilabel:`Exact`


The button **[Add Entry]** adds a color to the individual color-table. 
**[Delete Entry]** deletes a color from the individual color-table and the 
**[Sort]** button sorts the color table according to the pixel values in the 
value column. Double-Clicking on the value-column lets you insert a 
specific value. Double clicking on the color-column opens the dialog 
:guilabel:`Select color` where you can select a color to apply on that value. 
Further you can also add labels for each color but this value won't be displayed 
when you use the identify feature tool.   

Alternatively you can click on the button 
|mActionNewAttribute| :sup:`Load colormap from Band`, which 
tries to load the table from the band (if it has any).

The block :guilabel:`Generate new color map` allows you to create newly
categorized colormaps. You only need to select the :guilabel:`number of classes` 
|selectnumber| and press the button :guilabel:`Classify`. Currently
only one :guilabel:`Classification mode: Equal Interval` |selectstring| is
supported. 

.. _label_generaltab:

General Tab
-------------

The :guilabel:`General` tab displays basic information about the selected raster,
including the layer source and  display name in the legend (which can be
modified). This tab also shows a thumbnail of the layer, its legend symbol,
and the palette.

Additionally scale-dependent visibility can be set in this tab. You need to
check the checkbox and set an appropriate scale where your data will be
displayed in the map canvas.

Also the coordinate reference system (CRS) is printed here as a PROJ.4-string.
This can be modified by hitting the **[Specify]** button.

.. index:: Metadata

Metadata Tab
-------------

The :guilabel:`Metadata` tab displays a wealth of information about the raster layer,
including statistics about each band in the current raster layer. Statistics
are gathered on a 'need to know' basis, so it may well be that a given layers
statistics have not yet been collected.

This tab is mainly for information. You cannot change any values printed
inside this tab. To update the statistics you need to change to tab
:guilabel:`Histogram` and press the button **[Refresh]** on the bottom right,
(see :ref:`label_histogram`).

.. index:: Pyramids

Pyramids Tab
-------------

Large resolution raster layers can slow navigation in QGIS. By creating lower
resolution copies of the data (pyramids), performance can be considerably
improved as QGIS selects the most suitable resolution to use depending on the
level of zoom.

You must have write access in the directory where the original data is stored
to build pyramids. 

Several resampling methods can be used to calculate the pyramids:
   * :guilabel:`Average`
   * :guilabel:`Nearest Neighbour`


When checking the checkbox |checkbox| :guilabel:`Build pyramids internally if possible` 
QGIS tries to build pyramids internally.

Please note that building pyramids may alter the original data file and once
created they cannot be removed. If you wish to preserve a 'non-pyramided'
version of your raster, make a backup copy prior to building pyramids.


.. _label_histogram:

Histogram Tab
---------------

.. index:: Histogram

The :guilabel:`Histogram` tab allows you to view the distribution
of the bands or colors in your raster. It is 
generated automaticaly when you open :guilabel:`Histogram` tab. You can 
choose which bands to display by selecting them in the list box at the bottom 
left of the tab. 

.. %% FIXME not supported at the moment
.. %Two different chart types are allowed:

.. [label=--]
.. %*  Bar chart
.. %*  Line graph

.. %You can define the number of chart columns to use and decide whether you want
.. %to \checkbox{Allow approximation} or display \checkbox{out of range} values
.. %Once you view the histogram, you'll notice that the band statistics have been
.. %populated on the |tab| :guilabel:`metadata} tab... )`

.. index:: Raster_statistics

.. tip::
   **Gathering Raster Statistics**

   To gather statistics for a layer, select pseudocolor rendering and
   click the **[Apply]** button. Gathering statistics for a layer can be time
   consuming. Please be patient while QGIS examines your data!
