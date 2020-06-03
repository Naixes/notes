## vue

### keep-alive

#### 自定义是否使用缓存页面

> 问题：
>
> 从详情返回列表页时保留状态，但是从编辑页面或者在详情中修改了数据，返回后的数据就是旧的数据

- 解决方案：

  keepAlive是表示需不需要缓存和needKeep的含义不一样

  在路由meta中增加一个needKeep的标识用来标识需不需要使用缓存的页面，在列表页的beforeRouteEnter和activated判断该标识来决定需不需要重新获取数据，该值在列表页可以直接跳转的并且会对列表数据进行修改的详情页或者编辑页的beforeRouteLeave中设置

