---
title: 重写和扩展生成的类
description: 了解 DSL 定义是如何构建基于域特定语言的强大工具集的平台。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122034261"
---
# <a name="override-and-extend-the-generated-classes"></a>重写和扩展生成的类

DSL 定义是一个平台，可以基于域特定语言生成一组功能强大的工具。 通过重写和扩展从 DSL 定义生成的类，可以进行许多扩展和调整。 这些类不仅包括你在 DSL 定义关系图中显式定义的域类，还包括定义工具箱、资源管理器、序列化等的其他类。

## <a name="extensibility-mechanisms"></a>扩展性机制

提供了多种机制，用于扩展生成的代码。

### <a name="override-methods-in-a-partial-class"></a>重写分部类中的方法

分部类定义允许在多个位置定义类。 这样，你可以将生成的代码与自己编写的代码分开。 在手动编写的代码中，可以重写由生成的代码继承的类。

例如，如果在 DSL 定义中定义名为 的域类，可以编写 `Book` 添加替代方法的自定义代码：

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
> 若要重写生成的类中的方法，请始终将代码写入与生成的文件分隔的文件中。 通常，该文件包含在名为 CustomCode 的文件夹中。 如果对生成的代码进行更改，则从 DSL 定义重新生成代码时，这些更改将丢失。

若要发现可以重写的方法，请键入 **类中的 override，** 后跟空格。 IntelliSense 工具提示将告诉你可以重写的方法。

### <a name="double-derived-classes"></a>Double-Derived类

生成的类中的大多数方法都继承自建模命名空间中的一组固定类。 但是，某些方法是在生成的代码中定义的。 通常，这意味着不能重写它们;不能在一个分部类中重写在同一类的另一分部定义中定义的方法。

不过，可以通过为域类设置"生成双重派生" **标志来替代** 这些方法。 这将导致生成两个类，一个类是另一个的抽象基类。 所有方法和属性定义都位于基类中，并且只有构造函数位于派生类中。

例如，在示例 Library.dsl 中， `CirculationBook` 域类的 `Generates``Double Derived` 属性设置为 `true` 。 该域类生成的代码包含两个类：

- `CirculationBookBase`，它是一个抽象 的 ，包含所有方法和属性。

- `CirculationBook`，派生自 `CirculationBookBase` 。 它为空，其构造函数除外。

若要重写任何方法，请创建派生类的分部定义，例如 `CirculationBook` 。 可以重写生成的方法和从建模框架继承的方法。

可以将此方法用于所有类型的元素，包括模型元素、关系、形状、关系图和连接器。 还可以重写其他生成的类的方法。 某些生成的类（如 ToolboxHelper）始终为双派生类。

### <a name="custom-constructors"></a>自定义构造函数

不能重写构造函数。 即使在双派生类中，构造函数也必须位于派生类中。

如果要提供自己的构造函数，可以通过在 DSL 定义中为 `Has Custom Constructor` 域类设置 来这样做。 单击" **转换所有模板"** 时，生成的代码将不包含该类的构造函数。 它将包括对缺少的构造函数的调用。 生成解决方案时，这会导致错误报告。 双击错误报告，在生成的代码中查看注释，说明应提供的内容。

在独立于生成的文件的文件中编写分部类定义，并提供构造函数。

### <a name="flagged-extension-points"></a>标记的扩展点

标记的扩展点是 DSL 定义中的一个位置，可在其中设置属性或复选框以指示你将提供自定义方法。 自定义构造函数就是一个示例。 其他示例包括将域属性的 设置为 Calculated 或 Custom 存储或在连接生成器中设置 `Kind` Is **Custom** 标志。

在每种情况下，设置 标志并重新生成代码时，都会导致生成错误。 双击错误以查看说明必须提供哪些项的注释。

### <a name="rules"></a>规则

事务管理器允许你定义在事务结束之前运行的规则，其中已发生指定事件，例如属性中的更改。 规则通常用于维护存储中不同元素之间的同步。 例如，规则用于确保关系图显示模型的当前状态。

规则是按类定义的，因此，不需要具有注册每个对象的规则的代码。 有关详细信息，请参阅 [规则在模型中传播更改](../modeling/rules-propagate-changes-within-the-model.md)。

### <a name="store-events"></a>存储事件

建模存储提供了一个事件机制，可用于侦听存储中特定类型的更改，包括添加和删除元素、更改属性值等。 在关闭进行更改的事务后，将调用事件处理程序。 通常，这些事件用于更新存储外部的资源。

### <a name="net-events"></a>.NET 事件

可以订阅形状上的一些事件。 例如，可以侦听形状上的鼠标单击。 必须编写代码来订阅每个 对象的 事件。 此代码可以重写 InitializeInstanceResources () 。

某些事件在 ShapeFields 上生成，用于在形状上绘制修饰器。 有关示例，请参阅 [如何：截获单击形状或修饰器](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)。

这些事件通常不会在事务内发生。 如果要在存储区中进行更改，应创建事务。
