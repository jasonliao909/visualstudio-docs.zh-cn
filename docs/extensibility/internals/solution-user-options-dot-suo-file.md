---
title: 解决方案用户选项 (。Suo) File |Microsoft Docs
description: 了解解决方案用户选项 (.suo) 文件，该文件包含以二进制格式存储的结构化存储文件中每用户的解决方案选项。
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
ms.openlocfilehash: cacbd9d9b8348e4404b035906d047229fb52839b9bed2178149cb90a0e0d93a2
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121337755"
---
# <a name="solution-user-options-suo-file"></a>解决方案用户选项 (.Suo) 文件
解决方案用户选项 (.suo) 文件包含每用户解决方案选项。 不应将此文件签入源代码管理。

 解决方案用户选项 (.suo) 文件是以二进制格式存储的结构化存储或复合文件。 将用户信息保存到流中，流的名称是密钥，用于标识 .suo 文件中的信息。 解决方案用户选项文件用于存储用户首选项设置，在保存解决方案Visual Studio自动创建。

 当环境打开 .suo 文件时，它会枚举当前加载的所有 VSPackage。 如果 VSPackage 实现 接口，则环境会调用 VSPackage 上的 方法，要求它从 .suo 文件加载其 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts> <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.LoadUserOptions%2A> 所有数据。

 VSPackage 负责了解它可能已写入 .suo 文件的流。 对于它所撰写的每个流，VSPackage 通过 调用回环境，以加载由密钥标识的特定流，该密钥是流 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A> 的名称。 然后，环境调用 VSPackage 以读取传递流名称和指向 方法的指针的特定 `IStream` <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A> 流。

 此时，将进行另一次调用， `LoadUserOptions` 以查看是否必须读取 .suo 文件的另一部分。 此过程将继续，直到环境读取和处理 .suo 文件的所有数据流。

 保存或关闭解决方案时，环境使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.SavePackageSolutionProps%2A> 指向 方法的指针调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.SaveUserOptions%2A> 方法。 包含要保存的二进制信息的 将传递给 方法，该方法随后会将信息写入 .suo 文件，并再次调用 方法，以查看是否有另一个信息流要写入 `IStream` <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.WriteUserOptions%2A> `SaveUserOptions` .suo 文件。

 对于要保存到 .suo 文件的每个信息流，以递归方式调用这两种方法（ 和 ），并传递 `SaveUserOptions` `WriteUserOptions` 指向 的指针 `IVsSolutionPersistence` 。 它们以递归方式调用，以允许将多个流写入 .suo 文件。 这样，用户信息会随解决方案一起保留，并且保证下次打开解决方案时，用户信息会存在。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>
- [解决方案](../../extensibility/internals/solutions-overview.md)
