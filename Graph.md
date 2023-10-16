# Graph

## 概念

每个 mxCell 对象都有一个 isVertex() 方法，用于判断该元素是否是一个顶点（vertex）。顶点是图形元素的一种类型，通常用于表示节点或形状。

## 方法

### `addClickHandler`

添加点击监听

类型：function

参数：highlight、beforeClick、onClick

```javascript
graph.addClickHandler(clickHandler);
```

### `allowAutoPanning`

允许自动平移

默认值：true

```javascript
无
```
### `allowLoops`

允许自己连接自己

【可以用于限制图形的结构，防止出现自环的情况】

默认值：true

```javascript
无
```
### `alternateEdgeStyle`

启用或禁用交替边样式。

【通过设置交替边样式，可以为连接图形中的节点的边应用不同的样式，例如线条颜色、线条类型、箭头样式等。】

默认值：“vertical”

```javascript
无
```
### `autoTranslate`

是否自动平移图形元素以适应视口的改变

默认值：false

```javascript
var graph = new mxGraph(container);
graph.autoTranslate = true;
```
### `background`

为图形指定一个背景颜色或背景图像，将影响整个图形的背景样式

```javascript
graph.background = '#F2F2F2'; // 设置为灰色背景
graph.background = 'url(path/to/image.png)'; // 设置背景图像
```
### `backgroundImage`

无

```javascript
无
```
### `backgroundPage`

设置图形的背景页面

【该页面可以是一个包含图像、文本或其他图形元素的画布。背景页面将位于图形的底层，并在图形上方显示】

```javascript
var background = new mxCell();
background.setVertex(true);
background.setConnectable(false);
background.setStyle('fillColor=#F2F2F2'); // 设置背景颜色

graph.backgroundPage = background;
```
### `cellEditor`

设置图形元素的编辑器

【为图形元素指定一个自定义的编辑器，以实现对该元素内容的编辑。编辑器可以是一个文本输入框、下拉列表、复选框等】

```javascript
var cell = graph.insertVertex(parent, null, 'Hello', 20, 20, 80, 30);
cell.cellEditor = new mxCellEditor(graph, new mxTextEditor());
```
### `cellMobileParentMap`

无

```javascript
无
```
### `cellRenderer`

mxCellRenderer 类，该类用于渲染和呈现图形元素（mxCell）。

【将图形元素渲染为可视化表示的核心组件之一。它负责处理图形元素的外观、样式和布局，以及将其绘制在画布上。可以自定义图形元素的渲染方式，包括颜色、形状、边框、文本等】

```javascript
var renderer = graph.cellRenderer;

renderer.registerShape('customShape', CustomShape);

function CustomShape(state, canvas) {
  mxShape.call(this, state, canvas);
}

CustomShape.prototype = new mxShape();
CustomShape.prototype.constructor = CustomShape;

CustomShape.prototype.paintVertexShape = function(c, x, y, width, height) {
  // 自定义绘制形状的逻辑
};

var cell = graph.insertVertex(parent, null, 'Hello', 20, 20, 80, 30);
cell.setVertex(true);
cell.setStyle('shape=customShape');
```
### `click`

点击事件

类型：function

```javascript
graph.addListener(mxEvent.CLICK, function(sender, evt) {
  var cell = evt.getProperty('cell');
  if (cell != null) {
    console.log('Cell clicked:', cell.getValue());
  }
});
```
### `connectVertex`

连接两个顶点（vertices）

【使用该方法来创建边（edge）连接它们】

参数：source、direction、length、evt、forceClone、ignoreCellAt、targetCell

```javascript
var parent = graph.getDefaultParent();
var v1 = graph.insertVertex(parent, null, 'Vertex 1', 20, 20, 80, 30);
var v2 = graph.insertVertex(parent, null, 'Vertex 2', 200, 20, 80, 30);

var edge = graph.connectVertex(parent, null, '', v1, v2);
```
### `connectionArrowsEnabled`

启用或禁用连接线的箭头显示

默认值：true

```javascript
var graph = new mxGraph(container);

// 启用连接线的箭头显示
graph.connectionArrowsEnabled = true;
```
### `connectionHandler`

用于处理连接操作的对象，负责管理连接线的创建、连接目标顶点以及处理连接事件等

【可以自定义连接操作的行为，如限制连接的类型、添加验证逻辑以及在连接完成后执行自定义操作】

```javascript
// 创建一个自定义的连接处理器
var customConnectionHandler = new mxConnectionHandler(graph);

// 设置连接处理器的回调函数
customConnectionHandler.connect = function(source, target, evt, dropTarget) {
  // 自定义的连接操作逻辑
  // 这里可以进行验证、添加样式等操作
  console.log('Connecting:', source, target);
};

// 将自定义的连接处理器设置为默认的连接处理器
graph.connectionHandler = customConnectionHandler;
```
### `constrainChildren`

控制顶点（vertex）的约束行为

【可以用于限制顶点的位置，使其在父节点（容器）内部移动时保持约束】

默认值：false

```javascript
var parent = graph.getDefaultParent();

// 创建一个父节点
var container = graph.insertVertex(parent, null, 'Container', 20, 20, 400, 200);

// 创建一个子节点
var child = graph.insertVertex(container, null, 'Child', 40, 40, 80, 40);

// 设置子节点的约束行为
child.setConnectable(false);
child.setVertex(true);
child.setConstrainChildren(true);
```
### `constrainRelativeChildren`

无

默认值：true

```javascript
无
```
### `container`

容纳图形元素的对象，可以是顶级容器或嵌套在其他容器中

【顶级容器用于承载整个图形，类似于画布的概念。可以在顶级容器中添加和管理其他图形元素，例如顶点（vertices）和边（edges）】

```javascript
var parent = graph.getDefaultParent();

// 创建一个顶级容器
var container = graph.insertVertex(parent, null, 'Container', 20, 20, 400, 200);
```
### `createHandler`

创建图形元素处理器

【允许自定义和配置各种图形元素的处理行为，例如顶点、边等】

```javascript
var vertexHandler = graph.createHandler();
vertexHandler.getInitialCellForEvent = function(evt) {
  // 自定义逻辑来获取初始的顶点单元格
  return graph.getDefaultParent();
};
vertexHandler.isConnectableCell = function(cell) {
  // 自定义逻辑来判断顶点是否可连接
  return cell.isVertex();
};
vertexHandler.previewColor = '#00FF00'; // 自定义预览颜色

// 将处理器应用到顶点
graph.getSelectionModel().addListener(mxEvent.CHANGE, function() {
  var cells = graph.getSelectionCells();
  if (cells.length === 1 && cells[0].isVertex()) {
    graph.addCellOverlay(cells[0], vertexHandler);
  } else {
    graph.removeCellOverlay(cells[0]);
  }
});
```
### `cumulativeZoomFactor`

控制累积缩放因子

【管理图形的缩放级别，并可以通过设置不同的值来改变缩放级别的累积效果】

默认值：1

```javascript
// 将 cumulativeZoomFactor 设置为较小的值
graph.cumulativeZoomFactor = 0.2;
```
### `currentEdgeStyle`

当前边（edge）样式

【用于获取和设置当前边的样式，包括线条颜色、线条宽度、线型等。】

```javascript
// 获取当前边的样式
var edgeStyle = graph.currentEdgeStyle;

// 设置当前边的样式
graph.currentEdgeStyle = 'strokeColor=#FF0000;strokeWidth=2;rounded=1;';
```
### `currentScale`

当前缩放比例

【获取和设置当前图形的缩放比例】

默认值：1

```javascript
// 获取当前图形的缩放比例
var scale = graph.currentScale;

// 设置当前图形的缩放比例
graph.currentScale = 0.8;
```
### `currentStyle`

当前图形元素样式

【获取和设置当前图形元素的样式，包括填充颜色、线条颜色、线条宽度、字体等】

```javascript
// 获取当前图形元素的样式
var style = graph.currentStyle;

// 设置当前图形元素的样式
graph.currentStyle = 'fillColor=#FFFF00;strokeColor=#FF0000;strokeWidth=2;fontSize=14;';
```
### `currentTranslate`

表示当前图形的平移坐标

【获取和设置当前图形在画布上的平移位置】

```javascript
// 获取当前图形的平移坐标
var translate = graph.currentTranslate;

// 设置当前图形的平移坐标
graph.currentTranslate = new mxPoint(100, 50);
```
### `currentVertexStyle`

表示当前顶点（vertex）样式

【获取当前顶点的样式信息，也可以通过修改属性值来改变当前顶点的样式】

```javascript
// 获取当前顶点的样式
var vertexStyle = graph.currentVertexStyle;

// 设置当前顶点的样式
graph.currentVertexStyle = 'shape=rectangle;fillColor=#FFFF00;strokeColor=#FF0000;strokeWidth=2;';
```
### `customLinkClicked`

无

类型：function

参数：link

```javascript
无
```
### `dblClick`

双击事件

类型：function

参数：evt、cell

```javascript
// 监听双击事件
graph.addListener(mxEvent.DOUBLE_CLICK, function(sender, evt){
    var cell = evt.getProperty('cell');
    // 执行双击操作的逻辑
    console.log('双击了图形元素:', cell);
});
```
### `defaultParent`

指定图形元素的默认父级容器

【当你在 draw.io 中创建新的图形元素时，它们需要被放置在一个父级容器中。如果你没有指定特定的父级容器，那么这些新的图形元素将会被放置在 defaultParent 所指定的默认父级容器中】

```javascript
// 获取默认父级容器
var defaultParent = graph.getDefaultParent();

// 设置默认父级容器
graph.setDefaultParent(someParentCell);
```
### `addClickHandler`

指定图形编辑器的渲染方言或画图模式

【draw.io 支持多种不同的渲染方言，如 mxGraph、svg、vml、html 和 xml 等。这些方言使用不同的技术和标记语言来呈现和操作图形】

```javascript
// 获取当前图形编辑器的渲染方言
var currentDialect = graph.dialect;

// 设置图形编辑器的渲染方言
graph.dialect = 'svg';
```
### `domainPathUrl`

无

```javascript
无
```
### `domainUrl`

指定图形编辑器的基本 URL

【domainUrl 属性定义了 draw.io 编辑器加载资源（如图像、样式表等）的基本路径。这对于正确加载和渲染图形编辑器的各种组件非常重要】

```javascript
// 获取当前图形编辑器的基本 URL
var currentDomainUrl = editorUi.editor.getUrl('domainUrl');

// 设置图形编辑器的基本 URL
editorUi.editor.setUrl('domainUrl', 'https://example.com/drawio/');
```
### `dropEnabled`

控制图形编辑器是否允许拖放操作

【当 dropEnabled 属性被设置为 true 时，用户可以将外部元素拖放到图形编辑器中，例如从文件系统中拖放图像文件到编辑器中创建图形元素】

```javascript
// 获取当前的 dropEnabled 属性值
var isDropEnabled = graph.dropEnabled;

// 启用或禁用拖放功能
graph.dropEnabled = true;

// 当拖放操作发生时，执行相应的逻辑
graph.addListener(mxEvent.DROP, function(sender, evt) {
  // 处理拖放操作的逻辑
  var element = evt.getProperty('event').dataTransfer.getData('text/plain');
  console.log('拖放的元素:', element);
});
```
### `duplicateCells`

用于复制选定的图形单元格或图形元素

参数：cells、append

```javascript
// 复制选定的图形单元格
var duplicatedCells = graph.duplicateCells(graph.getSelectionCells(), true);

// 在图形编辑器中插入复制的图形单元格
graph.setSelectionCells(graph.importCells(duplicatedCells));
```
### `editLink`

用于编辑指定图形元素的链接

【为图形元素添加或修改超链接。用户可以单击图形元素，然后编辑链接的目标 URL 或其他相关属性】

```javascript
// 编辑指定图形元素的链接
graph.editLink(cell);
```
### `enableFlowAnimation`

无

默认值：true

```javascript
无
```
### `eventListeners`

用于管理图形编辑器中的事件监听器

【eventListeners 对象允许你添加、移除和触发各种事件监听器，以响应图形编辑器中发生的不同事件】

```javascript
// 添加事件监听器
graph.eventListeners.add(mxEvent.CLICK, function(sender, evt) {
  console.log('点击事件已触发');
});

// 触发事件
graph.eventListeners.fireEvent(new mxEventObject(mxEvent.CLICK));
```
### `fireMouseEvent`

无

类型：function

参数：evtName、me、sender

```javascript
无
```
### `firstClickSource`

无

```javascript
无
```
### `firstClickState`

用于指示图形编辑器中的第一个点击状态

firstClickState 属性的值可以是以下之一：

- null：表示尚未发生第一个点击。
- "select": 表示第一个点击是选择操作。
- "connect": 表示第一个点击是连接操作。
- "create": 表示第一个点击是创建操作。

```javascript
// 获取第一个点击的状态
var firstClickState = graph.firstClickState;

// 检查第一个点击的状态
if (firstClickState === "select") {
  console.log("第一个点击是选择操作");
} else if (firstClickState === "connect") {
  console.log("第一个点击是连接操作");
} else if (firstClickState === "create") {
  console.log("第一个点击是创建操作");
} else {
  console.log("尚未发生第一个点击");
}
```
### `foldingEnabled`

用于控制图形编辑器中的折叠功能是否启用

【图形编辑器中的图形元素是否可以进行折叠和展开操作】

```javascript
// 启用折叠功能
graph.foldingEnabled = true;

// 禁用折叠功能
graph.foldingEnabled = false;
```
### `freeHand`

一个绘图对象，用于以自由曲线的形式进行绘图

【可以在图形编辑器中绘制自由曲线，类似于手绘的效果】

```javascript
无
```
### `getCursorForCell`

用于获取指定单元格的鼠标光标样式

参数：cell

```javascript
// 获取指定单元格的鼠标光标样式
var cursorStyle = graph.getCursorForCell(cell);

// 输出鼠标光标样式
console.log("鼠标光标样式：" + cursorStyle);
```
### `getCursorForMouseEvent`

无

参数：me

```javascript
无
```
### `getExportVariables`

无

```javascript
无
```
### `getGlobalVariables`

无

```javascript
无
```
### `getInsertPoint`

用于获取指定单元格的插入点位置

【插入点是指在单元格中插入新元素时的位置，通常是在单元格内部的某个位置】

```javascript
// 获取指定单元格的插入点位置
var insertPoint = graph.getInsertPoint(cell);

// 输出插入点的坐标
console.log("插入点坐标：x=" + insertPoint.x + ", y=" + insertPoint.y);
```
### `addClickHandler`

无

```javascript
无
```
### `addClickHandler`

无

```javascript
无
```
### `addClickHandler`

无

```javascript
无
```
### `addClickHandler`

无

```javascript
无
```
### `addClickHandler`

无

```javascript
无
```
### `addClickHandler`

无

```javascript
无
```
### `addClickHandler`

无

```javascript
无
```
### `addClickHandler`

无

```javascript
无
```