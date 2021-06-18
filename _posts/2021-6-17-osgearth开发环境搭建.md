---
layout: mypost
title: osgEarth开发环境搭建
categories: [OSG]
---

以前做项目使用到了<strong style="color:#9b2ebd;">osgEarth</strong>三维地球，所以整理一份环境的安装搭建。

## 所需工具（包含依赖）

- [OpenSceneGraph-3.6.5](https://github.com/openscenegraph/OpenSceneGraph/releases/tag/OpenSceneGraph-3.6.5)

- [osgEarth-3.1.0](http://osgearth.org/)

  - [curl-7.65.3](https://curl.se/download/curl-7.65.3.zip)
  - [proj6.2.0](https://proj.org/download.html)
  - [SQLite3](https://www.sqlite.org/download.html)

- [CMake3.20.4](https://cmake.org/download/)

- VS2019

- Qt5.12.0

  **（备注：博主提供编译好的库下载，如果需要请留言。）**

## 编译OpenSceneGraph

1. 使用CMake配置目标工程

   CMake配置好目录直接点击generate按钮选择vs2019和x64即可。

   ![conf1](conf1.png)

2. 编译生成好的工程

   打开目录后用vs2019打开编译好的sln工程，然后直接编译即可。（记得debug和release都编译一遍。）

   ![vsbuild1](vsbuild1.png)

## 编译osgEarth

osgEarth的编译比较复杂，需要把依赖项全部都编译出来。

### 编译curl-7.65.3

下载解压后打开CMake选择目录

![conf2](conf2.png)

打开工程编译进行编译，得到库文件

![lib1](lib1.png)

### 编译sqlite3

1. 首先下载三个压缩包：

   [sqlite-amalgamation-3350500.zip](https://www.sqlite.org/2021/sqlite-amalgamation-3350500.zip)

   [sqlite-dll-win64-x64-3350500.zip](https://www.sqlite.org/2021/sqlite-dll-win64-x64-3350500.zip)

   [sqlite-tools-win32-x86-3350500.zip](https://www.sqlite.org/2021/sqlite-tools-win32-x86-3350500.zip)

2. 新建一个文件夹sqlite3，将三个压缩包内的文件都解压到sqlite3文件夹中：

   ![folder1](folder1.png)

3. 打开vs2019命令行工具，进入sqlite3目录。

   然后输入`lib /def:sqlite3.def /machine:x64`生成lib文件：

   ![vsbuild2](vsbuild2.png)

### 编译proj6.2.0

1. 解压后配置CMake路径生成工程：

   ![conf3](conf3.png)

2. 打开工程编译：

   