---
title: MSBuild 词汇表
description: 了解描述生成引擎及其组件的 Microsoft 生成引擎 (MSBuild) 术语表词汇。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: f767d8e4-24d8-4803-80eb-e857202dbe2c
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 3da3236b9d8cef954c4457b5710956751679b059
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126736681"
---
# <a name="msbuild-glossary"></a>MSBuild 词汇表

这些术语用于描述 Microsoft 生成引擎 (MSBuild) 及其组件。

## <a name="assemblyfoldersex"></a>AssemblyFoldersEx

注册表位置，第三方供应商将其支持的每个框架版本的路径存储在此，设计时解析可在此处查找参考程序集。

## <a name="batching"></a>批处理

批处理是指根据项元数据，将项划分为不同类别（称为批次），然后使用每个批次运行目标或任务。 批处理相当于 MSBuild for 循环构造。 有关详细信息，请参阅[批处理](../msbuild/msbuild-batching.md)。

## <a name="build-scope"></a>生成范围

生成范围描述全局属性等 MSBuild 对象，该对象对项目和在多项目生成中创建的任何子项目都可见。

## <a name="child-project"></a>子项目

请参阅 *项目，子项目*。

## <a name="condition"></a>condition

可根据条件定义多个 MSBuild 元素；也就是说，元素中会出现 `Condition` 属性。 除非条件的计算结果为 `true`，否则会忽略条件元素的内容。 有关详细信息，请参阅[条件](../msbuild/msbuild-conditions.md)。

## <a name="definition-item"></a>定义，项

请参阅 *项定义*。

## <a name="emit-item"></a>发出项

在生成的执行阶段，可通过具有 `Output` 子元素（具有 `ItemName` 属性）的任务来创建或修改项。 该任务会“发出”新项。

## <a name="emit-property"></a>发出属性

在生成的执行阶段，可通过具有 `Output` 子元素（具有 `PropertyName` 属性）的任务来创建或修改属性。 该任务会“发出”新属性。

## <a name="evaluation-phase"></a>评估阶段

评估是项目生成的第一个阶段。 所有属性和项按其在项目中的显示顺序进行评估。 对于导入的项目，其出现在项目中时才进行评估。 在执行阶段前不会运行目标和任务，且评估期间将忽略它们声明或发出的任何属性或项。

## <a name="execution-phase"></a>执行阶段

执行是项目生成的第二个阶段。 会生成所选目标并运行任务。 与其评估值相比，属性和项可进行创建或修改。

## <a name="function-property"></a>函数，属性

请参阅 *属性函数*。

## <a name="function-item"></a>函数，项

请参阅项函数。

## <a name="item"></a>item

项是生成系统的输入，并基于其元素名组成不同的项类型。 项通常表示文件。 由于项根据其所属项类型命名，因此术语 *项* 和 *项值* 可互换使用。 有关详细信息，请参阅[项](../msbuild/msbuild-items.md)。

## <a name="item-definition"></a>项定义

项定义组包含将默认元数据添加到任何项类型的项定义。 与已知元数据一样，默认元数据与指定项类型的所有项关联。 可在项定义中显式重写默认元数据。 有关详细信息，请参阅[项定义](../msbuild/item-definitions.md)。

## <a name="item-function"></a>项函数

项函数可获取项目中项的相关信息。 这些函数简化 Distinct() 项的获取过程，并且比循环遍历项的速度更快。 有的函数可操纵项路径和字符串。 有关详细信息，请参阅[项函数](../msbuild/item-functions.md)。

## <a name="item-metadata"></a>项元数据

请参阅 *元数据，项*。

## <a name="item-type"></a>项类型

项类型是项的命名列表，可用作任务参数。 任务使用项值来执行生成过程。 有关详细信息，请参阅[项](../msbuild/msbuild-items.md)。

## <a name="metadata-item"></a>元数据，项

项元数据是与项关联的名称/值对集合。 元数据为项提供描述性信息，且除已知元数据外，其他元数据是可选的。 有关详细信息，请参阅[项](../msbuild/msbuild-items.md)。

## <a name="metadata-well-known"></a>元数据，已知

已知元数据是通过使用预定义值初始化的只读项元数据。 已知元数据为引用文件的项提供描述性信息。 例如，名为 `FullPath` 的已知元数据的值是所引用文件的完整路径。 有关详细信息，请参阅[项](../msbuild/msbuild-items.md)。

## <a name="multitargeting"></a>Multitargeting — 多目标

应用程序或程序集项目从 MSBuild 和 Visual Studio 瞄准多个不同 CLR 和框架的能力。

## <a name="profile"></a>个人资料

完整框架的子集。 用于最大程度减少需下载到计算机的量。

## <a name="project-file"></a>项目文件

项目文件包含控制生成的 MSBuild 脚本。 项目文件通常具有以“proj”结尾的文件扩展名（如 .csproj 或 .vbproj）  。 项目文件可能会导入属性文件和目标文件。

## <a name="property"></a>property

属性是用来控制生成过程的键值对。 详情请参阅 [MSBuild 属性](../msbuild/msbuild-properties.md)。

## <a name="property-environment"></a>属性，环境

环境属性是自动初始化为同名系统环境变量值的属性。 详情请参阅 [MSBuild 属性](../msbuild/msbuild-properties.md)。

## <a name="property-file"></a>属性文件

属性文件是包含大部分指导生成的属性组和项组的项目文件。 按照约定，其文件扩展名为 .props。 通常在关联的项目文件的开头导入属性文件。

## <a name="property-function"></a>属性，函数

属性函数是可用于评估 MSBuild 脚本的系统属性或方法。 可使用属性方法读取系统时间、比较字符串、匹配正则表达式以及执行其他操作。 有关详细信息，请参阅[属性函数](../msbuild/property-functions.md)。

## <a name="property-function-nested"></a>属性函数，嵌套

可将属性函数组合成更复杂的函数。 例如，

 `$([MSBuild]::BitwiseAnd(32,   $([System.IO.File]::GetAttributes(tempFile))))`

有关详细信息，请参阅[属性函数](../msbuild/property-functions.md)。

## <a name="property-global"></a>属性，全局

全局属性是用来控制生成过程的键值对。 可在命令提示符下或使用 [MSBuild 任务](../msbuild/msbuild-task.md) 的 `Properties` 特性设置全局属性，并且在生成的评估阶段无法修改该属性。 详情请参阅 [MSBuild 属性](../msbuild/msbuild-properties.md)。

## <a name="property-local"></a>属性，本地

本地属性是用来控制生成过程的键值对。 此术语仅用于区分全局属性以外的属性。

## <a name="property-registry"></a>属性，注册表

注册表属性具有使用特殊语法设置的值，该语法可读取系统注册表子项的值。 详情请参阅 [MSBuild 属性](../msbuild/msbuild-properties.md)。

## <a name="property-reserved"></a>属性，保留

保留属性是用来控制生成过程的键值对。 保留属性将自动初始化为预定义的值。 详情请参阅 [MSBuild 属性](../msbuild/msbuild-properties.md)。

## <a name="project-scope"></a>项目范围

项目范围描述本地属性等 MSBuild 对象，仅在包含的项目文件中对其导入的任何项目可见。

## <a name="project-child"></a>项目，子项目

在项目生成期间，由 MSBuild 任务创建的子项目。 此新项目是项目的子项目，该父项目需包含或导入具有 MSBuild 任务的目标。 除非使用 `Properties` 属性进行了修改，否则子项目会继承父项目的全局属性。

## <a name="redist-list"></a>redist 列表

重新分发列表：对应于给定框架的程序集列表。

## <a name="reference-assembly"></a>引用程序集

设计时期间用于创建应用程序的程序集。 可从引用程序集删除实际代码和私有接口，仅留下元数据和公共接口。

## <a name="registry-property"></a>注册表属性

请参阅 *属性，注册表*。

## <a name="target"></a>目标

目标按特定的顺序将任务组合到一起，并将项目文件的各个部分作为生成过程入口点公开。 有关详细信息，请参阅[目标](../msbuild/msbuild-targets.md)。

## <a name="target-building"></a>目标，生成

请参阅目标，运行。

## <a name="target-evaluating"></a>目标，评估

由于增量编译，必须针对属性和项可能出现的更改进行目标分析。 即使跳过该目标，也必须进行更改。 评估目标意味着执行此分析并进行更改。 有关详细信息，请参阅[增量生成](../msbuild/incremental-builds.md)。

## <a name="target-executing"></a>目标，执行

执行目标意味着对其进行评估并执行所有没有任何条件，或其条件评估结果均为 true 的任务。 增量编译期间可能会跳过或执行目标，但始终会进行评估。 有关详细信息，请参阅目标，评估。

## <a name="target-running"></a>目标，运行

不会运行条件评估结果为 false 的目标，也就是说，它不会影响生成。 运行的目标已执行或跳过。 在任一情况下，都会对目标进行评估。 有关详细信息，请参阅目标，评估。

## <a name="target-skipping"></a>目标，跳过

如果增量编译确定所有输出文件都是最新的，则跳过目标，也就是说，会对目标进行评估，但不执行目标内的任务。 有关详细信息，请参阅目标，评估。

## <a name="target-framework-moniker"></a>目标框架名字对象

描述目标框架（例如 .NETFramework、Silverlight 等）、版本和配置文件（例如客户端、服务器等）的名称。

## <a name="targeting-pack"></a>目标包

随给定框架和该框架的引用程序集一起分发的程序集列表。

## <a name="targets-file"></a>目标文件

目标文件是包含大部分指导生成的目标和任务的项目文件。 按照约定，其文件扩展名为 .targets。 通常在关联的项目文件的结尾导入目标文件。

## <a name="task"></a>task

任务是 MSBuild 项目用于执行生成操作的可执行代码单元。 例如，任务可能编译输入文件或运行外部工具。 有关详细信息，请参阅[任务](../msbuild/msbuild-tasks.md)。

## <a name="transform"></a>转换

转换是指采用一对一的方式将一个项集合转换为另一集合。 除了使项目转换项集合外，转换也可让目标在其输入和输出间标识直接映射。 有关详细信息，请参阅[转换](../msbuild/msbuild-transforms.md)。

## <a name="well-known-metadata"></a>已知元数据

请参阅 *元数据，已知*。

## <a name="see-also"></a>另请参阅

- [MSBuild](../msbuild/msbuild.md)
