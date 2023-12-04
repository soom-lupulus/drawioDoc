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

参数：cell

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
### `getLinkTitle`

获取链接（连接）的标题

【链接是指在 draw.io 图形编辑器中创建的连接线，用于连接不同的图形元素。每个链接可以具有一个标题，用于描述该链接的目的或关联】

参数：href

```javascript
// 获取链接的标题
var linkTitle = graph.getLinkTitle(link);

// 输出链接的标题
console.log("链接标题：" + linkTitle);
```
### `getPagePadding`

获取图形编辑器页面的边距（页边距）

【页面边距（页边距）是指图形编辑器页面边缘与实际绘图区域之间的空白区域。通过调整页面边距，你可以控制图形元素与页面边缘之间的距离】

```javascript
// 获取图形编辑器页面的边距
var pagePadding = editor.getPagePadding();

// 输出页面边距
console.log("页面边距：" + pagePadding);
```
### `getPreferredPageSize`

获取图形编辑器中首选的页面大小

【首选页面大小是指在图形编辑器中默认情况下使用的页面大小。该方法返回一个对象，包含首选页面的宽度和高度】

参数：bounds、width、height

```javascript
// 获取首选页面大小
var preferredPageSize = editor.getPreferredPageSize();

// 输出页面宽度和高度
console.log("首选页面宽度：" + preferredPageSize.width);
console.log("首选页面高度：" + preferredPageSize.height);
```
### `getRubberband`

获取橡皮筋选择（rubberband selection）的状态

【橡皮筋选择是指在图形编辑器中通过鼠标拖拽创建一个矩形区域，用于选择多个图形元素的操作。getRubberband 方法可以告诉你橡皮筋选择是否正在进行中】

```javascript
// 获取橡皮筋选择的状态
var rubberbandActive = graph.getRubberband();

// 输出橡皮筋选择的状态
console.log("橡皮筋选择状态：" + rubberbandActive);
```
### `getSubtree`

参数：initialCell

```javascript
无
```
### `globalVars`

无

```javascript
无
```
### `graphHandler`

处理图形编辑器中的各种图形操作和事件的对象

【graphHandler 对象是 draw.io 库中的一个核心组件，它负责处理用户与图形编辑器之间的交互。它包含了处理鼠标事件、键盘事件、元素选择、移动、调整大小等操作的方法和逻辑】

通过 graphHandler 对象，你可以对图形编辑器的行为进行自定义和扩展，以满足特定的需求

以下是一些 graphHandler 常用的方法和功能：

- 处理鼠标事件：graphHandler 可以捕获和处理鼠标的按下、移动和释放事件，以便进行图形元素的选择、移动、调整大小等操作。
- 处理键盘事件：graphHandler 可以捕获和处理键盘按键事件，例如删除图形元素、复制和粘贴等操作。
- 元素选择：graphHandler 提供了方法来处理图形元素的选择，包括单个元素选择、多个元素选择、取消选择等操作。
- 移动和调整大小：graphHandler 允许用户通过鼠标拖动来移动和调整图形元素的大小。
- 连接线操作：graphHandler 提供了方法来创建和编辑连接线，包括连接线的创建、调整连接点、修改连接线样式等操作。

```javascript
无
```
### `graphModelChangeListener`

它是一个接口或事件监听器，用于监听图形模型的变化

【图形模型是指图形编辑器中绘图区域中的图形元素和连接线的表示。当图形模型发生变化时，例如添加、删除或修改图形元素，graphModelChangeListener 可以监听这些变化并触发相应的事件或回调函数】

通过实现 graphModelChangeListener 接口或添加该事件监听器，你可以在图形模型发生变化时进行自定义的处理和操作。

```javascript
// 创建图形模型变化监听器
var graphModelChangeListener = {
  // 图形模型变化时触发的回调函数
  modelChanged: function(evt) {
    console.log("图形模型发生变化:", evt);
    // 进行自定义操作...
  }
};

// 添加图形模型变化监听器
graph.getModel().addListener(mxEvent.CHANGE, graphModelChangeListener);
```

### `gridEnabled`

控制图形编辑器中网格的显示与隐藏

【网格是图形编辑器中的一种辅助线，用于对齐和定位图形元素。通过设置 gridEnabled 属性，你可以决定是否显示网格。】

```javascript
// 获取当前的网格状态
var isGridEnabled = graph.isGridEnabled();

// 输出当前的网格状态
console.log("网格状态：" + isGridEnabled);

// 设置网格状态为启用
graph.setGridEnabled(true);

// 设置网格状态为禁用
graph.setGridEnabled(false);
```

### `gridSize`

设置图形编辑器中网格的大小

【网格是图形编辑器中的一种辅助线，用于对齐和定位图形元素。通过设置 gridSize 属性，你可以定义网格的大小，即网格单元的宽度和高度】

```javascript
// 获取当前的网格大小
var currentGridSize = graph.gridSize;

// 输出当前的网格大小
console.log("当前网格大小：" + currentGridSize);

// 设置网格大小为 20 x 20
graph.gridSize = new mxPoint(20, 20);
```

### `horizentalPageBreaks`

控制水平页面分隔线的显示

【水平页面分隔线是在 draw.io 中用于分隔图形编辑器中的页面的线条。它们帮助用户可视化地了解图形编辑器中的页面布局，并提供了页面之间的参考线】

```javascript
// 获取当前的水平页面分隔线状态
var isHorizontalPageBreaksVisible = graph.horizontalPageBreaksVisible;

// 输出当前的水平页面分隔线状态
console.log("水平页面分隔线状态：" + isHorizontalPageBreaksVisible);

// 设置水平页面分隔线状态为显示
graph.horizontalPageBreaksVisible = true;

// 设置水平页面分隔线状态为隐藏
graph.horizontalPageBreaksVisible = false;
```

### `imageBundles`

一个配置属性，用于加载自定义图像包

【图像包是一组自定义图像文件，可以被添加到 draw.io 中以扩展可用的图形库。通过配置 imageBundles 属性，你可以指定要加载的自定义图像包，使其在图形编辑器中可用】

```javascript
// 定义自定义图像包的配置
var customImageBundles = [
  {
    name: 'MyImages',
    url: 'path/to/my/image-bundle.xml'
  }
];

// 将自定义图像包配置添加到 imageBundles 属性
mxSettings.imageBundles = customImageBundles;
```

### `isBlankLink`

一个属性，用于指定链接在新的浏览器选项卡中打开还是在当前选项卡中打开

【当 isBlankLink 属性设置为 true 时，链接将在新的浏览器选项卡中打开，而不会改变当前的选项卡。这通常被称为在新标签页中打开链接。】

```javascript
// 设置链接在新标签页中打开
graph.isBlankLink = true;
```

### `isCellLocked`

检查指定单元格是否被锁定

【锁定单元格意味着该单元格不能被编辑或移动。通过调用 isCellLocked 方法，并传入要检查的单元格作为参数，你可以确定该单元格是否被锁定。】

```javascript
// 检查单元格是否被锁定
var isLocked = graph.isCellLocked(cell);

// 输出单元格的锁定状态
console.log("单元格锁定状态：" + isLocked);
```

### `isCellMobile`

无

```javascript
无
```

### `isHtmlLabel`

单元格属性，用于指定单元格标签是否以 HTML 格式呈现

【默认情况下，draw.io 的单元格标签是以纯文本形式呈现的，即将标签中的所有内容作为普通文本显示。但是，通过将单元格的 isHtmlLabel 属性设置为 true，你可以指定标签以 HTML 格式呈现，从而支持更丰富的文本样式和布局。】

```javascript
// 将单元格标签设置为 HTML 格式
cell.isHtmlLabel = true;
```

### `isMouseDown`

检查鼠标的按下状态

【isMouseDown 方法用于确定鼠标是否处于按下状态，即是否有鼠标按键被按下。这在处理与鼠标事件相关的逻辑时非常有用】

```javascript
// 检查鼠标的按下状态
var isMouseDown = graph.isMouseDown();

// 输出鼠标的按下状态
console.log("鼠标按下状态：" + isMouseDown);
```

### `isMouseInsertPoint`

无

```javascript
无
```

### `isMouseTrigger`

无

```javascript
无
```

### `isToggleEvent`

检查事件是否为切换事件

【切换事件通常用于在用户交互中切换某些状态或选项。通过调用 isToggleEvent 方法，你可以确定给定的事件是否被视为切换事件】

```javascript
// 检查事件是否为切换事件
var isToggle = graph.isToggleEvent(evt);

// 输出事件是否为切换事件
console.log("事件是否为切换事件：" + isToggle);
```

### `isZoomWheelEvent`

检查事件是否为缩放滚轮事件

【缩放滚轮事件通常在用户交互中用于缩放图形视图。通过调用 isZoomWheelEvent 方法，你可以确定给定的事件是否被视为缩放滚轮事件。】

```javascript
// 检查事件是否为缩放滚轮事件
var isZoomWheel = graph.isZoomWheelEvent(evt);

// 输出事件是否为缩放滚轮事件
console.log("事件是否为缩放滚轮事件：" + isZoomWheel);
```

### `labelLinkClicked`

无

```javascript
无
```

### `lastEvent`

获取最后一个触发的事件对象

【lastEvent 属性返回最近一次触发的事件对象，可以用于获取事件的详细信息，例如鼠标位置、键盘按键等】

```javascript
// 获取最后一个触发的事件对象
var lastEvent = graph.lastEvent;

// 输出最后一个触发的事件对象
console.log("最后一个触发的事件对象：", lastEvent);
```

### `lastMouseX`

获取最后一次鼠标事件发生时的鼠标 X 坐标

```javascript
// 获取最后一次鼠标事件的鼠标 X 坐标
var lastMouseX = graph.lastMouseX;

// 输出最后一次鼠标事件的鼠标 X 坐标
console.log("最后一次鼠标事件的鼠标 X 坐标：" + lastMouseX);
```

### `lastMouseY`

获取最后一次鼠标事件发生时的鼠标 Y 坐标

```javascript
// 获取最后一次鼠标事件的鼠标 Y 坐标
var lastMouseX = graph.lastMouseY;

// 输出最后一次鼠标事件的鼠标 Y 坐标
console.log("最后一次鼠标事件的鼠标 Y 坐标：" + lastMouseY);
```

### `layoutMannager`

一个对象，用于管理图形的布局

【layoutManager 对象负责自动调整和排列图形元素，以实现更好的布局效果。它提供了多种布局算法和选项，可以根据需要进行配置和使用】

```javascript
// 创建布局管理器实例
var layoutManager = new mxLayoutManager(graph);

// 配置布局参数
var layout = new mxCompactTreeLayout(graph);

// 设置布局参数
layout.horizontal = false;
layout.levelDistance = 40;
layout.nodeDistance = 20;

// 应用布局
layoutManager.getLayout = function(cell) {
  if (graph.getModel().isVertex(cell) &&
      graph.getChildCount(cell) > 0) {
    return layout;
  }
};

// 执行布局
layoutManager.execute();
```

### `lazyZoom`

设置是否启用惰性缩放

【启用 lazyZoom 后，当用户进行连续的缩放操作时，draw.io 会在缩放操作结束后才进行实际的重绘和布局。这可以提高性能，避免在用户连续缩放时频繁地进行重绘和布局操作】

```javascript
// 启用惰性缩放
graph.lazyZoom = true;

// 禁用惰性缩放
graph.lazyZoom = false;
```

### `lightbox`

一个插件或特性，用于在图形编辑器中显示图像、视频或其他媒体内容的浮动窗口

【Lightbox 功能使用户能够以浮动窗口的形式查看和操作媒体内容，而无需离开图形编辑器界面。这对于查看和编辑包含嵌入式媒体的图形非常有用】

Lightbox 功能可能需要在 draw.io 中启用或安装相应的插件

以下是一个示例，展示如何在 draw.io 中使用 lightbox 功能来显示媒体内容：

1. 在 draw.io 中打开图形编辑器。
2. 在编辑器中选择一个图形元素，该元素包含嵌入式媒体内容，例如图像或视频。
3. 右键单击所选图形元素，选择 "Lightbox" 选项。
4. 将以浮动窗口的形式显示媒体内容。

```javascript
无
```

### `mathEnabled`

启用或禁用数学公式的支持

【当 mathEnabled 设置为 true 时，draw.io 将支持使用数学标记语言（如 LaTeX 或 MathML）编写和渲染数学公式】

```javascript
// 启用数学公式支持
graph.mathEnabled = true;

// 禁用数学公式支持
graph.mathEnabled = false;
```

### `minimumGraphSize`

设置图形的最小尺寸

【minimumGraphSize 属性定义了图形在编辑器中的最小尺寸限制。当图形的大小小于最小尺寸时，用户将无法进一步缩小图形】

```javascript
// 设置图形的最小尺寸
graph.minimumGraphSize = new mxRectangle(0, 0, 200, 200);
```

### `model`

一个对象，用于表示图形的数据模型

【model 对象包含了图形的结构和属性信息，包括图形元素、连接线、样式、标签等。通过操作 model 对象，你可以修改图形的结构、属性和样式，以实现图形的创建、编辑和保存等功能】

```javascript
// 获取当前图形的模型
var model = graph.getModel();

// 在模型中添加一个图形元素
var parent = graph.getDefaultParent();
model.beginUpdate();
try {
  var vertex = graph.insertVertex(parent, null, 'New Vertex', 20, 20, 80, 30);
} finally {
  model.endUpdate();
}

// 修改图形元素的标签
model.setValue(vertex, 'Updated Vertex');

// 删除图形元素
model.beginUpdate();
try {
  model.remove(vertex);
} finally {
  model.endUpdate();
}
```

### `mouseListeners`

一个属性，管理鼠标事件的监听器

【mouseListeners 属性是一个数组，用于存储注册到图形编辑器上的鼠标事件监听器。通过添加和移除监听器，你可以对鼠标事件进行捕捉和处理，以实现自定义的交互行为】

```javascript
// 添加鼠标事件监听器
var listener = {
  mouseDown: function(sender, evt) {
    console.log('Mouse down event');
  },
  mouseUp: function(sender, evt) {
    console.log('Mouse up event');
  }
};

graph.mouseListeners.push(listener);

// 移除鼠标事件监听器
var index = graph.mouseListeners.indexOf(listener);
if (index !== -1) {
  graph.mouseListeners.splice(index, 1);
}
```

### `moveCells`

用于移动图形编辑器中的图形元素

【moveCells() 方法允许你在图形编辑器中移动一个或多个图形元素到指定的位置。你可以指定移动的目标位置、移动的距离以及要移动的图形元素】

```javascript
// 定义要移动的图形元素的 ID
var cellId = 'cell1';

// 获取图形元素对象
var cell = graph.getModel().getCell(cellId);

// 定义移动的距离
var dx = 100; // 在水平方向上移动 100 个单位
var dy = 50;  // 在垂直方向上移动 50 个单位

// 移动图形元素
graph.moveCells([cell], dx, dy);
```

### `multiplicities`

定义图形元素之间的连线约束

【multiplicities 属性允许你指定图形元素之间的连接规则，包括最小和最大连接数，以及允许的连接类型。通过定义 multiplicities 属性，你可以限制图形元素之间的连线方式，以确保符合特定的约束条件】

```javascript
// 定义连线约束规则
var multiplicities = [
  {
    source: 'sourceType',
    target: 'targetType',
    type: 'edgeType',
    min: 1,
    max: 1
  },
  {
    source: 'sourceType',
    target: 'targetType',
    type: 'edgeType',
    min: 0,
    max: 1
  }
];

// 将连线约束规则应用到图形编辑器
graph.multiplicities = multiplicities;
```

### `pageBreaksVisible`

控制页面分页符的可见性

【pageBreaksVisible 属性允许你在绘图编辑器中显示或隐藏页面分页符。页面分页符是用于指示绘图区域在打印或导出时如何分页的可视化标记】

```javascript
// 设置页面分页符可见性为 true（可见）
graph.pageBreaksVisible = true;

// 设置页面分页符可见性为 false（隐藏）
graph.pageBreaksVisible = false;
```

### `pageFormat`

设置页面的格式，包括页面尺寸、方向和边距等

【可以使用 pageFormat 属性来自定义页面的外观和布局】

```javascript
// 设置页面格式
var pageFormat = new mxRectangle(0, 0, 800, 600); // 页面尺寸为 800x600
graph.pageFormat = pageFormat;
```

### `pageScale`

设置页面的缩放比例

【pageScale 属性允许你定义页面的缩放级别，控制图形在绘图编辑器中的显示比例。通过设置 pageScale 属性，你可以调整页面的缩放级别，使图形在编辑器中显示得更大或更小】

```javascript
// 设置页面缩放比例为 0.75（75%）
graph.pageScale = 0.75;

// 设置页面缩放比例为 1.5（150%）
graph.pageScale = 1.5;
```

### `pageVisible`

控制页面的可见性

【pageVisible 属性允许你显示或隐藏绘图编辑器中的页面。当 pageVisible 设置为 true 时，页面将可见；当设置为 false 时，页面将隐藏。】

```javascript
// 设置页面可见性为 true（可见）
graph.pageVisible = true;

// 设置页面可见性为 false（隐藏）
graph.pageVisible = false;
```

### `panningHandler`

处理平移操作的处理程序

【panningHandler 用于处理绘图编辑器中的平移操作，使用户能够通过拖动画布来移动视图中的图形内容。当启用 panningHandler 后，用户可以在绘图编辑器中平移图形，以便查看和编辑大型图表】

```javascript
// 启用平移处理程序
graph.panningHandler.useLeftButtonForPanning = true;
```

### `panningManager`

管理平移操作的管理器

【panningManager 用于管理绘图编辑器中的平移操作，它提供了更高级的平移控制和功能。通过 panningManager，你可以定义平移的触发方式、平移的速度和边界限制等】

```javascript
// 创建 PanningManager 实例
var panningManager = new mxPanningManager(graph);

// 设置平移的触发方式
panningManager.setPanningTrigger(50);

// 设置平移速度
panningManager.normalPanSpeed = 4;

// 设置边界限制
panningManager.border = 0;
```

### `popupMenuHandler`

处理右键菜单的处理程序

【popupMenuHandler 用于在绘图编辑器中处理右键菜单的显示和操作。通过使用 popupMenuHandler，你可以自定义右键菜单的内容和行为，以满足特定的需求】

```javascript
// 创建 PopupMenuHandler 实例
var popupMenuHandler = new mxPopupMenuHandler(graph);

// 定义右键菜单项
var menu = new mxPopupMenu();
menu.addItem('菜单项1', function() {
  // 处理菜单项1的操作
});
menu.addItem('菜单项2', function() {
  // 处理菜单项2的操作
});

// 设置右键菜单
popupMenuHandler.setMenu(menu);
```

### `preferPageSize`

是否优先使用页面的尺寸

【默认情况下，当绘图编辑器中存在图形时，draw.io 会自动调整画布的尺寸以适应图形。然而，通过设置 preferPageSize 属性，你可以控制是否优先使用页面的尺寸而不是图形的尺寸】

```javascript
// 设置优先使用页面尺寸
graph.preferPageSize = true;
```

### `removeCells`

从图形编辑器中移除指定的单元格（cells）

需要注意的是，移除单元格时，它们将从图形编辑器中彻底删除，包括它们的所有连接和相关的图形元素。因此，在调用 removeCells 方法之前，请确保你真正想要从编辑器中移除这些单元格。

另外，removeCells 方法还接受一个可选的布尔参数，用于指定是否在删除单元格时同时删除与之相关的边。默认情况下，该参数的值为 true，即删除与单元格相关的边。如果你想保留与单元格相关的边，请将该参数设置为 false

```javascript
// 从图形编辑器中移除指定的单元格
graph.removeCells(cellsToRemove);

graph.removeCells(cellsToRemove, false);
```

### `renderHint`

设置图形编辑器的渲染提示

【通过设置 renderHint 属性，你可以指定图形编辑器在渲染图形时采用的优化方式，以提高性能或满足特定需求】

以下是一些常用的 renderHint 属性值：

- fast: 使用快速渲染模式。在此模式下，编辑器将使用一些简化的渲染技术，以获得更快的性能。但是，这可能会导致一些视觉细节的丢失或不准确。

- exact: 使用准确渲染模式。在此模式下，编辑器将尽可能准确地渲染图形，以保留所有视觉细节和精确性。但是，这可能会导致性能稍微下降。

- quality: 使用高质量渲染模式。在此模式下，编辑器将使用更高质量的渲染技术，以获得最佳的视觉效果和精确性。但是，这可能会导致性能较慢。

```javascript
// 设置渲染提示为 "fast"
graph.renderHint = "fast";
```

### `resetEdgesOnConnect`

控制在连接单元格时是否重置边缘

【当在图形编辑器中连接两个单元格时，边缘的连接点可能会自动调整以适应新的连接。通过设置 resetEdgesOnConnect 属性，你可以控制是否在连接时重置边缘的形状】

```javascript
// 设置在连接单元格时重置边缘
graph.resetEdgesOnConnect = true;
```

### `resetViewOnRootChange`

控制在更改根节点时是否重置视图

【当你在图形编辑器中更改根节点时，即更改图形的根节点元素时，resetViewOnRootChange 属性可以控制是否重置视图以适应新的根节点】

```javascript
// 设置在更改根节点时重置视图
graph.resetViewOnRootChange = true;
```

### `scrollbars`

控制图形编辑器是否显示滚动条

```javascript
// 设置滚动条可见
graph.scrollbars = true;
```

### `selectRegion`

在图形编辑器中选择指定区域内的元素

【x、y 是选择区域的左上角坐标，width、height 是选择区域的宽度和高度】

通过调用 selectRegion 方法，你可以在图形编辑器中选择指定区域内的元素。选择区域将以矩形框的形式显示，并且与该区域重叠的元素将被选中。

需要注意的是，selectRegion 方法只会选择与指定区域相交的元素。如果一个元素完全包含在选择区域之内，它将被选中。如果一个元素只是部分地与选择区域相交，它也会被选中。

通过使用 selectRegion 方法，你可以在 draw.io 中以编程方式选择特定区域内的元素，以执行进一步的操作，如移动、删除或修改这些元素。

```javascript
// 选择指定区域内的元素
graph.selectRegion(x, y, width, height);
```

### `selectionCellsHandler`

处理图形编辑器中选定的单元格（cells）的操作

```javascript
// 处理选定的单元格
graph.selectionCellsHandler = function(cells) {
  // 在此处执行对选定单元格的操作
};
```

### `selectionModel`

管理图形编辑器中的选择模型

【选择模型负责跟踪图形编辑器中当前选定的单元格（cells）。通过访问 selectionModel 属性，你可以获取和操作当前选定的单元格】

```javascript
// 获取当前选定的单元格
var selectedCells = graph.selectionModel.cells;

// 设置当前选定的单元格
graph.selectionModel.cells = selectedCellsArray;
```

### `setDefaultParent`

设置默认的父级单元格（parent cell）

【默认父级单元格是在图形编辑器中创建新元素时，新元素将被放置在其中的父级单元格。这对于组织和管理图形元素非常有用】

```javascript
// 设置默认的父级单元格
graph.setDefaultParent(parentCell);
```

### `shadowVisible`

控制图形元素是否显示阴影效果

```javascript
// 设置图形元素的阴影可见性
cell.style.shadowVisible = true;
```

### `sizeDidChange`

在图形元素的大小发生变化时执行相应的操作

```javascript
// 定义图形元素大小变化的处理函数
function onSizeChange(cell, newSize) {
  // 在此处执行图形元素大小变化后的操作
  console.log("图形元素大小已变化:", cell, newSize);
}

// 注册图形元素大小变化的处理函数
graph.sizeDidChange = onSizeChange;
```

### `standalone`

指定图形编辑器是否在独立模式下运行

【当 standalone 属性设置为 true 时，图形编辑器将以独立模式运行。这意味着编辑器将以完整的功能和界面显示，而不是嵌入到其他应用程序或网页中。】

```javascript
// 设置图形编辑器为独立模式
var isStandalone = true;
graph.standalone = isStandalone;
```

### `stylesheet`

定义和应用样式表（CSS）规则来自定义图形元素的外观

```javascript
// 定义自定义样式表规则
var customStylesheet = `
  .custom-style {
    fill: #ff0000;
    stroke: #0000ff;
    stroke-width: 2px;
  }
`;

// 应用自定义样式表
graph.stylesheet = customStylesheet;
```

### `tapAndHoldInProgress`

检测用户是否正在进行长按（tap and hold）操作

```javascript
// 检测长按操作是否进行中
var isTapAndHoldInProgress = graph.tapAndHoldInProgress;
```

### `tapAndHoldValid`

无

```javascript
无
```

### `themes`

应用不同的主题样式来改变图形编辑器的外观

```javascript
// 应用指定的主题
graph.setTheme('dark');
```

### `timerAutoScroll`

设置自动滚动的定时器的时间间隔（以毫秒为单位）

【通过设置 timerAutoScroll 属性，你可以控制自动滚动的定时器的时间间隔。自动滚动是指当用户将鼠标或触摸移动到绘图区域的边缘时，图形编辑器会自动滚动以便用户能够继续绘制或编辑图形】

通过调整 timerAutoScroll 的值，你可以改变自动滚动的速度和响应时间。较小的值会使滚动更为灵敏和迅速，而较大的值会使滚动速度变慢

```javascript
// 设置自动滚动的定时器时间间隔为500毫秒
graph.timerAutoScroll = 500;
```

### `tooltipHandler`

自定义图形元素的工具提示（tooltip）内容和行为

【通过设置 tooltipHandler 属性，你可以自定义图形元素的工具提示内容和行为。你可以根据需要返回不同的工具提示内容，甚至可以根据图形元素的属性进行动态生成。此外，你还可以控制工具提示在鼠标悬停时的显示和隐藏行为】

```javascript
// 自定义图形元素的工具提示
graph.tooltipHandler = {
  getTooltipForCell: function(cell) {
    // 返回图形元素的工具提示内容
    return 'This is a custom tooltip for the cell: ' + cell.id;
  },
  isHideOnHover: function() {
    // 指定工具提示是否在鼠标悬停时隐藏（可选）
    return false;
  }
};
```

### `transparentBackground`

设置图形编辑器的背景是否透明

【透明背景可以使绘图区域的背景透过，让下方的元素或背景图像可见】

```javascript
// 设置图形编辑器的背景为透明
graph.transparentBackground = true;
```

### `updateMouseEvent`

无

```javascript
无
```

### `useCssTransforms`

是否使用 CSS 转换（CSS transforms）来渲染图形

【CSS 转换是一种在浏览器中进行图形变换和平移的技术，通过使用 GPU 加速，可以提高图形的渲染性能和平滑度】

默认情况下，useCssTransforms 的值为 false，即不使用 CSS 转换。在某些情况下，如果你的应用或场景需要更好的性能和渲染效果，你可以将 useCssTransforms 设置为 true，以启用使用 CSS 转换来渲染图形

```javascript
// 启用使用 CSS 转换来渲染图形
graph.useCssTransforms = true;
```

### `verticalPageBreaks`

设置或获取垂直页面分隔线的位置

【通过设置 verticalPageBreaks 属性，你可以定义垂直页面分隔线的位置。这些分隔线用于在绘图区域中指示页面的边界。当图形编辑器的画布大小超过单个页面时，垂直页面分隔线可以帮助你对内容进行分页和布局】

你可以传递一个数字数组给 verticalPageBreaks 属性，其中的数字表示页面分隔线相对于画布左侧的位置（以像素为单位）。通过调整这些值，你可以自定义垂直页面分隔线的位置。

使用 verticalPageBreaks 属性，你可以根据设计需求在图形编辑器中设置垂直页面分隔线，以提供更好的页面布局和导航体验

```javascript
// 设置垂直页面分隔线的位置
graph.verticalPageBreaks = [100, 200, 300];
```

### `view`

控制图形编辑器的视图和显示

1. 设置缩放级别
2. 设置滚动位置
3. 获取当前可见区域

```javascript
// 将缩放级别设置为 100%
graph.view.scale = 1;

// 将滚动位置设置为 (100, 200)
graph.view.setTranslate(100, 200);

// 获取当前可见区域的矩形
var bounds = graph.view.getGraphBounds();
```

--end