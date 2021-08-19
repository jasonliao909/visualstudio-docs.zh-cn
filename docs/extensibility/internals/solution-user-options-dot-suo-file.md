---
title: 解决方案用户选项 (。.Suo) 文件 |Microsoft Docs
description: 了解解决方案用户选项 ( .suo) file，其中包含以二进制格式存储的结构化存储文件中的每用户解决方案选项。
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
ms.openlocfilehash: c5f17eace2b46458f11b2277d44a2db3da8539bb
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122102319"
---
# <a name="solution-user-options-suo-file"></a>解决方案用户选项 (.Suo) 文件
解决方案用户选项 ( .suo) 文件包含每用户解决方案选项。 不应将此文件签入到源代码管理中。

  ( .suo) 文件的解决方案用户选项是以二进制格式存储的、以二进制格式存储的、以二进制格式存储的文件。 将用户信息保存到流，并将流的名称保存为密钥，该密钥将用于标识 .suo 文件中的信息。 解决方案用户选项文件用于存储用户首选项设置，在 Visual Studio 保存解决方案时，会自动创建该文件。

 当环境打开 .suo 文件时，它会枚举当前加载的所有 Vspackage。 如果 VSPackage 实现了 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts> 接口，则环境将对 VSPackage 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.LoadUserOptions%2A> 方法，要求其从 .suo 文件加载其所有数据。

 VSPackage 负责了解它可能已写入 .suo 文件的流。 对于它编写的每个流，VSPackage 将通过回调到环境 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A> 以加载由键标识的特定流，这是流的名称。 然后，环境回调 VSPackage，以读取传递流名称的特定流和 `IStream` 指向方法的指针 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A> 。

 此时，将进行另一次调用 `LoadUserOptions` 来查看 .suo 文件的另一个部分是否需要读取。 此过程将一直继续，直到该环境中的所有数据流都已读完并处理。

 保存或关闭解决方案时，环境将使用指向方法的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.SavePackageSolutionProps%2A> 指针调用方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.SaveUserOptions%2A> 。 一个 `IStream` 包含要保存的二进制信息的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.WriteUserOptions%2A> ，然后将其写入 .suo 文件，然后 `SaveUserOptions` 再次调用方法，以查看是否有另一个要写入到 .suo 文件的信息流。

 这两种方法（ `SaveUserOptions` 和 `WriteUserOptions` ）将以递归方式调用，以将每个要保存到 .suo 文件的信息流都进行递归调用 `IVsSolutionPersistence` 。 它们以递归方式调用，以允许向 .suo 文件写入多个流。 通过这种方式，用户信息会随解决方案一起保留，并且保证在下一次打开解决方案时存在。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>
- [解决方案](../../extensibility/internals/solutions-overview.md)
