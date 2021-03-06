---
layout: post
title: "Flexbox in React Native"
img: react.png # Add image post (optional)
date: 2018-03-16
description: Flexbox入门 # Add post description (optional)
tag: [React, React Native]
---

# Flexbox 入门

如果你不熟悉 Flexbox，那你有伴了，我也不会。哈哈开个玩笑。

每当我学习一门新技术，我都要先问一个问题“这种技术为何存在？” 对于 flexbox，这个问题的答案可能是使用 CSS 创建一个多用途的布局相当麻烦。而 flexbox 的目的就是创建一个更有效的方法来"布置、对齐和分配容器中项目之间的空间，即使它们的大小位置是未知 和/或 是动态的"。简而言之，flexbox 的主要用途在于创建动态布局。

Flexbox 的主要思想是使父元素能够控制其所有(*直接*!)子元素，而不是让每个子元素控制其自己的布局。当你这样做时，父元素变成了一个 **flex container**，而子元素变成了 **flex item**。一个例子是，我们不必让一个元素的所有子元素浮动到左侧，并为每一个添加边距，而是由父元素指定将所有子元素排列成一行，使它们之间的间距相等。这样，布局责任就从子元素转移到了父元素，进而使你对应用的整个布局具有更精细的调整控制。

此小节有很多内容，分解为以下部分

- Flexbox轴
- Flex 方向
- 对齐内容
  - Flex-Start
  - Center
  - Flex-End
  - Space-Between
  - Space-Around
- 对齐项目
  - Flex-Start
  - Center
  - Flex-End
  - Stretch
- 居中内容
- Flex 属性
- 对齐单个项目


## Flexbox轴

目前，我们需要了解的关于 Flexbox 的最重要的概念是它由不同的[轴](https://www.quora.com/What-is-the-plural-of-axis)组成，包括**主轴**和**交叉轴**。

![axis1](https://i.imgur.com/0RaIbhK.jpg)

​									**Flexbox的轴：主轴和交叉轴**

在 React Native 中，默认情况下，**主轴**为垂直的，而**交叉轴**为水平的。后面的所有东西都将构建在**主轴**和**交叉轴**之上。

当我说"…沿主轴对齐所有子元素"时，我是说默认情况下，父元素的所有子元素将从上到下垂直布置。如果我说"…沿交叉轴对其子元素"时，我是说默认情况下，所有的子元素将从左到右水平布置。

Flexbox 的其余部分只是决定如何在主轴和交叉轴上对齐、定位、拉伸、展开、收缩、居中和包裹子元素。



## Flex方向

你会注意到在说到**主轴**和**交叉轴**时，我特别提到了"默认行为"。这是因为你实际上可以更改哪个轴作为主轴，哪个作为交叉轴。这就涉及我们的第一个 flexbox 属性`flex-direction`（或 React Native 中的`flexDirection`）。

`flex-direction` 有两个值:

- `row`（行）
- `column`（列）

默认情况下，React Native 中的每个元素都有 `flexDirection: column` 声明。当一个元素的 `flex-direction` 为`列`时，它的*主*轴为垂直的，而它的*交叉*轴为水平的，就像我们在上图中看到的那样。但是，如果你给一个元素 `flexDirection: row` 声明，轴就颠倒过来了。主轴变为水平的，而交叉轴变为垂直的。再次说明，这非常重要，因为你的整个布局都取决于这两个轴。

![flex-direction](https://i.imgur.com/KCFRIMH.jpg)

​									`flex-direction` **会改变那个轴为主轴**



## 对齐内容

接下来的内容变得有趣了。我们来看看我们可以用来沿这些轴对齐子元素的不同属性和值。 我们先主要来看*主*轴

为了指定子元素如何沿主轴对齐，你要使用 `justifyContent` 属性。`justifyContent` 具有五个你可以用来改变子元素的对齐方式的不同值。

- `flex-start`
- `center`
- `flex-end`
- `space-around`
- `space-between`

喔。我刚扔出了很多陌生的词。我会详细讲解每一个，所以不用担心。

如果你想跟我一起演练（*强烈*建议），那么请创建一个新的 React Native 项目，命名为 "FlexboxExamples"，并使用以下代码换出你的 `App.js` 代码：

```react
import React, { Component } from 'react'
import { StyleSheet, Text, View, AppRegistry } from 'react-native'

class FlexboxExamples extends Component {
  render() {
    return (
      <View style={styles.container}>
        <View style={styles.box}/>
        <View style={styles.box}/>
        <View style={styles.box}/>
      </View>
    )
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  box: {
    height: 50,
    width: 50,
    backgroundColor: '#e76e63',
    margin: 10,
  }
})
```

注意使用以上代码，我们更改的唯一东西是 `styles` StyleSheet 对象中的 `container` 对象的样式。暂时忽略 `flex: 1`。



## 对齐内容：Flex-Start（交叉轴的起点对齐）

![3](https://i.imgur.com/Txffdc4.jpg)

​					`justifyContent: 'flex-start'`**会使flex项目出现在主轴的起点**



`justifyContent: 'flex-start'` 会朝主轴的起点位置对齐每个子元素。

```
container: {
  flex: 1,
  justifyContent: 'flex-start',
}
```

如果你之前对主轴和交叉轴的重要性还有所怀疑，希望你现在坚定了信心。因为 `flexDirection` 默认为 `column`，并且我们使用的是对准主轴的 `justifyContent`，所以我们的子元素会朝着主轴的*开始位置*（左上角）对其并向下排列。



## 对齐内容：Center(居中)

![4](https://i.imgur.com/lY1cinm.jpg)

​						`justifyContent: 'center'` **使flex项目出现在主轴的中心**



`justifyContent: 'center'` 会朝主轴的中心对齐每个子元素。 

```
container: {
  flex: 1,
  justifyContent: 'center',
}
```



##对齐内容：Flex-End（交叉轴的起点对齐）

![5](https://i.imgur.com/PLCY499.jpg)

​					`justifyContent: 'flex-end'` **会使flex项目出现在主轴的终点**



`justifyContent: 'flex-end'` 会朝主轴的终点对其每个子元素。 

```
container: {
  flex: 1,
  justifyContent: 'flex-end',
}
```



## 对齐内容：Space-Between（两端对齐）

![6](https://i.imgur.com/p63iJ1w.jpg)

​			`justifyContent: 'space-between'` **会使flex项目出现在主轴的两端，子元素之间有间隔**



`justifyContent: 'space-between'` 会沿主轴两端对其每个子元素，且每项之间的间隔都相等。 

```
container: {
  flex: 1,
  justifyContent: 'space-between',
}
```



## 对齐内容：Space-Around(每个子项间隔相等)

![7](https://i.imgur.com/Ms6PqzO.jpg)

​					`justifyContent: 'space-around'`**沿主轴等距离间隔flex项目**



`justifyContent: 'space-around'` 会沿主轴均匀地排列每个子元素。 

```
container: {
  flex: 1,
  justifyContent: 'space-around',
}
```

现在我想让你想一想，如果我们将容器的 `flexDirection` 更改为 `row`，而非默认值 `column`，会发生什么？结果就是我们的主轴将不再是垂直的，而是水平的。这意味着每个子元素将*水平*而不是*垂直*对齐。

```
container: {
  flex: 1,
  flexDirection: 'row',
  justifyContent: 'space-around',
}
```

![8](https://i.imgur.com/JXw4OMc.jpg)

​	将`justifyContent:space-around`设为`flex-direction:row`**会将主轴变为水平方向，并均匀地排列flex项目**

注意，我们更改的是 `flexDirection` 的值，它大大改变了我们的布局。现在你已经开始认识到 flexbox 的真正功能了。



## 对齐项目（交叉轴）

现在让我们将重点完全转向交叉轴。为了指定子元素如何沿交叉轴对齐，你可以使用 `align-items` 属性。

你会以为 `alignItems` 与 `justifyContent` 具有完全相同的值。这样猜测是合理的，但是你错了。此属性具有四个不同的值可以用来更改子元素沿交叉轴的对齐方式。

- `flex-start`

- `center`

- `flex-end`

- `stretch`

  ​

##对齐项目 - Flex-Start

![9](https://i.imgur.com/ITGjhPu.jpg)

​					`alignItems:flex-start`**使flex项目出现在交叉轴的起点**

`alignItems: 'flex-start'` 会朝交叉轴的起点对齐每个子元素。

```
container: {
  flex: 1,
  alignItems: 'flex-start',
}
```



## 对齐项目：Center（居中）



![10](https://i.imgur.com/bTgt8on.jpg)

​						`alignItems: center`**会使flex项目出现在交叉轴的中间**

`alignItems: 'center'` 会朝交叉轴的中间对齐每个子元素。 

```
container: {
  flex: 1,
  alignItems: 'center',
}
```



## 对齐项目：Flex-End（交叉轴的终点对齐）

![11](https://i.imgur.com/MSTkFN8.jpg)

​					`alignItems:flex-end`**会使flex项目出现在交叉轴的终点**

`alignItems: 'flex-end'` 会朝交叉轴的终点对齐每个子元素。 

```
container: {
  flex: 1,
  alignItems: 'flex-end',
}
```



## 对齐项目：Stretch

![12](https://i.imgur.com/6wBbF6Q.jpg)

​						`alignItem:stretch`**会使flex项目占满交叉轴的整个宽度**

`alignItems: 'stretch'` 会沿交叉轴拉伸每个子元素 - 只要子元素没有特定的宽度(`flexDirection: row`) 或高度 (`flexDirection: column`)。 

```
container: {
  flex: 1,
  alignItems: 'stretch',
},
box: {
  height: 50,
  backgroundColor: '#e76e63',
  margin: 10,
}
```



当你认为你完全掌握了它时，flexbox 总会让你出其不意。当你将 `alignItems` 设为 `stretch`，每个子元素将延伸到父容器的完全宽度或高度**（只要该子元素没有特定的宽或高）**。注意在框样式中，我删除了 `width: 50`，因为 `flexDirection` 默认设为 `column`，意味着 flex 项目将水平拉伸（因为我们在使用 `alignItems`）。

为了巩固这一点，如果我将样式改为下面这样，我们的 UI 会变成什么样？

```
const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'stretch',
    flexDirection: 'row',
  },
  box: {
    width: 50,
    backgroundColor: '#e76e63',
    margin: 10,
  }
})
```

注意我将 `flexDirection` 改成了 `row`，并重新添加了 `width: 50` 和删除了 `height: 50`。

![13](https://i.imgur.com/SOgHfoe.png)

​			`flex-direction:row`和`alignItems:stretch`**会使flex项目沿交叉轴垂直拉伸**

我们来分析一下。首先，主轴现在为水平的，因为我们添加了 `flexDirection: row`。这意味着 `alignItems` 将沿*垂直*轴对齐项目。由于我们删除了子元素的高度并添加了 `alignItems: stretch`，这些元素将沿其父组件的整个长度拉伸，在这个例子中是整个视图。

目前为止，我们只有一个 flex 容器或父元素。但是不要混淆；如果你创建更多嵌套的 flex 容器，上面的逻辑对于这些子元素（flex 项目）同样适用，但是它们并非与整个视图相关（例如在我们的示例中），而是根据它们的父组件确定位置。你的整个 UI 将构建在嵌套 flex 容器上。

到这里，你可以说是 React Native 样式跆拳道的红带级别了。但还有其他一些 flexbox 功能我们需要看看。

你很快会意识到 React Native 中没有基于百分比的样式。虽然我同意这增加了一点难度，但使用百分比可以做，使用 Flexbox 都可以做。记住我们在上述所有例子中使用的 `flex: 1` 声明，这是我们用于设置样式的属性。有趣的是，网上并没为此功能的精确比较，但是它类似于 `flex-grow`（如果你知道这是用来干嘛的）。

像我们前面一遍遍看到的，flexbox 的作用是将控制权交给父元素，由它来处理其子元素的布局。`flex` 属性有点不同，因为它允许子元素指定它们相比于兄弟元素的高或宽。解释 flex 的最佳方式是看一些例子。



## 居中内容

我们从这样的视图开始：

![14](https://i.imgur.com/Cofh5wx.jpg)

​									**沿主轴和交叉轴居中内容**

你会如何实现它？注意我们的主轴是垂直的，这给了我们一个信号，那就是我们使用的是 `flexDirection: row`。这些方框位于两个轴的中间，这意味着我们使用的是 `justifyContent: 'center'` 和 `alignItems: 'center'`。

```
const styles = StyleSheet.create({
  container: {
    flex: 1,
    flexDirection: 'row',
    justifyContent: 'center',
    alignItems: 'center',
  },
  box: {
    width: 50,
    height: 50,
    backgroundColor: '#e76e63',
    margin: 10,
  }
})
```



## Flex属性



![15](https://i.imgur.com/CvLnNu7.jpg)

​				**使用**`flex`**属性来更改Flex项目相比其他Flex项目增加其尺寸的速度**

在上图中，布局是完全一样的 -- 但现在中间部分的宽是其他部分的两倍！这就是 `flex` 属性让我们做的。下面是代码：

```react
class FlexboxExamples extends Component {
  render() {
    return (
      <View style={styles.container}>
        <View style={[styles.box, {flex: 1}]}/>
        <View style={[styles.box, {flex: 2}]}/>
        <View style={[styles.box, {flex: 1}]}/>
      </View>
    )
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    flexDirection: 'row',
    justifyContent: 'center',
    alignItems: 'center',
  },
  box: {
    width: 50,
    height: 50,
    backgroundColor: '#e76e63',
    margin: 10,
  }
})
```

注意我没有添加任何样式！我只是将中间元素设为 `flex: 2`，而其他兄弟元素设为 `flex: 1`。这基本上是说"确保中间元素沿主轴的大小是第一和第三个子元素的的两倍"。这就是为什么 `flex` 可以取代百分比，因为通常基于百分比的布局是特定元素相对于其他元素，正如我们上面所做的。同样重要的是，要注意如果你将一个元素设置为 `flex: 1`，那个元素会与父元素占用同等多的空间。这就是为什么在我们上面的大部分例子中，我们想让"布局区域"的大小与父元素的相同，这在我们的示例中是整个视口。

我们将在之后更深入探讨！



##对齐各个 Flex 项目

如果我们想要这样的布局呢？

![16](https://i.imgur.com/BaBjut0.jpg)

​					`alignSelf:flex-end`**将目标flex项目改为出现在交叉轴结尾处**

看起来第一个和第三个元素分别垂直和水平居中的，而第二个元素有自己的想法，它沿着交叉轴使用 `flex-end`。要实现它，我们需要一种方式来使子元素覆盖它从父元素收到的特定定位。好消息是：这正是 `alignSelf` 的功能所在！注意，它以 *align* 开头，所以像 `alignItems` 一样，它将沿交叉轴进行定位。它还与 `alignItems` 具有完全相同的选项（`flex-start`、`flex-end`、`center`、`stretch`）。

实现上图的代码是:

```react
class FlexboxExamples extends Component {
  render() {
    return (
      <View style={styles.container}>
        <View style={styles.box}/>
        <View style={[styles.box, {alignSelf: 'flex-end'}]}/>
        <View style={styles.box}/>
      </View>
    )
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    flexDirection: 'row',
    justifyContent: 'center',
    alignItems: 'center',
  },
  box: {
    width: 50,
    height: 50,
    backgroundColor: '#e76e63',
    margin: 10,
  }
})
```

注意，我们所做的是向第二个子元素添加了 `alignSelf: flex-end`，它覆盖了父元素的指示 (`alignItems: 'center'`)。

如果这些你都搞懂了，棒极了！我意识到讲的东西确实有点多，但是希望这些帮助你掌握了 React Native 上的样式布局（特别是 flexbox）。



##总结

React Native 利用 **flexbox** 的一个版本来构建组件布局。这主要是因为 flexbox 能够跨不同的屏幕尺寸提供一致的布局。

Flexbox 容器包含两个轴: 一个**主轴**和一个**交叉轴**。使用 flexbox 构建布局时要考虑的一些关键属性包括 `flex-direction`、`justify-content` 和 `align-items`。然而，React Native 对 flexbox 的实现*有点*不同。我们将在下一小节看到不同之处！

**进一步研究**

- [Flexbox 的完整指南](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [Flexbox Froggy](http://flexboxfroggy.com/)