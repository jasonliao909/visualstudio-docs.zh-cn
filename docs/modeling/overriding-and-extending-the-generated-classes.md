---
title: 重写和扩展生成的类
description: 了解 DSL 定义是一种平台，可在该平台上构建一组基于域特定语言的强大工具。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, providing overridable classes
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 4217f4f5ebc15ce32e138419f10cc412a40692e7
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663940"
---
# <a name="override-and-extend-the-generated-classes"></a>重写和扩展生成的类

DSL 定义是一种平台，可在该平台上构建一组基于域特定语言的强大工具。 可以通过重写和扩展从 DSL 定义生成的类来进行许多扩展和适应。 这些类不仅包括在 DSL 定义关系图中显式定义的域类，还包括用于定义工具箱、资源管理器、序列化等的其他类。

## <a name="extensibility-mechanisms"></a>扩展性机制

有几种机制可用来扩展生成的代码。

### <a name="override-methods-in-a-partial-class"></a>重写分部类中的方法

分部类定义允许在多个位置定义一个类。 这使你可以将生成的代码与你自己编写的代码分开。 在手动编写的代码中，你可以重写由生成的代码继承的类。

例如，如果在 DSL 定义中定义一个名为 `Book` 的域类，可以编写自定义代码来添加重写方法：

```csharp
public partial class Book
{
   protected override void OnDeleting()
   {
      MessageBox.Show("Deleting book " + this.Title);
      base.OnDeleting();
   }
}
```

> [!NOTE]
> 若要重写生成的类中的方法，请始终将你的代码写在一个与生成的文件分开的文件中。 通常，该文件包含在一个名为 CustomCode 的文件夹中。 如果你对生成的代码进行了更改，当你从 DSL 定义中重新生成代码时，它们将丢失。

若要发现可以重写的方法，请在类中输入 override，后面加一个空格。 IntelliSense 工具提示将告诉你哪些方法可以重写。

### <a name="double-derived-classes"></a>双重派生类

生成的类中的大多数方法都继承自建模命名空间中的一组固定的类。 然而，一些方法是在生成的代码中定义的。 通常，这意味着你不能重写它们；不能在一个分部类中重写在同一类的另一分部定义中定义的方法。

不过，可以通过为域类设置“生成双重派生”标记来替代这些方法。 这会生成两个类，一个类是另一个类的抽象基类。 所有方法和属性定义都在基类中，只有构造函数在派生类中。

例如，在示例 Library.dsl 中，`CirculationBook` 域类的 `Generates``Double Derived` 属性设置为 `true`。 为该域类生成的代码包含两个类：

- `CirculationBookBase`，它是一个抽象的类，其中包含所有方法和属性。

- `CirculationBook`，它派生自 `CirculationBookBase`。 除了其构造函数之外，它是空的。

若要重写任何方法，可以创建派生类的分部定义，例如 `CirculationBook`。 可以重写生成的方法和从建模框架继承的方法。

此方法可用于所有类型的元素，包括模型元素、关系、形状、关系图和连接符。 你还可以重写其他生成的类的方法。 一些生成的类（如 ToolboxHelper）始终是双重派生的。

### <a name="custom-constructors"></a>自定义构造函数

不能重写构造函数。 即使是在双重派生类中，构造函数也必须位于派生类中。

如果要提供自己的构造函数，可以通过在 DSL 定义中为域类设置 `Has Custom Constructor` 来这样做。 当你单击“转换所有模板”时，生成的代码将不包含该类的构造函数。 它将包括对缺少的构造函数的调用。 当你生成解决方案时，这会导致错误报告。 双击错误报告可以查看生成的代码中的注释，该注释说明了应提供的内容。

在独立于生成的文件的文件中编写分部类定义，并提供构造函数。

### <a name="flagged-extension-points"></a>标记的扩展点

标记的扩展点是 DSL 定义中的一个位置，你可以在其中设置属性或复选框，用于指示你将提供自定义方法。 自定义构造函数就是一个例子。 其他示例包括将域属性的 `Kind` 设置为“Calculated”或“Custom Storage”，或在连接生成器中设置“Is Custom”标记。

在每种情况下，当你设置标记并重新生成代码时，将导致生成错误。 双击错误可以查看注释，该注释说明了必须提供的内容。

### <a name="rules"></a>规则

使用事务管理器可以定义在发生指定事件的事务结束之前运行的规则，比如一个属性的变化。 规则通常用于保持存储中不同元素之间的同步性。 例如，规则用于确保关系图显示模型的当前状态。

规则是基于每个类定义的，因此你不需要为每个对象注册规则的代码。 有关详细信息，请参阅[模型中的规则传播更改](../modeling/rules-propagate-changes-within-the-model.md)。

### <a name="store-events"></a>存储事件

建模存储提供了一种事件机制，可用于在存储中侦听特定类型的更改，其中包括添加和删除元素、更改属性值等。 事件处理程序是在进行更改的事务结束后调用的。 通常，这些事件用于更新存储外部的资源。

### <a name="net-events"></a>.NET 事件

你可以订阅一些有关形状的事件。 例如，可以侦听形状上的鼠标单击。 你必须编写代码，为每个对象订阅事件。 可以在 InitializeInstanceResources() 的重写中编写此代码。

一些事件是在 ShapeFields 上生成的，用于在形状上绘制修饰器。 有关示例，请参阅[操作方法：截获对形状或修饰器的单击](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)。

这些事件通常不会在事务中发生。 如果要在存储中进行更改，应创建一个事务。
