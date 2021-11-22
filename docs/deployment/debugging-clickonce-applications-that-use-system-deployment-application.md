---
title: 调试使用 System.Deployment.Application 的 ClickOnce 应用
description: 了解如何通过访问 System.Deployment.Application 提供的部署对象模型来使用和自定义高级 ClickOnce 部署功能。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, debugging
- debugging, ClickOnce applications
- debugging, System.Deployment
- deploying applications [ClickOnce], debugging
ms.assetid: 86f31948-2ca8-47c0-8e8b-c2b817bbf79f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: d91b59b6f4eb86c905fcddd28dc5298b1a18f761
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664875"
---
# <a name="debug-clickonce-applications-that-use-systemdeploymentapplication"></a>调试使用 System.Deployment.Application 的 ClickOnce 应用程序
在 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] 中，通过 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署可以配置应用程序的更新方式。 但是，如果你需要使用和自定义高级 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署功能，将需要访问 <xref:System.Deployment.Application> 提供的部署对象模型。 可以将 <xref:System.Deployment.Application> API 用于高级项目，例如：

- 在应用程序中创建“立即更新”选项

- 有条件的、按需下载各种应用程序组件

- 直接集成到应用程序中的更新

- 确保客户端应用程序始终是最新的

  由于 <xref:System.Deployment.Application> API 仅在使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 技术部署应用程序时工作，因此对其进行调试的唯一方法是使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署应用程序、附加到应用程序，然后对其进行调试。 可能会很难提前附加调试器，因为此代码通常在应用程序启动时运行，并在可以附加调试器之前执行。 解决方法是在更新检查代码或按需代码之前添加中断（或者对 Visual Basic 项目添加暂停）。

  建议的调试技术如下所示：

1. 在开始之前，请确保已存档符号 (.pdb) 和源文件。

2. 部署应用程序的版本 1。

3. 创建新的空白解决方案。 在“文件”菜单中，单击“新建”，然后单击“项目”。 在“新建项目”对话框中，打开“其他项目类型”节点，然后选择“Visual Studio 解决方案”文件夹  。 在“模板”窗格中，选择“空白解决方案” 。

4. 将存档的源位置添加到该新解决方案的属性中。 在“解决方案资源管理器”中，右击解决方案节点，然后单击“属性”。  在“属性页面”对话框中，选择“调试源文件”，然后添加存档源文件的目录。  否则，调试器会找到过期的源文件，因为源文件路径记录在 .pdb 文件中。 如果调试器使用过期的源文件，则会看到一条消息提示源不匹配。

5. 确保调试器可以找到 .pdb 文件。 如果已使用应用程序部署这些文件，那么调试程序会自动找到它们。 它始终首先显示在问题中的程序集旁边。 否则，将需要将存档路径添加到 Symbol file (.pdb) 位置（若要访问该选项，请从“工具”菜单单击“选项”，然后打开“正在调试”节点并单击“符号”）。   

6. 调试 `CheckForUpdate` 和 `Download`/`Update` 方法调用之间发生的情况。

    例如，更新代码可能如下所示：

   ```vb
       Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
           If My.Application.Deployment.IsNetworkDeployed Then

               If (My.Application.Deployment.CheckForUpdate()) Then

                   My.Application.Deployment.Update()
                   Application.Restart()

               End If

           End If
       End Sub
   ```

7. 部署版本 2。

8. 在下载版本 2 的更新时，尝试将调试程序附加到版本 1 应用程序。 或者，可以使用 `System.Diagnostics.Debugger.Break` 方法或直接使用 Visual Basic 中的 `Stop`。 当然，不应将这些方法调用保留在生产代码中。

    例如，假设你正在部署 Windows 窗体应用程序，并拥有适用于该方法的包含更新逻辑的事件处理程序。 若要对此进行调试，只需在按下按钮前进行附加，然后设置断点（确保打开相应的存档文件并在此处设置断点）。

   仅在部署应用程序时使用 <xref:System.Deployment.Application.ApplicationDeployment.IsNetworkDeployed%2A> 属性调用 <xref:System.Deployment.Application> API；不会在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中进行调试时调用 API。

## <a name="see-also"></a>另请参阅
- <xref:System.Deployment.Application>