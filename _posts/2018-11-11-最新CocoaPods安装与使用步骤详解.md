   # 一、 CocoaPods简介
1、CocoaPods 是 iOS 最常用的第三方类库管理工具，可以解决库与库之间的依赖关系，有名的开源类库都支持 CocoaPods。
2、使用CocoaPods可以很方便地查找使用新的第三方库，这些类库是比较“标准的”，可以让我们方便快捷找到真正好用的类库。
3、CocoaPods 是用 ruby 实现的，要想使用它首先需要有 ruby 的环境。幸运的是macOS系统默认已经可以运行 ruby 了。
但是有时候 ruby 版本过低是无法正常支持 CocoaPods 的使用，所以需要先安装更新升级 rvm 和 ruby。


# 二、 CocoaPods安装过程
## 写在前面
1.安装需要用到Ruby，虽然Mac自带了Ruby，不过版本有点老了，最好选择更新一下。
2.查看当前Ruby版本,检查本地Mac是否 已经安装了。rvm (ruby version manager)命令。
## 引入概念：
**RVM:**
全称是 Ruby Version Manager ，是一款由 Wayne E. Seguin  开发的一款命令行工具。rvm 能够让你轻松的安装、管理 ruby 生产力环境，诸如不同版本的解释器和 gem。
*  rvm 的项目官网：http://rvm.io/gemsets/basics
* CocoaPods项目的地址：https://github.com/CocoaPods/CocoaPods
*   CocoaPods官方指南地址 [https://guides.cocoapods.org](https://guides.cocoapods.org/)
**Ruby:**
 Ruby，一种简单快捷的 [面向对象](https://baike.baidu.com/item/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1/2262089) （ [面向对象程序设计](https://baike.baidu.com/item/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1/24792) ） [脚本语言](https://baike.baidu.com/item/%E8%84%9A%E6%9C%AC%E8%AF%AD%E8%A8%80/1379708) ，在20世纪90年代由日本人松本行弘( [Yukihiro Matsumoto](https://baike.baidu.com/item/Yukihiro%20Matsumoto) )开发，遵守 [GPL](https://baike.baidu.com/item/GPL) 协议和Ruby License。
## 1 .安装并载入rvm环境
###  （1). 检查本地是否已安装rvm
打开终端，输入指令
  ```$  rvm -v```
1）  如果不存在，则会出现下面的情况： ![](https://upload-images.jianshu.io/upload_images/5387585-838dd69d0925393b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)2）如果存在，则会打印rvm的版本信息：![](https://upload-images.jianshu.io/upload_images/5387585-639d09e9d5d5a0e4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如果不存在，先要进行安装一下；

### （ 2 ). 安装rvm
1）安装指令是
```$ curl -L https://get.rvm.io | bash -s stable```
按下回车即进入下载安装的状态，期间会自动通过homebrew安装依赖包.（Homebrew 是一个软件包管理器，用于在mac上安装一些macos 上没有的UNiX工具；类似于360软件管理器。）
等待一段时间就可以安装好Rvm。
2）载入RVM环境：
```$ source ~/.rvm/scripts/rvm```
3）检查是否安装成功：
 ``` $ rvm -v ```
 下图即为安装成功后，显示的版本号![](https://upload-images.jianshu.io/upload_images/5387585-1a79c57118d5e342.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

   
### （3）RVM命令安装Ruby环境
   1）查看当前ruby版本 
```$ ruby -v ```（检查当前版本,当ruby版本低于2.2.2时，安装cocoapods会报错）![](https://upload-images.jianshu.io/upload_images/5387585-aadb904772f3dc94.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

   2）查看所有ruby版本
```$ rvm list known ```    查询当前所有已知的ruby环境。
![](https://upload-images.jianshu.io/upload_images/5387585-82d5d1319bf970ff.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如果版本低于2.2.2，请更新一下。vrm list known命令会查询所有的ruby版本，找到最高版本号进行安装；
若版本库里没有最新版本，输入：
 ``` $   rvm get head ```     升级到最新的存储库源版本
   3）安装指定版本
输入指令：
 ```$   rvm install 2.5.1```  (选择较高版本)，
然后根据提示按“enter”键，第二次按之后会提示你输入密码。
等待漫长的下载，编译过程，完成以后，Ruby, Ruby Gems 就自动安装好了。
![](https://upload-images.jianshu.io/upload_images/5387585-142ced4ad08fa42f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) ![](https://upload-images.jianshu.io/upload_images/5387585-abd6859322285851.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  4）查看已经安装的ruby版本
　```$  rvm list```
       ![](https://upload-images.jianshu.io/upload_images/5387585-ba007c1d7707ac6d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 卸载一个已安装版本
    ``` $  rvm  remove  2.5.1```

## 2.  设置默认Ruby版本
安装好RVM之后可以指定特定Ruby版本为系统默认版本
输入命令： 
```$   rvm  2.5.01 - - default```
也可以指定其他版本号，前提是有用rvm install 安装过那个版本

## 3. 检查更新ruby版本环境
　　cocoapods是用gem ruby实现的，想要使用它首先需要有gem ruby的环境。且Mac的macos系统默认已经可以运行ruby。
　（建议gem bury包环境升级到2.6.x以上。）

###    (1).检查gem ruby版本号：
``` $  ruby -v```
 ```$  gem -v```
得到如下结果：
   ![](https://upload-images.jianshu.io/upload_images/5387585-50e778fe6dc37b41.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Gem是管理Ruby库和程序的标准包，如果它的版本过低也可能导致安装失败，解决的办法是更新gem版本
###    (2).更新gem ruby版本
```$ gem update  - -system ```    更新gem ruby版本号：

## 4.检查ruby源并移除。
### （1)、检查ruby源
```$ gem sources -l   ```
检查ruby源,结果如下：
![](https://upload-images.jianshu.io/upload_images/5387585-0989410c8162a9c5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  因为Ruby环境默认的的软件源rubygems.org被屏蔽了，国内那面永远需要翻     越的墙，你懂的~，我们需要来修改更换源，把源切换至ruby-china；

### （2)、移除掉原有的源
 ``` $ gem sources  - - remove https://rubygems.org/```
![](https://upload-images.jianshu.io/upload_images/5387585-06fdc9dd7f5db457.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###   (3)、添加国内最新的源。ruby-china
```$ gem sources -a https://gems.ruby-china.com```
![](https://upload-images.jianshu.io/upload_images/5387585-2e550d07ddab129d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这里注意一下https://gems.ruby-china.org 已经不能使用。后缀要改成com
![](https://upload-images.jianshu.io/upload_images/5387585-3c04ad78ed20aaa2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)![](https://upload-images.jianshu.io/upload_images/5387585-b6fffbfebb58609b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### （4)、检查是否添加成功
  ```$ gem sources -l```
![](https://upload-images.jianshu.io/upload_images/5387585-0386944759d30f9f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
 到这里就已经把Ruby环境安装成功！接下来需要对cocoapods进行安装。

## 5. 安装CocoaPods
```$ gem install -n /usr/local/bin cocoapods```
![](https://upload-images.jianshu.io/upload_images/5387585-68809ec1481016bd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 6. 查看是否安装成功并更新
### （1）查看是否成功
```$ pod  - - version  ```   查看pod版本
![](https://upload-images.jianshu.io/upload_images/5387585-c9896d658355b9bf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### （2)  更新Podspec索引文件，创建本地索引库,如果没有报错，就说明一切安装成功了；这个过程需要一些时间。
```$ pod setup```
![](https://upload-images.jianshu.io/upload_images/5387585-49506b67f81a126b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 三、CocoaPods的使用
## 1、用Xcode创建（打开）一个工程，并创建podfile配置文件
###   （1）、进入项目目录
``` $  cd ~```

在没有导入库时，项目中import库 会报错
![](https://upload-images.jianshu.io/upload_images/5387585-436ec22706c811bb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)![](https://upload-images.jianshu.io/upload_images/5387585-32cccec3f308206b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)![](https://upload-images.jianshu.io/upload_images/5387585-55562a2e5109bd3e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



###  （2）、创建Podfile文件
``` $  touch Podfile ```  
 创建一个podfile文件，然后打开编辑;
或是使用```$ vi podfile ```  输入```i ```进入编辑，编辑完成后按 esc 然后输入``` ：wq  ``` 按回车键  ，保存并退出。
###  （3）、编辑Podfile文件。
我们可以在Podfile文件中写入需要用到的第三方库按如下格式：
>platform :ios, '9.0'
use_frameworks!
>target 'TestDemo' do
>pod 'Alamofire', '~> 4.0.1'
pod 'Kingfisher', '~> 3.1.1'
>end

Swift的pod文件在于use_frameworks! 这一句是必须的，作用是把三方库打包成静态库，而oc是不需要的。

另外，也可在github中找到所需要的库，里面有podfile格式内容

![](https://upload-images.jianshu.io/upload_images/5387585-54dbffcc0c54ac88.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 2、安装依赖库
  ```$ pod install  ```    (后续添加框架可直接pod update)
![](https://upload-images.jianshu.io/upload_images/5387585-61a821683feba130.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

若出现以下错误时，在Podfile 文件中添加如下一行内容：
>xcodeproj ‘你的工程名.xcodeproj’

这是由于你多次移动你项目的路径，以至于再次update你的Podfile项目时，出现找不到工程路径的问题![](https://upload-images.jianshu.io/upload_images/5387585-2ef7b4d6fe8b36a3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 3、进入项目时，再次打开，编译报错就消失了。安装完成！
![](https://upload-images.jianshu.io/upload_images/5387585-131ca16bfa1d877e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/5387585-9e65851eb176e745.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/5387585-23bf24ee99a4d979.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##CocoaPods工作原理
CocoaPods的工作主要是通过ProjectName.xcworkspace来组织的，在打开ProjectName.xcworkspace文件后，发现Xcode会多出一个Pods工程。它是将所有的依赖库都放到名为Pods项目中，然后让主项目依赖Pods项目，就这样，源码管理工作都从主项目移到了Pods项目中。
# 完结！！！
