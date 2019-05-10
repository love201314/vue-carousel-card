# vue-carousel-card

> A vue-carousel-card component development based on [vue-carousel-card](https://github.com/jekorx/vue-carousel-card) `@jekorx`)

> vue 轮播卡片组件 在 vue-carousel-card@1.0.1 的基础上修改翻页按钮可超出轮播图的范围，如下

![vue-carousel-card](screenshot/pic2.png)

### 示例

> [demo 展示](https://jekorx.github.io/vue-carousel-card)

![vue-carousel-card](screenshot/pic0.png)
![vue-carousel-card](screenshot/pic1.png)

**PS：** 组件中间图片默认显示的宽度为父容器的50%; 如果需要改变图片的宽度， 适应自己的项目，提供一个只改`css`的思路，`fork`一下作者的项目，更改`index.css`文件，作如下更改

```css
.carousel-card-item-card.is-active {
  width: 776px; /* 改变宽度 */
  z-index: 2;
  left: -90px; /* 适当更改left值 */
}
```

**水平有限，只能这样改了😭**

### 用法

```bash
# 安装依赖
yarn add vue-carousel-card
# or
npm i vue-carousel-card -S
```

> 引入依赖，SPA，非 SSR

```javascript
// 样式需要单独引入
import { CarouselCard, CarouselCardItem } from 'vue-carousel-card'
import 'vue-carousel-card/styles/index.css'

export default {
  // 注册组件
  components: { CarouselCard, CarouselCardItem }
}
```

> 引入依赖，服务端渲染（SSR）中使用，以 Nuxtjs 为例

```javascript
// @/plugins/vue-carousel-card.js
import Vue from 'vue'
import { CarouselCard, CarouselCardItem } from 'vue-carousel-card'
import 'vue-carousel-card/styles/index.css'

export default () => {
  Vue.component(CarouselCard.name, CarouselCard)
  Vue.component(CarouselCardItem.name, CarouselCardItem)
}

// nuxt.config.js
plugins: ['@/plugins/vue-carousel-card']
```

```html
<!-- 使用组件 -->
<CarouselCard :interval="7000" height="300px" type="card" arrow="always">
  <CarouselCardItem v-for="i in 6" :key="i">
    <h1 v-text="i"></h1>
  </CarouselCardItem>
</CarouselCard>
```

```css
/* 示例样式 */
h1 {
  height: 100%;
  padding: 0;
  margin: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
  background: linear-gradient(
    90deg,
    rgba(88, 140, 236, 1),
    rgba(106, 106, 207, 1)
  );
}
```

### 参数

##### Carousel Attributes

| 参数               | 说明                                  | 类型    | 可选值             | 默认值 |
| :----------------- | :------------------------------------ | :------ | :----------------- | :----- |
| height             | 走马灯的高度                          | string  | —                  | —      |
| initial-index      | 初始状态激活的幻灯片的索引，从 0 开始 | number  | —                  | 0      |
| trigger            | 指示器的触发方式                      | string  | click              | —      |
| autoplay           | 是否自动切换                          | boolean | —                  | true   |
| interval           | 自动切换的时间间隔，单位为毫秒        | number  | —                  | 3000   |
| indicator-position | 指示器的位置                          | string  | outside/none       | —      |
| arrow              | 切换箭头的显示时机                    | string  | always/hover/never | hover  |
| type               | 走马灯的类型                          | string  | card               | —      |
| loop               | 是否循环显示                          | boolean | -                  | true   |

##### Carousel Events

| 事件名称 | 说明             | 回调参数                               |
| :------- | :--------------- | :------------------------------------- |
| change   | 幻灯片切换时触发 | 目前激活的幻灯片的索引，原幻灯片的索引 |

##### Carousel Methods

| 方法名        | 说明               | 参数                                                                        |
| :------------ | :----------------- | :-------------------------------------------------------------------------- |
| setActiveItem | 手动切换幻灯片     | 需要切换的幻灯片的索引，从 0 开始；或相应 carousel-card-item 的 name 属性值 |
| prev          | 切换至上一张幻灯片 | —                                                                           |
| next          | 切换至下一张幻灯片 | —                                                                           |

##### Carousel-Item Attributes

| 参数  | 说明                                      | 类型   | 可选值 | 默认值 |
| :---- | :---------------------------------------- | :----- | :----- | :----- |
| name  | 幻灯片的名字，可用作 setActiveItem 的参数 | string | —      | —      |
| label | 该幻灯片所对应指示器的文本                | string | —      | —      |
