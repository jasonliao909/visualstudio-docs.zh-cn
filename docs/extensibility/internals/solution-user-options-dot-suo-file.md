---
title: 解决方案用户选项 (.suo) 文件|Microsoft Docs
description: 了解解决方案用户选项 (.suo) 文件，该文件包含以二进制格式存储的结构化存储文件中的每用户解决方案选项。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- .suo files, VSPackages
- suo files, VSPackages
- solutions, .suo files
- solutions, user options
- solution user options (.suo) file
ms.assetid: 75258e0d-600d-4a3d-94f4-3d7ac12cb47c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 7a5a106a856248d3f08adf71b400eb0a9d032bd9
ms.sourcegitcommit: 4264e57e45dede8bf55ddf0f7e81738a42580081
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2022
ms.locfileid: "145183445"
---
# <a name="solution-user-options-suo-file"></a>解决方案用户选项 (.suo) 文件

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]
解决方案用户选项 (.suo) 文件包含每用户解决方案选项。 不应将此文件签入源代码控制。

 解决方案用户选项 (.suo) 文件是一个结构化存储或复合文件，以二进制格式存储。 将用户信息保存到流中，其名称为密钥，用于标识 .suo 文件中的信息。 解决方案用户选项文件用于存储用户首选项设置，并在Visual Studio保存解决方案时自动创建。

 当环境打开 .suo 文件时，它会枚举当前加载的所有 VSPackage。 如果 VSPackage 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts> 接口，则环境会在 VSPackage 上调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.LoadUserOptions%2A> 该方法，要求它从 .suo 文件加载其所有数据。

 VSPackage 负责知道它可能已写入 .suo 文件中的流。 对于写入的每个流，VSPackage 会调用回环境 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A> ，以加载由密钥标识的特定流，该流是流的名称。 然后，环境调用 VSPackage 来读取该特定流，并传递流的名称和 `IStream` 指向该方法的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A> 指针。

 此时，会发出另一个调用来 `LoadUserOptions` 查看必须读取的 .suo 文件的另一部分。 此过程一直持续到 .suo 文件中的所有数据流都已由环境读取和处理。

 保存或关闭解决方案时，环境使用指向该方法的<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.SaveUserOptions%2A>指针调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.SavePackageSolutionProps%2A>该方法。 `IStream`将包含要保存的二进制信息传递给<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.WriteUserOptions%2A>该方法，然后将信息写入 .suo 文件，并再次调用`SaveUserOptions`该方法，以查看是否有另一个要写入 .suo 文件的信息流。

 这两种方法 `SaveUserOptions` ，对于 `WriteUserOptions`要保存到 .suo 文件的每个信息流（传入指向的指针 `IVsSolutionPersistence`）以递归方式调用。 它们以递归方式调用，以允许将多个流写入 .suo 文件。 这样一来，用户信息会随解决方案一起持久保存，并且保证下次打开解决方案时会存在。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>
- [解决方案](../../extensibility/internals/solutions-overview.md)
