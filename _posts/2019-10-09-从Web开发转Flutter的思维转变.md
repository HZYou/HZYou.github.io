---
layout:     post
title:      从Web开发转Flutter的思维转变
subtitle:   页面的一切都是类的实例--对象
date:       2019-10-08
author:     You
header-img: img/flutter-img.png
catalog: true
tags:
    - Flutter
    - 技术
---



## Web 对应到 Flutter

### 基本布局操作
#### 文本样式与对齐
css 中的文本字体样式、大小及其他文本属性对应Text widget中的TextStyle中的属性。

#### 设置box 的背景色
- 通过Container的decoration 属性(值为BoxDecoration对象)设置
- 通过Container的color 设置

#### 居中元素
Center widget 可以将子元素水平和垂直剧中。
```flutter
var container = Container(
  child:Center(
    child:Text('这是居中文本'),
  ),
  width:100,
  height:100,
  color:Colors.grey[300],
)
```

#### 设置容器宽度
用`Container` 的 width 属性。要设置最大、最小宽度用`constraints` 属性,其值为`BoxConstraints widget`;当父元素宽度小于子元素时，子元素会调整大小来匹配父元素大小。

#### 操控位置与大小
##### 绝对定位
默认情况下，子元素相对父元素定位。
要通过x-y坐标指定widget的绝对位置，把widget嵌套在Positioned wedget 中，Positioned再嵌套在一个 Stack widget中的TextStyle中的属性。
例如：
```
<div class="greybox">
  <div class="redbox">
    Lorem ipsum
  </div>
</div>

.greybox {
  background-color: #e0e0e0; /* grey 300 */
  width: 320px;
  height: 240px;
  font: 900 24px Roboto;
  position: relative; 
}
.redbox {
  background-color: #ef5350; /* red 400 */
  padding: 16px;
  color: #ffffff;
  position: absolute;
  top: 24px;
  left: 24px; 
}
```
对应Flutter代码：
```flutter
var container = Container(
  child:Stack(
    children:[
      Positioned(
        child:Container(
          child:Text('这是文本',style:bold24Roboto),
          padding:EdgeInsets.all(16),
          decoration:BoxDecoration(
            color:Colors.red[400],
          ),
        ),
        left:24,
        top:24
      )
    ],
  ),
  width:320,
  height:240,
  color:Colors.grey[300],
);
```

##### 旋转元素
嵌套在`Transform widget`中，使用 Transform widget 的 alignment 和 origin 属性分别指定转换的原点（支点）的相对和绝对位置。
对于简单的 2D 旋转，widget 是依据弧度在 Z 轴上旋转的。(角度 × π / 180)

flutter 示例代码
```flutter
var container = Container(
  child: Center(
    child: Transform(
      child: Container(
        child: Text('这是旋转的文本',
            style: bold24Roboto, textAlign: TextAlign.center),
        padding: EdgeInsets.all(16),
        color: Colors.red[400],
      ),
      alignment: Alignment.center,
      transform: Matrix4.identity()..rotateZ(15 * 3.1415927 / 180),
    ),
  ),
  width: 240,
  height: 240,
  color: Colors.grey[300],
);
```