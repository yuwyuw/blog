---
title: 如何使用TypeScript
date: 2018-01-22 11:21:10
tags:
---
TypeScript的几种开发环境介绍
<!-- more -->
###### 搭建TypeScript
1.安装TypeScript
```
cnpm install -g typescript
```
2.创建一个项目
```
#创建一个typescript_demo的项目以及主要的文件夹
mkdir -p typescript_demo/src/{css,image}
#使用VScode打开
```
3.创建package.json文件
```
npm init
```
4.创建tsconfig.json文件
```
tsc --init
```
5.在src下创建index.js文件
```js
function greeter(person) {
    return "Hello, " + person;
}

let user = "Jane User";

document.body.innerHTML = greeter(user);
```
6.在根目录下创建index.html文件
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title></title>
</head>
<body>
  <script src="./src/index.js"></script>
</body>
</html>
```
7.目录结构图
```ASCII
ts_vscode/
    |-- src/
    |    |--css/
    |    |--image/
    |    |--index.ts
    |
    |--index.html
    |--package.json
    |--tsconfig.json
```
8.安装live-server，来帮助我们启动一个服务器环境
```
npm install -g live-server
```
9.修改package.json中的scripts
```js
"scripts": {
    "test": "tsc -w & live-server"
}
```
10.在终端中输入npm t 可以启动项目了
```
npm t
```
###### 搭建WebPack+TypeScript
1.安装TypeScript
```
cnpm i -g typescript
```
2.安装WebPack
```
$ cnpm i webpack --save-dev
#如果需要webpack开发工具
cnpm install webpack-dev-server --save-dev
```
3.安装ts-loader
```
cnpm i ts-loader --save-dev
```
4.创建package.json文件
```
npm init
```
5.创建tsconfig.json文件
```
tsc --init
```
6.目录结构图
```
typescript_demo/
    |--src/
    |    |--css/
    |    |--image/
    |    |--index.ts
    |--dist/
    |    |--bundle.js
    |    |--index.html 
    |--package.json
    |--tsconfig.json
    |--webpack.config.js
```
7.配置tsconfig.json
```
{
  "compilerOptions": {
    "outDir": "./dist/",
    "noImplicitAny": true,
    "module": "es6",
    "target": "es5",
    "jsx": "react",
    "allowJs": true
  }
}
```
8.配置项目目录中的webpack.config.js
```js
const path = require('path');
module.exports = {
  entry: './src/index.ts',
  devtool: 'inline-source-map',
  devServer: {
    contentBase: './dist'
  },
  module: {
    rules: [
      {
        test: /\.tsx?$/,
        use: 'ts-loader',
        exclude: /node_modules/
      }
    ]
  },
  resolve: {
    extensions: [ '.tsx', '.ts', '.js' ]
  },
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
};
```
9.配置package.json
```json
"scripts": {
    "watch": "webpack --watch",
    "start": "webpack-dev-server --open"
  },
```
10.配置editorconfig文件
```
root = true
[*]
charset = utf-8
indent_style = space
indent_size = 2
end_of_line = lf
insert_final_newline = true
trim_trailing_whitespace = true
```
11.html内容
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title></title>
</head>
<body>
  <script src="./bundle.js"></script>
</body>
</html>
```
11.输入npm start 启动项目
```
npm start
```
###### TypeScript+React
1.安装React依赖
```
npm install -g create-react-app
```
2.创建一个名为「react_typescript」的项目
```
create-react-app react_typescript --scripts-version=react-scripts-ts
```
3.执行npm start
```
npm start
```
