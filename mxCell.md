# mxCell

## 方法

### `getId()`

示例中的单元格实例名为 `cell`，可以通过 `cell.getId()` 获取单元格的唯一标识符。

```javascript
let cellId = cell.getId();
```

### `setId(id)`

示例中的单元格实例名为 `cell`，可以使用 `cell.setId("cell1")` 将单元格的唯一标识符设置为 "cell1"。

```javascript
cell.setId("cell1");
```

### `getValue()`

示例中的单元格实例名为 `cell`，可以通过 `cell.getValue()` 获取单元格的值。

```javascript
let cellValue = cell.getValue();
```

### `setValue(value)`

示例中的单元格实例名为 `cell`，可以使用 `cell.setValue("Hello, world!")` 将单元格的值设置为 "Hello, world!"。

```javascript
cell.setValue("Hello, world!");
```

### `getStyle()`

示例中的单元格实例名为 `cell`，可以通过 `cell.getStyle()` 获取单元格的样式。

```javascript
let cellStyle = cell.getStyle();
```

### `setStyle(style)`

示例中的单元格实例名为 `cell`，可以使用 `cell.setStyle("shape=rectangle;fillColor=red")` 设置单元格的样式为 "shape=rectangle;fillColor=red"。

```javascript
cell.setStyle("shape=rectangle;fillColor=red");
```

### `isVertex()`

示例中的单元格实例名为 `cell`，可以使用 `cell.isVertex()` 检查单元格是否为节点。

```javascript
let isVertex = cell.isVertex();
```

### `setVertex(vertex)`

示例中的单元格实例名为 `cell`，可以使用 `cell.setVertex(true)` 将单元格设置为节点。

```javascript
cell.setVertex(true);
```

### `isEdge()`

示例中的单元格实例名为 `cell`，可以使用 `cell.isEdge()` 检查单元格是否为关系线。

```javascript
let isEdge = cell.isEdge();
```

### `setEdge(edge)`

示例中的单元格实例名为 `cell`，可以使用 `cell.setEdge(true)` 将单元格设置为关系线。

```javascript
cell.setEdge(true);
```

### `isConnectable()`

示例中的单元格实例名为 `cell`，可以使用 `cell.isConnectable()` 检查单元格是否可以连接。

```javascript
let isConnectable = cell.isConnectable();
```

### `setConnectable(connectable)`

示例中的单元格实例名为 `cell`，可以使用 `cell.setConnectable(true)` 设置单元格可以连接。

```javascript
cell.setConnectable(true);
```

### `isCollapsed()`

示例中的单元格实例名为 `cell`，可以使用 `cell.isCollapsed()` 检查单元格是否被折叠。

```javascript
let isCollapsed = cell.isCollapsed();
```

### `setCollapsed(collapsed)`

示例中的单元格实例名为 `cell`，可以使用 `cell.setCollapsed(true)` 将单元格折叠起来。

```javascript
cell.setCollapsed(true);
```

### `isVisible()`

示例中的单元格实例名为 `cell`，可以使用 `cell.isVisible()` 检查单元格是否可见。

```javascript
let isVisible = cell.isVisible();
```

### `setVisible(visible)`

示例中的单元格实例名为 `cell`，可以使用 `cell.setVisible(false)` 将单元格设置为不可见。

```javascript
cell.setVisible(false);
```

### `getParent()`

示例中的单元格实例名为 `cell`，可以通过 `cell.getParent()` 获取父级单元格。

```javascript
let parentCell = cell.getParent();
```

### `setParent(parent)`

示例中的单元格实例名为 `cell`，可以使用 `cell.setParent(parentCell)` 将单元格的父级设置为 `parentCell`。

```javascript
cell.setParent(parentCell);
```

### `getChildCount()`

示例中的单元格实例名为 `parentCell`，可以通过 `parentCell.getChildCount()` 获取子级单元格的数量。

```javascript
let childCount =parentCell.getChildCount();
```

### `getChildAt(index)`

示例中的单元格实例名为 `parentCell`，可以使用 `parentCell.getChildAt(index)` 获取指定索引处的子级单元格。

```javascript
let childCell = parentCell.getChildAt(index);
```

### `insert(child, index)`

示例中的单元格实例名为 `parentCell`，可以使用 `parentCell.insert(childCell, index)` 在指定索引处插入子级单元格。

```javascript
parentCell.insert(childCell, index);
```

### insertEdge(edge, index)

实例中的edge是需要添加的edge节点，第二个参数是作为source(true)插入还是作为target(false)插入    

```javascript
cell.insertEdge(edge, true)
```

### clone()

克隆返回一个新的cell

```javascript
const cloneCell = cell.clone()
```

### `remove(child)`

示例中的单元格实例名为 `parentCell`，可以使用 `parentCell.remove(childCell)` 移除指定的子级单元格。

```javascript
parentCell.remove(childCell);
```

<br/>

## 属性

### id

该属性用于唯一标识一个单元格。

### value

该属性用于存储单元格的值,比如文字内容、形状等。

### geometry

该属性用于存储单元格的几何信息,比如位置、大小等。

### style

该属性用于存储单元格的样式信息,比如颜色、字体大小等。

### vertex

如果单元格是一个实体,该属性为true;如果是一个连接线,则为false。

### edge

如果单元格是一个连接线,该属性为true;如果是一个实体,则为false。

### parent

该属性存储单元格的父单元格。

### source

如果单元格是一个连接线,该属性存储连接线的源单元格。

### target

如果单元格是一个连接线,该属性存储连接线的目标单元格。

### visible

该属性存储单元格是否可见的状态。

### collapsed

该属性存储单元格是否折叠的状态。

### connectable

这个属性标识该图形对象是否可以连接其他对象。

### tooltip

该属性存储单元格鼠标 hover 时显示的 tooltip 内容。

### 

## 其它

### `new mxCell()`

通过此方法，可以新建一个cell，返回新建的cell对象

```javascript
/**
 * @param {any} value cell的value
 * @param {mxGeometry} geometry cell的位置，宽高
 * @param {string} style cell的style
 * @param [string] value cell的objType
*/
const cell = new mxCell('元素1', new mxGeometry(10, 20, 50, 100), 'html=1;shape=text;')
```

### `mxGeometry`

- x：  x坐标
- y：  y坐标
- width： 宽
- height： 高
- relative:  相对位置还是绝对位置
- offset：  设置偏移的x，y
- points： 关系线的端点
- sourcePoint：  设置edge在source的连接位置
- targetPoint：   设置edge在target的连接位置
- traslate()： 偏移
- scale()：     缩放
- rotate()：  旋转