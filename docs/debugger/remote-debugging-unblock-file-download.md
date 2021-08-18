---
title: 取消阻止远程工具下载
description: 取消阻止在 Windows Server 上下载远程工具；由于默认的 IE 安全设置，此类下载可能很耗时。
ms.custom: SEO-VS-2020
ms.date: 07/19/2018
ms.topic: troubleshooting
helpviewer_keywords:
- remote debugging, unblock download
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 8ec0b81a6e97faf6a3dae42ea90a66cb62fb57c7
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122153792"
---
# <a name="how-to-unblock-the-download-of-the-remote-tools-on-windows-server"></a>如何：取消阻止在 Windows Server 上下载远程工具

Windows Server 上 Internet Explorer 中的默认安全设置可能会使下载组件（如远程工具）变得很耗时。

* Internet Explorer 上启用了增强的安全配置，除非显式允许包含资源的域（即受信任域），否则它会阻止你打开网站和访问 Web 资源。 尽管可禁用此设置，但建议不要这样做，因为这可能会带来安全风险。

* 在 Windows Server 2016 上，“Internet 选项” > “安全性” > “Internet” > “自定义级别” > “下载”中的默认设置也会禁用文件下载    。 如果选择直接在 Windows Server 上下载远程工具，则必须启用文件下载。

若要在 Windows Server 上下载工具，建议执行以下操作之一：

* 在另一台计算机（例如运行 Visual Studio 的计算机）上下载远程工具，然后将 .exe 文件复制到 Windows Server。

* 从 Visual Studio 计算机上的[文件共享](../debugger/remote-debugging.md#fileshare_msvsmon)运行远程调试器。

* 直接在 Windows Server 上下载远程工具，并接受提示以添加受信任的站点。 新式网站通常包含许多第三方资源，这可能导致出现很多提示。 而且，可能需要手动添加任何重定向的链接。 开始下载之前，可以选择添加一些受信任的站点。 转到“Internet 选项”>“安全性”>“受信任的站点”>“站点”，然后添加以下站点。

  * visualstudio.microsoft.com
  * download.visualstudio.microsoft.com
  * about:blank

  对于 my.visualstudio.com 上较早版本的调试程序，请添加下列附加站点来确保登录成功：

  * microsoft.com
  * go.microsoft.com
  * download.microsoft.com
  * my.visualstudio.com
  * login.microsoftonline.com
  * login.live.com
  * secure.aadcdn.microsoftonline-p.com
  * msft.sts.microsoft.com
  * auth.gfx.ms
  * app.vssps.visualstudio.com
  * vlscppe.microsoft.com
  * query.prod.cms.rt.microsoft.com

    如果选择在下载远程工具时添加这些域，请在出现提示时选择“添加”。

    ![“已阻止内容”对话框](../debugger/media/remotedbg-blocked-content.png)

    下载软件时，会收到授权加载各种网站脚本和资源的请求。 建议在 my.visualstudio.com 上添加其他域，以确保登录成功。