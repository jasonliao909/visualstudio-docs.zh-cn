---
title: 向依赖项关系图添加自定义属性
description: 了解如何在为依赖项关系图编写扩展代码时，将值与依赖项关系图上的任意元素一起存储。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- dependency diagrams, adding custom properties
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: e67ccec3405dfb0cf50f914ff9e91fbec2d8d604
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122157730"
---
# <a name="add-custom-properties-to-dependency-diagrams"></a>向依赖项关系图添加自定义属性

为依赖项关系图编写扩展代码时，可以将值与依赖项关系图上的任何元素一起存储。 保存并重新打开关系图时，值将保留。 还可以让这些属性显示在"属性 **"** 窗口中，以便用户可以查看和编辑它们。 例如，您可以让用户为每一层指定正则表达式，并编写验证代码来确认每层中的类名称符合用户指定的模式。

## <a name="non-visible-properties"></a>不可见属性

如果只想让代码将值附加到依赖项关系图中的任意元素，则无需定义 MEF 组件。 `Properties` [ILayerElement 中有一个名为 的字典](/previous-versions/ff644511(v=vs.140))。 只需将可封送的值添加到任何层元素的字典。 它们将被保存为依赖项关系图的一部分。

## <a name="editable-properties"></a>可编辑属性

**初始准备**

> [!IMPORTANT]
> 若要显示属性，请对希望层属性可见的每台计算机进行以下更改：
>
> 1. 使用记事本运行 **来运行 。** 打开 *%ProgramFiles%\Microsoft Visual Studio [version]\Common7\IDE\Extensions\Microsoft\Architecture Tools\ExtensibilityRuntime\extension.vsixmanifest*。
> 2. 在 **Content 元素** 中，添加：
>
>     ```xml
>     <MefComponent>Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.Provider.dll</MefComponent>
>     ```
>
> 3. 在应用程序 **Visual Studio Tools** 菜单的"Visual Studio"部分下，打开 **"开发人员命令提示"。** 输入：
>
>      `devenv /rootSuffix /updateConfiguration`
>
>      `devenv /rootSuffix Exp /updateConfiguration`
> 4. 重启 Visual Studio。

**确保你的代码在 VSIX 项目中**

如果属性是命令、手势或验证项目的一部分，则无需添加任何内容。 自定义属性的代码应在 Visual Studio 扩展性项目中定义，并定义为 MEF 组件。 有关详细信息，请参阅 [将命令和手势添加到依赖项关系图](../modeling/add-commands-and-gestures-to-layer-diagrams.md) 或向 [依赖项关系图添加自定义体系结构验证](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)。

**定义自定义属性**

若要创建自定义属性，请定义如下类：

```csharp
[Export(typeof(IPropertyExtension))]
public class MyProperty : PropertyExtension<ILayerElement>
{
  // Implement the interface.
}
```

可以在 [ILayerElement](/previous-versions/ff644511(v=vs.140)) 或任何其派生类上定义属性，其中包括：

- `ILayerModel` - 模型

- `ILayer` - 每个层

- `ILayerDependencyLink` - 层之间的链接

- `ILayerComment`

- `ILayerCommentLink`

## <a name="example"></a>示例

以下代码是典型的自定义属性描述符。 它在层模型 (`ILayerModel`) 上定义了一个布尔属性，用户可以使用该布尔属性来为自定义的验证方法提供值。

```csharp
using System;
using System.ComponentModel.Composition;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer;

namespace MyNamespace
{
  /// <summary>
  /// Custom properties are added to the Layer Designer via a custom
  /// Property Descriptor. We have to export this Property Descriptor
  /// using MEF to make it available in the Layer Designer.
  /// </summary>
  [Export(typeof(IPropertyExtension))]
  public class AllTypesMustBeReferencedProperty
      : PropertyExtension<ILayerModel>
  {
    /// <summary>
    /// Each custom property must have a unique name.
    /// Usually we use the full name of this class.
    /// </summary>
    public static readonly string FullName =
      typeof(AllTypesMustBeReferencedProperty).FullName;

    /// <summary>
    /// Construct the property. Notice the use of FullName.
    /// </summary>
    public AllTypesMustBeReferencedProperty()
            : base(FullName)
    {  }

    /// <summary>
    /// The display name is shown in the Properties window.
    /// We therefore use a localizable resource.
    /// </summary>
    public override string DisplayName
    {
      get { return Strings.AllTypesMustBeReferencedDisplayName; }
    }

    /// <summary>
    /// Description shown at the bottom of the Properties window.
    /// We use a resource string for easier localization.
    /// </summary>
    public override string Description
    {
      get { return Strings.AllTypesMustBeReferencedDescription; }
    }

    /// <summary>
    /// This is called to set a new value for this property. We must
    /// throw an exception if the value is invalid.
    /// </summary>
    /// <param name="component">The target ILayerElement</param>
    /// <param name="value">The new value</param>
    public override void SetValue(object component, object value)
    {
      ValidateValue(value);
      base.SetValue(component, value);
    }
    /// <summary>
    /// Helper to validate the value.
    /// </summary>
    /// <param name="value">The value to validate</param>
    private static void ValidateValue(object value)
    {  }

    public override Type PropertyType
    { get { return typeof(bool); } }

    /// <summary>
    /// The segment label of the properties window.
    /// </summary>
    public override string Category
    {
      get
      {
        return Strings.AllTypesMustBeReferencedCategory;
      }
    }
  }
}
```

## <a name="see-also"></a>请参阅

- [扩展依赖项关系图](../modeling/extend-layer-diagrams.md)
