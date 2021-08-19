---
title: 模板目录说明 (。Vsdir) Files |Microsoft Docs
description: 了解模板目录说明文件如何使 Visual Studio IDE 显示与项目关联的文件夹、.vsz 文件和模板。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- .vsdir files
- VSDIR files
- template directory description files
ms.assetid: 9df51800-190e-4662-b685-fdaafcff1400
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 01ecd11c47edf00fb6e7126d496bb55c24f74973
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122158822"
---
# <a name="template-directory-description-vsdir-files"></a>模板目录说明 (.Vsdir) 文件
模板目录说明文件 (.vsdir) 是一个文本文件，它使集成开发环境 (IDE) 能够在对话框中显示与项目关联的文件夹、向导 .vsz 文件和模板文件。 内容包括每个文件或文件夹一条记录。 尽管通常只提供一个 .vsdir 文件来描述多个文件夹、向导或模板文件，但引用位置的所有 .vsdir 文件都是合并的。

 文件夹 (子目录) .vsdir 文件中引用的文件以及 .vsdir 文件本身都位于同一目录中。 当 IDE 运行向导或在"新建 **Project"** 或"添加新项"对话框中显示文件夹或文件时，IDE 将检查包含已执行文件的目录，以确定 .vsdir 文件是否存在。 如果找到 .vsdir 文件，IDE 会读取该文件，以确定它是否包含所执行或显示的文件夹或文件的条目。 如果找到条目，IDE 将使用执行向导或显示内容时的信息。

 以下代码示例来自 \<EnvSDK> \BscPrj\BscPrj\BscPrj\BscPrjProjectItems\Source_Files注册表项中的 SourceFiles.vsdir 文件：

```
HeaderFile.h|{E59935A1-6156-11d1-87A6-00A0C91E2A46}|#125|130|#126|0|0|0|#127
SourceFile.cpp|{E59935A1-6156-11d1-87A6-00A0C91E2A46}|#122|110|#123|0|0|0|#124
```

 在这种情况下，两条记录在一个文件中。 一个新行 (回车符) 分隔每条记录。 每一行表示不同的文件类型。 一个 (&#124;) 分隔每条记录中的字段的管道。 单个目录可以包含多个文件名不同的 .vsdir 文件，也可以为每种文件类型提供一个 .vsdir 文件。

## <a name="fields"></a>字段
 下表列出了为每条记录指定的字段。

| 字段 | 说明 |
| - | - |
| RelPathName (的相对路径)  | 文件夹、模板或 .vsz 文件的名称，例如 HeaderFile.h 或 MyWizard.vsz。 此字段还可以是用于表示文件夹的名称。 |
| {clsidPackage} | VSPackage 的 GUID，用于访问 VSPackage 的附属动态链接库 (DLL) 资源中的本地化字符串，例如 LocalizedName、Description、IconResourceId 和 SuggestedBaseName。 如果未提供 DLLPath，则 IconResourceId 适用。 **注意：**  此字段是可选的，除非前面的一个或多个字段是资源标识符。 对于与未本地化其文本的第三方向导相对应的 .vsdir 文件，此字段通常为空。 |
| LocalizedName | 模板文件或向导的本地化名称。 此字段可以是字符串或"#ResID"形式的资源标识符。 此名称显示在"添加新 **项"** 对话框中。 **注意：**  如果 LocalizedName 是资源标识符，则 {clsidPackage} 是必需的。 |
| SortPriority | 一个整数，表示此模板文件或向导的相对优先级。 例如，如果此项的值为 1，则此项显示在值为 1 的其他项旁边，并位于排序值为 2 或更大的所有项之前。<br /><br /> 排序优先级相对于同一目录中的项。 同一目录中可能存在多个 .vsdir 文件。 在这种情况下，来自所有 的项 <em>。</em>将合并该目录中的 vsdir 文件。 优先级相同的项按显示名称的不区分大小写的字典顺序列出。 `_wcsicmp`函数用于对项排序。<br /><br /> .vsdir 文件中未描述的项包含的优先级数字大于 .vsdir 文件中列出的最高优先级编号。 结果是这些项位于显示列表的末尾，而不考虑其名称。 |
| 说明 | 模板文件或向导的本地化说明。 此字段可以是字符串或"#ResID"形式的资源标识符。 选择项时，此 **字符串Project"** 新建项"或"添加新项"对话框中。 |
| DLLPath 或 {clsidPackage} | 用于加载模板文件或向导的图标。 使用 IconResourceId 将图标作为资源从.dll或.exe文件中加载。 可以使用.dll VSPackage .exe GUID 来标识此文件或文件。 VSPackage 的实现 DLL 用于加载图标 (而不是附属 DLL) 。 |
| IconResourceId | DLL 或 VSPackage 实现 DLL 中的资源标识符，用于确定要显示的图标。 |
| 标志 <xref:Microsoft.VisualStudio.Shell.Interop.__VSDIRFLAGS> ()  | 用于禁用或启用"添加新 **项**"对话框中的"名称"**和"位置**"字段。 Flags **字段的值** 是所需位标志组合的十进制等效值。<br /><br /> 当用户在"新建"选项卡上选择项时，项目将确定是否在首次显示"添加新项"对话框时显示"名称"字段和"位置"字段。 通过 .vsdir 文件，项只能控制在选择项时是启用还是禁用字段。 |
| SuggestedBaseName | 表示文件、向导或模板的默认名称。 此字段是字符串或"#ResID"形式的资源标识符。 IDE 使用此值为项提供默认名称。 此基值追加一个整数值，使名称唯一，例如 MyFile21.asp。<br /><br /> 在上一列表中，Description、DLLPath、IconResourceId、Flags 和 SuggestedBaseNumber 仅适用于模板和向导文件。 这些字段不适用于文件夹。 \<EnvSDK>\BscPrj\BscPrj\BscPrj\BscPrjProjectItems 注册表项中 BscPrjProjectItems 文件的代码说明了这一事实。 此文件包含三条 (一条记录，每个文件夹) 每条记录有四个字段：RelPathName、{clsidPackage}、LocalizedName 和 SortPriority。<br /><br /> `General&#124;{E59935A1-6156-11d1-87A6-00A0C91E2A46}&#124;#110&#124;100`<br /><br /> `Source_Files&#124;{E59935A1-6156-11d1-87A6-00A0C91E2A46}&#124;#111&#124;110`<br /><br /> `Env&#124;{E59935A1-6156-11d1-87A6-00A0C91E2A46}&#124;#112&#124;120` |

 创建向导文件时，还应考虑以下问题。

- 没有有意义的数据的任何非必需字段应包含 0 (零) 作为占位符。

- 如果未提供本地化名称，则向导文件中会使用相对路径名称。

- DLLPath 替代图标位置的 clsidPackage。

- 如果未定义任何图标，IDE 将替换具有该扩展名的文件的默认图标。

- 如果未提供建议的基名称，则使用"Project"。

- 如果删除 .vsz 文件、文件夹或模板文件，还必须从 .vsdir 文件中删除其关联记录。

## <a name="see-also"></a>请参阅
- [向导](../../extensibility/internals/wizards.md)
- [向导 (.Vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
