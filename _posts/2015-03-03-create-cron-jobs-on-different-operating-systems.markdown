---
layout: post
title: "create cron jobs on different operating systems"
date: 2015-03-03 14:03:15 +0800
comments: true
categories: 
---

## 序

不同的操作系统环境下，定时任务的创建方式也是不一样的。Windows上面，是通过任务计划实现的。Mac OSX跟其他Linux系统上，则可以直接通过命令行crontab来创建。

## 文

以获取当前blockchain上面的比特币兑换行情为例。

#### Windows OS

首先，需要写一小段VBScript代码：

	' VBS script to send HTTP POST request to a URL.
	' author: Lyon Sun <sunly917@gmail.com>
	' last modified: 2015-03-03 14:07:31

	' URL to open....
	sUrl = "https://blockchain.info/ticker"

	' log file destination
	sDestFolder = ""
	logFile = "cron_job_btc_" & Year(Date) & "_" & Month(Date) & "_" & Day(Date) & "_" Hour(Date) & "_" & Minute(Date) & "_" & Second(Date) & ".log"

	' comment out next line to have a dialog notifying task is done.
	' WScript.Echo "Done..."

	' call HTTPGet function
	HTTPGet sUrl

	' HTTPGet function to send request
	Function HTTPGet(sUrl)

		set oHTTP = CreateObject("Microsoft.XMLHTTP")
		oHTTP.open "GET", sUrl, false
		oHTTP.send
		HTTPResp = oHTTP.responseText

		' write log into log file
		If oHTTP.Status = 200 Then 
			With CreateObject("ADODB.Stream")
				.Type = 1
				.Open
				.Write oHTTP.responseBody
				.SaveToFile logFile
				.Close
			End With
		End If

	End Function

存储这段代码在磁盘的任何位置，如桌面。

然后，在开始菜单，附件，系统工具下找到任务计划程序。点击打开。

Trigger里面设置该程式运行的频次。Action里面选择启动一个程序，然后在文件选择窗里选择刚才存储的VBScript代码文件。在参数与启动文件夹输入框里面，分别同时填上该代码所在的文件夹的绝对路径。

启动该任务计划。取决于Trigger里面设置的频次，该任务计划将在设定时间运行。

#### Mac OSX及其他Linux Distribution

相对来说，在osx或者Linux上面建立定时任务，要简单得多。

打开命令行终端，输入：

	crontab -e

按键盘按键`i`进入编辑模式。然后添加如下一行代码：

	0 0 * * * * /usr/bin/curl --silent --compressed https://blockchain.info/ticker > cron_job_btc.log

完成。该任务计划将每天运行一次。

## 尾

Windows操作系统上，POST请求稍有不同，具体见该[Gist代码片段](https://gist.github.com/lyonsun/cda807ad2dd949610dc6). 另外，Windows上面创建任务计划时，一定要注意在Action里面填写参数及启动文件夹输入框。否则，Vista等要求UAC的系统版本里面，可能任务计划执行不了。


