---
title: 自定义和扩展域特定语言
description: 了解 VMSDK Visual Studio建模和可视化 SDK (VMSDK) 提供了多个级别，可在这些级别定义建模工具。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools, creating solutions
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 5c6a6572e8e26f6ab60a8af620d18642a3c35dbd
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122055570"
---
# <a name="customize-and-extend-a-domain-specific-language"></a>自定义和扩展域特定语言

Visual StudioVMSDK (建模和可视化 SDK) 提供了多个级别，可在这些级别定义建模工具：

1. 使用 DSL 定义关系图 (DSL) 域特定语言。 可以使用关系图表示法、可读 XML 窗体以及生成代码和其他项目所需的基本工具快速创建 DSL。 有关详细信息，请参阅 [How to Define a Domain-Specific Language](../modeling/how-to-define-a-domain-specific-language.md)。

2. 使用 DSL 定义的更高级功能微调 DSL。 例如，可以在用户创建元素时显示其他链接。 这些技术主要在 DSL 定义中实现，有些技术需要几行程序代码。

3. 使用程序代码扩展建模工具。 VMSDK 专门用于轻松将扩展和从 DSL 定义生成的代码相集成。 有关详细信息，请参阅 [编写代码以自定义Domain-Specific语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)。

> [!NOTE]
> 更新 DSL 定义文件后，在重新生成解决方案之前，不要忘记单击解决方案工具栏解决方案资源管理器"转换所有模板"。 

## <a name="article-reference"></a>文章参考

|实现此效果|请参阅本主题|
|-|-|
|允许用户设置形状的颜色和样式属性。|右键单击形状或连接器类，指向" **添加公开"，** 然后单击项。|
|不同类的模型元素在关系图上看起来类似，共享初始高度和宽度、颜色、工具提示等属性。|在形状或连接器类之间使用继承。 派生形状和派生域类之间的映射继承父类的映射详细信息。<br /><br /> 或者，将不同的域类映射到同一形状类。|
|模型元素的类由不同的形状上下文显示。|将多个形状类映射到同一个域类。 生成解决方案时，请遵循错误报告并提供请求的代码，确定要使用哪个形状。|
|形状颜色或其他功能（如字体）指示当前状态。|请参阅 [更新形状和连接器以反映模型](../modeling/updating-shapes-and-connectors-to-reflect-the-model.md)。<br /><br /> 创建更新公开属性的规则。 请参阅 [规则在模型中传播更改](../modeling/rules-propagate-changes-within-the-model.md)。<br /><br /> 或者，使用 OnAssociatedPropertyChanged () 更新未公开的功能，例如链接箭头或字体。|
|形状更改图标以指示状态。|在"DSL 详细信息"窗口中设置修饰器映射的可见性。 在同一位置找到多个图像修饰器。 请参阅  [更新形状和连接器以反映模型](../modeling/updating-shapes-and-connectors-to-reflect-the-model.md)。<br /><br /> 或者，重写 `ImageField.GetDisplayImage()` 。 请参阅 中的示例 <xref:Microsoft.VisualStudio.Modeling.Diagrams.ImageField> 。|
|在任何形状上设置背景图像|重写 InitializeInstanceResources () 添加定位的 ImageField。|
|将形状嵌套到任何深度|设置递归嵌入树。 定义 BoundsRules 以包含形状。|
|在元素边界上的固定点附加连接器。|定义由关系图上的小端口表示的嵌入式终端元素。 使用 BoundsRules 修复就地端口。 请参阅可视化和建模 [SDK 中的线路图示例](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db)。|
|文本字段显示派生自其他值的值。|将文本修饰器映射到"计算"或"自定义存储属性。 有关详细信息，请参阅计算[和自定义存储属性](../modeling/calculated-and-custom-storage-properties.md)。|
|传播模型元素之间或形状之间的更改|请参阅 [在语言中Domain-Specific验证](../modeling/validation-in-a-domain-specific-language.md)。|
|将更改传播到存储Visual Studio扩展等资源。|请参阅 [事件处理程序在模型 外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)。|
|属性窗口显示相关元素的属性。|设置属性转发。 请参阅 [自定义属性窗口](../modeling/customizing-the-properties-window.md)。|
|属性类别|属性窗口划分为称为"类别"的部分。 设置 **域属性** 的"类别"。 类别名称相同的属性将显示在同一部分中。 还可以设置关系 **角色** 的"类别"。|
|控制用户对域属性的访问|将 **Is Browsable** 设置为 false 可防止域属性属性窗口运行时出现在域中。 仍可以映射到文本修饰器。<br /><br /> **UI 只读是否** 阻止用户更改域属性。<br /><br /> 对域属性的程序访问不受影响。|
|更改 DSL 模型资源管理器中节点的名称、图标和可见性。|请参阅 [自定义模型资源管理器](../modeling/customizing-the-model-explorer.md)。|
|启用复制、剪切和粘贴|在 DSL **资源管理器中设置** 编辑器节点的"启用复制粘贴"属性。|
|复制元素时复制引用链接及其目标。 例如，复制附加到项的注释。|设置 **源角色的** "传播复制"属性 (DSL 定义关系图中域关系一侧的行表示) 。<br /><br /> 编写代码以重写 ProcessOnCopy 以实现更复杂的效果。<br /><br /> 请参阅 [自定义复制行为](../modeling/customizing-copy-behavior.md)。|
|删除元素时删除、重定父元素或重新链接相关元素。|设置 **关系角色的"** 传播删除"值。 对于更复杂的效果，请重写 类中的 和 `ShouldVisitRelationship` `ShouldVisitRolePlayer` 方法（在 `MyDslDeleteClosure` **DomainModel.cs 中定义**）。|
|在复制和拖放时保留形状布局和外观。|将形状和连接器添加到复制的 `ElementGroupPrototype` 。 最方便的重写方法是 `ElementOperations.CreateElementGroupPrototype()`<br /><br /> 请参阅 [自定义复制行为](../modeling/customizing-copy-behavior.md)。|
|在所选位置（例如当前光标位置）粘贴形状。|重写 `ClipboardCommandSet.ProcessOnCopy()` 以使用 特定于位置的 版本 `ElementOperations.Merge().` ，请参阅 [自定义复制行为](../modeling/customizing-copy-behavior.md)。|
|在粘贴时创建其他链接|替代 ClipboardCommandSet.ProcessOnPasteCommand () |
|启用此关系图、其他 DSL 和Windows拖放|请参阅 [如何：添加拖放处理程序](../modeling/how-to-add-a-drag-and-drop-handler.md)|
|允许将形状或工具拖动到子形状（如端口）上，就像将其拖动到父形状上一样。|在目标对象类上定义元素合并指令，将删除的对象转发给父级。 请参阅 [自定义元素创建和移动](../modeling/customizing-element-creation-and-movement.md)。|
|允许将形状或工具拖动到形状上，并创建其他链接或对象。 例如，允许将注释放到要链接到的项上。|在目标域类上定义元素合并指令，并定义要生成的链接。 在复杂情况下，可以添加自定义代码。 请参阅 [自定义元素创建和移动](../modeling/customizing-element-creation-and-movement.md)。|
|使用一个工具创建一组元素。 例如，具有一组固定端口的组件。|重写 ToolboxHelper.cs 中的工具箱初始化方法。 使用包含元素及其 (链接的 EGP) 元素组原型。 请参阅 [自定义工具和工具箱](../modeling/customizing-tools-and-the-toolbox.md)。<br /><br /> 在 EGP 中包括主体和端口形状，或定义 BoundsRules 以在实例化 EGP 时定位端口形状。|
|使用一个连接工具实例化多种类型的关系。|向工具连接的连接生成器 () 将 LINK (指令添加到连接生成器。 LCD 根据两个元素的类型确定关系的类型。 若要使这取决于元素状态，可以添加自定义代码。 请参阅 [自定义工具和工具箱](../modeling/customizing-tools-and-the-toolbox.md)。|
|粘滞工具 - 用户可以双击任何工具，连续创建多个形状或连接器。|在 DSL 资源管理器中，选择 `Editor` 节点。 在属性窗口中，设置"**使用粘滞工具箱项"。**|
|定义菜单命令|请参阅 [如何：修改标准菜单命令](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md)|
|使用验证规则约束模型|请参阅 [以语言Domain-Specific验证](../modeling/validation-in-a-domain-specific-language.md)|
|从 DSL 生成代码、配置文件或文档。|[从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)|
|自定义如何将模型保存到文件。|请参阅[自定义文件存储和 XML 序列化](../modeling/customizing-file-storage-and-xml-serialization.md)|
|将模型保存到数据库或其他媒体。|替代 *YourLanguage* DocData<br /><br /> 请参阅[自定义文件存储和 XML 序列化](../modeling/customizing-file-storage-and-xml-serialization.md)|
|集成多个 DLL，以便它们作为一个应用程序的一部分工作。|请参阅[使用模型总线 Visual Studio模型](../modeling/integrating-models-by-using-visual-studio-modelbus.md)。|
|允许 DSL 由第三方扩展，并控制扩展。|[使用 MEF 扩展 DSL](../modeling/extend-your-dsl-by-using-mef.md)<br /><br /> [使用 DSL 库在 DSL 之间共享类](../modeling/sharing-classes-between-dsls-by-using-a-dsl-library.md)<br /><br /> [定义锁定策略以创建只读段](../modeling/defining-a-locking-policy-to-create-read-only-segments.md)|

## <a name="see-also"></a>请参阅

- [如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)
- [编写代码以自定义Domain-Specific语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)
- [Visual Studio 的建模 SDK - 特定于域的语言](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
