---
layout: post
title: Zoho Inventory 使用指南（上）
date: 2019-07-04T09:33:08+03:00
comments: true
categories: [work]
tags: [zoho]
published: true
---

公司业务转移，为了更好地协调各系统间的作业，库存系统也随之调整变化。之前使用的是金蝶软件出品的精斗云云进销存系统，此系统功能十分强大，而且简单易用。选择弃用的主要原因是这个系统的外部对接接口不够完善，很难与其他系统对接整合，具体细节这里不做详述。以下内容着重于从精斗云往Zoho Inventory转移过程中，如何录入期初库存，期间因出错而反复的各种问题的解决办法，Zoho Inventory库存管理系统的一些使用须知，以及其他等等。

## 注册账号

首先，当然是注册一个zoho账号。这个步骤很简单，跟这篇文章的主要内容相关性不大，所以也不做详述。如下提供两个网址，应该是可以任取其一均可：

[Zoho 账号注册页面](https://www.zoho.com/signup.html)

[Zoho Inventory 账号注册页面](https://www.zoho.com/inventory/signup/)

## 新建组织机构

按要求填写公司信息跟其他设置（如地区时区设置等）即可。

## 完善商品设置

值此文撰写时（2019年7月），Zoho Inventory 推出的其中一个新的功能Item Categories，为库存商品的分类提供了更多的选项。默认设置中，这个字段是未启用状态。为了给商品库存进行不同分类，遵循以下步骤，打开这个首选项设置。

首先，点击右上角的`设置`按钮，然后点击`首选项`：

![alt-text](/assets/images/zoho/settings-landing.png "Zoho全局设置入口")

进入首选项页面之后，点击`品目`栏，在该页面的最后`补充说明`中，勾选`类别`字段所在行的复选框：

![alt-text](/assets/images/zoho/item-categories-setting.png "品目类别设置入口")

最后点击下方的`保存`按钮以保存设置。

至此，商品的分类设置设置完成。点击左侧侧边栏上方的`返回`按钮到`仪表板`主页面，下一步，导入商品品目及其期初库存。

## 导入商品品目

### 进入商品品目页面

点击左侧侧边栏的`品目`主菜单选项，然后继续点击其下拉菜单里的`品目`副菜单选项，进入品目主页面：

![alt-text](/assets/images/zoho/items-page.png "品目主页面")

点击该页面右上角菜单按钮，然后点击其中的`导入品目`选项，进入品目导入主页面：

![alt-text](/assets/images/zoho/import-items-landing.png "品目导入页面入口")

### 下载并熟悉CSV导入文件

下载一份示例文件，该文件类型为CSV文件。示例CSV文件，以逗号`,`作为分隔符。以在MacOS使用Excel编辑修改内容为例，可能会遇到文件导入问题。

#### CSV文件导入问题

CSV是英文Comma-Separated Values的缩写，原意是逗号分割的数据值。基本规则有：

1. 每一行为一组数据

2. 每组数据使用逗号分割单个数据

3. 每组数据的个数，即每行单个数据的总数量，应该相同

4. 每组数据的顺序也应该相同

5. 单个数据内容中本身就含有分隔符的话，需要用双引号`"`包裹整个数据内容

CSV的使用中，尤其是部分欧洲国家中，习惯使用分号`;`而非逗号`,`来分割单个数据。但不管是哪种情形，在MacOS中最好的解决办法是：

1. 打开Excel应用程序

2. 新建一个空文档

3. 在文件菜单中选择导入

4. 选择CSV file，然后点击导入

5. 在文件选择框中选择下载下来的样本文件，点击获取数据

6. 选择`分割`单选框，然后点击下一步

7. 勾选`分号`为分隔符，然后点击下一步

8. 可以暂时不管数据类型，全部保持默认通用设置，点击完成，点击OK

9. 修改完成之后，保存为CSV格式的文件

### 修改样本文件

样本CSV文件一共有23列，也就是说23个不同的字段：

`Item Name`，`Sales Description`，`Selling Price`，`Sales Account`，`Tax Name`，`Tax Percentage`，`Tax Type`，`Unit`，`SKU`，`UPC`，`EAN`，`ISBN`，`Part Number`，`Exemption Reason`，`Purchase Price`，`Purchase Account`，`Purchase Description`，`Inventory Account`，`Reorder Level`，`Item Type`，`Preferred Vendor`，`Opening Stock`，`Opening Stock Value`

其中有些字段可以选择不导入数据。结合本文的应用场景，导入商品品目的同时，我们还需要导入期初库存。因此，需要注意以下几个地方：

1. 需要填写的字段共有8个：`Item Name`，`Sales Description`，`Sales Account`，`SKU`，`Purchase Description`，`Item Type`，`Opening Stock`，`Opening Stock Value`

2. 需要增加2个字段，`Brand`与`Category Name`，分别指定品目的品牌及分类。

3. `Item Name`跟`SKU`可选择性地填写为同一个值，`Sales Description`跟`Purchase Description`也可以选择性地填写为同一值，`Sales Account`意义不明确，暂时按照样本示例填写为`Sales`，`Item Type`同样意义不明确，暂按示例填写为`Inventory`。

4. `Opening Stock`与`Opening Stock Value`，分别指定商品品目地期初库存值，以及该商品期初库存单件单价数额。

#### 其他需要注意的事项

1. 应该注意，如本文示例，需要在SKU中记入商品尺码，且商品尺码存在半码的情况下，最好以美式记小数法用`.`来记录半码，以免因用逗号`,`记录而与CSV分割符所用的逗号`,`出现冲突的问题。

2. 需要注意将原SKU转换为text文本类型，以免出现，在Excel中，位数过多的全是数字的SKU，最后一位或者多位被强制改写为0的情况。

### 导入品目CSV文件

选择已修改并保存好的CSV文件，`覆盖`重复记录，`分号(;)`为文件分隔符，点击下一步。

进入匹配字段页面，需要注意以下几点：

1. `售价`，`购买价格`，`期初存货值`都是价格，都带有小数，因此，需要注意使用的计数方式

2. `品牌`对应字段选择`Brand`，`类别名称`对应字段选择`Category Name`

3. 勾选`保存这些选择为将来的导入时使用。`

点击下一步继续，进入预览页面。

确保预览页面没有跳过的记录数，点击导入，即可导入商品品目及其期初库存。

## 总结

这部分介绍了如何注册账号，新建组织结构，完善商品设置，以及最后导入商品品目及其期初库存。下一个部分将继续讨论如何销货以及如何多仓共存。这期间可能遇到的主要问题在于需要重新导入所有仓库全部商品品目及其期初库存至主分仓，重置错误商品品目SKU的期初库存。完成这些步骤之后，最后需要通过调拨转移部分主分仓的期初库存至其他分仓，以保证各分仓的库存独立共存。
