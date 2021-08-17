---
title: 管理应用程序ClickOnce的更新|Microsoft Docs
description: 了解自动或编程方式检查应用程序更新ClickOnce选项。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122089974"
---
# <a name="how-to-manage-updates-for-a-clickonce-application"></a>如何：管理 ClickOnce 应用程序的更新
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序可以自动或以编程方式检查更新。 作为开发人员，你可以灵活地指定何时以及如何执行更新检查、更新是否是必需的以及应用程序应在何处检查更新。

 可以将应用程序配置为在应用程序启动之前自动检查更新，或在应用程序启动后按设置的间隔检查更新。 此外，可以指定所需的最低版本;也就是说，如果用户的版本低于所需版本，则安装更新。

 可以将应用程序配置为基于事件（如用户请求）以编程方式检查更新。 本主题中的"以编程方式检查更新"过程演示了如何编写代码，该代码使用 类根据事件 <xref:System.Deployment.Application.ApplicationDeployment> 检查更新。

 还可以从一个位置部署应用程序，然后从另一个位置进行更新。 请参阅过程"指定其他更新位置"。

 有关详细信息，请参阅[选择更新ClickOnce策略](../deployment/choosing-a-clickonce-update-strategy.md)。

 更新行为在"**应用程序更新"** 对话框中进行管理，可从设计器的"发布"页 **Project操作。**

### <a name="to-check-for-updates-before-the-application-starts"></a>在应用程序启动之前检查更新

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击" **更新** "按钮以打开 **"应用程序更新** "对话框。

4. 在 **"应用程序更新** "对话框中，确保选中"应用程序 **应检查** 更新"复选框。

5. 在"**选择应用程序应检查更新的时间"** 部分中，选择"**应用程序启动之前"。** 这可确保连接到网络的用户始终使用最新更新运行应用程序。

### <a name="to-check-for-updates-in-the-background-after-the-application-starts"></a>在应用程序启动后在后台检查更新

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击" **更新** "按钮以打开 **"应用程序更新** "对话框。

4. 在 **"应用程序更新** "对话框中，确保选中"应用程序 **应检查更新"** 复选框。

5. 在"**选择应用程序何时应检查更新"** 部分中，选择 **"应用程序启动后"。** 应用程序将这样启动更快，然后在后台检查更新，并且仅在更新可用时通知用户。 安装后，在重启应用程序之前，更新不会生效。

6. 在"**指定应用程序** 检查更新的频率"部分中，选择"每次运行应用程序时检查 **" (默认**) 或"检查每个"并输入数字和时间间隔。 

### <a name="to-specify-a-minimum-required-version-for-the-application"></a>指定应用程序所需的最低版本

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击" **更新** "按钮以打开 **"应用程序更新** "对话框。

4. 在 **"应用程序更新** "对话框中，确保选中"应用程序 **应检查** 更新"复选框。

5. 选中"**指定此应用程序的最低所需** 版本"复选框，然后输入应用程序的"主要"、次要版本、"生成"和"修订号"。  

### <a name="to-specify-a-different-update-location"></a>指定其他更新位置

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击" **更新** "按钮以打开 **"应用程序更新** "对话框。

4. 在 **"应用程序更新** "对话框中，确保选中"应用程序 **应检查** 更新"复选框。

5. 在"更新 **位置**"字段中，使用格式 为 的完全限定 URL 输入更新位置，或输入格式为 *http://Hostname/ApplicationName* *\\ \Server\ApplicationName* 的 UNC路径，或单击"浏览"按钮浏览更新位置。

### <a name="to-check-for-updates-programmatically"></a>以编程方式检查更新

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击" **更新** "按钮以打开 **"应用程序更新** "对话框。

4. 在 **"应用程序更新** "对话框中，确保"应用程序 **应检查更新"** 复选框已清除。  (，可以选择此复选框以编程方式检查更新，还允许运行时ClickOnce自动检查更新。) 

5. 在"更新 **位置**"字段中，使用格式 为 的完全限定 URL 输入更新位置，或输入格式为 *http://Hostname/ApplicationName* *\\ \Server\ApplicationName* 的 UNC路径，或单击"浏览"按钮浏览更新位置。 更新位置是应用程序查找自身更新版本的位置。

6. 在窗体上创建按钮、菜单项或其他用户界面Windows用户将选择该窗体来检查更新。 从该项的事件处理程序中，调用 方法来检查和安装更新。 可以在如何：使用 Visual Basic API 以编程方式检查应用程序更新中查找此类方法的 Visual Basic 和 Visual C#[代码ClickOnce示例](../deployment/how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api.md)。

7. 生成应用程序。

## <a name="see-also"></a>请参阅
- <xref:System.Deployment.Application.ApplicationDeployment>
- ["应用程序更新"对话框](/previous-versions/visualstudio/visual-studio-2010/axw1fa38(v=vs.100))
- [选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布ClickOnce发布应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
- [如何：使用部署 API 以编程方式ClickOnce更新](../deployment/how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api.md)
