---
title: 更新形状和连接线以反映模型
description: 了解在 Visual Studio 域特定语言中，可以使形状的外观反映基础模型的状态。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 0f667821a9940603f887850a9b26fc1d8ca2f073
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663856"
---
# <a name="update-shapes-and-connectors-to-reflect-the-model"></a>更新形状和连接线以反映模型

在 Visual Studio 域特定语言中，可以使形状的外观反映基础模型的状态。

本主题中的代码示例应添加到 `.cs` 项目中 `Dsl` 的文件中。 每个文件中都需要以下指令：

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
```

## <a name="set-shape-map-properties-to-control-the-visibility-of-a-decorator"></a>设置形状地图属性以控制修饰器的可见性

可以通过在 DSL 定义中配置形状和域类之间的映射来控制修饰器的可见性，而无需编写程序代码。 有关详细信息，请参阅 [How to Define a Domain-Specific Language](../modeling/how-to-define-a-domain-specific-language.md)。

## <a name="expose-the-color-and-style-of-a-shape-as-properties"></a>将形状的颜色和样式公开为属性

在 DSL 定义中，右键单击形状类，指向"添加公开 **"，** 然后单击其中一项，如"填充 **颜色"。**

形状现在具有可在程序代码或用户中设置的域属性。 例如，若要在命令或规则的程序代码中设置它，可以编写：

`shape.FillColor = System.Drawing.Color.Red;`

如果要仅在程序控制下而不是由用户设置属性变量，请在 DSL 定义关系图中选择新的域属性，例如"填充颜色"。 然后，在 属性窗口中，将 Is **Browsable** 设置为 `false` 或将 **Is UI Readonly** 设置为 `true` 。

## <a name="define-change-rules-to-make-color-style-or-location-depend-on-model-element-properties"></a>定义更改规则，使颜色、样式或位置依赖于模型元素属性
 可以定义规则，这些规则根据模型的其他部分更新形状的外观。 例如，可以在模型元素上定义更改规则，以根据模型元素的属性更新其形状的颜色。 有关更改规则详细信息，请参阅 [规则在模型中传播更改](../modeling/rules-propagate-changes-within-the-model.md)。

 应仅使用规则来更新在 Store 中维护的属性，因为执行 Undo 命令时不会调用规则。 这不包括一些图形功能，例如形状的大小和可见性。 若要更新形状的这些功能，请参阅 [更新非存储图形功能](#OnAssociatedProperty)。

 以下示例假定已公开为域属性 `FillColor` ，如上一部分所述。

```csharp
[RuleOn(typeof(ExampleElement))]
  class ExampleElementPropertyRule : ChangeRule
  {
    public override void ElementPropertyChanged(ElementPropertyChangedEventArgs e)
    {
      base.ElementPropertyChanged(e);
      ExampleElement element = e.ModelElement as ExampleElement;
      // The rule is called for every property that is updated.
      // Therefore, verify which property changed:
      if (e.DomainProperty.Id == ExampleElement.NameDomainPropertyId)
      {
        // There is usually only one shape:
        foreach (PresentationElement pel in PresentationViewsSubject.GetPresentation(element))
        {
          ExampleShape shape = pel as ExampleShape;
          // Replace this with a useful condition:
          shape.FillColor = element.Name.EndsWith("3")
                     ? System.Drawing.Color.Red : System.Drawing.Color.Green;
        }
      }
    }
  }
  // The rule must be registered:
  public partial class OnAssociatedPropertyExptDomainModel
  {
    protected override Type[] GetCustomDomainModelTypes()
    {
      List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
      types.Add(typeof(ExampleElementPropertyRule));
      // If you add more rules, list them here.
      return types.ToArray();
    }
  }
```

## <a name="use-onchildconfigured-to-initialize-a-shapes-properties"></a>使用 OnChildConfigured 初始化形状的属性

若要在首次创建形状时设置形状的属性，请重写关系图类的部分 `OnChildConfigured()` 定义中的 。 DSL 定义中指定了关系图类，生成的代码位于 **Dsl\Generated Code\Diagram.cs 中**。 例如：

```csharp
partial class MyLanguageDiagram
{
  protected override void OnChildConfigured(ShapeElement child, bool childWasPlaced, bool createdDuringViewFixup)
  {
    base.OnChildConfigured(child, childWasPlaced, createdDuringViewFixup);
    ExampleShape shape = child as ExampleShape;
    if (shape != null)
    {
      if (!createdDuringViewFixup) return; // Ignore load from file.
      ExampleElement element = shape.ModelElement as ExampleElement;
      // Replace with a useful condition:
      shape.FillColor = element.Name.EndsWith("3")
          ? System.Drawing.Color.Red : System.Drawing.Color.Green;
    }
    // else deal with other types of shapes and connectors.
  }
}
```

此方法可用于域属性和非存储功能，例如形状的大小。

## <a name="use-associatevaluewith-to-update-other-features-of-a-shape"></a><a name="OnAssociatedProperty"></a> 使用 AssociateValueWith () 更新形状的其他特征

对于形状的一些功能（例如它是具有阴影还是连接器的箭头样式）来说，没有将特征公开为域属性的内置方法。  对此类功能的更改不由事务系统控制。 因此，不适合使用规则更新它们，因为当用户执行 Undo 命令时不会调用规则。

相反，可以使用 更新此类功能 <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.OnAssociatedPropertyChanged%2A> 。 在下面的示例中，连接器的箭头样式由连接器显示的关系中的域属性的值控制：

```csharp
public partial class ArrowConnector // My connector class.
{
    /// <summary>
    /// Called whenever a registered property changes in the associated model element.
    /// </summary>
    /// <param name="e"></param>
    protected override void OnAssociatedPropertyChanged(VisualStudio.Modeling.Diagrams.PropertyChangedEventArgs e)
    {
      base.OnAssociatedPropertyChanged(e);
      // Can be called for any property change. Therefore,
      // Verify that this is the property we're interested in:
      if ("IsDirected".Equals(e.PropertyName))
      {
        if (e.NewValue.Equals(true))
        { // Update the shape's built-in Decorator feature:
          this.DecoratorTo = LinkDecorator.DecoratorEmptyArrow;
        }
        else
        {
          this.DecoratorTo = null; // No arrowhead.
        }
      }
    }

    // OnAssociatedPropertyChanged is called only for properties
    // that have been registered using AssociateValueWith().
    // InitializeResources is a convenient place to call this.
    // This method is invoked only once per class, even though
    // it is an instance method.
    protected override void InitializeResources(StyleSet classStyleSet)
    {
      base.InitializeResources(classStyleSet);
      AssociateValueWith(this.Store, Wire.IsDirectedDomainPropertyId);
      // Add other properties here.
    }
}
```

`AssociateValueWith()` 对于要注册的每个域属性，应调用一次 。 调用指定属性后，对指定属性的任何更改都将在呈现属性的模型元素的任何形状 `OnAssociatedPropertyChanged()` 中调用。

不需要调用每个 `AssociateValueWith()` 实例。 虽然 InitializeResources 是一个实例方法，但对于每个形状类，它只调用一次。
