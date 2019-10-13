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

  

### 点击商品跳转到商品详情页

- 这里使用了一种叫 **编程式导航**的方法

  - 按照常规操作是使用`router-link`创建a标签来定义导航链接，其实我们可以借助router的实例方法，通过编写代码来实现

  - 上面这句话的意思是原先本来将div标签变成router-link标签，但是现在不改变div标签了。

  - 第一步：先给要跳转的div注册一个点击事件，在点击事件里面`console.log(this)`，会输出下面的代码：

    ```js
    VueComponent {_uid: 17, _isVue: true, $options: {…}, _renderProxy: Proxy, _self: VueComponent, …}
    
    # 点击开上面这个输出的this，其实就是vue的实例
    # 会发现下面两个属性：
    
    #我们需要的是这两个属性
    
    $route: Object  # 我们经常使用 this.$route 获取URL地址中传递的参数 所以这个简称为路由参数对象
    # 所有路由中的参数 包括params  query 都属于它
    
    $router: VueRouter #this.$router 是一个路由导航对象，用它可以方便的使用JS代码，实现路由的前进，后退，跳转到新的URL地址
    
    ```

  - 根据文档中写的使用方法是：

    ```js
    router.push(loacation , onComplete? , onAbort)
    ```

  - 之前用的router-link的方法的时候，其实内部调用的就是router.push方法。

  - `router.push`会向history栈添加一个新的记录，所以，当用户点击浏览器后退按钮时，会回到之前的URL

  - 这个方法的参数可以是一个字符串路径或者一个描述地址的对象

    ```js
        # 第一种是最简单的输入字符串
       this.$router.push('/home/goodsinfo/' + id)
    
        #  第二种是传递对象
        this.$router.push({ path:  "/home/goodsinfo/" + id })
    
        # 第三种是传递命名的路由 => 这里需要在router.js中给  path 的属性中增加一个name
        { path: '/home/goodsinfo/:id', component: GoodsInfo , name: 'goodsinfo' }
        this.$router.push({name: "goodsinfo" , params: {id}})
    ```

    

    

    

### 商品详情页的结构

- 分析可以知道，商品详情页由三部分组成，这个结构可以在mui里面找到，将这个结构复制到商品详情页的结构里面就可以了

- 商品详情页中的轮播图组件和首页的轮播图组件是相同的，但是由于之前我们是直接将轮播图组件写入到了首页中，所以我们要想共享这个轮播图组件，必须将轮播图这个组件给抽离出来，这里就涉及到了**如何抽离公共组件**：

  ```js
  # 在公共组件文件夹里面，建立一个放轮播图的组件的文件，然后将轮播图相关的结构和css样式放入到那个文件中
  # 然后再回到之前需要轮播图的文件，将轮播图导入进入
    # 导入第一步：
    import import swiper from '../subcomponents/swiper.vue'
    # 导入第二步：在methods下面新增一个components对象
    components: { //使用轮播图组件第二步：在这里建立一个components
      swiper
    }
    # 导入第三步： 在应该放置轮播图的地方放入上面的标签 并将轮播图的数据传递过去
    <swiper :lunbotuList="lunbotuList"></swiper>
  ```

- 封装好公共组件部分之后，发现还是出现了问题，轮播图的宽度在每个轮播图中的要求是不一样的，这也就引出了另外一个问题：**抽离公共组件后出现了分歧如何解决**。

  ```js
  # 抽离公共组件之后，出现了公共组件中有些东西需要自适应的问题，我们首先应该去分析出现问题的地方是哪里，哪个地方需要被再次抽离出来，设置出自适应的方法，需要的地方导入，不需要的地方就不导入
  
  # 在这个问题中，发现是宽度的问题，首页的宽度需要100%，详情页的宽度不需要100%.所以可以单独在样式中定义一个类，谁需要谁就去把这个类导入进入
  
  # 第一步: 将公共组件里面设置img的样式的地方的宽度先删除
  img {
        // width: 100%;   //因为首页和详情页的图片大小不一致，详情页中的图片的宽度被拉大了，所以这里使用这个不行
        height: 100%;
      }
  
  # 第二步: 在公共样式中，设置一个新的类，将宽度100%放入这个类中
  .full {       //使用class定义一个类，再使用对象结合布尔值的形式，将宽度100%灵活绑定给需要的和不需要的组件
    width: 100%;
  }
  
  # 第三步：在props中放入isfull这个属性
   props: ["lunbotuList" , "isfull"] 
  
  
  # 第四步: 在公共组件的轮播图结构中找到img标签，通过class的方式，将设置的类放进来
   <img :src="item.img" alt=“” :class="{'full' :isfull }" />
     
     
  # 第五步：因为首页的图片需要100%的宽度，所以将属性isfull的布尔值设置为true，就代表这个img的宽度100%被采用了
   <swiper :lunbotuList="lunbotuList" :isfull="true"></swiper>
  ```

## Vuex

- vuex是vue配套的公共数据管理工具，它可以把一些共享的数据，保存到vuex中，方便整个程序中的任何组件直接获取或者修改我们的公共数据

- 举个例子：

  ```
  有A B C三个组件，然后B组件里面有个D的子组件，如果B组件有个info属性，D组价想要使用，B怎么样才能将这个传递给D？=>答案是通过属性绑定的形式，父组件向子组件传值
  那么反过来，D组件怎么传值给B组件，也就是子组件怎么传值给父组件，往外传，也就是通过事件调用的形式，
  如果B组件外面还有个E组件，那么D子子组件的msg怎么传递给E组件，可以直接丢过去吗？
  必须先在E里面定义一个函数，这个函数传递给组价B，B组件再传给组件D，D组件通过$emit()触发当前实例上的事件，但是这个函数是不属于B的，是属于E的，那么B不需要这个东西，但是却要做这个第三帮助传递数据，很尴尬
  能不能是E组件想过使用D组件里面的数据 ，可以直接去某个地方去取，而不是必须要通过B这个中间价来传递这个数据
  
  也就是说D可以把自己的数据共享出去，放到一个公共的地方，D不知道谁会去使用这个数据，谁想用，谁就去这个地方拿，这样就不需要层层传递了
  
  ```

- Vuex是为了**保存组件之间共享数据**而诞生的，如果组件之间有要共享的数据，可以直接挂载到vuex中，而不必通过父子组件之间传值，如果组件的数据不需要共享，此时，这些不需要共享的私有数据，没有必要放到Vuex中

- 需要注意的是：**只有共享的数据，才有权利放到vuex中**，组件内部私有的数据，只要放到组件的data中即可。

- props 和 data 和vuex的区别是：

  ```js
  # 根据刚才的描述，我们可以得出一个结论：
  # Vuex是一个全局的共享数据存储区域，就相当于是一个数据仓库
  ```

  ```js
  # props可以是数组或者对象，用来接收来自父组件的数据
  # 父组件可以通过props把数据传给子组件，但是这个props是写在子组件里面的，用来接收父组件传给子组件的数据
  ```

  ```js
  # data是Vue实例的数据对象。
  # Vue会将data的属性转为getter和setter，也就是Object.defineProperty方法，
  # 这个对象必须是纯粹的对象，这里面的数据都是被监控的，所以说这里面最好放的是视图层的数据，如果说不是视图层的数据，可以放在外面或者VM对象上。如果视图里面不用显示的话就没必要写在data里面，这样可以减少开销，提高性能
  ```

  ### vuex的使用方法

  ``` js 
  # 第一步：在项目中安装vuex
  npm install vuex -s
  
  #第二步：在main.js中导入vuex文件
  import Vuex from 'vuex'
  
  #第三步：在导入文件后，注册vuex到vue中
  Vue.use(Vuex)
  
  #第四步：创建一个vuex的公共仓库
  const store = new Vuex.store({
    state: { #这个state是用来放置公共数据的，和组件中的data的功能一样
            # 需要注意的是 
            如果想要在其他组件中访问这个里面的数据，必须使用 this.$store.state.xxx来访问
            
    }
    mutations: { # 这个是仓库的管理员，
    			# 其他组件想要对仓库的数据进行增删改查的工作，必须通过这个仓管员来操作，而不是组件本身自己
   # 如果这里面定义了方法，其他组件想要使用这个方法，必须通过 this.$store.commit('父组件中的方法名')
    
    
   # 在mutations中定义的方法的参数只有两个：
   # 第一个是state 状态 
   # 第二个是 通过commit提交过来的参数
  })
  
  # 第五步是将  store 注册到 vm实例 身上
  const vm = new Vue({
    el: '#app',
    render: c => c(App),
    store  //5.将vuex创建的store 挂载到Vm实例上，只要挂载到了vm上， 任何组件都能够使用store来存取数据
  })
  ```

  ### vuex中的mutations中的getters方法

  ```js
  getters: {
      //注意; 这里的getters，只负责 对外提供数据，不负责修改数据，如果想要修改state中的数据，请去找 mutations
      optCount: function(state){
        return '当前最新的count值是：' + state.count
      }
      // 经过我们回顾对比，发现getter中的方法， 和组件中的过滤器比较类似，因为过滤器和getters 都没有修改原数据，都是把原数据做了一层包装， 提供给了调用者
      // 其次，getters也和computed比较像， 只要state中的数据发生了变化，那么，如果getters也正好引用了这个数据，那么就会立刻触发getters的重新求值
    }
  ```

  



