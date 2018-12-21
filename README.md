> 

## 安装

```sh
npm install my-color-picker
```

## 使用

```js
<template>
  <div>
    <my-color-picker />
  </div>
</template>

<script>
import MyColorPicker from 'my-vue-color-picker'

export default {
  components: {
    MyColorPicker
  }
}
</script>
```

## props开放接口说明

```js
    isShowText: {// 是否显示文本
      type: Boolean,
      default: true
    },
    isClickEqualPick: {// 文本点击效果是否与pick点击一致,pick即点击展开/关闭颜色选择区域的区域
      type: Boolean,
      default: false
    },
    pickWidth: {//  pick宽度
      type: Number,
      default: 20
    },
    pickHeight: {// pick高度
      type: Number,
      default: 20
    },
    width: {//  颜色选择区域宽度
      type: Number,
      default: 200
    },
    height: {// 颜色选择区域高度
      type: Number,
      default: 200
    },
    colors: {// 颜色选择区域颜色组成数组
      type: Array,
      default: () => ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet']
    },
    italic: {//  是否倾斜颜色方向,角度默认45’,默认水平方向,与下面的vertical,ritalic互斥
      type: Boolean,
      default: false
    },
    vertical: {//  竖直方向
      type: Boolean,
      default: false
    },
    ritalic: {//  第二象限倾斜135'
      type: Boolean,
      default: false
    }
```

## 属性

参数 | 类型 | 可选值 | 默认值 | 说明
--- | --- | --- | --- | ---


## 事件

事件名称 | 说明 | 回调参数
pick-color | 返回选中的颜色值 | string


## 更新日志

- 0.1.0
添加 初始版本发布

## Build Setup

```
# 安装依赖
npm install

# 本地运行
npm run serve

# 编译构建
npm run build
```