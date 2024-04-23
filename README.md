# lc-vue-size-scale

尺寸刻度尺

常用场景：

- xxx

## Demo

[demo](https://unpkg.com/lc-vue-size-scale/docs/.vitepress/dist/index.html) 

## 安装 

```
npm i lc-vue-size-scale
```

## 例子

```vue
<template>
  <div style='position: relative; height: 500px; display: flex; flex-direction: column;'>
    <div style='height: 20px; display: flex;'>
      <div style='width: 20px;' />
      <div style='flex: 1; position: relative;'>
        <px-scale />
      </div>
      <div style='width: 20px;' />
    </div>
    <div style='flex: 1;display: flex;'>
      <div style='width: 20px; position: relative;'>
        <px-scale placement='left' />
      </div>
      <div style='flex: 1; position: relative;' />
      <div style='width: 20px; position: relative;'>
        <px-scale placement='right' />
      </div>
    </div>
    <div style='height: 20px; display: flex;'>
      <div style='width: 20px;' />
      <div style='flex: 1; position: relative;'>
        <px-scale placement='bottom' />
      </div>
      <div style='width: 20px;' />
    </div>
  </div>
</template>

<script setup lang="ts">
import { PxScale } from 'lc-vue-size-scale';

</script>

<style scoped>

</style>
```

## API

### Attributes

| 属性名 | 说明 | 类型 | 默认值 |
| ---- | ---- | ---- | ---- |
| v-model/modelValue | 绑定值 | string/array | - |


### Events

| 事件名 | 说明 | 类型 |
| ---- | ---- | ---- | 
| update:model-value | 数据绑定事件 | string/array |

### Slots

| 插槽名 | 说明 | 参数 |
| ---- | ---- | ---- | 
| default | 右侧图标 | - |