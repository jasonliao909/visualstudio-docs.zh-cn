---
title: 如何：设置 SharePoint 部署命令| Microsoft Docs
description: 了解如何通过设置 SharePoint 部署前和部署后命令来自定义部署过程。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, deploying
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: dc3ad57702b7063edd0c03f305a8ffc3722eebd6
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665279"
---
# <a name="how-to-set-sharepoint-deployment-commands"></a>如何：设置 SharePoint 部署命令
  可以通过设置部署前和部署后命令来自定义部署过程。 当你从 Visual Studio 调试 SharePoint 解决方案时，这些命令会在其他部署操作之前和之后运行。

### <a name="to-add-a-pre-deployment-command"></a>添加部署前命令

1. 在菜单栏上，依次选择“项目” > “\<*ProjectName*> 属性” 。

2. 选择“SharePoint”选项卡。

3. 在“部署前命令行”文本框中，输入 MS-DOS 或 MSBuild 命令自定义此步骤。

     例如，若要在部署完成之前列出目录内容，请输入 dir。

### <a name="to-add-a-post-deployment-command"></a>添加部署后命令

1. 在菜单栏上，依次选择“项目” > “\<*ProjectName*> 属性” 。

2. 选择“SharePoint”选项卡。

3. 在“部署后命令行”文本框中，输入 MS-DOS 或 MSBuild 命令自定义此步骤。

     例如，若要在部署完成之后列出目录内容，请输入 dir。 若要使用 MSBuild 变量从生成目录中复制程序集，请输入 copy $(TargetPath) c:\DeploymentDirectory。

## <a name="see-also"></a>另请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
