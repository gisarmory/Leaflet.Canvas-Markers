中文 | [English](./README-en.md)

# Leaflet.Canvas-Markers

一个Leaflet插件，基于Canvas方式绘制Marker，相比于传统的DOM方式，性能可以得到极大提升（下文会有对比测试）。

插件定义了一个`L.canvasIconLayer`的图层，将marker添加到这个图层后，图层内部会使用Canvas的方式来绘制Marker。

插件还支持添加文字，使用图片和文字组合可以实现标签的功能。

支持leaflet1.0.0及更高版本。



## 在线示例

[加载10万个Marker](http://gisarmory.xyz/Leaflet.Canvas-Markers/examples/index.html)

[加载10万个标签](http://gisarmory.xyz/Leaflet.Canvas-Markers/examples/index_label.html)



## 安装和基本使用

下载此代码库，拷贝 `dist` 文件夹中的`leaflet.canvas-markers.js到项目中，并添加引用。

```html
<script src="leaflet.canvas-markers.js"></script>
```

定义一个`canvasIconLayer`图层并添加到地图，然后向图层添加Marker，图层会自动使用canvas方式绘制marker。

```js
// 添加一个图层
var ciLayer = L.canvasIconLayer({}).addTo(map);

// 定义一个marker 
var marker =  L.marker([58.5578, 29.0087], {icon: icon});

// 把marker添加到图层
ciLayer.addMarker(marker);
```



## 使用标签

在定义icon时，增加`text`、`textAnchor`、`textFont`、`textFillStyle`来设置标签里的文字。

```js
// 添加一个图层
var ciLayer = L.canvasIconLayer({}).addTo(map);

 //定义一个icon设置图片和文字
var icon = L.icon({
    iconUrl: './img/bg.png',	//背景图片
    iconSize: [84, 34],			//设置图标大小
    iconAnchor: [40, 20],		//设置图标偏移

    text:i.toString(),			//添加文字
    textAnchor: [5, 0],         //设置文本偏移
    textFont:'14px bold',       //设置字体大小和样式
    textFillStyle:'#FFFFFF'     //设置字体颜色
});

// 定义一个marker 
var marker =  L.marker([58.5578, 29.0087], {icon: icon});

// 把marker添加到图层
ciLayer.addMarker(marker);
```



## 对比测试

插件在谷歌浏览器v66和IE11上进行了测试。下面是加载10万个Marker的测试结果：

<table>
  <thead>
    <tr>
      <th>测试指标</th>
      <th>传统方式</th>
      <th><b>该插件</b></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>内存使用</td>
      <td>高达2.8 Gb</td>
      <td><b>大约 300 M</b></td>
    </tr>
    <tr>
      <td>首次加载时间</td>
      <td>160-200 秒</td>
      <td><b>1秒以内</b></td>
    </tr>
    <tr>
      <td>缩放和移动时间</td>
      <td>超过3分钟</td>
      <td><b>0.5 秒</b></td>
    </tr>
  </tbody>
</table>

效果很明显，传统的DOM方式无论是加载还是操作都很慢。所以，如果你的数据量很大，那就应该优先考虑使用该插件这种的Canvas方式加载数据。



## 方法

- **addMarker(marker)**: 向图层添加marker.。
- **addMarkers(markers)**: 向图层添加多个marker。
- **removeMarker(marker, redraw)**: 从图层中删除marker，删除后marker不会马上消失，除非调用**redraw()**方法或缩放和移动地图，marker才会消失。如果想一步到位删除marker，请将**redraw**设置为“true”，或者直接调用**removeLayer()**方法。
- **redraw()**: 重新绘制图层
- **addOnClickListener(eventHandler)**: 为图层添加鼠标单击的侦听事件
- **addOnHoverListener(eventHandler)**: 为图层添加鼠标悬停的侦听事件

也可以使用默认的**addLayer**、**addLayers**和**removeLayer**（相当于removeMarker(marker，true) 方法来实现marker的添加和删除。



## 和原代码库的区别

1. 解决了地图缩放时会飘的问题
2. 解决了移动端手指捏合缩放时会飘的问题
3. 增加了添加文字接口，可以实现标签功能。



## 参考

[https://github.com/corg/Leaflet.Canvas-Markers](https://github.com/corg/Leaflet.Canvas-Markers)

[https://github.com/eJuke/Leaflet.Canvas-Markers](https://github.com/eJuke/Leaflet.Canvas-Markers)

[https://github.com/yakitoritabetai/Leaflet.LabelTextCollision](https://github.com/yakitoritabetai/Leaflet.LabelTextCollision)