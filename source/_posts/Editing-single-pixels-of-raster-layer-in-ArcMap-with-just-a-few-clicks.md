title: Editing single pixels of raster layer in ArcMap with just a few clicks
date: 2015-02-17 21:42:56
comments: true
categories:
- GIS
tags:
- gis
- arcgis
---

Editing single pixels of a raster layer is a common task in daily GIS and RS practice. For example

* Removing misclassified pixels from a land cover classification result

* Creating a set of multiple raster layers with minor difference for model simulation

* etc.

In ArcMap we use Raster Calculator and Reclassification tool as many instructions suggest. However, these tools are designed to edit the layer as a whole and they are not flexible enough for minor modification. If ArcMap allows us to edit single features of a vector layer, why we cannot edit single pixels of a raster layer in ArcMap? That is the reason why the project ArcMap Raster Edit Suite (ARES) starts. It aims at providing an ArcMAp Add-In with tools to allows single raster pixels editing, just like what we can do with the vector layer. Flexible, quick and neat!
<!-- more -->
## Download and Install

---

This project is hosted and published at [GitHub](https://github.com/haoliangyu/ares). You can download the installation file at [Here](https://github.com/haoliangyu/ares/releases/download/0.1.3/AREA.0.1.3.zip)

After the download finishes, you need to choose the installation file that matches the ArcMap on your computer because this Add-In support ArcMap 10.0/10.1/10.2. There are two files in the folder and **ARES.esriAddin** is what you need:

{% asset_img unzipped_folder.png This is an example image %}

Double click and you could see the installation wizard.

{% asset_img install_wizard.png This is an example image %}

Just click **Install Add-In** and then you get it.

## Raster Editor Toolbar

----

Now you have a new toolbar **Raster Editor** installed in your ArcMap.

{% asset_img eidtor_toolbar.png This is an example image %}

This toolbar includes following tools:


* {% asset_img edit_tool.png This is an example image %}: **Select & Edit**, which is used to select pixels for editing.

* {% asset_img identify_tool.png This is an example image %}: **Identify**, which is used to select pixels in order to get their values, row/column indexes and zonal statistics.

* {% asset_img gotopixel_tool.png This is an example image %}: **Go To Pixel**, which is used to locate pixel with given row and column index.

The purpose of this toolbar is to provide tools for precise modification with known row and column index.

## Step by Step: Editing Raster Layer

---

In this section, I am going to show a brief guide on how to edit single pixels of raster layer in ArcMap.

* First of all, we have the layer imported in ArcMap.

* Then start the editing section at the ***Start Editor*** menu by clicking ***Start Editing*** button. You can only edit one raster layer at one time. If there are more than one raster layers in ArcMap, there will be a prompt-up window to let you choose one.

* Click the ***Select & Edit*** button to activate the tool.

* Click or drag a region of interest on the layer to selected pixels. All selected pixels will be highlighted on the map with a blue frame. **Noted that selecting too much pixels may lead to crash of ArcMap**.

{% asset_img select_pixels.png This is an example image %}

* Edit values of selected pixel at the **Raster Edit** Window. All edits will be highlighted on the map with a yellow symbol.

{% asset_img edit_pixels.png This is an example image %}

Make sure your input value is compatible with the pixel type of the raster layer. Any pixel left blank will be considered as NoData Pixel.

* Save edits to the raster file using ***Save Edits*** button on the ***Raster Editor*** menu. If you want to save edits to a new file, click the ***Save Edits As*** button. You will see the change of layer right after refreshing the ArcMap.

{% asset_img finish_editing.png This is an example image %}

* Stop the editing section by clicking ***Stop Editing*** button.

Now you finish the editing section and get the desired result.

## Why there is only one toolbar in the suite?

---

Well, we are working on anther toolbar so that we can make it a real tool suite. Please have a visit on our [project page](https://github.com/haoliangyu/ares) later.

If you like this project, give it a star :)
