---
title: 什么是Project设计器？
description: 了解如何使用Project设计器配置和自定义项目属性。
ms.custom: SEO-VS-2020
ms.date: 04/29/2022
ms.topic: reference
helpviewer_keywords:
- user interface [Visual Studio], projects
- projects [Visual Studio], user interface
ms.assetid: eec49aec-5474-48a7-889d-709045b9a475
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 5fe8e2e6942fb7476aedfc511d30fd154c0ff444
ms.sourcegitcommit: 3034382894e610b55f3ad07e737fa59b91680869
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2022
ms.locfileid: "144548444"
---
# <a name="what-is-the-project-designer"></a>什么是Project设计器？

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]

Visual Studio中的Project设计器是一个对话框，可用于指定项目的应用程序设置和属性。 Project设计器包含多个不同的项目属性页来与之交互。 你看到的内容取决于项目类型、平台或编程语言。

以下屏幕截图显示了Project设计器中 C# 控制台项目的项目属性页示例。 Project设计器显示在 **解决方案资源管理器** 中选择 [项目节点](../use-solution-explorer.md#tool-window)后，然后使用右键单击上下文菜单选择 **“属性**”。

::: moniker range="vs-2022"
:::image type="content" source="media/vs-2022/project-properties-designer.png" alt-text="Visual Studio 2022 中Project设计器的屏幕截图。":::
::: moniker-end

::: moniker range="vs-2019"
:::image type="content" source="media/vs-2019/project-properties-designer.png" alt-text="Visual Studio 2019 中Project设计器的屏幕截图。":::
::: moniker-end

::: moniker range="vs-2017"
:::image type="content" source="media/project-properties-designer-visual-studio-2017.png" alt-text="Visual Studio 2017 中Project设计器的屏幕截图。":::
::: moniker-end

> [!IMPORTANT]
> 可以使用Project设计器访问的项目属性不同于通过使用[解决方案资源管理器中的属性窗口](properties-window.md)访问的属性。

## <a name="project-properties-pages-in-project-designer"></a>Project设计器中的Project属性页

::: moniker range="vs-2022"

|页名称       |语言/平台      |说明                                                              |
|----------------|-----------------------|-------------------------------------------------------------------------|
|应用程序     | [C#](application-page-project-designer-csharp.md)、[Visual Basic](application-page-project-designer-visual-basic.md)、[UWP](application-page-project-designer-uwp.md)、WPF  | 使用此页可指定项目的应用程序设置和属性。 |
|生成           | [C#](build-page-project-designer-csharp.md)、WPF |  使用此窗格可指定项目的生成配置属性。 |
|生成事件    | [C#](build-events-page-project-designer-csharp.md)、Visual Basic、WPF | 使用此页可以指定生成配置说明。 |
|[代码分析](code-analysis-project-designer.md)  | C#、Visual Basic、WPF  | 使用此页配置代码分析工具。 |
|Compile         | Visual Basic | 使用此页可指定项目的编译属性。 |
|[调试页](debug-page-project-designer.md) | C#、Visual Basic、WPF | 使用此页指定项目的调试属性。 |
|包 | C#, Visual Basic | 使用此页在生成时生成NuGet包。 |
|[发布](publish-page-project-designer.md) | WPF | 使用此页配置 [!INCLUDE[ndptecclick](../../deployment/includes/ndptecclick_md.md)] 的属性。|
|参考      | Visual Basic | 使用此页管理项目所使用的引用。 |
|引用路径 | WPF                   | 使用此页可管理项目的引用路径。 |
|资源       | C#、Visual Basic、WPF |  使用此页可从 C# 项目的 解决方案资源管理器 访问 RESX 文件，为Visual Basic项目创建默认资源文件，或将资源添加到 WPF 项目。 |
|[服务](services-page-project-designer.md) | WPF、Windows 窗体 | 使用此页启用客户端应用程序服务。 |
|[设置](settings-page-project-designer.md) | C#、Visual Basic、WPF | 使用此页可以指定项目的应用程序设置。 |
|[签名](signing-page-project-designer.md) |  WPF | 使用此页对应用程序和部署清单及程序集进行签名。  (对于Visual Basic项目，[!INCLUDE[ndptecclick](../../deployment/includes/ndptecclick_md.md)].NET 项目的清单签名现在位于 **BuildPublish** > .)  |
|安全 |  [WPF](security-page-project-designer.md) | 使用此页配置使用 [!INCLUDE[ndptecclick](../../deployment/includes/ndptecclick_md.md)] 部署部署的应用程序的代码访问安全性设置。

::: moniker-end

::: moniker range="<=vs-2019"

| 标题 | 说明 |
| - | - |
| [“项目设计器”->“应用程序”页 (Visual Basic)](../../ide/reference/application-page-project-designer-visual-basic.md) | 使用此页指定 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 项目的应用程序设置和属性。 |
| [“项目设计器”->“应用程序”页 (C#)](../../ide/reference/application-page-project-designer-csharp.md) | 使用此页指定 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 项目的应用程序设置和属性。 |
| [“项目设计器”->“生成事件”页 (C#)](../../ide/reference/build-events-page-project-designer-csharp.md) | 使用此窗格指定生成配置说明。 |
| [“项目设计器”->“生成”页 (C#)](../../ide/reference/build-page-project-designer-csharp.md) | 使用此窗格指定 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 项目的生成配置属性。 |
| [“项目设计器”->“编译”页 (Visual Basic)](../../ide/reference/compile-page-project-designer-visual-basic.md) | 使用此窗格指定 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 项目的编译属性。 |
| [“项目设计器”-&gt;“调试”页](../../ide/reference/debug-page-project-designer.md) | 使用此页指定项目的调试属性。 |
| [“项目设计器”-&gt;“代码分析”](../../ide/reference/code-analysis-project-designer.md) | 使用此页配置代码分析工具。 |
| [“项目设计器”-&gt;“发布”页](../../ide/reference/publish-page-project-designer.md) | 使用此页配置 [!INCLUDE[ndptecclick](../../deployment/includes/ndptecclick_md.md)] 的属性。 |
| [项目设计器 -&gt;“引用”页 (Visual Basic)](../../ide/reference/references-page-project-designer-visual-basic.md) | 使用此页管理项目所使用的引用。 |
| [”项目设计器“ -&gt;“安全”页](../../ide/reference/security-page-project-designer.md) | 使用此页配置使用 [!INCLUDE[ndptecclick](../../deployment/includes/ndptecclick_md.md)] 部署部署的应用程序的代码访问安全性设置。 |
| [“项目设计器”-&gt;“签名”页](../../ide/reference/signing-page-project-designer.md) | 使用此页对应用程序和部署清单及程序集进行签名。 |

::: moniker-end

## <a name="see-also"></a>另请参阅

- [Visual Studio 中有哪些解决方案和项目？](../solutions-and-projects-in-visual-studio.md)
- [了解解决方案资源管理器](../use-solution-explorer.md)