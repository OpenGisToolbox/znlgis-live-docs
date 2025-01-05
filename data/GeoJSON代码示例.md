# GeoJSON代码示例

## 1. 读取GeoJSON文件

### 1.1 实现思路

```mermaid

graph TD
    A[读取GeoJSON文件] --> B[读取GeoJSON文件内容]
    B --> C[解析GeoJSON文件内容]
    C --> D[构建SimpleFeatureCollection]
    D --> E[返回SimpleFeatureCollection]

```

### 1.2 代码示例

```Java

    public static SimpleFeatureCollection readGeojson(String geojsonPath){
        File file = new File(geojsonPath);
        Charset encoding = CharsetDetector.detect(file);
        String geojsonString = FileUtil.readString(file, encoding);

        GeometryJSON gjson = new GeometryJSON(16);
        FeatureJSON fjson = new FeatureJSON(gjson);

        try {
            SimpleFeatureType simpleFeatureType = fjson.readFeatureCollectionSchema(geojsonString, true);
            ListFeatureCollection featureCollection = new ListFeatureCollection(simpleFeatureType);
            try (FeatureIterator<SimpleFeature> features = fjson.streamFeatureCollection(geojsonString)) {
                while (features.hasNext()) {
                    featureCollection.add(features.next());
                }
            }

            return featureCollection;
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }

```

## 2. 写入GeoJSON文件

### 2.1 实现思路

```mermaid

graph TD
    A[构建图层结构] --> B[写入要素]
    B --> C[关闭图层]
    C --> D[写入编码]

```

### 2.2 代码示例

```Java

    public static void writeGeojson(String geojsonPath, SimpleFeatureCollection featureCollection,Integer wkid){
        GeometryJSON gjson = new GeometryJSON(16);
        FeatureJSON fjson = new FeatureJSON(gjson);
        
        try {
            CoordinateReferenceSystem crs = CRS.decode("EPSG:" + wkid, true);
            featureCollection = new ForceCoordinateSystemFeatureResults(featureCollection, crs, false);

            String geojsonString = fjson.toString(featureCollection);
            FileUtil.writeString(geojsonString, geojsonPath, "utf-8");
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    }

```
