---
title: XslTransformation 任务 | Microsoft Docs
description: 了解 MSBuild 如何使用 XslTransformation 任务通过 XSLT 转换 XML 输入，并输出到输出设备或文件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, XslTransformation task
- XslTransformation task [MSBuild]
ms.assetid: 6f3a7d81-3ae3-4703-9a06-870b32b69d80
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 488af4bb29292d428b33a526c92768906868dfc4
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122093484"
---
# <a name="xsltransformation-task"></a>XslTransformation 任务

通过使用 XSLT 或编译的 XSLT 转换 XML 输入并输出到输出设备或文件。

## <a name="parameters"></a>参数

 下表描述了 `XslTransformation` 任务的参数。

|参数|说明|
|---------------|-----------------|
|`OutputPaths`|必选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定 XML 转换的输出文件。|
|`Parameters`|可选 `String` 参数。<br /><br /> 指定 XSLT 输入文档的参数。  提供将每个参数作为 `<Parameter Name="" Value="" Namespace="" />` 的原始 XML。|
|`XmlContent`|可选 `String` 参数。<br /><br /> 指定 XML 输入为字符串。|
|`XmlInputPaths`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定 XML 输入文件。|
|`XslCompiledDllPath`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定已编译的 XSLT。|
|`XslContent`|可选 `String` 参数。<br /><br /> 指定 XSLT 输入为字符串。|
|`XslInputPath`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定 XSLT 输入文件。|

## <a name="remarks"></a>备注

 除了具有表中列出的参数外，此任务还将从本身继承自 <xref:Microsoft.Build.Utilities.Task> 类的 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="example"></a>示例

在下面的示例中，XSL 转换文件 transform.xslt 用于修改 xml 文件 `$(XmlInputFileName)`。 转换后的 XML 将写入 `$(IntermediateOutputPath)output.xml`。 XSL 转换采用 `$(Parameter1)` 作为输入参数。

```xml
    <XslTransformation XslInputPath="transform.xslt"
                       XmlInputPaths="$(XmlInputFileName)"
                       OutputPaths="$(IntermediateOutputPath)output.xml"
                       Parameters="&lt;Parameter Name='Parameter1' Value='$(Parameter1)'/&gt;"/>
```

## <a name="see-also"></a>另请参阅

- [XSLT 参数](/dotnet/standard/data/xml/xslt-parameters)
- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
