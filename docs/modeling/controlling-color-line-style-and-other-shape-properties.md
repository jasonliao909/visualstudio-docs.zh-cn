---
title: 控制颜色、线型和其他形状属性
description: 提供有关控制形状属性（如颜色和线条样式）的信息。
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.custom: SEO-VS-2020
ms.workload:
- multiple
ms.openlocfilehash: 8f62d78e573f0fa2379fb3c36e91f0db971b8270
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665036"
---
# <a name="controlling-color-line-style-and-other-shape-properties"></a>控制颜色、线型和其他形状属性

某些形状属性（如颜色）可以“公开”。 也就是说，这些属性可以链接到形状的域属性。 其他属性必须直接控制。

## <a name="exposing-a-property"></a>公开属性
 某些形状属性（如颜色）可以链接到域属性的值。

 在 DSL 定义中，选择形状、连接器或关系图类。 在其右键单击菜单中，选择“添加已公开”，然后选择所需属性，例如“填充颜色”。

 形状现在具有可在程序代码中或以用户身份设置的域属性。

## <a name="dynamically-updating-an-exposed-property"></a>动态更新公开的属性
 通常，你想要使公开的属性依赖于另一个属性。 例如，你可能希望某个形状在每次特定域属性小于零时变成红色。 若要生成此依赖项，请创建一个[规则](../modeling/rules-propagate-changes-within-the-model.md)。 例如：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
namespace ExampleNamespace
{
 // Attribute associates the rule with class:
 [RuleOn(typeof(CarShape), FireTime = TimeToFire.TopLevelCommit)]
 // The rule is a class derived from one of the abstract rules:
 class CarShapeAddRule : AddRule
 {
 // Override the abstract method:
 public override void ElementAdded(ElementAddedEventArgs e)
 {
 base.ElementAdded(e);
 CarShape shape = e.ModelElement as CarShape;
 Store store = shape.Store;
 // Ignore this call if we're currently loading a model:
 if (store.TransactionManager.CurrentTransaction.IsSerializing)
  return;
 Car car = shape.ModelElement as Car;
 // Code here propagates change as required - for example:
 shape.FillColor = car.Somebool ? System.Drawing.Color.Red : System.Drawing.Color.Green;
 }
}
 // The rule must be registered:
 public partial class ExampleDomainModel
 {
 protected override Type[] GetCustomDomainModelTypes()
 {
  List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
  types.Add(typeof(CarShapeAddRule));
  // If you add more rules, list them here.
  return types.ToArray();
 }
 }
}
```