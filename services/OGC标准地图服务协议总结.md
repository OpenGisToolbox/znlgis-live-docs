# OGC标准地图服务协议总结

## 1. WMS

WMS（Web Map Service）是OGC（Open Geospatial Consortium）定义的一种地图服务协议。它允许客户端通过HTTP请求从多个远程服务器获取地理空间数据，并将这些数据渲染为地图。以下是一些WMS的主要特性：

1. **获取地图**：WMS的主要功能是获取地图。客户端可以发送一个GetMap请求，指定所需的地理空间范围、坐标系统、图层和样式，服务器会返回一个渲染后的地图图像。

2. **获取图层信息**：客户端可以发送一个GetCapabilities请求，获取服务器支持的图层、样式、坐标系统和其他元数据。这些信息可以帮助客户端构造GetMap请求。

3. **获取特性信息**：客户端可以发送一个GetFeatureInfo请求，获取地图上特定位置的特性信息。这个请求需要指定一个地图坐标和一个像素容差。

4. **支持多种格式**：WMS支持多种图像格式，包括PNG、JPEG、GIF和SVG。客户端可以在GetMap请求中指定所需的格式。

5. **支持多种坐标系统**：WMS支持多种坐标系统，包括地理坐标系统（如WGS84）和投影坐标系统（如Web Mercator）。客户端可以在GetMap请求中指定所需的坐标系统。

6. **支持样式**：WMS支持服务器端和客户端样式。服务器端样式是预定义的，可以在GetCapabilities响应中获取。客户端样式可以让客户端指定自己的渲染规则。

## 2. WFS

WFS（Web Feature Service）是OGC（Open Geospatial Consortium）定义的一种地图服务协议。与WMS不同，WFS允许客户端通过HTTP请求直接访问地理空间数据的特性，而不仅仅是渲染后的地图图像。以下是一些WFS的主要特性：

1. **获取特性**：WFS的主要功能是获取特性。客户端可以发送一个GetFeature请求，指定所需的图层和过滤条件，服务器会返回一个包含匹配特性的GML（Geography Markup Language）文档。

2. **获取图层信息**：客户端可以发送一个GetCapabilities请求，获取服务器支持的图层、特性类型、坐标系统和其他元数据。这些信息可以帮助客户端构造GetFeature请求。

3. **事务操作**：WFS支持事务操作，这意味着客户端可以发送Insert、Update和Delete请求，修改服务器上的特性。这个功能需要服务器支持WFS-T（Web Feature Service - Transactional）。

4. **支持多种格式**：WFS支持多种数据格式，包括GML、GeoJSON和KML。客户端可以在GetFeature请求中指定所需的格式。

5. **支持多种坐标系统**：WFS支持多种坐标系统，包括地理坐标系统（如WGS84）和投影坐标系统（如Web Mercator）。客户端可以在GetFeature请求中指定所需的坐标系统。

6. **过滤**：WFS支持强大的过滤功能，可以让客户端指定复杂的过滤条件，如空间关系（如交叉、包含和相邻）和属性比较（如等于、大于和小于）。

## 3. WCS

WCS（Web Coverage Service）是OGC（Open Geospatial Consortium）定义的一种地图服务协议。WCS允许客户端通过HTTP请求直接访问地理空间数据的覆盖（如栅格数据和统计数据），而不仅仅是特性或渲染后的地图图像。以下是一些WCS的主要特性：

1. **获取覆盖**：WCS的主要功能是获取覆盖。客户端可以发送一个GetCoverage请求，指定所需的图层、空间范围、坐标系统和输出格式，服务器会返回一个包含匹配覆盖的数据文件。

2. **获取图层信息**：客户端可以发送一个GetCapabilities请求，获取服务器支持的图层、覆盖类型、坐标系统和其他元数据。这些信息可以帮助客户端构造GetCoverage请求。

3. **支持多种格式**：WCS支持多种数据格式，包括GeoTIFF、NetCDF和HDF。客户端可以在GetCoverage请求中指定所需的格式。

4. **支持多种坐标系统**：WCS支持多种坐标系统，包括地理坐标系统（如WGS84）和投影坐标系统（如Web Mercator）。客户端可以在GetCoverage请求中指定所需的坐标系统。

5. **子集和插值**：WCS支持子集和插值操作，可以让客户端指定所需的空间范围和分辨率。服务器会根据这些参数提取或插值覆盖，以满足客户端的需求。

## 4. WMTS

WMTS（Web Map Tile Service）是OGC（Open Geospatial Consortium）定义的一种地图服务协议。WMTS允许客户端通过HTTP请求获取预渲染的地图瓦片，这些瓦片可以组合在一起合成连续的地图。以下是一些WMTS的主要特性：

1. **获取地图瓦片**：WMTS的主要功能是获取地图瓦片。客户端可以发送一个GetTile请求，指定所需的图层、样式、瓦片矩阵集、瓦片矩阵、行和列，服务器会返回一个渲染后的地图瓦片。

2. **获取图层信息**：客户端可以发送一个GetCapabilities请求，获取服务器支持的图层、样式、瓦片矩阵集和其他元数据。这些信息可以帮助客户端构造GetTile请求。

3. **支持多种格式**：WMTS支持多种图像格式，包括PNG、JPEG和GIF。客户端可以在GetTile请求中指定所需的格式。

4. **支持多种坐标系统**：WMTS支持多种坐标系统，包括地理坐标系统（如WGS84）和投影坐标系统（如Web Mercator）。每个瓦片矩阵集都对应一个坐标系统。

5. **高性能**：由于WMTS使用预渲染的地图瓦片，因此它通常比WMS和WFS更快。这使得WMTS非常适合用于实时数据和大规模数据。

## 5. WPS

WPS（Web Processing Service）是OGC（Open Geospatial Consortium）定义的一种地图服务协议。WPS允许客户端通过HTTP请求执行地理空间数据处理操作，这些操作可以是预定义的（如缓冲区分析和空间插值）或者是用户定义的。以下是一些WPS的主要特性：

1. **执行处理操作**：WPS的主要功能是执行处理操作。客户端可以发送一个Execute请求，指定所需的处理操作、输入数据和参数然后服务器会执行处理操作并返回结果。

2. **获取处理操作信息**：客户端可以发送一个GetCapabilities请求，获取服务器支持的处理操作和其他元数据。这些信息可以帮助客户端构造Execute请求。

3. **获取处理操作描述**：客户端可以发送一个DescribeProcess请求，获取处理操作的详细描述，包括输入数据、参数和输出结果的类型和格式。

4. **支持多种格式**：WPS支持多种数据格式，包括GML、GeoJSON、KML和CSV。客户端可以在Execute请求中指定输入数据和输出结果的格式。

5. **支持异步执行**：WPS支持异步执行，这意味着客户端可以发送一个Execute请求后立即返回，然后在稍后的时间点获取结果。这个功能对于耗时的处理操作非常有用。

## 6. CSW

CSW（Catalogue Service for the Web）是OGC（Open Geospatial Consortium）定义的一种地图服务协议。CSW允许客户端通过HTTP请求搜索、浏览和查询地理空间数据和服务的元数据。以下是一些CSW的主要特性：

1. **搜索元数据**：CSW的主要功能是搜索元数据。客户端可以发送一个GetRecords请求，指定所需的元数据模式和过滤条件，服务器会返回一个包含匹配元数据的XML文档。

2. **获取元数据信息**：客户端可以发送一个GetCapabilities请求，获取服务器支持的元数据模式、查询语言和其他元数据。这些信息可以帮助客户端构造GetRecords请求。

3. **获取元数据描述**：客户端可以发送一个DescribeRecord请求，获取元数据模式的详细描述，包括元数据的结构和语义。

4. **支持多种查询语言**：CSW支持多种查询语言，包括CQL（Contextual Query Language）和Filter Encoding。客户端可以在GetRecords请求中指定所需的查询语言。

5. **支持多种元数据模式**：CSW支持多种元数据模式，包括ISO 19115、Dublin Core和FGDC。客户端可以在GetRecords请求中指定所需的元数据模式。
