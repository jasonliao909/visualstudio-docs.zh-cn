---
title: "\"URL 选取器\"对话框 (SharePoint开发) "
description: 了解"URL 选取器"对话框，该对话框允许用户选择位于其项目或运行 SharePoint 的本地服务器上的文件。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.VWD.URLPicker
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, URL picker
- SharePoint development in Visual Studio, designer
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 31cf65b473c7053dabe2f2044992fa5e66eed2a83be871bc3134f89b4a7d30d0
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121367390"
---
# <a name="url-picker-dialog-box-sharepoint-development-in-visual-studio"></a>"URL 选取器" (SharePoint中开发Visual Studio) 
  在“URL 选取器”对话框中，您可以选择文件，如位于项目中或运行 SharePoint 的本地服务器上的母版页文件或图像文件。

 在能够选择某个文件以设置属性时，将会显示该对话框。 可以通过在"属性"窗口中选择"移动设计器 (ASP.NET ![旁边的](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")省略号) 打开 **此** 对话框。 在设计器的"源"视图中为某些属性赋值时，省略号按钮也显示为 IntelliSense提示符。

## <a name="uielement-list"></a>UIElement 列表
 **Project文件夹** 显示项目或运行 SharePoint 的本地服务器上定义的文件夹SharePoint。 选择展开按钮可显示子文件夹。

 展开 **"Project"** 节点以选择项目中的文件。 若要在对话框中显示为可选项，项目中的文件必须满足以下条件：

- 该文件必须包含在映射文件夹中。

- 必须将文件添加到解决方案包。

- 该文件不能位于另一个项目中。

  如果要引用不符合这些条件的文件，必须手动输入文件的路径。

  展开 **"** 服务器"节点，选择位于运行 SharePoint 的本地服务器上的文件。 若要在对话框中显示为可选项，这些文件必须满足以下条件：

- 该文件必须位于以下映射文件夹之一：图像、布局或 **ControlTemplates**。  

- 该文件不能位于SharePoint数据库中。

  如果要引用不符合这些条件的文件，必须手动输入文件的路径。

  **文件夹的内容** 显示所选文件夹中的文件列表。 选择文件，然后选择"确定 **"** 按钮以关闭对话框，并将所选内容发送到调用它的进程。

  **类型的文件** 允许你从适合所执行任务的文件列表中选择。

## <a name="see-also"></a>另请参阅
- [为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)
- [为 SharePoint 创建 Web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)
- [为 Web 部件或应用程序页创建可重用控件](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)
