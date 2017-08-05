# sell

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

## 路由配置
采用脚手架的模式即可
## router.go('/goods');会不停刷新页面的问题
使用`router.push('/goods');`即可
## 在index.js中加入`  linkActiveClass: 'active',`可改变链接默认class值
## :after伪类选择元素之后
## 处理不同手机屏幕显示的缩放
位于common/stylus/base.styl
## vue-resource的使用
```javascript
created() {
  this.$http.get('/api/seller').then((response) => {
    response = response.body;
    if (response.errno === ERR_OK) {// 通过变量命名来实现
      this.seller=response.data;
      console.log(this.seller);
    }
  });
},
```
bulletin-wrapper 公告-包装
## 模板间传值
```javascript
// 引用模板
  <v-header :seller="seller"></v-header>

// 模板中
  export default {
    props:{
      seller:{
        type:Object
      }
    }
  };

<img  width="64" height="64" :src="seller.avatar" >// 头像要预编译
```

## 使用v-if来解决数据初始为空的问题
```HTML
<div v-if="seller.supports" class="support">
  <span class="icon"></span>
  <span class="text">{{seller.supports[0].description}}</span>
</div>
```

## 处理空白字符占位问题
```
.content-wrapper
  padding:24px 12px 18px 24px;
  font-size: 0;// 设置父元素字符大小为0；
  .avatar
    display: inline-block;
  .content
    display: inline-block;
    font-size: 14px;// 再设置子元素字符大小即可
```

## span本身不占内容空间使用`display:inline-block`指定内容空间

## style中引用styl文件是不可以用简写的
```HTML
<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl";
</style>
```

## 顶部对齐`vertical-align: top;`

## 媒体查询配合stylus
```
  @media(-webkit-min-device-pixel-ratio:3),(min-device-pixel-ratio:3)
  background-image: url($url+"@3x.png")
```
## 另外一种去<span>除空白间隙的方法是直接不回车换行

## 使用`filter: blur(10px);`对img包裹图片模糊处理

## Sticky footers问题
```
.clearfix
  display: inline-block;
  &:after
    display: block;
    content: ".";
    height: 0;
    line-height: 0;
    clear:both;
    visibility: hidden;
```

## 使用`let score = Math.floor(this.score*2)/2;`向下取整

## 星星组件存在bug

## flex布局
[阮一峰的网络日志](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html?utm_source=tuicool)

- 当样式不生效时候，不要慌张首先查看样式是否符对应到了正确的class
- vue中实现动画的确套路
使用transition属性
- vue中for循环index使用发生了变化，[链接网址](http://www.cnblogs.com/mzzz/p/6382590.html)
之前可以这样:
```
<ul id="example">
    <li v-for="item in items">
        {{$index}}
        {{$key}}
    </li>
</ul>
```
现在是这样使用
```
<ul id="example">
    <li v-for="(item,index) in items">
        {{item}}
        {{index}}
    </li>
</ul>
```

- `display: table;`菜单文字垂直居中的小技巧
- better-scroll库的使用，**看看源码？**
- [使用Vue2.0构建高仿饿了么外卖平台](https://github.com/SimonZhangITer/VueDemo_Sell_Eleme)
- vue2.0使用`let foodList = this.$refs.foodsWrapper.querySelectorAll('.food-list-hook');`而vu1.0使用的是`let foodList = this.$els.foodsWrapper.getElementsByClassName('.food-list-hook');`
- 技巧使用`box-sizing: border-box;`减小计算传统盒模型的步骤
```
width: 56px;
height: 56px;
box-sizing: border-box;
```

- 数据绑定没有立即生效是因为vue对于对象本身没有的属性是不会跟踪的，可以使用`.set()`方法
```
import Vue from 'vue';// 先获得vue对象

if(!this.food.count) {
  Vue.set(this.food,'count',1);
  // 使用this.food.count=1;是不会数据绑定的
}
```
- 使用padding属性增加按钮的可点击区域
- v-ref使用问题
- vue事件问题
```javascript
// goods.vue
data() {
  return {
    goods: [],
    listHeight:[],
    scrollY:0,
    eventHub: new Vue()
  };
},

// cartcontrol.vue
this.$parent.eventHub.$emit('cart.add',event.target);
// shopcart.vue
this.$parent.eventHub.$on('cart.add',this.drop)

```

- vue2 动画先写内层元素，再写外层元素(小球动画处)
```javascript
//el.style.webkitTransform = `translate3d(0,${y}px,0)`
//el.style.transform = `translate3d(0,${y}px,0)`
let inner = el.querySelector('.inner-hook')
inner.style.webkitTransform = `translate3d(${x}px,0,0)`
inner.style.transform = `translate3d(${x}px,0,0)`
el.style.webkitTransform = `translate3d(0,${y}px,0)`
el.style.transform = `translate3d(0,${y}px,0)`
```
