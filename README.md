
#### 导语
> 之前一直都是在博客园写博客，前几天无意中看到用hexo搭建的博客，风格让我很喜欢，使用markdown语法去写博客简直是帅呆了，于是一不做二不休，搭建好博客。下面给出一点遇到的问题。

### 一、怎么安装
按照官网的[hexo.io](https://hexo.io/zh-cn/)的提示，一步步安装，nodejs，git等环境配置好，这里不多说.

### 二、本地部署完之后怎么和你的github关联
首先你得去github创建个仓库，仓库名很讲究，必须是：your_name.github.io,否则创建不成功
创建好之后，在你的项目根目录配置文件_config.yml文件中配置如下，tanxuxu是我的gitname

![配置](../1.png)

重新部署项目即可
这里列出几点hexo的常用指令

#### 关于简写的
* hexo n "我的博客" == hexo new "我的博客" #新建文章
* hexo p == hexo publish
* hexo g == hexo generate#生成
* hexo s == hexo server #启动服务预览
* hexo d == hexo deploy#部署

#### 关于服务器的
* hexo server #Hexo 会监视文件变动并自动更新，您无须重启服务器。
* hexo server -s #静态模式
* hexo server -p 5000 #更改端口
* hexo server -i 192.168.1.1 #自定义 IP
* hexo clean #清除缓存 网页正常情况下可以忽略此条命令
* hexo g #生成静态网页
* hexo d #开始部署

#### 关于文件监视的
* hexo generate #使用 Hexo 生成静态文件快速而且简单
* hexo generate --watch #监视文件变动

#### 关于部署的
* hexo generate --deploy
* hexo deploy --generate

#### 关于草稿的
* hexo publish  <title>

#### 关于模版
* hexo new "postName" #新建文章
* hexo new page "pageName" #新建页面
* hexo generate #生成静态页面至public目录
* hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
* hexo deploy #将.deploy目录部署到GitHub
* hexo new <title>
* hexo new photo "My Gallery"
* hexo new "Hello World" --lang tw

### 三、你可能会遇到的问题
#### 报错ERROR Deployer not found: git

    npm install hexo-deployer-git --save

### 怎么和你的域名关联
你可以去github去设置

![github域名配置](../2.png)

你也可以在source根目录下创建文件CNAME 把你的域名写上去，注意不要写http://

### 四、怎么更换主题
单纯的更换主题还是比较简单的，将下载的主题放到themes目录下，配置文件中的主题名字改成对应的注意名字

    theme: next
