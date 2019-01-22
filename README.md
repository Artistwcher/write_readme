# &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;国科大高级软件工程大作业
项目名称：果壳书评网  
项目地址：[https://salty-citadel-37632.herokuapp.com/](https://salty-citadel-37632.herokuapp.com/)  
项目成员：  
&emsp;&emsp;组长：王常辉  
&emsp;&emsp;组员：李泽阳、周正、杨彬彬、马荣杰  
## 项目简介
- 这是一个轻量级的书评网站  
- 用户分为游客和注册用户  
- 游客只能查看书籍以及书的评论与已有评分  
- 登录/注册后的用户可对书进行评论以及添加一些自己喜欢的书  
- 用户可以对自己的评论与评分增删改查  
- 一本书的推荐度是该书所有评分的平均值  
- 一本书显示的内容主要有作者、推荐度、简介等  
## 项目展示
1.注册/登录模块
![](https://github.com/Artistwcher/write_readme/blob/master/public/1.png)
2.系统主界面
![](https://github.com/Artistwcher/write_readme/blob/master/public/2.png)
3.添加书籍
![](https://github.com/Artistwcher/write_readme/blob/master/public/3.png)
4.编辑书籍
![](https://github.com/Artistwcher/write_readme/blob/master/public/4.png)
5.添加评论
![](https://github.com/Artistwcher/write_readme/blob/master/public/5.png)
6.评论显示
![](https://github.com/Artistwcher/write_readme/blob/master/public/6.png)
7.搜索模块
![](https://github.com/Artistwcher/write_readme/blob/master/public/7.png)
8.书籍分类
![](https://github.com/Artistwcher/write_readme/blob/master/public/8.png)
## 项目使用
在C9工作区新建一个工作区间  
```
$ gem install rails
$ git clone git@github.com:lizeyang18/bookreview.git
$ cd bookreview
$ rvm install ruby-2.5.0  //安装Ruby
$ bundle install 
$ sudo apt-get update   //这行与下一行安装imagemagick插件
$ sudo apt-get install imagemagick --fix-missing 
$ rails server -b $IP -p $PORT  //即可运行
```
普通用户：  
用户名：`278845421@qq.com`  
密码：`123456`  
## 部署到heroku
通过上述C9的实施成功后，就可以将项目部署到heroku上  
```
$ heroku login
$ heroku create
$ git push heroku master
```
实施到这一步发现报错：预编译失败  
解决方法：  
```
$ rm -rf ~/.bundle/ ~/.gem/ .bundle/ Gemfile.lock
$ bundle install
$ git add .
$ git commit -m "commiting Gemfile.lock"
$ git push heroku master -f
```
push到heroku时可能会有`You must use Bundler 2 or greater with this lockfile`这个问题  
再运行：  
```
$ heroku buildpacks:set https://github.com/bundler/heroku-buildpack-bundler2
$ git add .
$ git commit -m "commiting Gemfile.lock"
$ git push heroku master -f
```
如果没问题就不用运行上面三句  
部署到heroku上发现assets/images目录下的显示推荐度的星星图片丢失  
解决方法：  
- 将`config/environments/production.rb`里的`config.assets.compile = false`改成`config.assets.compile = true`
- `$ rake assets:precompile  //先在本地预编译静态资源`
- `$ git add .`
- `$ git commit -m "commiting Gemfile.lock"`
- `$ git push heroku master -f`
## 存在的问题
&emsp;&emsp;由于使用的是heroku免费用户，再重启heroku时，存储在public/system下的图片会被heroku自动删除，使得上传网站的图片丢失不显示  
## 待完善
&emsp;&emsp;录入大量用户实现书的智能推荐  
&emsp;&emsp;将用户上传的图片不存入public/system，而是存入assets/images目录下，防止被heroku删除  

