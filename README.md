制作首页App组件



## 完成Header区域，使用的是Mint-UI中的Header组件



- 1.完成Header区域，使用的是Mint-U的header组件

- 2.制作底部的Tabber区域，使用的是MUI的Tabber.html

  - 在设置下面的小图标的时候，操作会相对多一下

  - 打开`git clone`下面的的文件夹，找到`examples` => `hello-mui` => `examples` => `icon-extra.html`

  - 找这个文件后，打开，看看是否有自己需要的图标，然后查看源代码，把源代码里面的class里面的东西拷贝到    之前的标签里面

  - 上一步做完之后，重启会发现显示不出来，是因为没有加载对应的文件。

  - 因为是额外的图标，所以需要额外的css文件，找到`examples` => `hello-mui` => `css` => `icons-extra.css`，将这个css文件放到`src` => `lib` => `mui` => `css` 

  - 又因为图标格式是`ttf`格式的，所以需要另外的文件解析,找到`examples` => `hello-mui` => `fonts` => `mui.ttf`,将这个文件拷贝到`src` => `lib` => `mui` => `fonts` 下面，再重试一下，就会解析成功了

    

- 3.要在中间放置一个router-view来展示路由匹配到的组件



## 改造tabbar为router-link**



**## 设置路由高亮**



**## 点击tabbar中的路由链接，展示对应的路由组件**



**## 制作首页轮播图布局**



**## 加载首页轮播图数据**



  1.获取数据，如何获取呢，使用vue-resource

  2.使用vue-resource的this.$http.get获取数据

  3.获取到的数据，要保存到data身上

  4.使用v-for循环渲染每个item项



**## 改造九宫格的样式**



**## 改造新闻资讯路由连接**



**## 新闻资讯页面制作**



- 1.绘制页面，使用mui中的media-list.html
- 2.使用vue-resource获取数据
- 3.渲染真实数据



**## 实现 新闻资讯列表 点击跳转到新闻详情**



1.把列表中每一项改造为router-link，同时，在跳转的时候应该提供唯一的Id标识符

2.创建新闻详情的组件页面 NewsInfo.vue

3.在路由模块中，将新闻详情的路由地址和组件页面对应起来



**## 实现新闻详情的页面布局和数据渲染**



**### 在新闻详情的陀下面 -  单独封装一个comment.vue评论子组件**



1.先创建一个单独的comment.vue组件模板

2.在需要使用comment组件的页面中，先手动导入comment组件

   `import comment from './comment.vue`

3.在父组价中，使用`components`属性，将刚才导入的comment组件，注册为自己的子组件

4.将在注册子组件的时候的注册名称，以标签形式，在页面中引用即可



**### 获取所有的评论数据显示到页面中**



**### 实现点击加载更多评论的功能**



1.为加载更多按钮，绑定点击事件，在事件中，请求下一页数据，

2.点击加载更多，让pageIndex++，然后重新调用this.getComments()方法重新获取最新一页的数据

3.为了防止新数据覆盖老数据的情况，我们在点击加载更多的时候，每当获取到新数据，应该让老数据调用新数组的concat方法，拼接上新数组



**### 发表评论的方法**



1.把文本框做双向数据绑定

2.为发表按钮绑定一个事件

3.校验评论内容是否为空，如果为空则提示用户评论内容不能为空

4.通过vue-resource发送一个请求，把评论内容提交给服务器

5.当发表评论完成之后，重新刷新列表，查看最新的评论

6.如果调用getComments方法重新刷新评论列表的话，可能只能得到最后一页的评论，前几页的评论获取不到,换一种思路：当评论成功后，在客户端，手动拼接出一个最新的评论对象，然后，调用数组的unshift方法，把最新的评论添加到data中的comments的开头中，这样，就能完美实现刷新评论到列表的需求



## 实现点击图片分享跳转到相对应的路由链接并显示对应的组件页面



1.先找到主页面的文件`HomeContainer.vue`,找到`图片分享`的a标签，将a标签改为`router-link`标签，将a标签的href属性改为`to="./home/photolist"`,这一步就设置好了路由跳转的路径

2.在`components`文件夹里面新建一个文件夹`photos`,在这个新建的文件夹里面创建一个`PhotoList.vue`文件，然后在这个文件里面写下如下的模板结构:

```javascript
   <template lang="">
        <div>
​          <h3>图片列表</h3>
​        </div>
​      </template>
      <script>
​      export default {}
​      </script>
      <style lang="stylus" scoped>
​      </style>
```

3.上面两步之后，路由改造好了，组件模板结构也写好了，这一步就是将这个两个联系起来。找到`router.js`，导入对应的路由组件`import PhotoList from './components/photos/PhotoList.vue`, 在配置路由规则`routes`的数组里面配置路由规则`{ path: '/home/photolist' , component: PhotoList}`,然后就可以实现点击`图片分享`按钮，跳转到’/home/photolist‘的功能了！

```javascript
  mui('.mui-scroll-wrapper').scroll({
​        deceleration: 0.0005 //flick 减速系数，系数越大，滚动速度越慢，滚动距离越小，默认值0.0006
​ });
```

2.1 在`PhotoList.vue`中导出一个对象：

```javascript
        // 配置实现mui中的slider功能 => 1.导入mui中的js文件
​        import mui from "../../lib/mui/js/mui.js"
​        // 配置实现mui中的slider功能 => 2.初始化滑动控价
​        mui(".mui-scroll-wrapper").scroll({
​          deceleration: 0.0005 //flick 减速系数，系数越大，滚动速度越慢，滚动距离越小，默认值0.0006
​        });
​        export default {
​          data() {
​            return {};
​          },
​          methods: {}
​        };
```

2.2 在配置完上面的代码之后出现了以下的报错：

```
​```javascript
  log.js:24 [HMR] Waiting for update signal from WDS...
```

​      mui.js:3964 Uncaught TypeError: 'caller', 'callee', and 'arguments' properties may not be accessed on strict mode functions or the arguments objects for calls to them
​          at Function.Class.extend (mui.js:3964)
​          at eval (mui.js:4197)
​          at eval (mui.js:5206)
​          at Module../src/lib/mui/js/mui.js (bundle.js:3783)
​          at **__webpack_require__** (bundle.js:727)
​          at fn (bundle.js:101)
​          at eval (PhotoList.vue?./node_modules/babel-loader/lib!./node_modules/vue-loader/lib??vue-loader-options:2)
​          at Module../node_modules/babel-loader/lib/index.js!./node_modules/vue-loader/lib/index.js?!./src/components/photos/PhotoList.vue?vue&type=script&lang=js& (bundle.js:865)
​          at **__webpack_require__** (bundle.js:727)
​          at fn (bundle.js:101)
​    ```

出现这个报错的原因是因为`mui.js`这个文件中用到了`caller`,`callee`,`arguments`这几个东西，但是`webpack`打包好的`bundle.js`中，默认是启动严格模式的，所以，这两者冲突了。

解决方案是：

1.把miu.js中的非严格模式的代码改掉，但是不现实

2.把webpack中打包时候的严格模式禁用

   2.1 因为vue项目用的是最新的babel7版本,在.babel.config.js中使用的还是之前的插件.babel7之后的插件一般都       是以@babel开头的,下载新版的babel安装包之后再运行就可以了

 安装改为

```js
 npm i @babel/plugin-transform-modules-commonjs @babel/plugin-transform-strict-mode -D
```

​    2.2 在babel.config.js中进行配置

```
 ```js
    plugins: [
​          ["@babel/plugin-transform-modules-commonjs", { "strictMode": false }]
​      ]
```

 在处理完严格模式之后，又报错：`Uncaught ReferenceError: _Header is not defined`,解决方法是：

```js
import {Header,Swipe, SwipeItem,Button} from ‘mint-ui’
​      Vue.component(Header.name,Header)
​      Vue.component(Swipe.name, Swipe)
​      Vue.component(SwipeItem.name, SwipeItem)
​      Vue.component(Button.name, Button)
```

以上方式使用mint-ui这个框架的方式改为全局引用就可以解决这个问题了。

```js
    import mint from ‘mint-ui’
​    Vue.use(mint)
```

处理完上面的错误后会发现导航栏的那个条只能刷新之后才能动，原因是因为没有刷新的时候其实DOM还没有渲染完，所以必须加一个生命周期函数,将之前配置的初始化滑动控价放在这个生命周期组件里面，再次重新启动就能在最开始滑动了：

```js
export default {
  data() {
    return {};
  },
  mounted() {  
    // 当组件中的DOM结构已经被渲染好，并放到页面中后，会执行这个钩子函数
    // 如果要操作元素，最好在mounted里面，因为这个时的DOM元素是最新的
    // 配置实现mui中的slider功能 => 2.初始化滑动控价
    mui(".mui-scroll-wrapper").scroll({
      deceleration: 0.0005 //flick 减速系数，系数越大，滚动速度越慢，滚动距离越小，默认值0.0006
    });
  },
  methods: {}
};
```

当滑动条调试成功后，发现 tabbar 无法正常工作了，这个时候需要把` <router-link class="mui-tab-item-llb" to="/home">`中的class改个名字`mui-tab-item-llb`,然后将涉及到的css样式代码都加入到style标签中：

```js
.mui-bar-tab .mui-tab-item-llb.mui-active {
    color: #007aff;
}

.mui-bar-tab .mui-tab-item-llb {
    display: table-cell;
    overflow: hidden;
    width: 1%;
    height: 50px;
    text-align: center;
    vertical-align: middle;
    white-space: nowrap;
    text-overflow: ellipsis;
    color: #929292;
}

.mui-bar-tab .mui-tab-item-llb .mui-icon {
    top: 3px;
    width: 24px;
    height: 24px;
    padding-top: 0;
    padding-bottom: 0;
}

.mui-bar-tab .mui-tab-item-llb .mui-icon~.mui-tab-label{
  font-size: 11px;
  display: block;
  overflow: hidden;
  text-overflow: ellipsis;
}

```

### 图片分享区域的数据渲染

1.在`PhotoList.vue`中通过`methods`定义获取图片分类的方法：

```js
methods: {
  getAllCategory (){
    //获取图片的分类
    this.$http.get("api/getimgcategory").then(result => {
      if(result.body.status === 0){
        # 手动拼接一个最完整的分类数据
        result.body.message.unshift({ title: "全部"， id: 0})
      }else {
        Toast('获取图片失败')
      }
    })
  }
}
```

2.然后在生命周期函数`created`中调用这个方法：

```js
  created(){
    this.getAllCategory();
  },
```

3.通过v-for循环每个li标签，获取数组中的数据：

```js
# 这里需要注意的是需要按照id来指定样式 属性选择器，第一个是每个li标签都需要的样式，第二个是通过三元表达式来适当选择选择器
<a :class="['mui-control-item',item.id == 0 ? 'mui-active' : '']"  v-for="item in cates" :key="item.id">
		{{ item.title }}
</a>
```

### 制作图片列表区域

1.图片列表需要使用懒加载技术，我们可以使用Mint-UI提供的组件`lazy-load`

2.根据`lazy-load`使用文档，尝试使用

```js
# 第一步 ： 本来是按需加载的，但是由于之前报错，变成引入全部的组件，所以这里就不需要搞按需加载了
# 第二步 ； 在顶部滑动条区域外，加入下面的ul代码
      <ul>
        <li v-for="item in list">
          <img v-lazy="item">
        </li>
      </ul>
# 第三步 ： 在style中加入下面的样式 => 但是这里加上这个懒加载之后报错了，所以我注释掉了
      image[lazy=loading] {
        width: 40px;
        height: 300px;
        margin: auto;
      }
```

3.渲染图片列表数据

```js
# 1.现在data中加入图片列表的数组
data(){
  return {
      cates: [] , 
      list: []  //图片列表的数组 => 这个是数据库提供的数组
  } 
}

# 2.为a标签注册一个点击事件
<a :class="['mui-control-item',item.id == 0 ? 'mui-active' : '']"  v-for="item in cates" :key="item.id" @click="getPhotoListByCateId(item.id)">
	{{ item.title }}
</a>

# 3.将点击事件写入方法中，通过这个方法拿到数据
getPhotoListByCateId(cateId){
      //根据分类Id获取图片列表
      this.$http.get("api/getimages/" + cateId).then(result => {
        if(result.body.status === 0){
          this.list = result.body.message;
        }
   })
}

# 4.这里需要注意的是，我们一进入页面中，图片就需要马上渲染出来，然后点击其他选项的时候，其他选项的再渲染，所以这里这个方法需要被调用两次，一次是在刚创建的时候,一次是在点击的时候
  created() {
    this.getAllCategory();
    // 默认进入页面，就主动请求所有图片列表的数据
    this.getPhotoListByCateId(0);
  },
```

### 处理图片上的文字

1.在图片下面加上一个显示文字的div 然后把标题和摘要都放进对应的标签里面

```js
# 在图片下面加上一个显示文字的div 然后把标题和摘要都放进对应的标签里面
<div class="info">
          <h1 class="info-title">{{ item.title }}</h1>
          <div class="info-body">{{ item.zhaiyao }}</div>
</div>
```

2.给这个文字的div添加各种样式

```scss
.photo-list {
  list-style: none;
  padding: 0;
  margin: 10px;
  padding-bottom: 10px;
  li {
    background-color: #ccc;
    text-align: center;
    margin-bottom: 5px;
    box-shadow: 0 0 9px #999;
    position: relative;
    img {
      width: 100%;
      vertical-align: middle;
    }
    img[lazy="loading"] {
      width: 40px;
      height: 300px;
      margin: auto;
    }
    .info{
      color: white;
      text-align: left;
      position: absolute;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.3);
      max-height: 84px;
      .info-title{
        font-size: 14px;
      }
      .info-body{
        font-size: 13px;
      }
    }
  }
```

3.处理完之后这步就完成了

### 点击图片显示图片详情页

1.将显示图片的li标签改为`router-link`，并指定要去往的路由`/home/photoinfo/`

```html
# 这里需要注意的是本来是使用to属性，但是由于to里面涉及到了字符串拼接 已经变成JS表达式了 所以要在前面加个：
<router-link class="li" v-for="item in list" :key="item.id" :to="'/home/photoinfo/' + item.id">
```

2.将li标签改为router-link之后，原本的li标签的样式就失效了，需要在router-link里面添加一个属性`tag="li"`，指定渲染为li元素

3.photos文件夹下创建一个文件`PhotoInfo.vue`,然后在里面建立基本的模板

```vue
<template >
  <div>
    <h3>图片详情</h3>
  </div>
</template>
<script>
export default {
}
</script>
<style lang="scss" scoped>
</style>
```

4.之前的router-link指向的文件已经建立好了，现在就是将路由关系建立起来。打开`router.js`，先导入对应的路由组件，然后创建路由对象。

```js
# 先导入对应的路由组件
import PhotoInfo from './components/photos/Photoinfo.vue'
# 然胡创建路由对象
{ path: '/home/photoinfo/:id', component: PhotoInfo }
```

### 实现详情页的布局和美化，同时获取数据渲染页面

1.先将详情页上面部分的页面先画出来

```js
<div class="photoinfo-container">
    <h3>{{ photoinfo.title }}</h3>
    <p class="subtitle">
      <span>发表时间：{{ photoinfo.add_time | dateFormat }}</span>
      <span>点击：{{ photoinfo.click }}次</span>
    </p>
    <hr>
</div>

<style lang="scss" scoped>
    .photoinfo-container{
        padding: 3px;
        h3{
          color: #26A2FF;
          font-size: 15px;
          text-align: center;
          margin: 15px 0;
        }
        .subtitle{
          display: flex;
          justify-content: space-between;
          font-size: 13px;
        }
        .content{
          font-size: 13px;
          line-height: 30px;
        }
    }
</style>
```

2.发表评论部分是和之前的评论组件是一样的，所以直接引用过来就行

```js
# 第一步：在PhotoInfo.vue文件的script标签中引入评论子组件
import comment from '../subcomponents/comment.vue'

# 第二步：在export default中注册components子组件
components: { //2.注册评论子组件
    'cmt-box': comment
  }

# 第三步：在页面中以标签形式引入将子组件放到要template中要显示的区域
<!-- 3.在页面中以标签形式引入 -->
<cmt-box :id="id"></cmt-box>
```

3.设置图片区域 

```js
# 第一步： 在template中设置一个放置图片的区域
<div class="content" v-html="photoinfo.content"></div>

# 第二步： 因为要在路由中获取id，所以索性直接将其放入data中，还有将图片数据也放入data中
data(){
    return {
      id: this.$route.params.id,   //从路由中获取到的图片id
      photoinfo: {}, //图片详情 
    };
  },
    
# 第三步：从数据库中将数据拿出来
getPhotoInfo(){
      //获取图片的详情数据
      this.$http.get("api/getimageInfo/" + this.id).then(result => {
        if(result.body.status === 0){
          this.photoinfo = result.body.message[0]
        }
      })
    },
      
#第四步：将方法在生命周期created中调用
created(){
    this.getPhotoInfo();
  },
```

4.设置缩略图样式

```js
# 第一步：先安装一个插件：vue-preview 
npm install vue-preview -s

# 第二步：按照github上提示，在main.js中导入vue-preview，并挂载到Vue身上
import VuePreview from 'vue-preview'
Vue.use(VuePreview)

# 第三步：根据说明，在template中的缩略图区域，放入缩略图的div标签
 <!-- 缩略图区域 -->
<div class="thumbs">
        <vue-preview :slides="list" @close="handleClose"></vue-preview>
</div>

# 第四步：根据说明，在methods中加入以下的方法：
 getThumbs(){
      //获取缩略图
      this.$http.get('api/getthumimages/' + this.id).then(result => {
        if(result.body.status === 0){
          // 循环每个图片数据，补全图片的宽和高
          result.body.message.forEach(item => {
            item.w = 600;
            item.h = 400;
            item.msrc = item.src;
          });
          this.list = result.body.message;
        }
      })
    },
handleClose(){
      console.log('close event')
    },
      
# 第五步：将list数据放入data中
data(){
    return {
      id: this.$route.params.id,   //从路由中获取到的图片id
      photoinfo: {}, //图片详情
      list: []  //缩略图数组
    };
  },

# 第六步：将getThumbs方法写入生命周期函数中：
  created(){
    this.getPhotoInfo();
    this.getThumbs();
  },
    
# 第七步：将以下样式写入style标签中
  .thumbs{
    /deep/ .my-gallery{
      display: flex;
      flex-wrap: wrap;
      figure{
        width: 30%;
        margin: 5px;
        img{
          width: 100%;
          box-shadow: 0 0 8px #999;
          border-radius: 5px;
        }
      }
    }
  }
```

## 绘制商品列表-页面结构基本美化

- 还是和之前创建其他路由的步骤一样：

  - 先将商品列表的a标签变成router-link标签，将href属性改成to属性，to属性指向要跳转的路由,记得加`tag="div"`,不然样式会发生变化
  - 创建一个文件添加基本的结构
  - 将上面两个步骤联系起来，在router.js中，先导入新创建的组件，然后将路径添加到routes中，这样子点击商品列表就能实现路由跳转

- 然后开始在页面中写结构和css，写完之后，将数据从数据库中取出，导入到页面结构中，完成这个功能

  



