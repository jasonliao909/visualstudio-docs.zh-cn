---
title: Project输出输出|Microsoft Docs
description: 了解每个配置可以支持的生成过程，以及可用于提供输出项的接口和方法。
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
ms.openlocfilehash: dc071f765756007ceb2c3e50c424bd758a9111437d3218f0da20db7d2fd50c65
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121388562"
---
# <a name="project-configuration-for-output"></a>用于输出的项目配置
每个配置都可以支持一组生成输出项（如可执行文件或资源文件）的生成过程。 这些输出项是用户私有的，可以放置在链接相关类型的输出（如可执行文件 (.exe、.dll、.lib) 和源文件 (.idl、.h 文件) ）的组中。

 可以通过 方法提供输出 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput2> 项，并通过 方法枚举 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumOutputs> 输出项。 若要对输出项进行分组，项目还应实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputGroup> 接口。

 通过实现 开发的 `IVsOutputGroup` 构造允许项目根据使用情况对输出进行分组。 例如，DLL 可以按其程序数据库和 PDB (分组) 。

> [!NOTE]
> PDB 文件包含调试信息，在生成调试或调试时指定了"生成调试信息".dll创建.exe。 通常仅为调试项目配置生成 .pdb 文件。

 项目必须针对它支持的每个配置返回相同的组数，即使组中包含的输出数可能因配置而异。 例如，项目 Matt 的 DLL 在调试配置中mattd.dll和 mattd.pdb，但仅matt.dll零售配置中。

 这些组还具有相同的标识符信息，例如规范名称、显示名称和组信息（从配置到项目中的配置）。 即使配置更改，这种一致性也允许部署和打包继续运行。

 组还可以有一个密钥输出，该输出允许打包快捷方式指向有意义的内容。 给定配置中任何组可能为空，因此不应对组的大小做出任何假设。 任何 (每个) 的输出数的大小可能不同于同一配置中另一个组的大小。 它还可能不同于另一个配置中同一组的大小。

 ![输出组图形](../../extensibility/internals/media/vsoutputgroups.gif "vsOutputGroups") 输出组

 接口的主要用途是提供对生成、部署和调试管理对象的访问权限，并允许项目自由对输出 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg> 进行分组。 有关使用此接口详细信息，请参阅配置Project[对象](../../extensibility/internals/project-configuration-object.md)。

 在上图中，组生成具有跨配置的关键输出 (bD.exe 或 b.exe) 因此用户可以创建"生成"的快捷方式，并知道无论部署的配置如何，快捷方式都将正常工作。 组源没有密钥输出，因此用户无法创建其快捷方式。 如果调试组生成具有密钥输出，但零售组生成没有，则这是不正确的实现。 然后，如果任何配置具有不包含任何输出的组，并且因此没有密钥文件，则包含该组的其他包含输出的配置不能具有密钥文件。 安装程序编辑器假定组规范名称和显示名称以及密钥文件的存在不会基于配置更改。

 请注意，如果项目具有不希望打包或部署的 ，则无需将输出 `IVsOutputGroup` 放入组中即可。 仍可通过实现 方法正常枚举输出，该方法返回配置的所有输出，而不 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg.EnumOutputs%2A> 考虑分组。

 有关详细信息，请参阅 MPF for Projects 的自定义Project `IVsOutputGroup` 示例中[的实现](https://github.com/tunnelvisionlabs/MPFProj10)。

## <a name="see-also"></a>另请参阅
- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)
- [用于生成的项目配置](../../extensibility/internals/project-configuration-for-building.md)
- [项目配置对象](../../extensibility/internals/project-configuration-object.md)
- [解决方案配置](../../extensibility/internals/solution-configuration.md)
