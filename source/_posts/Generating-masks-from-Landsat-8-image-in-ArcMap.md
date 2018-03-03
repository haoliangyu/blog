title: Generating masks from Landsat 8 image in ArcMap
date: 2015-05-08 21:38:02
comments: true
categories:
- GIS
tags:
- landsat
- remote sensing
- arcgis
---

Two months ago I have written a small python package [pymasker](https://github.com/haoliangyu/pymasker) to generate mask from the Quality Assessment band of Landsat 8 image and MODIS land products. This package is gaining popularity, But scripting may not be convenient for users who are not familiar with programming, therefore I create a ArcMap python toolbox based on this package for interactive masking.
<!-- more -->
The **ArcMasking** toolbox contains two script tools, one designed for Landsat 8 QA band and one for generic quality assessment bits in other NASA remote sensing products like MODIS.

This tool can be download at [GitHub](https://github.com/haoliangyu/arcmasker/releases/tag/ArcMasker_0.1). After unzipping the package, you could open the ArcMasker.tbx file at the Catalog window in ArcMap and find following tools.

## From Landsat 8 QA Band

---

{% asset_img Masking_from_Landsat_8.png This is an example image %}

This tool is used to create masks from the Quality Assessment band of Landsat 8 OLI image. It requires several inputs:

* **Quality Assessment Band** of Landsat 8 image

* **Mask type** including cloud, cirrus, water, snow or vegetation

* **Confidence Level** that indicates the likelihood of existing of specific situation. You can also choose to include confidence level above what has been selected.

* **Output Mask** saving path

## From Quality Assessment Bits

---

{% asset_img Masking_from_Quality_Assessment_Bits.png This is an example image %}

This tool is used to create masks from other NASA remote sensing products with general quality assessment bit like [MODIS land products](https://github.com/haoliangyu/pymasker/wiki/MODIS-use-sample). As each portion of QA bits suggests a certain condition of the image, this toolbox simply examines the value of specific portion of QA bits and generates mask accordingly. Required inputs include:

* **Quality Assessment Band**

* **Bit Position** that indicates where the desired portion of bits starts.

* **Bit Length** that indicates the length of bits.

* **Bit Value** that indicates the desired situation.

* **Output Mask** saving path
