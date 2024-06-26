---
title: 安装插件提高开发体验
---
经过第一章节 [《快速开始》](/easy-query-doc/startup/quick-start) 的快速开始体验,我相信你应该已经把项目跑起来了。

那么你是否对这种开发感觉有点麻烦,毕竟需要先`build-project`,然后还需要刷新`Maven`然后还要添加接口,那么是否有办法可以简化这些操作呢,答案是有的就是这一章节的插件


::: warning 说明!!!
> 如果您非旗舰版idea可能无法使用当前插件您可以进群联系作者,我会给您编译一个社区版本支持的插件
:::

## 安装插件
插件的安装可以帮助我们针对自动生成的文件进行快速管理无感.
<img src="/plugin-search.png">

## 快速生成接口

<img src="/startup5.png">


::: warning 说明!!!
> 如果EasyQueryImplement没有效果请检查类是否添加了`@EntityProxy`或者`@EntityFileProxy`
:::

<img src="/startup6.png">

::: tip 说明!!!
> 插件的功能并非这些我们将会在后续的章节对插件的使用进行详细介绍目前您只需要知道这两点就可以解决掉上述的apt缺点和您的疑虑
:::