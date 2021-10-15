---
title: Visual Studio 工作负荷和组件 ID
titleSuffix: ''
description: 使用工作负载和组件 ID 通过命令行安装 Visual Studio 或指定为 VSIX 清单中的依赖项
keywords: ''
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.date: 10/12/2021
ms.topic: reference
helpviewer_keywords:
- workload ID, Visual Studio
- component ID, Visual Studio
- install Visual Studio, administrator guide
ms.assetid: 34e19ef1-abfb-44fd-aad2-33c5d7874482
ms.prod: visual-studio-windows
ms.technology: vs-installation
open_to_public_contributors: false
ms.openlocfilehash: d5acfc9ac5ffd6491e807049afbd12a53715868d
ms.sourcegitcommit: 8fae163333e22a673fd119e1d2da8a1ebfe0e51a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2021
ms.locfileid: "129969328"
---
# <a name="visual-studio-workload-and-component-ids"></a>Visual Studio 工作负荷和组件 ID

单击下表中的版本名称，查看使用命令行安装 Visual Studio 或指定为 VSIX 清单中的依赖项所需的工作负载和组件 ID。

::: moniker range="vs-2017"

针对[版本 15.9](/visualstudio/releasenotes/vs2017-relnotes/) 而更新

| **版本** | **ID** | **说明** |
| ----------- | ------ | --------------- |
| [Visual&nbsp;Studio Enterprise&nbsp;2017](workload-component-id-vs-enterprise.md?view=vs-2017&preserve-view=true) | Microsoft.VisualStudio.Product.Enterprise | 面向任何规模的团队的工作效率和协作的 Microsoft DevOps 解决方案 |
| [Visual&nbsp;Studio Professional&nbsp;2017](workload-component-id-vs-professional.md?view=vs-2017&preserve-view=true) | Microsoft.VisualStudio.Product.Professional | 面向小团队的开发人员工具和服务 |
| [Visual&nbsp;Studio Community&nbsp;2017](workload-component-id-vs-community.md?view=vs-2017&preserve-view=true) | Microsoft.VisualStudio.Product.Community | 面向学生、开源和个人开发人员的功能完备的免费 IDE |
| [Visual&nbsp;Studio Team&nbsp;Explorer&nbsp;2017](workload-component-id-vs-team-explorer.md?view=vs-2017&preserve-view=true) | Microsoft.VisualStudio.Product.TeamExplorer | 与 Team Foundation Server 和 Azure DevOps Services 交互，不包含 Visual Studio 开发人员工具集 |
| [Visual Studio Desktop Express 2017](workload-component-id-vs-express.md?view=vs-2017&preserve-view=true) | Microsoft.VisualStudio.Product.WDExpress | 通过语法感知代码编辑、源代码管理和工作项管理，生成原生和托管应用，如 WPF、WinForms 和 Win32。 现已支持 C#、Visual Basic 和 Visual C++。 |
| [Visual&nbsp;Studio Build&nbsp;Tools&nbsp;2017](workload-component-id-vs-build-tools.md?view=vs-2017&preserve-view=true) | Microsoft.VisualStudio.Product.BuildTools | 使用 Visual Studio 生成工具，无需借助 Visual Studio IDE，即可生成本机和托管的基于 MSBuild 的应用程序。 这些选项用于安装 Visual C++ 编译器和库、MFC、ATL 以及 C++/CLI 支持。 |
| [Visual&nbsp;Studio Test&nbsp;Agent&nbsp;2017](workload-component-id-vs-test-agent.md?view=vs-2017&preserve-view=true)  | Microsoft.VisualStudio.Product.TestAgent | 支持运行自动测试和远程加载测试 |
| [Visual&nbsp;Studio Test&nbsp;Controller 2017](workload-component-id-vs-test-controller.md?view=vs-2017&preserve-view=true) | Microsoft.VisualStudio.Product.TestController | 将自动测试分发到多台计算机 |
| [Visual&nbsp;Studio Test&nbsp;Professional&nbsp;2017](workload-component-id-vs-test-professional.md?view=vs-2017&preserve-view=true) | Microsoft.VisualStudio.Product.TestProfessional | Visual Studio Test Professional 2017 |
| [Visual&nbsp;Studio Feedback&nbsp;Client&nbsp;2017](workload-component-id-vs-feedback-client.md?view=vs-2017&preserve-view=true) | Microsoft.VisualStudio.Product.FeedbackClient | Visual Studio Feedback Client 2017 |

有关如何使用这些列表的详细信息，请参阅[使用命令行参数安装 Visual Studio 2017](use-command-line-parameters-to-install-visual-studio.md?view=vs-2017&preserve-view=true) 页和[如何：将扩展性项目迁移到 Visual Studio 2017](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md?view=vs-2017&preserve-view=true) 页。

::: moniker-end

::: moniker range="vs-2019"

已针对[版本 16.11](/visualstudio/releases/2019/release-notes/) 进行更新

| **版本** | **ID** | **说明** |
| ----------- | ------ | --------------- |
| [Visual&nbsp;Studio Enterprise&nbsp;2019](workload-component-id-vs-enterprise.md?view=vs-2019&preserve-view=true) | Microsoft.VisualStudio.Product.Enterprise | 面向任何规模的团队的工作效率和协作的 Microsoft DevOps 解决方案 |
| [Visual&nbsp;Studio Professional&nbsp;2019](workload-component-id-vs-professional.md?view=vs-2019&preserve-view=true) | Microsoft.VisualStudio.Product.Professional | 面向小团队的开发人员工具和服务 |
| [Visual&nbsp;Studio Community&nbsp;2019](workload-component-id-vs-community.md?view=vs-2019&preserve-view=true) | Microsoft.VisualStudio.Product.Community | 面向学生、开源和个人开发人员的功能完备的免费 IDE |
| [Visual&nbsp;Studio Team&nbsp;Explorer&nbsp;2019](workload-component-id-vs-team-explorer.md?view=vs-2019&preserve-view=true) | Microsoft.VisualStudio.Product.TeamExplorer | 与 Team Foundation Server 和 Azure DevOps Services 交互，不包含 Visual Studio 开发人员工具集 |
| [Visual&nbsp;Studio 生成&nbsp;工具&nbsp; 2019](workload-component-id-vs-build-tools.md?view=vs-2019&preserve-view=true) | Microsoft.VisualStudio.Product.BuildTools | 使用 Visual Studio 生成工具，无需借助 Visual Studio IDE，即可生成本机和托管的基于 MSBuild 的应用程序。 这些选项用于安装 Visual C++ 编译器和库、MFC、ATL 以及 C++/CLI 支持。 |
| [Visual&nbsp;Studio Test&nbsp;Agent&nbsp;2019](workload-component-id-vs-test-agent.md?view=vs-2019&preserve-view=true)  | Microsoft.VisualStudio.Product.TestAgent | 支持运行自动测试和远程加载测试 |
| [Visual&nbsp;Studio Load&nbsp;Test&nbsp;Controller 2019](workload-component-id-vs-test-controller.md?view=vs-2019&preserve-view=true) | Microsoft.VisualStudio.Product.TestController | 将自动测试分发到多台计算机 |

有关如何使用这些列表的详细信息，请参阅[使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md?view=vs-2019&preserve-view=true) 页和[如何：将扩展性项目迁移到 Visual Studio](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md?view=vs-2019&preserve-view=true) 页面。

> [!NOTE]
> 有关上一个版本的工作负载和组件 ID 的列表，请参阅 [Visual Studio 2017 工作负载和组件 ID](workload-and-component-ids.md?view=vs-2017&preserve-view=true)

::: moniker-end

::: moniker range=">=vs-2022"

| **版本** | **ID** | **说明** |
| ----------- | ------ | --------------- |
| [Visual&nbsp;Studio Enterprise&nbsp;2022](workload-component-id-vs-enterprise.md?view=vs-2022&preserve-view=true) | Microsoft.VisualStudio.Product.Enterprise | 面向任何规模的团队的工作效率和协作的 Microsoft DevOps 解决方案 |
| [Visual&nbsp;Studio Professional&nbsp;2022](workload-component-id-vs-professional.md?view=vs-2022&preserve-view=true) | Microsoft.VisualStudio.Product.Professional | 面向小团队的开发人员工具和服务 |
| [Visual&nbsp;Studio Community&nbsp;2022](workload-component-id-vs-community.md?view=vs-2022&preserve-view=true) | Microsoft.VisualStudio.Product.Community | 面向学生、开源和个人开发人员的功能完备的免费 IDE |
| [Visual&nbsp;Studio Team&nbsp;Explorer&nbsp;2022](workload-component-id-vs-team-explorer.md?view=vs-2022&preserve-view=true) | Microsoft.VisualStudio.Product.TeamExplorer | 与 Team Foundation Server 和 Azure DevOps Services 交互，不包含 Visual Studio 开发人员工具集 |
| [Visual&nbsp;Studio Build&nbsp;Tools&nbsp;2022](workload-component-id-vs-build-tools.md?view=vs-2022&preserve-view=true) | Microsoft.VisualStudio.Product.BuildTools | 使用 Visual Studio 生成工具，无需借助 Visual Studio IDE，即可生成本机和托管的基于 MSBuild 的应用程序。 这些选项用于安装 Visual C++ 编译器和库、MFC、ATL 以及 C++/CLI 支持。 |
| [Visual&nbsp;Studio Test&nbsp;Agent&nbsp;2022](workload-component-id-vs-test-agent.md?view=vs-2022&preserve-view=true)  | Microsoft.VisualStudio.Product.TestAgent | 支持运行自动测试和远程加载测试 |
| [Visual&nbsp;Studio Load&nbsp;Test&nbsp;Controller 2022](workload-component-id-vs-test-controller.md?view=vs-2022&preserve-view=true) | Microsoft.VisualStudio.Product.TestController | 将自动测试分发到多台计算机 |

有关如何使用这些列表的详细信息，请参阅[使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md?view=vs-2022&preserve-view=true) 页和[更新 Visual Studio 2022 的 Visual Studio 扩展](../extensibility/migration/update-visual-studio-extension.md)页。

> [!NOTE]
> 有关上一个版本的工作负载和组件 ID 的列表，请参阅 [Visual Studio 2019 工作负载和组件 ID](workload-and-component-ids.md?view=vs-2019&preserve-view=true)

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [适用于 Visual Studio 的 Visual Studio 管理员指南](visual-studio-administrator-guide.md)
* [使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
  * [命令行参数示例](command-line-parameter-examples.md)
* [创建 Visual Studio 的脱机安装](create-an-offline-installation-of-visual-studio.md)
