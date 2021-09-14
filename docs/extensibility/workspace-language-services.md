---
title: 工作区和语言服务Visual Studio |Microsoft Docs
description: 了解语言服务如何为打开文件夹用户提供与使用解决方案和项目时相同的丰富语言功能。
ms.custom: SEO-VS-2020
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 815cfb9e17fed38b519719010acd997f7fdc5242
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664253"
---
# <a name="workspaces-and-language-services"></a>工作区和语言服务

语言服务可以为 [打开文件夹](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md) 用户提供与使用解决方案和项目时相同的丰富语言功能。 语言服务可能会基于打开的文档的文件扩展名或内容自行激活，但此"宽松文件"语言服务仅限于语法突出显示。 编辑/查看源代码时，需要其他信息才能提供更丰富的体验。 每个语言服务都有自己的 API，用于通过此额外的文档上下文数据进行初始化。 这通常由项目系统管理，该项目系统与语言服务和生成系统紧密耦合。

## <a name="initialization"></a>初始化

在 [工作区中](workspaces.md)，语言服务由仅在该语言服务中专门化的扩展点初始化，并且 <xref:Microsoft.VisualStudio.Workspace.Intellisense.ILanguageServiceProvider> 不知道任何生成创作。 这样，语言服务所有者就可以维护单个打开文件夹扩展名，而不管文件夹和文件中有多少种模式在生成期间运行编译器 (例如 MSBuild、生成文件等) 。 在磁盘上更改了创建文件上下文的文件并刷新文件上下文时，语言服务提供程序会收到更新的文件上下文集的通知。 然后，语言服务提供商可以更新其模型。

在编辑器中打开文档时，Visual Studio仅考虑需要文件上下文类型（可找到匹配文件上下文提供程序）的语言服务提供程序。 然后，它将文件上下文 (从) 提供程序 (传递给) 语言服务提供程序 `ILanguageServiceProvider.InitializeAsync` 。 语言服务提供程序对该文件上下文数据所执行的内容是语言服务提供程序的实现详细信息，但预期的用户体验是打开的文档的更丰富的语言服务。

## <a name="using-ilanguageserviceprovider"></a>使用 ILanguageServiceProvider

使用与语言服务器导出属性的值之一匹配的 创建文件上下文时，将通知语言 `ContextType` `SupportedContextTypes` 服务。

若要支持语言服务，扩展将需要：

- 唯一 `Guid` 的 。 这将在 对象 `SupportedContextTypes` 中用于属性参数和 `FileContext` 。
- 语言文件上下文
  - 提供程序工厂
    - `ExportFileContextProviderAttribute` 属性，在 中唯一 `Guid` 生成上述属性 `SupportedContextTypes`
    - 实现 `IWorkspaceProviderFactory<IFileContextProvider>`
  - 的提供程序实现 `IFileContextProvider.GetContextsForFileAsync`
    - 构造一个新的 `FileContext` ， `contextType` 将构造函数参数作为唯一生成的 `Guid`
    - 使用 `Context` 的 属性 `FileContext` 向 提供其他数据 `ILanguageServiceProvider`
- 语言服务
  - 提供程序工厂
    - `ExportLanguageServiceProvider` 属性，在 中唯一 `Guid` 生成上述属性 `SupportedContextTypes`
    - 实现 `IWorkspaceProviderFactory<ILanguageServiceProvider>`
  - 提供程序
    - 实现 `ILanguageServiceProvider`
    - 使用 `ILanguageServiceProvider.InitializeAsync` 在打开文件时为提供的参数启用语言服务
    - 使用 `ILanguageServiceProvider.UninitializeAsync` 在文件关闭时为提供的参数禁用语言服务

>[!WARNING]
>`ILanguageServiceProvider`方法可能由主线程上的工作区调用。 请考虑在不同的线程上计划工作，以避免引入 UI 延迟。

## <a name="language-server-protocol"></a>语言服务器协议

`Microsoft.VisualStudio.Workspace.*`API 不是在"打开文件夹"中启用语言服务的唯一方法。 另一个选项是使用语言服务器。 有关详细信息，请阅读语言 [服务器协议](language-server-protocol.md)。

## <a name="related-interfaces"></a>相关接口

- <xref:Microsoft.VisualStudio.Workspace.Intellisense.ILanguageServiceProvider> 当打开或关闭匹配文件类型的文件进行编辑时，将调用 。

## <a name="next-steps"></a>后续步骤

* [工作区生成](workspace-build.md)- 打开文件夹支持生成系统，MSBuild和生成文件。