title: Converting C# Data Value to ArcObject Raster Pixel Value
date: 2015-03-21 21:30:54
comments: true
categories:
- GIS
tags:
- arcobject
- C#
---

The length of remote sensing pixel value is constrained by a predefined pixel value type. It is an unchangeable property for each remote sensing image and saving an unsupported value to a image may cause unpredictable errors like application crash or information loss resulted from implicit data type conversion.
<!-- more -->
If you are developing application based on ArcObject, you could know the pixel type of a raster layer simply with following code.

``` csharp
IRasterLayer rasterLayer = (IRasterLayer)layer;
IRasterProps rasterProps = (IRasterProps)rasterLayer.Raster;

// Get the pixel type of you raster layer
rstPixelType pixelType = rasterProps.PixelType;
```

You can find a full list and detailed explanation of ArcObject raster pixel types in [this page](http://resources.esri.com/help/9.3/arcgisengine/java/api/arcobjects/com/esri/arcgis/geodatabase/rstPixelType.html).

Not every raster pixel types has a corresponding C# value type. So I make a list for those pixels types having relative in C# so that we can make correct conversion while developing.

ArcMap Pixel Type  | Description                     | Corresponding C# Data Type  | Supported
------------------ | ------------------------------- | --------------------------- |-----------
PT_UNKNOWN         | unknown                         |                             | No
PT_U1              | 1 bit                           |                             | No
PT_U2              | 2 bit                           |                             | No
PT_U4              | 4 bit                           |                             | No
PT_UCHAR           | unsigned 8 bit integer          | Byte                        | Yes
PT_CHAR            | 8 bit integer                   | SByte                       | Yes
PT_USHORT          | unsigned 16 bit integer         | UInt16                      | Yes
PT_SHORT           | 16 bit integer                  | Int16                       | Yes
PT_ULONG           | unsigned 32 bit integer         | UInt32                      | Yes
PT_LONG            | 32 bit integer                  | Int32                       | Yes
PT_FLOAT           | single precision floating point | Single                      | Yes
PT_DOUBLE          | double precision floating point | Double                      | Yes
PT_COMPLEX         | single precision complex        |                             | No
PT_DCOMPLEX        | double precision complex        |                             | No
PT_CSHORT          | short integer complex           |                             | No
PT_CLONG           | long integer complex            |                             | No


Based on this table, I write a function to wrap the conversion from C# data type to valid ArcObject pixel value type. I use it in my project [ArcMap Raster Edit Suite](https://github.com/haoliangyu/ares) and it work pretty well.

```csharp
/// <summary>
/// Convert the csharp value to the ArcObject pixel value.
/// </summary>
/// <param name="csharpValue">Cshapr value</param>
/// <param name="pixelValueType">The pixel type of ouput value</param>
/// <param name="pixelValue">Output pixel value</param>
/// <returns>A value indicating whether the convention is successful</returns>
public static bool CSharpValue2PixelValue(object csharpValue, rstPixelType pixelValueType, out object pixelValue)
{
    try
    {
        switch (pixelValueType)
        {
            case rstPixelType.PT_UCHAR:
                pixelValue = (object)Convert.ToByte(csharpValue);
                return true;
            case rstPixelType.PT_CHAR:
                pixelValue = (object)Convert.ToSByte(csharpValue);
                return true;
            case rstPixelType.PT_SHORT:
                pixelValue = (object)Convert.ToInt16(csharpValue);
                return true;
            case rstPixelType.PT_USHORT:
                pixelValue = (object)Convert.ToUInt16(csharpValue);
                return true;
            case rstPixelType.PT_CLONG:
                pixelValue = (object)Convert.ToInt32(csharpValue);
                return true;
            case rstPixelType.PT_ULONG:
                pixelValue = (object)Convert.ToUInt32(csharpValue);
                return true;
            case rstPixelType.PT_FLOAT:
                pixelValue = (object)Convert.ToSingle(csharpValue);
                return true;
            case rstPixelType.PT_DOUBLE:
                pixelValue = (object)Convert.ToDouble(csharpValue);
                return true;
            default:
                pixelValue = null;
                return false;
        }
    }
    catch (Exception)
    {
        pixelValue = null;
        return false;
    }
}
```
