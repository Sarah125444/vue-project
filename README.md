# 这是一个好玩的项目
## 用心去感受每一行代码的有趣
### 我们是有灵魂的程序员 所以 我们的代码富有诗意

## 制作首页App组件
### 完成Header区域，使用的是Mint-UI中的Header组件
- 1.完成Header区域，使用的是Mint-U的header组件
- 2.制作底部的Tabber区域，使用的是MUI的Tabber.html
  + 在设置下面的小图标的时候，操作会相对多一下
  + 打开`git clone`下面的的文件夹，找到`examples` => `hello-mui` => `examples` => `icon-extra.html`
  + 找这个文件后，打开，看看是否有自己需要的图标，然后查看源代码，把源代码里面的class里面的东西拷贝到之前的标签里面
  + 上一步做完之后，重启会发现显示不出来，是因为没有加载对应的文件。
  + 因为是额外的图标，所以需要额外的css文件，找到`examples` => `hello-mui` => `css` => `icons-extra.css`，将这个css文件放到`src` => `lib` => `mui` => `css` 
  + 又因为图标格式是`ttf`格式的，所以需要另外的文件解析,找到`examples` => `hello-mui` => `fonts` => `mui.ttf`,将这个文件拷贝到`src` => `lib` => `mui` => `fonts` 下面，再重试一下，就会解析成功了
- 3.要在中间放置一个router-view来展示路由匹配到的组件



## 改造tabbar为router-link
## 设置路由高亮
## 点击tabbar中的路由链接，展示对应的路由组件
## 制作首页轮播图布局
## 加载首页轮播图数据
  + 1.获取数据，如何获取呢，使用vue-resource
  + 2.使用vue-resource的this.$http.get获取数据
  + 3.获取到的数据，要保存到data身上
  + 4.使用v-for循环渲染每个item项

## 改造九宫格的样式