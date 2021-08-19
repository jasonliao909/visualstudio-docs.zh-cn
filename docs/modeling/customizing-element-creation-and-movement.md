---
title: 自定义元素创建和移动
description: 了解如何允许将元素从 "工具箱" 或 "粘贴" 或 "移动" 操作拖动到另一个元素。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.dsltools.dsldesigner.elementmergedirective
helpviewer_keywords:
- Domain-Specific Language, element merge directives
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 5ef80f1b377acdecc32a774ebc2d8a199a6189de
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122027833"
---
# <a name="customizing-element-creation-and-movement"></a>自定义元素创建和移动

可以通过工具箱或粘贴或移动操作，允许将元素拖至另一个元素上。 您可以使用您指定的关系将移动的元素链接到目标元素。

元素合并指令 (EMD) 指定将一个模型元素 *合并* 到另一个模型元素时会发生的情况。 在以下情况下会发生这种情况：

- 用户将 "工具箱" 拖动到关系图或形状上。

- 用户使用资源管理器或隔离舱形状中的 "添加" 菜单创建元素。

- 用户将项从一个泳道移到另一个泳道。

- 用户粘贴元素。

- 程序代码将调用元素合并指令。

尽管创建操作似乎不同于复制操作，但它们实际上是以相同的方式工作的。 添加元素（例如，从 "工具箱"）时，将复制该元素的原型。 原型以与从模型的另一部分复制的元素相同的方式合并到模型中。

EMD 的责任是决定如何将对象或对象组合并到模型中的特定位置。 具体而言，它会确定应实例化哪些关系以将合并组链接到模型。 您还可以对其进行自定义以设置属性和创建其他对象。

![当 E M D 确定如何添加新元素时，显示一个前后的元素树及其引用关系的关系图。](../modeling/media/dsl-emd_merge.png)

当您定义嵌入关系时，将自动生成 EMD。 当用户将新的子实例添加到父级时，此默认 EMD 将创建关系的实例。 可以通过添加自定义代码来修改这些默认 EMDs。

你还可以在 DSL 定义中添加自己的 EMDs，以允许用户拖动或粘贴合并类和接收类的不同组合。

## <a name="defining-an-element-merge-directive"></a>定义元素合并指令

您可以向域类、域关系、形状、连接符和关系图添加元素合并指令。 可以在 "接收域" 类下的 "DSL 资源管理器" 中添加或查找它们。 接收类是已在模型中的元素的域类，新的或复制的元素将合并到该类中。

![DSL 资源管理器的屏幕截图，显示要添加的 ExampleElement 被选为索引类并选中 "应用于子类" 选项。](../modeling/media/dsl-emd_details.png)

**索引类** 是可合并到接收类的成员中的元素的域类。 索引类的子类的实例还将通过此 EMD 合并，除非您将应用于 **子类** 设置为 False。

有两种类型的 merge 指令：

- **进程合并** 指令指定应将新元素链接到树中的关系。

- **正向合并** 指令将新元素重定向到另一个接收元素，通常是父级。

您可以将自定义代码添加到合并指令：

- Set **使用自定义接受** 添加您自己的代码，以确定是否应将索引元素的特定实例合并到目标元素。 当用户从 "工具箱" 拖动时，如果代码不允许合并，则会显示 "无效" 指针。

   例如，您可以仅在接收元素处于特定状态时允许合并。

- Set **使用自定义合并** 来添加自己的代码，以定义执行合并时对模型所做的更改。

   例如，您可以使用模型中的数据从其新位置设置合并元素中的属性。

> [!NOTE]
> 如果你编写自定义合并代码，它只会影响使用此 EMD 执行的合并。 如果有其他 EMDs 合并相同类型的对象，或者存在其他在不使用 EMD 的情况下创建这些对象的自定义代码，则它们将不会受到自定义合并代码的影响。
>
> 如果要确保新元素或新关系始终由您的自定义代码进行处理，请考虑 `AddRule` 在嵌入关系和 `DeleteRule` 元素的域类上定义。 有关详细信息，请参阅 [规则在模型内部传播更改](../modeling/rules-propagate-changes-within-the-model.md)。

## <a name="example-defining-an-emd-without-custom-code"></a>示例：定义不含自定义代码的 EMD

下面的示例通过从 "工具箱" 拖到现有形状上，使用户能够同时创建一个元素和一个连接器。 该示例将 EMD 添加到 DSL 定义。 在进行此修改之前，用户可以将工具拖动到关系图上，而不是拖到现有形状上。

用户还可以将元素粘贴到其他元素上。

### <a name="to-let-users-create-an-element-and-a-connector-at-the-same-time"></a>允许用户同时创建一个元素和一个连接器

1. 使用 **最小语言** 解决方案模板创建新的 DSL。

    当你运行此 DSL 时，它允许你在形状之间创建形状和连接线。 不能将新的 **ExampleElement** 形状从工具箱拖到现有形状上。

2. 若要允许用户将元素合并到 `ExampleElement` 形状上，请在域类中创建新的 EMD `ExampleElement` ：

   1. 在 **DSL 资源管理器** 中，展开 " **域类**"。 右键单击 `ExampleElement` ，然后单击 " **添加新元素合并指令**"。

   2. 确保 " **DSL 详细信息** " 窗口处于打开状态，以便您可以查看新 EMD 的详细信息。  (菜单： "**查看**"、"**其他 Windows**"、" **DSL 详细信息**"。 ) 

3. 在 "DSL 详细信息" 窗口中设置 **索引类** ，以定义可合并到对象的元素类 `ExampleElement` 。

    对于此示例，请选择 `ExampleElements` ，以便用户可以将新元素拖动到现有元素上。

    请注意，索引类将成为 DSL 资源管理器中的 EMD 的名称。

4. 在 " **通过创建链接进行处理合并**" 下，添加两个路径：

   - 一个路径将新元素链接到父模型。 需要输入的路径表达式将从现有元素导航到父模型的嵌入关系。 最后，在新链接中指定将向其分配新元素的角色。 路径如下：

      `ExampleModelHasElements.ExampleModel/!ExampleModel/.Elements`

   - 其他路径将新元素链接到现有元素。 路径表达式指定要向其分配新元素的引用关系和角色。 此路径如下所示：

      `ExampleElementReferencesTargets.Sources`

      可以使用路径导航工具创建每个路径：

      1. 在 " **通过创建指向路径的链接处理合并**" 下，单击 **\<add path>** 。

      2. 单击列表项右侧的下拉箭头。 此时将显示一个树视图。

      3. 展开树中的节点，以形成要指定的路径。

5. 测试 DSL：

   1. 按 **F5** 重新生成并运行解决方案。

        重新生成的时间比平时长，因为生成的代码将从文本模板中更新以符合新的 DSL 定义。

   2. Visual Studio 的实验实例启动后，打开 DSL 的模型文件。 创建一些示例元素。

   3. 从 **示例元素** 工具拖到现有形状上。

        此时将显示一个新形状，并将其链接到使用连接符的现有形状。

   4. 复制现有形状。 选择另一个形状并粘贴。

        将创建第一个形状的副本。  它有一个新名称，并使用连接器链接到第二个形状。

请注意此过程中的以下几点：

- 通过创建元素合并指令，可以允许任何类元素接受任何其他类。 EMD 是在接收域类中创建的，并且在 " **索引类** " 字段中指定了接受的域类。

- 通过定义路径，可以指定应使用哪些链接将新元素连接到现有模型。

     指定的链接应包含一个嵌入关系。

- EMD 会影响 "工具箱" 和 "粘贴" 操作的两项创建。

     如果编写用于创建新元素的自定义代码，则可以使用方法显式调用 EMD `ElementOperations.Merge` 。 这将确保你的代码以与其他操作相同的方式将新元素链接到模型。 有关详细信息，请参阅 [自定义复制行为](../modeling/customizing-copy-behavior.md)。

## <a name="example-adding-custom-accept-code-to-an-emd"></a>示例：将自定义接受代码添加到 EMD

通过将自定义代码添加到 EMD，可以定义更复杂的合并行为。 此简单示例防止用户向关系图中添加超出固定数目的元素。 该示例修改嵌入关系中附带的默认 EMD。

### <a name="to-write-custom-accept-code-to-restrict-what-the-user-can-add"></a>编写自定义接受代码以限制用户可以添加的内容

1. 使用 **最小语言** 解决方案模板创建 DSL。 打开 DSL 定义关系图。

2. 在 DSL 资源管理器中，展开 **域类** `ExampleModel` 、、 **元素合并指令**。 选择名为 的元素合并指令 `ExampleElement` 。

     此 EMD 控制用户如何在模型中创建新对象，例如通过 `ExampleElement` 从工具箱拖动。

3. 在 **"DSL 详细信息"** 窗口中，选择"**使用自定义接受"。**

4. 重新生成解决方案。 这比平时要长，因为生成的代码会从模型更新。

     将报告生成错误，类似于："Company.ElementMergeSample.ExampleElement 不包含 CanMergeExampleElement...的定义"

     必须实现 方法 `CanMergeExampleElement` 。

5. 在 Dsl 项目中创建新的 **代码** 文件。 将其内容替换为以下代码，将 命名空间更改为项目的 命名空间。

    ```csharp
    using Microsoft.VisualStudio.Modeling;

    namespace Company.ElementMergeSample // EDIT.
    {
      partial class ExampleModel
      {
        /// <summary>
        /// Called whenever an ExampleElement is to be merged into this ExampleModel.
        /// This happens when the user pastes an ExampleElement
        /// or drags from the toolbox.
        /// Determines whether the merge is allowed.
        /// </summary>
        /// <param name="rootElement">The root element in the merging EGP.</param>
        /// <param name="elementGroupPrototype">The EGP that the user wants to merge.</param>
        /// <returns>True if the merge is allowed</returns>
        private bool CanMergeExampleElement(ProtoElementBase rootElement, ElementGroupPrototype elementGroupPrototype)
        {
          // Allow no more than 4 elements to be added:
          return this.Elements.Count < 4;
        }
      }
    }
    ```

    此简单示例限制可合并到父模型中的元素数。 对于更有趣的条件，方法可以检查接收对象的任何属性和链接。 它还可以检查合并元素的属性，这些属性在 中携带 <xref:Microsoft.VisualStudio.Modeling.ElementGroupPrototype> 。 有关 有关详细信息 `ElementGroupPrototypes` ，请参阅 [自定义复制行为](../modeling/customizing-copy-behavior.md)。 若要详细了解如何编写读取模型的代码，请参阅在程序代码中导航和更新 [模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

6. 测试 DSL：

    1. 按 **F5** 重新生成解决方案。 打开该实例的实验Visual Studio，打开 DSL 的实例。

    2. 通过多种方式创建新元素：

        - 将" **示例元素"** 工具拖到关系图上。

        - 在示例 **模型资源管理器中**，右键单击根节点，然后单击"**添加新示例元素"。**

        - 在关系图上复制并粘贴元素。

    3. 验证不能使用上述任一方法向模型添加四个以上元素。 这是因为它们都使用元素合并指令。

## <a name="example-adding-custom-merge-code-to-an-emd"></a>示例：将自定义合并代码添加到 EMD

在自定义合并代码中，可以定义当用户将工具拖动或粘贴到元素上时会发生什么情况。 有两种方法可以定义自定义合并：

1. Set **使用自定义合并** ，并提供所需的代码。 代码将替换生成的合并代码。 如果要完全重新定义合并功能，请使用此选项。

2. 重写 `MergeRelate` 方法，并选择性地重写 `MergeDisconnect` 方法。 为此，必须设置域类 **的"生成双派生** "属性。 代码可以在基类中调用生成的合并代码。 如果要执行合并后执行其他操作，请使用此选项。

   这些方法仅影响使用此 EMD 执行的合并。 如果要影响创建合并元素的所有方式，另一种替代方法是在嵌入关系上定义 ，在合并域类上 `AddRule` `DeleteRule` 定义 。 有关详细信息，请参阅 [规则在模型中传播更改](../modeling/rules-propagate-changes-within-the-model.md)。

### <a name="to-override-mergerelate"></a>重写 MergeRelate

1. 在 DSL 定义中，确保已定义要添加代码的 EMD。 如果需要，可以添加路径并定义自定义接受代码，如前面的部分所述。

2. 在 DslDefinition 关系图中，选择合并的接收类。 通常它是嵌入关系的源端中的类。

     例如，在从最小语言解决方案生成的 DSL 中，选择 `ExampleModel` 。

3. 在"**属性"** 窗口中，将 **"生成双重派生"设置为** **true。**

4. 重新生成解决方案。

5. 检查 **Dsl\Generated Files\DomainClasses.cs 的内容**。 搜索名为 的方法 `MergeRelate` 并检查其内容。 这有助于编写自己的版本。

6. 在新的代码文件中，为接收类编写分部类，并重写 `MergeRelate` 方法。 请记得调用基方法。 例如：

    ```csharp
    partial class ExampleModel
    {
      /// <summary>
      /// Called when the user drags or pastes an ExampleElement onto the diagram.
      /// Sets the time of day as the name.
      /// </summary>
      /// <param name="sourceElement">Element to be added</param>
      /// <param name="elementGroup">Elements to be merged</param>
      protected override void MergeRelate(ModelElement sourceElement, ElementGroup elementGroup)
      {
        // Connect the element according to the EMD:
        base.MergeRelate(sourceElement, elementGroup);

        // Custom actions:
        ExampleElement mergingElement = sourceElement as ExampleElement;
        if (mergingElement != null)
        {
          mergingElement.Name = DateTime.Now.ToLongTimeString();
        }
      }
    }
    ```

### <a name="to-write-custom-merge-code"></a>编写自定义合并代码

1. 在 **Dsl\Generated Code\DomainClasses.cs** 中，检查名为 的方法 `MergeRelate` 。 这些方法创建新元素和现有模型之间的链接。

    此外，检查名为 的方法 `MergeDisconnect` 。 这些方法在要删除某个元素时将其从模型取消链接。

2. 在 **DSL 资源管理器** 中，选择或创建要自定义的元素合并指令。 在 **"DSL 详细信息"** 窗口中，设置"**使用自定义合并"。**

    设置此选项时，将忽略"处理 **合并** "和" **转发合并** "选项。 代码将改为使用。

3. 重新生成解决方案。 由于生成的代码文件会从模型进行更新，因此其时间比平时长。

    将显示错误消息。 双击错误消息以查看生成的代码中的说明。 这些说明要求你提供两种方法 `MergeRelate` *：YourDomainClass* 和 `MergeDisconnect` *YourDomainClass*

4. 在单独的代码文件中将方法写入分部类定义中。 前面检查过的示例应建议你所需的功能。

   自定义合并代码不会影响直接创建对象和关系的代码，并且不会影响其他 EMD。 若要确保实现其他更改，而不考虑如何创建 元素，请考虑改为编写 `AddRule` 和 `DeleteRule` 。 有关详细信息，请参阅 [规则在模型中传播更改](../modeling/rules-propagate-changes-within-the-model.md)。

## <a name="redirecting-a-merge-operation"></a>重定向合并操作

转发合并指令重定向合并操作的目标。 通常，新目标是初始目标的嵌入父级。

例如，在使用组件关系图模板创建的 DSL 中，"端口"嵌入在"组件"中。 端口在组件形状的边缘显示为小形状。 用户通过拖动"端口"工具到"组件"形状来创建端口。 但有时，用户错误地将端口工具拖动到现有端口而不是组件上，操作会失败。 当存在多个现有端口时，这是一个容易的错误。 为了帮助用户避免这种干扰，可以允许将端口拖动到现有端口上，但将操作重定向到父组件。 操作的工作方式就像目标元素是组件一样。

可以在组件模型解决方案中创建转发合并指令。 如果编译并运行原始解决方案，应会看到用户可以将任意数目的输入 **端口** 或 **输出端口** 元素从工具箱 **拖动到****Component** 元素。 但是，它们不能将端口拖动到现有端口。 "不可用"指针会提醒他们此移动未启用。 但是，可以创建转发合并指令，以便将现有输入端口上意外删除的端口转发到 **Component** 元素。 

### <a name="to-create-a-forward-merge-directive"></a>创建转发合并指令

1. 使用 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 组件模型模板创建解决方案。

2. 通过打开 DslDefinition.dsl 显示 **DSL** 资源管理器。

3. 在 **DSL 资源管理器中**，展开 **"域类"。**

4. **ComponentPort** 抽象域类是 **InPort** 和 **OutPort 的基类**。 右键单击 **"ComponentPort"，** 然后单击"**添加新元素合并指令"。**

    新的" **元素合并指令"** 节点显示在 **"元素合并指令"节点** 下。

5. 选择" **元素合并指令"** 节点并打开 **"DSL 详细信息"** 窗口。

6. 在"索引类"列表中，选择 **"ComponentPort"。**

7. 选择 **"将合并转发到其他域类"。**

8. 在路径选择列表中，展开 **"ComponentPort"，** 展开 **"ComponentHasPorts"，** 然后选择"组件 **"。**

    新路径应类似于以下路径：

    **ComponentHasPorts.Component/！Component**

9. 保存解决方案，然后单击工具栏上最右边的按钮 **解决方案资源管理器模板。**

10. 生成并运行解决方案。 此时将显示 Visual Studio 的新实例。

11. 在 **解决方案资源管理器** 中，打开 mydsl。 将显示关系图和 **ComponentLanguage 工具箱** 。

12. 将 **输入端口** 从 **工具箱** 拖动到另一个 **输入端口。** 接下来，将 **OutputPort** 拖到 **InputPort** ，然后拖动到另一个 **OutputPort**。

     看不到不可用的指针，并且应该能够在现有的 **输入端口** 上删除现有的。 选择新的 **输入端口** 并将其拖到 **组件** 上的另一个点。

## <a name="see-also"></a>请参阅

- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [自定义工具和工具箱](../modeling/customizing-tools-and-the-toolbox.md)
- [线路示例 DSL](https://code.msdn.microsoft.com/Visualization-Modeling-SDK-763778e8)
