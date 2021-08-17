---
title: Project输出的配置 |Microsoft Docs
description: 了解每个配置可以支持的生成过程，以及可使输出项可用的接口和方法。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- project configurations, output
ms.assetid: a4517f73-45af-4745-9d7f-9fddf887b636
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: bde6407304114c7e5fb70388e43c9eabe6d53c31
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122049748"
---
# <a name="project-configuration-for-output"></a>用于输出的项目配置
每个配置都可以支持生成可执行文件或资源文件等输出项的一组生成过程。 这些输出项专用于用户，并且可放置在链接相关类型的输出（如可执行文件 (.exe、.dll、.lib) 和源文件 ( .idl、.h 文件) 的组中。

 输出项可以通过 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput2> 方法提供，并使用方法进行枚举 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumOutputs> 。 如果要对输出项进行分组，则项目还应实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputGroup> 接口。

 通过实现开发的构造 `IVsOutputGroup` 允许项目根据使用情况对输出进行分组。 例如，DLL 可能会将其程序数据库与 (PDB) 组合在一起。

> [!NOTE]
> PDB 文件包含调试信息，并且在生成 .dll 或 .exe 时指定了 "生成调试信息" 选项时创建。 通常只为调试项目配置生成 .pdb 文件。

 项目必须为其支持的每个配置返回相同数量的组，即使组中包含的输出数可能因配置而异。 例如，project Matt 的 DLL 可能在调试配置中包括 mattd.dll 和 mattd，但仅在零售配置中包括 matt.dll。

 这些组的标识符信息（如规范名称、显示名称和组信息）在项目中的配置和配置中也有相同的标识符信息。 即使配置发生更改，也可以通过此一致性进行部署和打包操作。

 组还可以有一个密钥输出，它允许打包快捷方式指向一些有意义的内容。 在给定的配置中，任何组都可能为空，因此不应对组的大小进行任何假设。 任何配置中每个组的输出)  (大小可能不同于同一配置中其他组的大小。 它还可以与另一配置中相同组的大小不同。

 ![输出组图](../../extensibility/internals/media/vsoutputgroups.gif "vsOutputGroups") 输出组

 接口的主要用途 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg> 是提供对生成、部署和调试管理对象的访问，并允许项目自由地对输出进行分组。 有关使用此接口的详细信息，请参阅[Project 配置对象](../../extensibility/internals/project-configuration-object.md)。

 在前面的关系图中，组生成的每个配置都有一个密钥输出 (bD.exe 或 b.exe) 因此，用户可以创建一个快捷方式来构建和知道无论部署的配置如何，快捷方式都可以正常工作。 组源没有密钥输出，因此用户无法创建它的快捷方式。 如果生成的调试组具有密钥输出，但生成的零售组不是，则不是正确实现。 接下来，如果有任何配置具有不包含任何输出的组，并且由于没有密钥文件，则具有包含输出的该组的其他配置不能包含密钥文件。 安装程序编辑器假定组的规范名称和显示名称以及密钥文件的存在，不会根据配置进行更改。

 请注意，如果项目具有不 `IVsOutputGroup` 希望打包或部署的，则必须将该输出放入组中。 仍可通过实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg.EnumOutputs%2A> 返回配置的所有输出的方法（与分组无关）来正常枚举输出。

 有关详细信息，请参阅 " `IVsOutputGroup` 自定义 Project" 中的 " [](https://github.com/tunnelvisionlabs/MPFProj10)实现"。

## <a name="see-also"></a>请参阅
- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)
- [用于生成的项目配置](../../extensibility/internals/project-configuration-for-building.md)
- [项目配置对象](../../extensibility/internals/project-configuration-object.md)
- [解决方案配置](../../extensibility/internals/solution-configuration.md)
