---
title: 使用 Hexo 和 GitHub Page 搭建自己的博客
date: 2019-09-21 00:28:44
tags: tech
---

虽然网上类似的文章已经很多了，但是感觉自己在搭建的时候还是走了很多的弯路，也没有找到一篇详细的讲解文章，所以把自己搭建的过程整理一下，后续应该会更新完善这个现在还很简陋的博客。

## 工具的准备

我们假定你对 git 和 github 有基础的了解，如果不清楚 git 的基本操作，请先去对 git 有一部分了解后再阅读此文章。

我们搭建的过程主要借助 GitHub Page 和 Hexo，选取的主题是广受好评的 NeXT (这个名字感觉在致敬乔布斯啊)，当然你也可以选择你自己喜欢的主题。

在 github 上新建一个  ${your.github.usrname}.github.io 的仓库，GitHub 就会自动的在 

  ${your.github.usrname}.github.io 的地址展示你仓库里的内容。

> 当然你也可以选择用自己的域名，或者干脆用自己的服务器，但是今天我们还是只关注最简单的部分，快速的搭建属于自己的博客。

新建 repo 之后我们就可以开始准备，这个时候我们新建一个 branch，取名为 source，用来存放源码，并在设置里更改新建的 branch 为 default branch.

之所以要这么做，是因为 hexo 部署的时候会上传生成的网页资源，覆盖掉原有的源代码和源文件，所以我们需要专门用一个分支存放我们的源代码和源文件。而 GitHub Page 只能展示 master 的内容。所以我们新建了一个 source branch 存放源码，并将其设为 default branch 来保证我们默认拉下来的是源码。

接下来我们需要准备的是本地的 hexo, hexo 需要本身已经安装了 npm 和 Node.js, 这两者的安装过程这里不再详述。

在 Terminal 输入下方的安装命令，就可以安装 hexo 到本地，更多的相关请参考[Hexo 官方文档](https://hexo.io/zh-cn/docs/) 。

```bash
npm install hexo-cli -g
```

git clone 我们刚刚创建的 repo, 在 terminal 下执行

```bash
hexo init ${path_of_your_repo}
```

就可以完成 init hexo 的操作。再在blog 文件夹下执行

```bash
npm install
npm install hexo-deployer-git --save
```

安装所需依赖

接下来参照 [NeXT repo](https://github.com/theme-next/hexo-theme-next) 里的指引，将 NeXT theme git clone 到 `${blog_repo}/themes/next` 中(可以参考 README.md 里的操作命令)。

接下来我们就可以来根据自己的需求更改`./_config.yml`和 `themes/next/_config.yml`两个文件了，两个文件内都有详细的注释，参数名称也很好认，推荐整个文件浏览一遍根据自己需求更改。

当然有一些选项诸如 theme 的选择，repo 的配置的肯定是必须的。

接下来我们就可以看一下效果了，在 terminal 运行 `hexo g` 就可以生成网页文件，运行 `hexo s` 就可以在localhost 预览效果，运行 `hexo d` 就可以部署到指定的 repo. 新建文章则只需要 `hexo new "${article title}"`  即可。*更多的操作请查看 hexo 官方文档和 next 官方文档*

hexo 本身有一篇 sample article，我们可以在本地查看一下效果，接下来你就可以新建自己的第一篇文章，然后部署上去啦~

注意我们这些都是在 source branch 下完成的，所以可以将我们的代码单独的 push 到 source branch，而生成的资源则需要部署到 master branch。

恭喜！至此你就有自己的博客啦！