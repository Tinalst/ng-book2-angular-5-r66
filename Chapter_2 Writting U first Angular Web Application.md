## Chapter_2 Writting U first Angular Web Application [编写你的第一个Angular应用]

###  2.1 概要
#### 本章你将学会如下几点：

1. • Building custom components
2. • Accepting user input from forms
3. • Rendering lists of objects into views
4. • Intercepting user clicks and acting on them
5. • Deploying our app to a server
6. • how to take an empty folder
7. • build a basicAngular application
8. • deploy it to production

### 2.2 Get Start
#### 2.2.1 安装NodeJS和Npm
> 去nodeJS官方下载安装包安装即可。确保NODE版本为6.9.0以上。
    NPM (Node Package Manage) 顾名思义，node包管理器的简称；
##### 检查安装成功的方式，在Terminal中输入
```
node -v
npm  -v
```
`取保npm的版本为3.0.0或者以上`
#### 2.2.2安装TypeScript
```
npm install -g typescript
```
`不一定非得安装TS，但是还是建议安装，虽然NG有ES5的API但是，NG是用TS写的，因为它更好，使用NG结合TS开发更好`
####  2.2.3开发环境之浏览器
##### 推荐使用Chrome, IE11或以上，IE11 You keng.
`如果使用的OS是OSX或者Linux,你可能会看到如下输出`
```
Could not start watchman; falling back to NodeWatcher for file system even
```
##### 意思就是没有安装watchman
```
$ brew install watchm   // 安装watchman
```
### 2.3创建工程
#### 2.3.1 创建新工程
```
ng new angular-hello-world  // 创建一个叫做angular-hello-world的工程
```
`工程的相关文件取决于@angular/cli的版本
创建工程时候会花点时间，当你创建成果后会看到如下显示`
![Alt text](./1515334267166.png)
#### 2.3.2 工程目录结构
```
e2e                    // 端到端测试
node_module            // 放置导入的依赖包的文件夹
src                    // 你写代码的地方
.angular-cli.json      // angular-cli这个工具的配置文件
.karma.conf.js         // 单元测试配置文件
package.json           // npm配置文件
pretractor.conf.js     // e2e测试配置文件
README.md              // 一个有用的README
tslint.json            // 编码格式配置文件
```
`可能你现在的目录还有其他文件，但是以上是一定有的`
#### -> src 目录结构
![Alt text](./1515334644707.png)
#### 2.3.3  让我们工程跑起来
#####使用命令行在NG工程的根目录下输入
```
ng serve
```
`如果你在RUN的时候遇到如下提示信息`
```
Port 4200 is already in use. Use '--port' to specify a different 
```
#####意思就是说，4200端口号被占用了，使用 --port 修改启动端口
```
ng serve --port 4888 // 设置在4888端口上跑端口
```
`有些机器localhost不行，就换127.0.0.1`
![Alt text](./1515334802532.png)
##### 运行成功！
### 2.4 创建Component（组件）
#### 2.4.1 什么是组件？为什么要有组件？
> 组件是angular里的一个一个很重要的概念。在NG中，我们通过HTML标记进行交互，但是浏览器只能识别浏览器定义时所能是别的一些基础标签比如<form> <video> etc. 那么如果我们想写一个新的标签比如<hello-world>,浏览器如何识别呢？ 这就是组件的用途，教会浏览器新的标签。如果你学过AngularJS,那么你可以理解为AngularJs里的direction。
##### 创建组件
```
ng generate component hello-world // 创建一个叫做hello-world 的组件
```
创建成果迹象
![Alt text](./1515334966668.png)
`1.一个组件必须要这四个文件吗？不一定的，一个basic Component  只需要component decorator（组件装饰器）和Class( 类)`
`2.注意component的文件格式是TS，浏览器是不能直接识别TS文件的，为了解决这个问题，在 ng serve 的时候命令行会自动动态编译TS文件为JS文件`
### 2.5 导入dependence (依赖)
型如：
```typescript
import { things } from wherever; // ES6语法 {things} 重构意思 导入things ,things 来自 wherever
```
```typescript
import { Component, OnInit } from '@angular/core';
// import  Component, OnInit 来自@angular/core ，告诉我们我们想找的的依赖来自哪里，这里是告诉编译器 @angular/core 定义和导出两个TS/JS对象一个叫做Component , 一个叫做OnInit
// import OnInit , OnInit 帮助我们在跑代码时候初始化Component
```
### 2.6 Compenent Decorators (组件装饰器)
```typescript
Component({
    // 我们使用@Component 装饰器，将CLASS(类) “装饰”成 Component(组件);
})
```
```
Component({
  selector: 'app-hello-world',
  templateUrl: './hello-world.component.html',
  styleUrls: ['./hello-world.component.css']
})
// 配置@Componrnt 的selector 属性为 app-hello-world ，这样就能在HTML静态文页面中使用<app-hello-world>这样的自定义标签
// <app-hello-world> 出现在任何的templete中都会编译和使用HelloWorldComponent 类并且能使用这个类里的任何功能
```
### 2.7 Template(模板)文件
#### 2.7.1 什么是Templete ？
> 就是我们常见的静态文件HTML
#### 2.7.2 添加template的两种方式
`1.template:`
```
@Component({
 selector: 'app-hello-world',
 template: `
 <p>
 hello-world works inline!
 </p>
 `
8 })
// 配置@Component的template 属性为静态文件正文
// 使用ES6新语法backbrick 来替代 " " + ""
```
` 2. templateUrl`
```
@Component({
  selector: 'app-hello-world',
  templateUrl: './hello-world.component.html',
  styleUrls: ['./hello-world.component.css']
})
// 配置@Component 的templeteUrl 属性为模板文件的路径
```
`关于对什么时候使用链接方式什么时候使用templet的思考没有固定的规矩，自己觉得这样方便就这么来`
### 2.8 导入样式
> Ng 中的组件的样式是只会作用于当前组件，而不会影响其他组件
#### 2.8.1 使用@Component的StyleUrl属性这是样式文件路径
```
@Component({
  styleUrls: ['./hello-world.component.css'] 
  // 你可能会注意到这个属性的参数类型和上面讲到的两个不一样，是一个Array 类型，也就是意味着，这个属性能加载多个样式文件
})
```
### 2.9 加载我们的组件
怎么加载呢？
以我本地为例 打开 F:\code\angular\angular-hello-world\src\app\app.component.html 文件，在文件中修改成我们刚刚自己NEW出来的组件
```
<h1>
  {{title}}
  <app-hello-world></app-hello-world>
</h1>
```
在浏览器中查看
![Alt text](./1515336490922.png)

