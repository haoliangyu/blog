title: Pymasker
date: 2015-01-21 22:03:02
categories:
- Project
tags:
- gis
- project
- python
---

Pymasker is a python package to generate various masks from the landsat 8 Quality Assessment band and MODIS products.
<!-- more -->
This project is hosted at [GitHub](https://github.com/haoliangyu/pymasker).

## Installation

The package can be shipped to your computer using pip.

```bash
pip install pymasker
```

Or just install it with the source code.

```bash
python setup.py install
```

This package depends on [**numpy**](http://www.numpy.org/). If you want to directly load the QA band file, [**GDAL**](https://pypi.python.org/pypi/GDAL/) is also in need if you want to .

## Releasse

* 0.1.0
	* First release of this package

* 0.1.2
	* Added multi-criteria masking
	* Added new confidence leve: none

* 0.1.3
	* Added *cumulative* options for multi-criteria masking
	* Fixed a default value problem in multi-criteria masking

* 0.1.4
	* Removed the dependence of GDAL

* 0.2.0
	* Added support for MODIS land products

* 0.2.3
	* Restructure package
