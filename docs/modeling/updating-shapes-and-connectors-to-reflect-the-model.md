---
title: 更新形状和连接线以反映模型
description: 了解在 Visual Studio 的域特定语言中，可以使形状的外观反映基础模型的状态。
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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663856"
---
# <a name="update-shapes-and-connectors-to-reflect-the-model"></a>更新形状和连接线以反映模型

在 Visual Studio 的域特定语言中，可以使形状的外观反映基础模型的状态。

应将本主题中的代码示例添加到 `Dsl` 项目中的 `.cs` 文件。 每个文件中都需要以下指令：

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
```

## <a name="set-shape-map-properties-to-control-the-visibility-of-a-decorator"></a>设置“形状映射”属性以控制修饰器的可见性

你可以通过在 DSL 定义中配置形状和域类之间的映射来控制修饰器的可见性，而无需编写程序代码。 有关详细信息，请参阅[如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)。

## <a name="expose-the-color-and-style-of-a-shape-as-properties"></a>将形状的颜色和样式公开为属性

在 DSL 定义中，右键单击形状类，指向“添加已揭示项”，然后单击其中一项，例如“填充颜色”。 

形状现在具有可在程序代码中或以用户身份设置的域属性。 例如，若要在命令或规则的程序代码中设置它，可以编写：

`shape.FillColor = System.Drawing.Color.Red;`

如果要仅通过程序控制（而不是用户控制）使属性可变，请在 DSL 定义关系图中选择新的域属性，例如“填充颜色”。 然后，在“属性”窗口中，将“Is Browsable”设置为 `false` 或将“Is UI Readonly”设置为 `true`。 

## <a name="define-change-rules-to-make-color-style-or-location-depend-on-model-element-properties"></a>定义“更改规则”，使颜色、样式或位置依赖模型元素属性
 你可以定义规则，这些规则可以更新依赖模型其他部分的形状的外观。 例如，你可以在模型元素上定义“更改规则”，此规则可以更新依赖模型元素的属性的形状的颜色。 有关“更改规则”的详细信息，请参阅[模型中的规则传播更改](../modeling/rules-propagate-changes-within-the-model.md)。

 规则应仅用于更新在应用商店中维护的属性，因为在执行“撤消”命令时不会调用规则。 这不包括某些图形功能，例如形状的大小和可见性。 若要更新形状的这些功能，请参阅[更新非应用商店图形功能](#OnAssociatedProperty)。

 以下示例假定已将 `FillColor` 公开为域属性，如上一部分所述。

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

若要在首次创建形状时设置其属性，请替代关系图类的部分定义中的 `OnChildConfigured()`。 DSL 定义中指定了关系图类，生成的代码位于 Dsl\Generated Code\Diagram.cs 中。 例如：

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

此方法可用于域属性和非应用商店功能，例如形状的大小。

## <a name="use-associatevaluewith-to-update-other-features-of-a-shape"></a><a name="OnAssociatedProperty"></a> 使用 AssociateValueWith () 更新形状的其他功能

对于形状的一些功能（例如它是具有阴影还是连接线的箭头样式），没有将功能公开为域属性的内置方法。  对此类功能的更改不由事务系统控制。 因此，不适合使用规则更新它们，因为当用户执行“撤消”命令时不会调用规则。

相反，可以使用 <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.OnAssociatedPropertyChanged%2A> 更新此类功能。 在下面的示例中，连接线的箭头样式由连接线显示的关系中域属性的值控制：

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

对于要注册的每个域属性，应调用一次 `AssociateValueWith()`。 调用后，对指定属性的任何更改都将在呈现属性的模型元素的任何形状中调用 `OnAssociatedPropertyChanged()`。

没有必要为每个实例调用 `AssociateValueWith()`。 虽然 InitializeResources 是一个实例方法，但只为每个形状类调用一次。
