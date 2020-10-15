# 虚拟 DOM

## 一、虚拟 DOM 是什么

- 一个能代表 DOM 树的对象，通常含有标签名、标签上的属性、事件监听和子元素们，以及其他属性。

## 二、虚拟 DOM 优点

### 1、减少 DOM 操作

- 为什么说虚拟 DOM 比真实 DOM 快？

  1.  减少操作次数：虚拟 DOM 可以减少 DOM 操作。将多次操作合并为一次操作，比如你添加 1000 个节点，DOM 可能要操作 1000 次，虚拟 DOM 可合并为一次操作。
  2.  缩小操作范围：虚拟 DOM 借助 DOM diff 可以把多余的操作省掉，比如你在原有的 990 个节点的基础上添加 10 个节点，把这 1000 个节点重新添加，虚拟 DOM 能分辨原有节点，只操作 10 个新增。

### 2、跨平台

- 跨平台
  1.  虚拟 DOM 不仅可以变成 DOM，还可以变成小程序 iOS 应用，安卓应用，因为虚拟 DOM 本质上只是一个 JS 对象

## 三、虚拟 DOM 缺点

- 需要额外的创建函数来创建虚拟 DOM，如 createElement 或 h，但可以通过 JSX 来简化成 XML 写法，或用 vue-loader。
  但是严重依赖打包工具。

- 规模太过庞大（节点超过几万十几万）的时候虚拟 DOM 反而比真实 DOM 更慢
  - 用 React 测试增加 100000 节点非常慢（不做任何优化的情况下）
  - 但 Vue 依然接近真实 DOM 的速度，很快（Vue 里默认自带了优化）

## 四、DOM diff

### 1. DOM diff 是什么

- 虚拟 DOM 的对比算法
- 就是一个函数，我们称之为 patch
- patches = patch(oldVNode, newVNode)
- patches 就是要运行的 DOM 操作，可能长这样:
  [
  {type: 'INSERT', vNode: ... },
  {type: 'TEXT', vNode: ... },
  {type: 'PROPS', propsPatch: [...]}
  ]

### DOM diff 优点

- 缩小操作范围：DOM diff 可以通过新旧节点的对比，把多余的操作省掉。比如在 1000 个节点中更新 10 个节点，DOM diff 会先对比新旧节点，只更操作不同之处。

### DOM diff 缺点

- 同级比较存在 bug

  - 砍掉左腿，右腿会变成左腿
  - 解决：加 key，给左右腿分别起名字
  - 注意：key 不能用 index！！！因为 index 会自动随着更新变化！！！

- 详见文章[《Vue2.0 v-for 中 :key 到底有什么用》](https://www.zhihu.com/question/61064119/answer/766607894)
