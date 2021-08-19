---
title: '发布向导 (Office在 Visual Studio) '
description: 了解如何使用发布向导将解决方案文件复制到指定位置、创建清单文件，以及如何在 Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.ProjectProperties.PublishWizard
- VST.PublishWizard.Publish.2007System
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ClickOnce deployment [Office development in Visual Studio], Publish Wizard
- deploying applications [Office development in Visual Studio], Publish Wizard
- Office applications [Office development in Visual Studio], Publish Wizard
- Publish Wizard, Office solutions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 5078179f4dbe0ba65ada1ec0dee6e3aeeefbc094
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122099537"
---
# <a name="publish-wizard-office-development-in-visual-studio"></a>发布向导 (Office在 Visual Studio) 
  使用 **发布向导** 将解决方案文件复制到指定位置、创建清单文件以及创建安装程序。

 若要访问此向导，请选择"生成 **"菜单** 上的"发布 *SolutionName"。*  还可以从 访问 **发布向导****解决方案资源管理器。** 打开项目节点的快捷菜单，然后选择"发布 **"。**

 以下每个部分都介绍了向导的页面。

## <a name="where-do-you-want-to-publish-the-application"></a>想要在何处发布应用程序？
 **指定发布此应用程序的位置** 必填。 发布位置是发布向导从生成中复制解决方案文件（如清单、程序集、临时证书和其他文件）的目录。 你必须对此目录具有写权限。

 键入位置作为磁盘路径、文件共享、FTP 站点或网站 URL，或单击"浏览"按钮浏览位置。 路径可以采用以下格式：

- 标准格式的相对或绝对Windows，例如 *C：\Deploy\MyApplication* 或 *\MyApplication*。

- UNC 命名路径 (通用) 约定，如 *\\ \ServerName\MyApplication \\*。

- 网站的 URL，例如 `http://www.contoso.com/MyApplication` 。

  默认情况下，如果已安装 IIS，则发布位置为 ;如果未安装 *http://localhost/projectname/* IIS，则发布位置为 publish\ 目录。

> [!NOTE]
> 如果目标计算机在 Vista 上运行，则Windows注意事项。 你必须是 Vista 计算机上Windows才能使用本地发布选项。 此外，无论是否安装了 *\\* IIS，默认位置始终是发布目录。

## <a name="what-is-the-default-installation-path-on-end-user-computers"></a>最终用户计算机上的默认安装路径是什么？
 安装路径是可选的。 如果愿意，可以稍后设置安装路径。 有关详细信息，[请参阅如何：更改](/previous-versions/bb608626(v=vs.110))解决方案 的Office路径。

 安装路径是最终用户将安装自定义项的目录。 这也是解决方案将用于检查更新的路径。 发布 **向导** 不会将解决方案部署到此位置，除非路径与在上一页上的"指定发布此应用程序的位置"框中输入的路径相同。

 **从网站** 指定最终用户安装解决方案时将遵循的 URL。

 **从 UNC 路径或文件共享** 指定最终用户将遵循的 UNC 路径来安装解决方案。

 **从 CD-ROM 或 DVD-ROM** 此选项不需要安装路径。

 Visual Studio不会消耗 CD 或 DVD。 必须手动将输出复制到 CD 或 DVD。

## <a name="see-also"></a>请参阅
- [使用 Office 部署 ClickOnce](../vsto/deploying-an-office-solution-by-using-clickonce.md)
- [发布页，Project设计器&#40;Office中开发Visual Studio&#41;](../vsto/publish-page-project-designer-office-development-in-visual-studio.md)
- [部署Office解决方案](../vsto/deploying-an-office-solution.md)