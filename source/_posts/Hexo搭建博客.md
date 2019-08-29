---
title: 使用Hexo+hexo-theme-matery搭建一个属于自己的博客
date: 2019-08-24 16:27:55
tags:
    - Hexo
---


最近无意看到Hexo博客框架，[官网](https://hexo.io/zh-cn/docs/)介绍得挺全的，想着可以利用Hexo+hexo-theme-matery搭建一个博客，用来记录自己的所学到的知识。

### 1. 安装 Hexo

`$ npm install -g hexo-cli`

### 2. 建站

安装 Hexo 完成后，执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。

`$ hexo init <folder>`
`$ cd <folder>`
`$ npm install`

新建完成后，指定文件夹的目录如下：
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes

启动服务
`$ hexo server`
默认情况下，访问网址为： http://localhost:4000/
选项	描述
-p,     --port	重设端口
-s,     --static	只使用静态文件
-l,     --log	启动日记记录，使用覆盖记录格式


### 3. 配置
hexo相关的配置都放在根目录 _config.yml 里面

### 4. 切换主题
hexo初始化之后默认的主题是landscape，如果想要切换主题， 可以将你下载好的主题放在 themes 文件夹内，我比较喜欢 [typora-vue-theme](https://github.com/blinkfox/hexo-theme-matery/blob/develop/README_CN.md) 这个主题，将它放到themes文件夹之后修改根目录的 _config.yml ，找到对应的 theme , 把该值改为对应的主题的文件夹名称

### 5. 国际化
每个主题下面会有个languages文件夹，修改 _config.yml 内的 language , 将该值改为为对应的languages文件夹里面的文件名称

### 6. 上传到github
6.1. 创建仓库
新建一个名为你的用户名.github.io的仓库，比如说，如果你的github用户名是test，那么你就新建test.github.io的仓库（必须是你的用户名，其它名称无效），将来你的网站访问地址就是 http://test.github.io 

几个注意的地方：

注册的邮箱一定要验证，否则不会成功；
仓库名字必须是：username.github.io，其中username是你的用户名；
仓库创建成功不会立即生效，需要过一段时间，大概10-30分钟，或者更久，我的等了半个小时才生效；
创建成功后，默认会在你这个仓库里生成一些示例页面，以后你的网站所有代码都是放在这个仓库里啦。

6.2 部署
安装 hexo-deployer-git。
`$ npm install hexo-deployer-git --save`

修改配置。
在_config.yml文件中，找到Deployment，然后按照如下修改

```yaml
deploy:
  type: git
  repo: git@github.com:Mandy-cen/Mandy-cen.github.io.git
  branch: master
```

1) 执行以下命令生成博客的静态页面
`$ hexo generate`
或者 `$ hexo g`
$ hexo deploy

2) 执行以下命令将我们生成的博客静态页面上传到GitHub
`$ hexo deploy`
或者 `$ hexo d`

3) 打开浏览器访问 username.github.io 即可访问我们刚部署到Github上的博客，比如我的就是  https://mandy-cen.github.io/

如果有遇到一些资源不对或者其他问题时，可以尝试执行以下命令清除已经生成的静态文件，再重新执行上面的 第 1 步 第 2 步 即可。
`$ hexo clean `# 删除已经生成的静态页面

### 7. 总结常用命令

1) 模版
```yaml
    hexo new "postName" #新建文章
    hexo new page "pageName" #新建页面
    hexo generate #生成静态页面至public目录
    hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
    hexo deploy #将.deploy目录部署到GitHub
    
    hexo new [layout] <title>
    hexo new photo "My Gallery"
    hexo new "Hello World" --lang tw
```

2) 草稿
```yaml
    hexo publish [layout] <title>
```

3) 服务器
```yaml
    hexo server #Hexo 会监视文件变动并自动更新，您无须重启服务器。
    hexo server -s #静态模式
    hexo server -p 5000 #更改端口
    hexo server -i 192.168.1.1 #自定义 IP
    
    hexo clean #清除缓存 网页正常情况下可以忽略此条命令
    hexo g #生成静态网页
    hexo d #开始部署
```

4) 推送到服务器上
```yaml
    hexo n #写文章
    hexo g #生成
    hexo d #部署 #可与hexo g合并为 hexo d -g
```

5) hexo
```yaml
    npm install hexo -g #安装  
    npm update hexo -g #升级  
    hexo init #初始化
```
### 8. 备份hexo代码
    对于一个开发人员来说保存和备份代码是非常重要的。使用hexo在githut上搭建博客，仓库里只有生成网页的静态文件，是没有hexo的源文件的，所以如果要换电脑开发写博客的话就会很麻烦。
    
    首先在本地仓库下的master分支下创建个hexo分支
    

    然后将hexo分支设为默认分支，执行git add，git commit -m "提交文件"，git push origin hexo来提交hexo网站源文件；
    
![](https://raw.githubusercontent.com/Mandy-cen/Mandy-cen.github.io/master/favicon.png)