title: Making masks with Landsat 8 Quality Assessment band using Python
date: 2015-01-18 21:13:06
update: 2016-08-14
comments: true
categories:
- GIS
tags:
- remote sensing
- landsat
- python
---

**Update** Since 0.2.0, the *qabmasker* has been renamed as *landsatmasker* and the function *getmask* has been renamed as *getmultimask* for better identification. Please update your script accordingly.

**Update** Since 0.3.0, most class and function names have been updated according to the pep8.

The Quality Assessment (QA) band is a standard product included in each Landsat 8 image downloaded from USGS, which contains the quality information of each pixel such as cloud, snow/ice, water body etc. The detailed information of this band can be found at [Landsat 8 Quality Assessment Band](http://landsat.usgs.gov/L8QualityAssessmentBand.php).
<!-- more -->
Although the bits structure of the QA band is easy-to-understand, it would several steps to extract the desired mask in [QGIS](http://courses.neteler.org/processing-landsat8-data-in-grass-gis-7/) or [L-LDOPE Toolbelt](https://hyspeedblog.wordpress.com/2014/08/27/working-with-landsat-8-using-and-interpreting-the-quality-assessment-qa-band/). In this article, I am going to introduce how to use *pymasker* to generate masks from Landsat 8 QA band in Python. This package is designed to provide a straightforward and intuitive way to generate masks from the QA band. It is an open-source package and the project is hosted at [GitHub](https://github.com/dz316424/pymasker).

## Installation

The package can be shipped to your computer using pip.

```python
pip install pymasker
```

Or just install it with the source code.

```python
python setup.py install
```

This package depends on [**numpy**](http://www.numpy.org/). If you want to directly load the QA band file, [**GDAL**](https://pypi.python.org/pypi/GDAL/) is also in need.

## Sample

First of all, you need to load the QA band into the *qabmaser* class.

```python
from pymasker import LandsatMasker

# load the QA band directly
masker = LandsatMasker('LC80170302014272LGN00_BQA.TIF')

# load a numpy array that contains band data
masker = LandsatMasker(bandarray)
```

The QA band contains the detection result of the following four specific conditions for each pixel:

* Cloud

* Cirrus

* Snow/Ice

* Vegetation

* Water body

For each condition, the algorithm gives a confidence to indicate its existence on the pixel.

```python
from pymasker import LandsatConfidence

# Algorithm has high confidence that this condition exists (67-100 percent confidence).
conf = LandsatConfidence.high

# Algorithm has medium confidence that this condition exists (34-66 percent confidence).
conf = LandsatConfidence.medium

# Algorithm has low to no confidence that this condition exists (0-33 percent confidence)
conf = LandsatConfidence.low

# Algorithm did not determine the status of this condition.
conf = LandsatConfidence.undefined

# Nothing, unspecified confidence
conf = LandsatConfidence.none
```

To generate a mask, you need to define a desired confidence for the target condition.

*Pymasker* provides several functions to get the most commonly used mask. The resulting mask is a binary numpy array with 1 representing existence of specific condition and 0 representing nonexistence.

```python
# Get mask indicating cloud pixels with high confidence
mask = masker.get_cloud_mask(LandsatConfidence.high)

# Get mask indicating cloud pixels with at least medium confidence
mask = masker.get_cloud_mask(LandsatConfidence.medium, cumulative = True)

# Get mask indicating snow/ice pixels with at least medium confidence
mask = masker.get_snow_mask(LandsatConfidence.medium, cumulative = True)

# Get mask indicating water body pixels with high confidence
mask = masker.get_water_mask(LandsatConfidence.high)

# Get mask indicating vegetation pixels with high confidence
mask = masker.get_veg_mask(LandsatConfidence.high)
```

*Pymasker* also provides a function for multi-criteria masking. In this function, you need to specify the confidence level of each condition. If you don't want the function consider one of conditions, you need to set it as confidence.none. Two different masking methods are provided:

* Inclusive	-	Mask pixels that meet at least one of all criteria.

* Exclusive -	Only Mask pixels that meet all criteria. (default)

Sample code for multi-criteria masking

```python
# Get mask indicating cloud pixels (high confidence) and cirrus pixels (high confidence).
# Exclusive and noncumulative
mask = masker.get_multi_mask(cloud = LandsatConfidence.high, water = LandsatConfidence.high)

# Save the result if you want.
masker.save_tif(mask, 'result.tif')
```

{% asset_img maskresult.png This is an example image %}

Now you have your mask! Nice and quick!
