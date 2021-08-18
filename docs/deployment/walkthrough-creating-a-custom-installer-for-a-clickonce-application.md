---
title: 为应用程序创建自定义ClickOnce安装程序
description: 了解自定义安装程序如何基于 ClickOnce 文件以无提示方式安装和更新.exe应用程序。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122133596"
---
# <a name="walkthrough-create-a-custom-installer-for-a-clickonce-application"></a>演练：为应用程序创建ClickOnce安装程序
自定义ClickOnce可以无提示.exe文件安装并更新基于该文件的任何应用程序。 自定义安装程序可以在安装过程中实现自定义用户体验，包括用于安全和维护操作自定义对话框。 为了执行安装操作，自定义安装程序使用 <xref:System.Deployment.Application.InPlaceHostingManager> 类。 本演练演示如何创建自定义安装程序，以无提示方式ClickOnce应用程序。

## <a name="prerequisites"></a>必备条件

### <a name="to-create-a-custom-clickonce-application-installer"></a>创建自定义应用程序ClickOnce安装程序

1. 在 ClickOnce应用程序中，添加对 System.Deployment 和 System 的引用。Windows。形式。

2. 将新类添加到应用程序并指定任何名称。 本演练使用名称 `MyInstaller`。

3. 将以下 `Imports` 或 `using` 指令添加到新类的顶部。

    ```vb
    Imports System.Deployment.Application
    Imports System.Windows.Forms
    ```

    ```csharp
    using System.Deployment.Application;
    using System.Windows.Forms;
    ```

4. 将以下方法添加到 类。

     这些方法调用方法下载部署清单、断言适当的权限、请求用户安装权限，然后将应用程序下载并安装到 ClickOnce <xref:System.Deployment.Application.InPlaceHostingManager> 缓存中。 自定义安装程序可以指定ClickOnce应用程序是预先受信任的，也可以将信任决策延迟到 <xref:System.Deployment.Application.InPlaceHostingManager.AssertApplicationRequirements%2A> 方法调用。 此代码预先信任应用程序。

    > [!NOTE]
    > 通过预先信任分配的权限不能超过自定义安装程序代码的权限。

    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/System.Deployment.Application.InPlaceHostingManager/VB/Form1.vb" id="Snippet1":::
    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/System.Deployment.Application.InPlaceHostingManager/CS/Form1.cs" id="Snippet1":::

5. 若要尝试从代码中安装，请调用 `InstallApplication` 方法。 例如，如果命名类 `MyInstaller` ，可以 `InstallApplication` 按照以下方式调用 。

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
 一ClickOnce应用程序还可以添加自定义更新逻辑，包括在更新过程中要显示的自定义用户界面。 有关详细信息，请参阅 <xref:System.Deployment.Application.UpdateCheckInfo>。 一ClickOnce应用程序还可使用 元素取消标准"开始"菜单、快捷方式和"添加或删除程序" `<customUX>` 条目。 有关详细信息，请参阅[ \<entryPoint> 元素和](../deployment/entrypoint-element-clickonce-application.md) <xref:System.Deployment.Application.DownloadApplicationCompletedEventArgs.ShortcutAppId%2A> 。

## <a name="see-also"></a>请参阅
- [ClickOnce应用程序清单](../deployment/clickonce-application-manifest.md)
- [\<entryPoint> 元素](../deployment/entrypoint-element-clickonce-application.md)
