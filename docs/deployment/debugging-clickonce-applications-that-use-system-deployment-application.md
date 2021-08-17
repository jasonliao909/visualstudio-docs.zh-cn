---
title: 调试ClickOnce System.Deployment.Application 的应用
description: 了解如何通过访问 System.Deployment.Application ClickOnce部署对象模型来使用和自定义高级部署功能。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122080658"
---
# <a name="debug-clickonce-applications-that-use-systemdeploymentapplication"></a>调试使用 System.Deployment.Application 的 ClickOnce 应用程序
在 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 中，部署允许你配置应用程序的更新方式。 但是，如果需要使用和自定义高级部署功能，则需要访问 提供的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署对象模型 <xref:System.Deployment.Application> 。 可以将 API <xref:System.Deployment.Application> 用于高级任务，例如：

- 在应用程序中创建"现在更新"选项

- 各种应用程序组件的条件按需下载

- 直接集成到应用程序中的更新

- 保证客户端应用程序始终为最新

  由于 API 仅在使用技术部署应用程序时工作，因此调试它们的唯一方法就是使用 部署应用程序，附加到该应用程序， <xref:System.Deployment.Application> [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 然后对其进行调试。 可能很难尽早附加调试器，因为此代码通常在应用程序启动和执行时运行，然后才能附加调试器。 一种解决方案是在更新检查 (或按需Visual Basic项目) 中断或停止。

  建议的调试方法如下：

1. 在启动之前，请确保将 (.pdb) 和源文件存档。

2. 部署应用程序版本 1。

3. 创建新的空白解决方案。 在“文件”菜单中，单击“新建”，然后单击“项目”。 在"**新建Project"** 对话框中，打开"其他Project **类型**"节点，然后选择"Visual Studio **解决方案**"文件夹。 在"**模板"窗格中**，选择"**空白解决方案"。**

4. 将存档的源位置添加到此新解决方案的属性。 在 **解决方案资源管理器** 中，右键单击解决方案节点，然后单击"属性 **"。** 在" **属性页** "对话框中，选择" **调试源文件"，** 然后添加已存档源代码的目录。 否则，调试器将查找过期的源文件，因为源文件路径记录在 .pdb 文件中。 如果调试器使用过期的源文件，则会看到一条消息，指出源不匹配。

5. 确保调试器可以找到 *.pdb* 文件。 如果已将它们与应用程序一起部署，调试器会自动查找它们。 它始终首先在有关程序集旁边查找。 否则，需要将存档路径添加到符号文件 **(.pdb)** 位置 (以访问此选项，在"工具"菜单中，单击"选项"，然后打开"调试"节点，然后单击"符号) "。  

6. 调试 和 方法 `CheckForUpdate` 调用 `Download` / `Update` 之间发生的情况。

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

8. 尝试在下载版本 2 的更新时将调试器附加到版本 1 应用程序。 或者，可以使用 方法 `System.Diagnostics.Debugger.Break` ，也可以直接 `Stop` 在 Visual Basic。 当然，不应在生产代码中保留这些方法调用。

    例如，假设要开发 Windows Forms 应用程序，并且此方法具有包含更新逻辑的事件处理程序。 若要调试此操作，只需在按下按钮之前附加，然后设置断点 (确保打开相应的存档文件，并将断点设置为) 。

   仅在部署应用程序时使用 属性调用 API;不应在 中调试 <xref:System.Deployment.Application.ApplicationDeployment.IsNetworkDeployed%2A> <xref:System.Deployment.Application> 期间调用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] API。

## <a name="see-also"></a>请参阅
- <xref:System.Deployment.Application>