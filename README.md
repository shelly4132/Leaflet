# Leaflet

## 簡介

[Leaflet](http://leafletjs.com/index.html) 是一套適用於各種平台的 JavaScript 地圖繪製工具，可以呈現類似 Google 地圖的效果。

它是一套開放原始碼的輕量級 JavaScript 網頁地圖函式庫，主要的特色是使用簡單、速度快，並且跨平台，許多知名網站（如 GitHub 與 Flickr 等）都是使用 Leaflet 來呈現地圖。

---

## 使用方式

### 基本地圖

首先再 `<head>` 區塊加入

```
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.2/dist/leaflet.css" />
<script src="https://unpkg.com/leaflet@1.0.2/dist/leaflet.js"></script>
```

接著在你想要呈現地圖的地方加入一個 `<div>`，並設定寬高。

```
<div id="mapid" style="width: 800px; height: 600px;"></div>
```

然後加入 JavaScript 的程式碼：

- 首先利用 `setView` 設定地圖的經緯度和 zoom level

```
var map = L.map('mapid').setView([22.9973, 120.2209], 15);
```

- 再來設定圖資來源，這邊用的是 OpenStreetMap

```
L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    maxZoom: 18,
}).addTo(map);
```

### 其他功能

#### L.marker

標記特定地點，比如說我要標記成大資訊系館，那我就把它的經緯度輸入進去。

```
var marker = L.marker([22.997255, 120.220792]).addTo(map);
```

#### L.circle

圈出特定區域，比如說我要圈出榕園就將榕園的經緯度設成中心，以半徑 90 公尺畫出一個圓。

```
var circle = L.circle(
    [23.000311, 120.216165],   // 圓心座標
    90,                // 半徑（公尺）
    {
        color: 'red',      // 線條顏色
        fillColor: '#f03', // 填充顏色
        fillOpacity: 0.5   // 透明度
    }
).addTo(map);
```

#### L.polygon

給定幾個點圈出多邊形區域，這裡是圈出成功湖。

```
var polygon = L.polygon([
    [23.0003531, 120.217004],
    [22.9998648, 120.2170156],
    [22.9998996, 120.2173902],
    [23.0003035, 120.2175811]
]).addTo(map);
```

#### bindPopup

加入訊息方塊

```
marker.bindPopup("<b>地標</b><br>成大資訊系館").openPopup();
circle.bindPopup("榕園");
polygon.bindPopup("成功湖");
```



#### 事件處理

當使用者點擊地圖時顯示該位置的經緯度


```
var popup = L.popup();
function onMapClick(e) {
  popup
	.setLatLng(e.latlng)
	.setContent("經緯度座標：" + e.latlng.toString())
	.openOn(map);
}

map.on('click', onMapClick);
```




