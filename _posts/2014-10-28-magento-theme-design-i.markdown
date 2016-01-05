---
layout: post
title: "magento theme design - I"
date: 2014-10-28 21:44:42 +0800
comments: true
categories: [magento, theme, learning]

---

## 序

这些天，开始接触Magento的方方面面，发现确实是个很不错的框架。只是对Zend Framework了解不多，所以刚开始总会有些摸不着内在的逻辑关系。不过，学习起来，还是很顺手的。下面的内容基本上参阅*Mastering Magento Theme Design*2013版这本书。这本书上讲解十分详尽，值得一读。

## 文

### Magento模版设计第一步:创建文件夹

在app文件夹下面创建模版文件夹（假定模版名demotheme）：

1. 创建文件夹**app/design/frontend/demotheme**;
2. 在该文件夹下面创建子文件夹**app/design/frontend/demotheme/default**;
3. 再在该文件夹下面创建三个子文件夹：

	- **app/design/frontend/demotheme/default/template**;
	- **app/design/frontend/demotheme/default/layout**;
	- **app/design/frontend/demotheme/default/locale**;
	
在skin文件夹下面创建模版文件夹：

1. 创建文件夹**skin/frontend/demotheme**;
2. 在该文件夹下面创建子文件夹**skin/frontend/demotheme/default**;
3. 再在该文件夹下面创建三个子文件夹：

	- **skin/frontend/demotheme/default/css**;
	- **skin/frontend/demotheme/default/images**;
	- **skin/frontend/demotheme/default/js**;
	
### Magento模版设计第二步：创建必要文件

Magento的模版设计，可以通过直接创建空白文件开始，也可以通过复制base模版里面的文件来开始。后者是更容易上手的一个方式。

复制**app/design/frontend/base/default/template**中的下列文件/文件夹到**app/design/frontend/demotheme/default/template**：

1. **page/1column.phtml**;
2. **page/2columns-left.phtml**;
3. **page/2columns-right.phtml**;
4. **page/3columns.phtml**;
5. **page/html/head.phtml**;
6. **page/html/header.phtml**;
7. **page/html/footer.phtml**;

创建**app/design/frontend/base/default/layout/layout.xml**文件，并在该文件中填入以下代码：

	<?xml version="1.0"?>

	<!-- 
	/**
 	* local.xml
 	* Local layout modifications for our local theme
 	* @category design
 	* @package  demotheme
 	* @copyright Copyright (c) 2014 Lyon Sun
 	*/
	 -->

	<layout version="0.1.0">
    	<default>
        
	    </default>
	</layout>
	
	
### Magento模版设计第三步：禁用缓存

为了避免开发过程中的不连续性，有必要将Magento的缓存系统禁用。

1. 进入Admin管理界面，系统 -> 缓存管理；
2. 全选所有项，在操作下拉列表里选择禁用，然后提交；


### Magento模版设计第四步：激活模版

对于单商铺网站，激活模版十分简单。

1. 进入Admin管理界面，系统 -> 配置；
2. 然后选择设计标签页；
3. 在包栏（第一栏）替换之前的包名rwd为demotheme，然后点击保存配置即可。

## 尾

至此，Magento模版开发的准备工作就绪。这时，打开Magento的前台界面，会发现页面已经没有任何设计风格了。这就为我们之后开始定制模版铺好了道路。

	






	
