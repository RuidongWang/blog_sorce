# 第一份博客 The first and not the last
## 踩了很多坑终于把我的博客搭建成功了。
一直以来都在想搭建我的博客，上周五才开始实施，周末lay了，今天踩了无数的坑，终于搭建成功了。

# 搭建步骤
我使用的是 Github + Hexo，以后可能会换个，毕竟使用这个组合仍有一些问题。

## Hexo 部分
安装 Hexo
```shell
npm install hexo-cli -g #全局安装 Hexo
hexo init #初始化网站 在所在文件夹下使用直接初始化本文件夹
npm install #使用 npm 安装所需的依赖
hexo g #生成或 hexo generate 这个指令是用于 build 网站，代码更新后需要使用
hexo s #启动本地服务器 或者 hexo server,这一步之后就可以通过http://localhost:4000 查看
```

