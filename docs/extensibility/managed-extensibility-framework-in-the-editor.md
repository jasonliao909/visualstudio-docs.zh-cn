---
title: Managed Extensibility Framework编辑器|Microsoft Docs
description: 了解Managed Extensibility Framework，通过它可生成自己的组件以扩展 Visual Studio SDK 中的编辑器。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - using MEF for extensions
ms.assetid: 3f59a285-6c33-4ae3-a4fb-ec1f5aa21bd1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: f7a98dee0c42188cfc684064744fde0c3e683d70c19d1909de98669edb46b1af
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121359125"
---
# <a name="managed-extensibility-framework-in-the-editor"></a>Managed Extensibility Framework编辑器中
编辑器是通过使用 MEF Managed Extensibility Framework (组件) 的。 可以生成自己的 MEF 组件来扩展编辑器，代码也可以使用编辑器组件。

## <a name="overview-of-the-managed-extensibility-framework"></a>概述Managed Extensibility Framework
 MEF 是一个 .NET 库，可用于添加和修改遵循 MEF 编程模型的应用程序或组件的功能。 该Visual Studio编辑器可以提供和使用 MEF 组件部件。

 MEF 包含在版本 *4* .NET Framework程序集System.ComponentModel.Composition.dll中。

 有关 MEF 详细信息，请参阅 Managed Extensibility Framework ([MEF) 。 ](/dotnet/framework/mef/index)

### <a name="component-parts-and-composition-containers"></a>组件部件和组合容器
 组件部件是一个类或类的成员，该类可以执行以下 (或) 操作：

- 使用另一个组件

- 由另一个组件使用

  例如，假设一个购物应用程序具有订单输入组件，该组件依赖于仓库库存组件提供的产品可用性数据。 在 MEF 术语中，库存部分 *可以导出* 产品可用性数据，订单输入部分可以 *导入* 数据。 订单输入部分和清单部件不需要彼此了解; *宿主应用程序* (组合容器) 负责维护导出集以及解析导出和导入。

  组合容器 <xref:System.ComponentModel.Composition.Hosting.CompositionContainer> 通常由主机拥有。 组合容器维护 *导出* 的组件部件的目录。

### <a name="export-and-import-component-parts"></a>导出和导入组件部件
 可以导出任何功能，只要它是作为公共类或类的公共成员实现的， (或方法) 。 不需要从 派生组件部件 <xref:System.ComponentModel.Composition.Primitives.ComposablePart> 。 相反，必须将 <xref:System.ComponentModel.Composition.ExportAttribute> 属性添加到要导出的类或类成员。 此属性指定另 *一* 个组件部件可以导入你的功能的协定。

### <a name="the-export-contract"></a>导出协定
 <xref:System.ComponentModel.Composition.ExportAttribute>定义要导出 (类、接口或) 实体。 通常，导出属性采用指定导出类型的参数。

```
[Export(typeof(ContentTypeDefinition))]
class TestContentTypeDefinition : ContentTypeDefinition {   }
```

 默认情况下， <xref:System.ComponentModel.Composition.ExportAttribute> 特性定义一个协定，该协定是导出类的类型。

```
[Export]
[Name("Structure")]
[Order(After = "Selection", Before = "Text")]
class TestAdornmentLayerDefinition : AdornmentLayerDefinition {   }
```

 在示例中，默认 `[Export]` 属性等效于 `[Export(typeof(TestAdornmentLayerDefinition))]` 。

 还可以导出属性或方法，如以下示例所示。

```
[Export]
[Name("Scarlet")]
[Order(After = "Selection", Before = "Text")]
public AdornmentLayerDefinition scarletLayerDefinition;
```

### <a name="import-a-mef-export"></a>导入 MEF 导出
 想要使用 MEF 导出时，必须知道协定 (协定类型) 导出时所根据的类型，并添加具有 <xref:System.ComponentModel.Composition.ImportAttribute> 该值的属性。 默认情况下，import 属性采用一个参数，这是它修改的类的类型。 以下代码行导入 <xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService> 类型。

```
[Import]
internal IClassificationTypeRegistryService ClassificationRegistry;
```

## <a name="get-editor-functionality-from-a-mef-component-part"></a>从 MEF 组件部件获取编辑器功能
 如果现有代码是 MEF 组件部分，可以使用 MEF 元数据来使用编辑器组件部件。

#### <a name="to-consume-editor-functionality-from-a-mef-component-part"></a>从 MEF 组件部件使用编辑器功能

1. 添加对 *System.Composition.ComponentModel.dll* 的引用，该引用位于 GAC (全局程序集缓存) 编辑器程序集。

2. 添加相关的 using 指令。

    ```
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio.Text;
    ```

3. 将 `[Import]` 属性添加到服务接口，如下所示。

    ```
    [Import]
    ITextBufferFactoryService textBufferService;
    ```

4. 获取服务后，可以使用其任何一个组件。

5. 编译程序集后，请放入 *.。应用程序安装的 \Common7\IDE\Components \* Visual Studio文件夹。

## <a name="see-also"></a>另请参阅
- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
