---
title: 部署到本地文件夹
description: 了解如何使用“发布”工具将 ASP.NET、ASP.NET Core、.NET Core 和 Python 应用从 Visual Studio 发布到文件夹。
ms.custom: SEO-VS-2020
ms.date: 09/23/2021
ms.topic: quickstart
helpviewer_keywords:
- deployment, local folder
ms.assetid: adb461c4-812a-4b8c-b2ab-96002379f6a9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: c3df338150c4cf4f72aec310084c32f3db16bcd8
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128429064"
---
# <a name="deploy-an-app-to-a-folder-using-visual-studio"></a>使用 Visual Studio 将应用部署到文件夹

可以使用“发布”工具将 ASP.NET、ASP.NET Core、.NET Core 和 Python 应用从 Visual Studio 发布到文件夹。 对于 Node.js，支持这些步骤但用户界面不同。

[!INCLUDE [quickstart-prereqs](includes/quickstart-prereqs.md)]
::: moniker range=">=vs-2017"
> [!NOTE]
> 如果需要将 Windows 桌面应用程序发布到文件夹，请参阅[使用 ClickOnce 部署 .NET Windows 桌面应用](quickstart-deploy-using-clickonce-folder.md)、[使用 ClickOnce 部署 .NET Framework Windows 桌面应用](how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。 对于 C++/CLR，请参阅[使用 ClickOnce 部署本机应用](/cpp/windows/clickonce-deployment-for-visual-cpp-applications)，或者对于 C/C++，请参阅[使用安装项目部署本机应用](/cpp/windows/walkthrough-deploying-a-visual-cpp-application-by-using-a-setup-project)。

::: moniker-end

::: moniker range=">=vs-2019"
> [!NOTE]
> 如果你需要将 .NET Core 3.1 或更高版本的 Windows 桌面应用程序发布到文件夹，请参阅[使用 ClickOnce 部署 .NET Windows 应用程序](quickstart-deploy-using-clickonce-folder.md)。

::: moniker-end

## <a name="deploy-to-a-local-folder"></a>部署到本地文件夹

1. 在解决方案资源管理器中，右键单击该项目并选择“发布”（或使用“生成” > “发布”菜单项）  。

    ![解决方案资源管理器中项目上下文菜单上的“发布”命令](../deployment/media/quickstart-publish.png "选择发布")

1. 如果先前配置了任何发布配置文件，则“发布”窗口会显示。 选择“新建”。

1. 在“发布”窗口中，选择“文件夹”。

   ![选择文件夹作为发布目标](../deployment/media/quickstart-publish-folder-new.png "选择文件夹")

   ::: moniker range=">=vs-2019"

   如果要部署 .NET Core 3.1 或更高版本的 Windows 应用程序，则可能需要在“特定目标”窗口中选择“文件夹” 。

   ![选择文件夹作为特定目标](../deployment/media/quickstart-publish-folder-targets.png "选择特定目标")

   如果你希望使用 ClickOnce 发布 .NET Core 3.1 或更高版本的 Windows 应用程序，请参阅[使用 ClickOnce 部署 .NET Windows 应用程序](quickstart-deploy-using-clickonce-folder.md)。
   ::: moniker-end

1. 输入路径，或选择“浏览”以指定文件夹。

   ![指定文件夹的路径](../deployment/media/quickstart-publish-folder-path.png "选择文件夹")

   ::: moniker range=">=vs-2019"
   单击“完成”保存配置文件。

   ![显示配置文件摘要的“发布”属性窗格](../deployment/media/quickstart-publish-folder-summary.png)
   ::: moniker-end

1. 选择“发布”。 Visual Studio 将生成项目并将其发布到指定文件夹。

   ::: moniker range="vs-2017"
   项目属性“发布”窗格出现，显示配置文件摘要。

   ![显示配置文件摘要的“发布”属性窗格](../deployment/media/quickstart-publish-folder-summary.png)
   ::: moniker-end

1. 要配置部署设置，请选择发布文件摘要中的“编辑”并选择“设置”选项卡 。

   你看到的设置取决于你的应用程序类型。 下图显示 ASP.NET Core 应用的示例设置。

    ![配置文件设置](../deployment/media/quickstart-profile-settings.png "配置文件设置")

    有关使用 .NET 选择设置的更多帮助，请参阅以下内容：

    - [依赖于框架的部署与自包含部署](/dotnet/core/deploying/)
    - [目标运行时标识符（可移植 RID 等）](/dotnet/core/rid-catalog)
    - [调试和发布配置](../ide/understanding-build-configurations.md)

1. 配置选项（如是部署“调试”配置还是“发布”配置），然后选择“保存”。

1. 若要重新发布，请选择“发布”。

可按照任何喜欢的方式部署已发布的文件。 例如，可以使用简单的复制命令将其打包为 .zip 文件，或者使用选择的任何安装包进行部署。

## <a name="next-steps"></a>后续步骤

对于 .NET 应用：

- [使用发布工具部署 .NET Core 应用程序](/dotnet/core/deploying/deploy-with-vs)
- [.NET Core 应用程序发布（依赖于框架的部署与自包含部署）](/dotnet/core/deploying/)
- [部署 .NET Framework 和应用程序](/dotnet/framework/deployment/)
::: moniker range=">=vs-2019"
- [使用 ClickOnce 部署 .NET Windows 应用程序](quickstart-deploy-using-clickonce-folder.md)。
 ::: moniker-end
