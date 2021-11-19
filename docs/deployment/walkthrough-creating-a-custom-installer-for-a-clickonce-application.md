---
title: 创建 ClickOnce 应用程序的自定义安装程序
description: 了解自定义安装程序如何以无提示方式安装和更新基于 .exe 文件的 ClickOnce 应用程序。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, custom installer
- installer [ClickOnce], custom
- deploying applications [ClickOnce], custom installer
- InPlaceHostingManager [ClickOnce], custom installer
- custom installer [ClickOnce]
ms.assetid: fb222cc5-8aeb-4b94-8c49-b93e342f5f69
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 4d19a93710b2134f7c4878faf8143209bff4e357
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664650"
---
# <a name="walkthrough-create-a-custom-installer-for-a-clickonce-application"></a>演练：创建 ClickOnce 应用程序的自定义安装程序
任何基于 *.exe* 文件的 ClickOnce 应用程序都可以由自定义安装程序进行静默安装和更新。 自定义安装程序可以在安装过程中实现自定义用户体验，包括安全和维护操作的自定义对话框。 若要执行安装操作，自定义安装程序使用 <xref:System.Deployment.Application.InPlaceHostingManager> 类。 本演练演示如何创建一个无提示安装 ClickOnce 应用程序的自定义安装程序。

## <a name="prerequisites"></a>先决条件

### <a name="to-create-a-custom-clickonce-application-installer"></a>创建自定义 ClickOnce 应用程序安装程序

1. 在 ClickOnce 应用程序中，添加对 system.web 和 system 的引用。Windows。域.

2. 向应用程序中添加一个新类并指定任意名称。 本演练使用名称 `MyInstaller`。

3. 将以下 `Imports` 或 `using` 指令添加到新类的顶部。

    ```vb
    Imports System.Deployment.Application
    Imports System.Windows.Forms
    ```

    ```csharp
    using System.Deployment.Application;
    using System.Windows.Forms;
    ```

4. 将以下方法添加到类。

     这些方法调用 <xref:System.Deployment.Application.InPlaceHostingManager> 方法以下载部署清单，断言适当的权限，要求用户提供安装权限，然后将应用程序下载并安装到 ClickOnce 缓存中。 自定义安装程序可以指定 ClickOnce 的应用程序是预信任的，也可以将信任决策推迟到 <xref:System.Deployment.Application.InPlaceHostingManager.AssertApplicationRequirements%2A> 方法调用。 此代码预信任应用程序。

    > [!NOTE]
    > 由预信任分配的权限不能超过自定义安装程序代码的权限。

    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/System.Deployment.Application.InPlaceHostingManager/VB/Form1.vb" id="Snippet1":::
    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/System.Deployment.Application.InPlaceHostingManager/CS/Form1.cs" id="Snippet1":::

5. 若要尝试从代码安装，请调用 `InstallApplication` 方法。 例如，如果你已将类命名为 `MyInstaller` ，则可以 `InstallApplication` 按以下方式调用。

    ```vb
    Dim installer As New MyInstaller()
    installer.InstallApplication("\\myServer\myShare\myApp.application")
    MessageBox.Show("Installer object created.")
    ```

    ```csharp
    MyInstaller installer = new MyInstaller();
    installer.InstallApplication(@"\\myServer\myShare\myApp.application");
    MessageBox.Show("Installer object created.");
    ```

## <a name="next-steps"></a>后续步骤
 ClickOnce 应用程序还可以添加自定义的更新逻辑，包括要在更新过程中显示的自定义用户界面。 有关详细信息，请参阅 <xref:System.Deployment.Application.UpdateCheckInfo>。 ClickOnce 应用程序还可以通过使用元素来取消标准 "开始"菜单条目、快捷方式和 "添加或删除程序" 项 `<customUX>` 。 有关详细信息，请参阅[ \<entryPoint> 元素](../deployment/entrypoint-element-clickonce-application.md)和 <xref:System.Deployment.Application.DownloadApplicationCompletedEventArgs.ShortcutAppId%2A> 。

## <a name="see-also"></a>另请参阅
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)
- [\<entryPoint> 元素](../deployment/entrypoint-element-clickonce-application.md)
