## 技術発表会

2015.12.14

清水　祐太

---
## OpenStreetMap

---
### OpenStreetMap(OSM) とは

* 無料地図の共同作成プロジェクト

* 2004年にイギリスで始動

* 編集にはアカウントが必要

* Apple、Flickr、Foursquare などが採用

* データを利用したサービスの作成が可能
  - 例：OpenSeaMap(海図に特化)

---
## Google Maps と比較してみる

---
### メリット
* 以下のような制限がない
 - 1日最大25,000回までの読み込み
 - 無料でアクセスできるページ限定 など

* Google Maps が規制されている国でも使える

* 地域によっては豊富に情報がある

---
###  デメリット
* 地域によっては情報が少ない

* 衛生写真が不足している
 - ストリートビューはない

* 住所検索が劣る

* API の情報がやや少ない

---
## API (OpenLayers / Leaflet)

---
### OpenLayers
* 機能が豊富（地図の回転など）

* ズーム、パンがスムーズ

* 2系 / 3系に分かれている

* 公式のサンプルが豊富

---
### Leaflet
* OpenLayers に比べると機能は少ない

* 軽量

* 記述がシンプル

* プラグインが豊富

---
### 地図表示例 (OpenLayers)

```
var zoom = 12;
var lat = 35.4750726;
var lng = 133.0673884;
var marker = 'images/marker.png';
var olMap = new ol.Map({
  target: 'open-layers',
  layers: [
    new ol.layer.Tile({
      source: new ol.source.OSM()
    })
  ],
  view: new ol.View({
    center: ol.proj.transform([lng, lat], "EPSG:4326", "EPSG:3857"),
    zoom: zoom
  })
});
```

---
### マーカー設置例 (OpenLayers)

```
var markerStyleDefault = new ol.style.Style({
  image: new ol.style.Icon(/** @type {olx.style.IconOptions} */ {
    src: marker
  })
});

var markerSource = new ol.source.Vector({
  features: [
    new ol.Feature({
      geometry: new ol.geom.Point(ol.proj.transform([lng, lat], "EPSG:4326", "EPSG:3857"))
    })
  ]
});

var markerLayer = new ol.layer.Vector({
  source: markerSource,
  style: markerStyleDefault
});

olMap.addLayer(markerLayer);
olMap.getView().setZoom(17);
```

---
### 地図表示例 (Leaflet)

```
var zoom = 12;
var lat = 35.4750726;
var lng = 133.0673884;
var marker = 'images/marker.png';

// Leaflet
var leafletMap = L.map('leaflet').setView([lat, lng], zoom);

L.tileLayer('http://{s}.tile.osm.org/{z}/{x}/{y}.png', {
  attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
  detectRetina: true
}).addTo(leafletMap);
```

---
### マーカー設置例 (Leaflet)
```
var greenIcon = L.icon({
  iconUrl: marker,
  iconAnchor: [16, 16]
});

L.marker([lat, lng], {icon: greenIcon}).addTo(leafletMap);
leafletMap.setZoom(17);
```

---
## デモ

---
### まとめ

* 現状は Google Maps

* Google Maps が使えない状況での代替としては十分
