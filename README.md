## 配置环境
- 安装 nodejs
- https://sspai.com/post/62441

## 启动服务（用于debug）
在项目根目录
hexo server

## 2个配置文件管网站展示
- _config.yml
- themes/next/_config.yml (主要是这个)


## 写博客
在 source/_posts 下新建 md 文件


## 部署
使用 GitHub Action
直接 push 即可触发

## 分支
source: 博客源码, 写md 博客也在这里
master: github action 自动编译上传的分支, 不动他
