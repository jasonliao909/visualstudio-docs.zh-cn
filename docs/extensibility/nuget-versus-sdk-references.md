---
title: 使用 NuGet 与扩展 SDK 添加引用
description: 了解将软件打包为NuGet包或软件开发工具包（在项目引用时Visual Studio之间的差异。
ms.custom: SEO-VS-2020
ms.date: 08/02/2019
ms.topic: conceptual
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- multiple
ms.openlocfilehash: 2ca8b3f2e7d0b75d0461a905832263635db5708f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122158549"
---
# <a name="nuget-versus-sdk-as-a-project-reference"></a>作为项目引用 NuGet 与 SDK

本文旨在帮助开发人员选择是将软件打包为 NuGet 包，还是打包为 SDK (软件开发) 。 具体而言，它讨论了在一个特定项目中引用这两者Visual Studio差异。

- [NuGet](/nuget)是一个开源包管理系统，可简化将库合并到项目中的过程。 对于 .NET (.NET Core) ，NuGet是 Microsoft 支持的用于共享代码的机制。 NuGet定义如何创建、托管和使用 .NET 包，并为每个角色提供工具。 在 Visual Studio中，NuGet用户界面向项目添加[程序包管理器包。](/nuget/consume-packages/install-use-packages-visual-studio)

- [SDK](../extensibility/creating-a-software-development-kit.md)是文件的集合，Visual Studio一个引用项。 选择"添加引用"Visual Studio中的"引用管理器"对话框列出与当前项目 **相关的所有 SDK。** 将 SDK 添加到项目时，可以通过 IntelliSense、"工具箱"窗口、设计器、对象浏览器、MSBuild、部署、调试和打包来访问该 SDK 的所有内容。

## <a name="which-mechanism-should-i-use"></a>应使用哪种机制？

下表可帮助你比较 SDK 与 NuGet 的引用功能。

| 特征 | SDK 支持 | SDK 说明 | NuGet 支持 | NuGet 说明 |
| - | - | - |---------------| - |
| 机制引用一个实体后，便可使用所有文件和功能。 | Y | 因此，可以使用“引用管理器”对话框添加 SDK，以便在开发工作流期间使用所有文件和功能。 | Y | |
| MSBuild 自动使用程序集和 Windows 元数据 (.winmd) 文件。 | Y | SDK 中的引用会自动传递给编译器。 | Y | |
| MSBuild 自动使用的 .h 或 .lib 文件。 | Y | *SDKName.props* 文件Visual Studio设置 Visual C++ 目录等，以便自动使用 *.h* 或 *.lib* 文件。 | N | |
| MSBuild 自动使用 .js 或 .css 文件。 | Y | 在 **解决方案资源管理器** 中，可以展开 JavaScript SDK 引用节点以显示单个.js *或 .css* 文件，然后通过将这些文件拖动 *到* 其源文件来 `<source include/>` 生成标记。 SDK 支持 F5 和包自动安装。 | Y | |
| MSBuild 自动添加“工具箱”中的控件。 | Y | “工具箱”可使用 SDK 并在指定的选项卡中显示控件。 | N | |
| 该机制支持扩展的 Visual Studio 安装程序 (VSIX)。 | Y | VSIX 具有特殊的清单和逻辑，用于创建 SDK 包 | Y | VSIX 可嵌入另一安装程序中。 |
| “对象浏览器”可枚举引用。 | Y | “对象浏览器”自动获取 SDK 中的引用列表并枚举它们。 | N | |
| 文件和链接自动被添加到“引用管理器”对话框（帮助链接等自动填充） | Y | “引用管理器”对话框连同帮助链接和 SDK 依赖项列表一起自动枚举 SDK。 | N | NuGet 提供其自身的“管理 NuGet 包”对话框。 |
| 该机制支持多个体系结构。 | Y | SDK 可以提供多个配置。 MSBuild 针对每个项目配置使用相应的文件。 | N | |
| 该机制支持多个配置。 | Y | SDK 可以提供多个配置。 根据项目体系结构，MSBuild 针对每个项目体系结构使用相应的文件。 | N | |
| 该机制可指定“不复制”。 | Y | 根据是否在 *\redist* 或 *\designtime* 文件夹中删除文件，可以控制要复制到使用应用程序的包中的文件。 | N | 需要声明包清单中要复制的文件。 |
| 内容显示在本地化文件中。 | Y | 自动包含 SDK 中已本地化的 XML 文档，以提供更好的设计时体验。 | N | |
| MSBuild 支持同时使用多个版本的 SDK。 | Y | SDK 支持同时使用多个版本。 | N | 这不会引用。 项目中不能一次同时拥有多个版本的 NuGet 文件。 |
| 该机制支持指定适用的目标框架、Visual Studio 版本和项目类型。 | Y | “引用管理器”对话框和“工具箱”仅显示适用于项目的 SDK，以便用户更轻松地选择适当的 SDK。 | Y（部分） | 透视是目标框架。 用户界面上没有筛选。 安装时可能会返回错误。 |
| 该机制支持为本机 WinMD 指定注册信息。 | Y | 可以在 中指定 .winmd 文件与 .dll 文件 *之间的SDKManifest.xml。* | N | |
| 该机制支持指定其他 SDK 上的依赖关系。 | Y | SDK 仅通知用户；用户仍需手动安装和引用它们。 | Y | NuGet 自动提取它们；用户不会收到通知。 |
| 该机制与 [!INCLUDE[win8_appstore_long](../debugger/includes/win8_appstore_long_md.md)] 概念（如应用清单和框架 ID）集成。 | Y | SDK 必须传递特定于 [!INCLUDE[win8_appstore_short](../ide/includes/win8_appstore_short_md.md)] 的概念，以便包装和 F5 可以与 [!INCLUDE[win8_appstore_short](../ide/includes/win8_appstore_short_md.md)] 提供的 SDK 一起正常工作。 | N | |
| 该机制与 [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] 应用的调试管道集成。 | Y | SDK 必须传递特定于 [!INCLUDE[win8_appstore_short](../ide/includes/win8_appstore_short_md.md)] 的概念，以便包装和 F5 可以与 [!INCLUDE[win8_appstore_short](../ide/includes/win8_appstore_short_md.md)] 提供的 SDK 一起正常工作。 | Y | NuGet 内容是项目的一部分。 无需特殊的 F5 考虑。 |
| 该机制与应用清单集成。 | Y | SDK 必须传递特定于 [!INCLUDE[win8_appstore_short](../ide/includes/win8_appstore_short_md.md)] 的概念，以便包装和 F5 可以与 [!INCLUDE[win8_appstore_short](../ide/includes/win8_appstore_short_md.md)] 提供的 SDK 一起正常工作。 | Y | NuGet 内容是项目的一部分。 无需特殊的 F5 考虑。 |
| 该机制部署非引用文件（例如，将部署要在其上运行 [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] 应用测试的测试框架）。 | Y | 如果将文件放在 *\redist* 文件夹中，则会自动部署这些文件。 | Y | |
| 该机制会在 Visual Studio IDE 中自动添加平台 SDK。 | Y | 如果将 [!INCLUDE[win8](../debugger/includes/win8_md.md)] SDK 或 Windows Phone SDK 放入具有特定布局的特定位置，SDK 会自动与所有 Visual Studio 功能集成。 | N | |
| 该机制支持干净的开发者计算机。 （即，无需安装，只需来自源代码管理的简单检索即可工作。） | N | 由于引用 SDK，因此必须单独签入解决方案和 SDK。 可从两个非注册表默认位置（MSBuild 从该位置循环访问 SDK）签入 SDK（有关详细信息，请参阅[创建软件开发工具包](../extensibility/creating-a-software-development-kit.md)）。 作为替代方法，如果自定义位置包含 SDK，可以在项目文件中指定以下代码：<br /><br />`<PropertyGroup>`<br />&nbsp;&nbsp;`<SDKReferenceDirectoryRoot>`<br />&nbsp;&nbsp;`C:\MySDKs`<br />&nbsp;&nbsp;`</SDKReferenceDirectoryRoot>`<br />`</PropertyGroup>`<br /><br /> 然后将 SDK 签入该位置。 | Y | 可以签出解决方案，Visual Studio 会立即识别并作用于文件。 |
| 可以加入大型现有包作者社区。 | 不适用 | 社区是新增功能。 | Y | |
| 可以加入大型现有包使用者社区。 | 不适用 | 社区是新增功能。 | Y | |
| 可以加入合作伙伴生态系统（自定义库和存储库等）。 | 不适用 | 可用的存储库包括 Visual Studio Marketplace、Microsoft 下载中心和 [!INCLUDE[win8_appstore_long](../debugger/includes/win8_appstore_long_md.md)]。 | Y | |
| 该机制与持续集成生成服务器集成，用于包创建和包使用。 | Y | SDK 必须将命令行上的签入位置（SDKReferenceDirectoryRoot 属性）传递到 MSBuild。 | Y | |
| 该机制同时支持稳定和预发布包版本。 | Y | SDK 支持向多个版本添加引用。 | Y | |
| 对于已安装的包，该机制支持自动更新。 | Y | 如果随附在 VSIX 或 Visual Studio 自动更新中，SDK 会自动发送通知。 | Y | |
| 该机制包含独立的 *.exe* 文件，用于创建和使用包。 | Y | SDK 包含 *MSBuild.exe*。 | Y | |
| 包可签入到版本控制。 | Y | 无法签入“文档”节点外的任何内容，这意味着可能无法签入扩展 SDK。 扩展 SDK 可能较大。 | Y | |
| 可使用 PowerShell 界面创建和使用包。 | Y（使用），N（创建） | 没有用于创建 SDK 的工具。 使用在命令行上正在执行 MSBuild。 | Y | |
| 可使用符号包调试支持。 | Y | 如果将 .pdb 文件放入 SDK 中，系统将自动提取它们。 | Y | |
| 该机制支持程序包管理器自动更新。 | 不适用 | SDK 通过 MSBuild 进行修订。 | Y | |
| 该机制支持轻型清单格式。 | Y | *SDKManifest.xml* 支持多个属性，但通常需要一小部分。 | Y | |
| 该机制适用于所有 Visual Studio 版本。 | Y | SDK 支持所有 Visual Studio 版本。 | Y | NuGet 支持所有 Visual Studio 版本。 |

## <a name="see-also"></a>请参阅

- [管理项目中的引用](../ide/managing-references-in-a-project.md)
- [管理项目中的应用 (Visual Studio for Mac)](/visualstudio/mac/managing-references-in-a-project)
