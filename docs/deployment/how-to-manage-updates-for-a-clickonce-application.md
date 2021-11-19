---
title: 管理 ClickOnce 应用程序的更新 | Microsoft Docs
description: 了解用于针对 ClickOnce 应用程序自动或以编程方式检查更新的选项。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- Microsoft.VisualStudio.Publish.ClickOnceProvider.Dialog.Update
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, managing applications
- ClickOnce deployment, updates
- updating data, ClickOnce
- application updates
ms.assetid: a3f23f05-e7f1-4620-b23c-2d68f9643684
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 988fc33a7f8d4f2d535a55fac636340c6dfb93ed
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665162"
---
# <a name="how-to-manage-updates-for-a-clickonce-application"></a>如何：管理 ClickOnce 应用程序的更新
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序可以自动或以编程方式检查更新。 作为开发人员，你可以灵活地指定何时以及如何执行更新检查、是否强制进行更新，以及应用程序应检查更新的位置。

 可以将应用程序配置为在应用程序启动前自动检查是否有更新，或在应用程序启动后按设置的时间间隔进行检查。 此外，还可以指定所需的最低版本；也就是说，如果用户的版本低于所需版本，则会安装更新。

 可以将应用程序配置为基于事件（例如用户请求）以编程方式进行检查更新。 本主题中的“以编程方式检查更新”过程说明了如何编写使用 <xref:System.Deployment.Application.ApplicationDeployment> 类来基于事件进行检查更新的代码。

 还可以从一个位置部署应用程序，并从另一个位置进行更新。 请参阅“指定不同的更新位置”过程。

 有关详细信息，请参阅[选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)。

 更新行为是在“应用程序更新”对话框中管理的，可以从“项目设计器”的“发布”页进行访问  。

### <a name="to-check-for-updates-before-the-application-starts"></a>在应用程序启动前检查更新

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击“更新”按钮以打开“应用程序更新”对话框 。

4. 在“应用程序更新”对话框中，确保已选中“应用程序应该检查更新”复选框 。

5. 在“选择应用程序何时应该检查更新”部分中，选择“应用程序启动前” 。 这可确保连接到网络的用户能始终运行包含最新更新的应用程序。

### <a name="to-check-for-updates-in-the-background-after-the-application-starts"></a>在应用程序启动后在后台检查更新

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击“更新”按钮以打开“应用程序更新”对话框 。

4. 在“应用程序更新”对话框中，确保已选中“应用程序应该检查更新”复选框 。

5. 在“选择应用程序何时应该检查更新”部分中，选择“应用程序启动后” 。 这样一来，应用程序将以更快的速度启动，然后它将在后台进行检查更新，并且仅在有可用更新时通知用户。 安装后，更新只有在应用程序重启之后才会生效。

6. 在“指定应用程序应进行检查更新的频率”部分中，选择“每当应用程序运行时检查”（默认选项），或选择“检查间隔”并输入数字和时间间隔  。

### <a name="to-specify-a-minimum-required-version-for-the-application"></a>指定所需的应用程序的最低版本

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击“更新”按钮以打开“应用程序更新”对话框 。

4. 在“应用程序更新”对话框中，确保已选中“应用程序应该检查更新”复选框 。

5. 选中“指定所需的此应用程序的最低版本”复选框，然后输入应用程序的“主要版本”、“次要版本”、“内部版本”和“修订版本”号    。

### <a name="to-specify-a-different-update-location"></a>指定不同的更新位置

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击“更新”按钮以打开“应用程序更新”对话框 。

4. 在“应用程序更新”对话框中，确保已选中“应用程序应该检查更新”复选框 。

5. 在“更新位置”字段中，使用完全限定的 URL 输入更新位置（格式为 *http://Hostname/ApplicationName* ）或使用 UNC 路径输入更新位置（格式为 *\\ \Server\ApplicationName*），或者单击“浏览”按钮以浏览更新位置 。

### <a name="to-check-for-updates-programmatically"></a>以编程方式检查更新

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击“更新”按钮以打开“应用程序更新”对话框 。

4. 在“应用程序更新”对话框中，确保已取消选中“应用程序应该检查更新”复选框 。 （可选：可以选中此复选框以编程方式检查更新，也可以让 ClickOnce 运行时自动检查更新。）

5. 在“更新位置”字段中，使用完全限定的 URL 输入更新位置（格式为 *http://Hostname/ApplicationName* ）或使用 UNC 路径输入更新位置（格式为 *\\ \Server\ApplicationName*），或者单击“浏览”按钮以浏览更新位置 。 应用程序将在更新位置查找自身的更新版本。

6. 在 Windows 窗体上创建一个按钮、菜单项或其他用户界面项，供用户用来执行检查更新。 从该项的事件处理程序中，调用方法来检查和安装更新。 有关此方法的 Visual Basic 和 Visual C# 代码示例，请参阅[操作说明：使用 ClickOnce 部署 API 以编程方式检查应用程序更新](../deployment/how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api.md)。

7. 生成你的应用程序。

## <a name="see-also"></a>另请参阅
- <xref:System.Deployment.Application.ApplicationDeployment>
- [“应用程序更新”对话框](/previous-versions/visualstudio/visual-studio-2010/axw1fa38(v=vs.100))
- [选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
- [如何：使用 ClickOnce 部署 API 以编程方式检查应用程序更新](../deployment/how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api.md)
