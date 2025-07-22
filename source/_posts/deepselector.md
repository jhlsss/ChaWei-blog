---
title: vue中深度选择器的使用以及区别（/deep/、>>>、::v-deep）
date: 2025-7-21
tags: 深度选择器
categories: vue
---

文章摘自：[程深度选择器探秘](https://segmentfault.com/a/1190000045079523)

在使用组件化开发时，我们时常需要修改组件内部的样式，但Vue的样式封装特性（如`<style scoped>`）会阻止外部样式直接作用于组件内部。

###  1.`/deep/`

- **Vue 2.x中的用法**：`/deep/`是Vue 2.x中用于穿透组件样式封装的一种方式，类似于Sass的`/deep/`或`/deep/`的别名`::v-deep`（但Vue 2.x官方文档中并未直接提及`::v-deep`）。
- **兼容性**：支持CSS预处理器（如Sass、Less）和CSS原生样式。
- **注意**：在Vue 3.x中，`/deep/`不再被官方直接支持，虽然一些构建工具或库可能仍然兼容，但推荐使用`::v-deep`。

###  2.`>>>`

- **CSS原生语法**：`>>>`是CSS原生中的深度选择器语法，用于穿透样式封装。但在Vue单文件组件（.vue）中，它并不总是被直接支持，因为Vue会将其视为普通CSS选择器的一部分。
- **兼容性**：仅在某些特定环境（如Webpack的css-loader配置中）和原生CSS中有效，Vue单文件组件中通常需要特定配置才能使用。
- **注意**：在Vue 3.x中，`>>>`同样不再被推荐使用，应使用`::v-deep`。

###  3.`::v-deep`

- **Vue 3.x中的推荐用法**：`::v-deep`是Vue 3.x中引入的官方深度选择器，用于替代Vue 2.x中的`/deep/`和原生CSS中的`>>>`。
- **兼容性**：支持CSS预处理器和CSS原生样式，是Vue 3.x中推荐使用的深度选择器。
- **优点**：与Vue 3的其他新特性相兼容，提供了更好的开发体验。

### 4.`v-deep()`（Vue 3 Composition API，<mark>vite</mark>）

- **特殊用法**：在Vue 3的Composition API中，可以通过`v-deep()`函数在`<style>`标签中动态应用深度选择器。这不是CSS语法的一部分，而是Vue 3特有的模板编译特性。
  
- **用法**：通常在`<style>`标签的`scoped`属性下，结合`v-bind:class`或`v-bind:style`在模板中动态绑定样式时使用。
  
- **示例**：
  
  ```html
  <template>
    <div :class="{'custom-class': true}">
      <ChildComponent />
    </div>
  </template>
  
  <script setup>
  // Composition API 逻辑
  </script>
  
  <style scoped>
  .custom-class::v-deep(.child-class) {
    /* 样式规则 */
  }
  /* 或者使用v-deep()函数（虽然不直接在<style>中，但说明其概念） */
  /* 注意：实际中v-deep()不直接用于<style>标签内，而是可能通过其他方式结合Composition API使用 */
  </style>
  ```