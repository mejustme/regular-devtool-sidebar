# regular-devtool-sidebar

## 先上效果图
![enter image description here](./assets/sidebar.gif)

## 介绍
> 通过控制台选择元素，实时在sidebar中展现这个元素所在的组件对象(展示加入中文说明，不改动真实$component实例)。
> 通过这个对象，我们可以方便查看该组件实例的所有属性情况。
> 全局环境实时更新$component指向该组件，可手动执行其中的函数。
> sidebar中的属性支持修改，通过调用$component.$update()刷新视图。


## 你该如何用
1. 在regular源码Regular函数中加入,下面3行代码。放心，对Regular毫无影响，且未装插件的用户更是毫无影响。

```
    this.$emit("$init");
    if( this.init ) this.init(this.data);
    env.isRunning = prevRunning;

  // check if regular-devtools-sidebar-exist
  // 加入下面3行代码
    if(window.__REGULAR_DEVTOOLS_SIDEBAR_GLOBAL_HOOK__ && this.group && this.group.children &&  this.group.children[0].node){
        var element = this.group.children[0].node();
        element.__regularUI = this;
    }
```
2. fork 工程 -> 拉到本地 -> chrome://extensions/ -> 加载已解压的扩展程序

## 优点
- regular 源码最小改动
- 支持所有组件的查看：内嵌组件、isolate组件、inject组件
- 属性配置中文说明

## tips
当修改视图中的数据，需要通过切换sidebar来刷新其中的视图，展现最新的属性。（切换$0元素也行）



## 下一步
- 增加一个panel, 展现各组件脏检查数量，以及脏检查时间与性能瓶颈
- 增加一个panel，可视化展现组件继承关系
- 增加一个panel, 可视化列表工程中的命令，点击直接执行，如: npm run pscom /npm run cssall....


## 最后
如果你觉得还想尝试新的 可以用用官方的[Regular-devtools](https://github.com/regularjs/regular-devtools)。

它的问题是：
- isolate 组件不能展现 `严重`
- 不能直接定位到嵌套组件，需要手动层层查找
- 目前只支持data数据展示 且 data属性不支持修改

优点：
- 视图更新后，数据展示自动更新 (本插件，要手动切换下sidebar)
- 官方v0.4.5后直接支持，目前还未发布（对源码改动较大）


## more
本插件及想法已@赵鑫晖(regular-devtools作者)有交流，感谢对chrome插件开发的指导，如其不能有效解决isolate问题，将可能采用本插件sidebar方式。
目前两插件都处于dev状态，欢迎大家有什么想法，加入我们。