title: The unofficial documentation for ArcGIS Open Data APIs
date: 2017-02-11 11:48:55
categories:
- Open Data
tags:
- arcgis
- open data
---

[ArcGIS Open Data](http://opendata.arcgis.com) is a great network of governmental and institutional open data. While the data portal service runs on APIs, there is no official documentation of public APIs for ArcGIS Open Data. So this post is to provide the unofficial documentation of ArcGIS Open Data APIs, which are discovered in my work (mostly by accident).

<!-- more -->

This documentation is also published at [GitHub Gist](https://gist.github.com/haoliangyu/0d0abcccfd3b25beb8b7597b4b2fc497);

## Dataset Search API

### Example

```
http://data.portal.com/datasets?q=test
```

### Parameters

* **q** (string)

  query string for full text search

* **bbox** (unknown)

  boundary box for geographic search

* **required_keywords** (unknown)

  dataset keywords (tags) for search

* **page** (integer)

  current page of results

* **per_page** (integer)

  number of results per page (default: 10)

* **sort_by** (string)

  returned results sorting method:

  * `updated_at` (default)
  * `relevance`

* **sort_order** (string)

  returned results order:

  * `desc` (default)
  * `asc`

### Response Example

``` json
{
  "data": [
    {
      "display_field": "FAC_CAT",
      "max_record_count": 2000,
      "record_count": 11,
      "geometry_type": "esriGeometryPoint",
      "object_id_field": "FID",
      "supported_extensions": "",
      "advanced_query_capabilities": {
        "supports_pagination": true,
        "supports_query_related_pagination": true,
        "supports_query_with_distance": true,
        "supports_returning_query_extent": true,
        "supports_statistics": true,
        "supports_order_by": true,
        "supports_distinct": true,
        "supports_query_with_result_type": true,
        "supports_sql_expression": true,
        "supports_advanced_query_related": true,
        "supports_returning_geometry_centroid": false
      },
      "supports_advanced_queries": true,
      "id": "dd62922ee5c14d11a187aaf30052404f_0",
      "landing_page": "https://www.arcgis.com/home/item.html?id=dd62922ee5c14d11a187aaf30052404f",
      "description": "This feature layer, utilizing data from the U.S. Environmental Protection Agency (EPA), displays regional offices. The EPA began operation on December 2, 1970 and it inherited two regional systems from predecessor agencies. The Federal Water Quality Administration which used a nine region system and the Environmental Health Service which had adopted the ten Standard Federal Regions suggested by the Office of Management and Budget (OMB). In order to facilitate easier operations with local and state governments as well as other federal agencies the EPA chose to adopt the OMB Standard Federal Regions which still exist today.<div><br /></div><div><div><img src=\"http://fedmaps.maps.arcgis.com/sharing/rest/content/items/26b532f4bfb14e0eb517c644dcda73c1/data\" /><br /></div><div><i>Regional Office locations</i></div><div><br /></div><div>For more information: <a href=\"https://www.epa.gov/aboutepa\" target=\"_blank\">About EPA</a></div><div>For feedback, please contact: <a href=\"mailto:ArcGIScomNationalMaps@esri.com\" target=\"_blank\">ArcGIScomNationalMaps@esri.com</a></div><div><div><br /></div><div><div>EPA sites of interest<b><br /></b></div><div><b><br /></b></div><div><img src=\"http://fedmaps.maps.arcgis.com/sharing/rest/content/items/d543cdf1e9694f5f985eae5b2dcd36f8/data\" /> <a href=\"https://epa.maps.arcgis.com/home/index.html\" target=\"_blank\">ArcGIS Online Organizational Homepage</a><b><br /></b></div><div><b><br /></b></div><div>Other Federal User Community federally focused content that may interest you</div><div><b><br /></b></div><div><img src=\"http://fedmaps.maps.arcgis.com/sharing/rest/content/items/f83c3452ec074ee08c7f04975578c212/data\" /> <a href=\"http://fedmaps.maps.arcgis.com/home/search.html?q=owner%3AFederal_User_Community%20AND%20tags%3AUS%20EPA&amp;t=content&amp;restrict=false\" target=\"_blank\">U.S. Environmental Protection Agency</a>           <img src=\"http://fedmaps.maps.arcgis.com/sharing/rest/content/items/46785cfb399344a6af50d4514d6ef0f9/data\" /> <a href=\"http://open.fedmaps.opendata.arcgis.com/datasets?q=US+EPA&amp;sort_by=relevance\" target=\"_blank\">Open Data: U.S. EPA</a> </div></div></div></div>",
      "extent": {
        "coordinates": [
          [
            -125.676,
            24.242
          ],
          [
            -65.559,
            50.089
          ]
        ]
      },
      "fields": [
        {
          "name": "FID",
          "type": "esriFieldTypeInteger",
          "alias": "FID",
          "domain": null,
          "statistics": {
            "duration": 0
          },
          "updated_at": "2017-02-06T21:06:49.399Z"
        }
      ],
      "item_name": "EPA Regional Offices",
      "type": "ItemLayer",
      "item_type": "Feature Layer",
      "license": "<p><img src=\"http://downloads.esri.com/blogs/arcgisonline/esrilogo_new.png\" />This work is licensed under the Esri Master License Agreement.<br /></p><p><a href=\"http://links.esri.com/tou_summary\" target=\"_blank\">View Summary</a> | <a href=\"http://links.esri.com/agol_tou\" target=\"_blank\">View Terms of Use</a></p>",
      "name": "EPA Regional Offices",
      "owner": "Federal_User_Community",
      "tags": [
        "A-16",
        "A16",
        "U.S. Environmental Protection Agency",
        "U.S. EPA",
        "EPA",
        "regional offices",
        "regions",
        "Environmental Protection Agency",
        "places",
        "boundaries"
      ],
      "thumbnail_url": "https://www.arcgis.com/sharing/rest/content/items/dd62922ee5c14d11a187aaf30052404f/info/thumbnail/EPA_-_Regional_Offices_-_screen_capture.png",
      "public": true,
      "created_at": "2016-09-02T11:50:55.000Z",
      "updated_at": "2017-02-06T21:06:50.911Z",
      "url": "https://services2.arcgis.com/FiaPA4ga0iQKduv3/arcgis/rest/services/EPA_RegionalOffices/FeatureServer/0",
      "views": null,
      "quality": 86,
      "coverage": "global",
      "current_version": 10.41,
      "comments_enabled": true,
      "service_spatial_reference": {
        "wkid": 102100,
        "latestWkid": 3857
      },
      "metadata_url": null,
      "org_id": "FiaPA4ga0iQKduv3",
      "metadata": {
        "published": null,
        "present": false,
        "url": null,
        "online_resources": []
      },
      "structured_license": {
        "type": "custom",
        "text": "This work is licensed under the Esri Master License Agreement.<a href=\"http://links.esri.com/tou_summary\" target=\"_blank\">View Summary</a> | <a href=\"http://links.esri.com/agol_tou\" target=\"_blank\">View Terms of Use</a>"
      },
      "use_standardized_queries": true,
      "sites": [
        {
          "title": "PACI",
          "url": "http://paci-esridubaioffice.opendata.arcgis.com",
          "logo": null
        }
      ],
      "main_group_title": "Open Data - Derived US Independent Establishments and Gov't Corps",
      "main_group_description": "<span style='line-height: 24px; background-color: rgb(255, 255, 255);'><font face='Verdana' size='3'>The group contains a set of map services, web maps and map packages that can be used in a web browser or downloaded to your ArcGIS Desktop application.  The maps may be used as base maps and operational layers to support a variety of applications.</font></span>",
      "main_group_thumbnail_url": null
    }
  ],
  "metadata": {
    "query_parameters": {
      "bbox": null,
      "page": 1,
      "per_page": 1,
      "q": "*",
      "required_keywords": [],
      "sort_by": "updated_at",
      "sort_order": "desc"
    },
    "stats": {
      "count": 1,
      "total_count": 192,
      "top_tags": [
        { "name": "ocean", "count": 62 }
      ]
    }
  }
}
```
