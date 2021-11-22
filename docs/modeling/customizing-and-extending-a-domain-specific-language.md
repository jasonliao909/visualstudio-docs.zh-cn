---
title: 自定义和扩展域特定语言
description: 了解 Visual Studio 建模和可视化 SDK (VMSDK) 如何提供可定义建模工具的多个级别。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665517"
---
# <a name="customize-and-extend-a-domain-specific-language"></a>自定义和扩展域特定语言

Visual Studio 建模和可视化 SDK (VMSDK) 提供可定义建模工具的多个级别：

1. 使用 DSL 定义关系图定义域特定语言 (DSL)。 可以通过关系图表示法、可读 XML 格式以及生成代码和其他项目所需的基础工具快速创建 DSL。 有关详细信息，请参阅[如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)。

2. 使用 DSL 定义的更多高级功能微调 DSL。 例如，可以在用户创建元素时显示其他链接。 这些技术主要在 DSL 定义中实现，而有些技术则需要几行程序代码。

3. 通过使用程序代码扩展模型工具。 VMSDK 专门用于轻松将扩展和从 DSL 定义生成的代码相集成。 有关详细信息，请参阅[编写代码以自定义域特定语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)。

> [!NOTE]
> 在更新 DSL 定义文件后，不要忘记在重新生成解决方案之前，先在“解决方案资源管理器”的工具栏中单击“转换所有模板”。

## <a name="article-reference"></a>文章参考

|实现此效果|请参阅本主题|
|-|-|
|允许用户设置形状的颜色和样式属性。|右键单击形状或连接线类，指向“添加已揭示项”，然后单击某一项。|
|关系图上不同类的模型元素看起来类似，共享初始高度和宽度、颜色和工具提示等属性。|使用形状或连接线类之间的继承。 派生形状和派生域类之间的映射继承父级的映射详细信息。<br /><br /> 或者，将不同的域类映射到同一个形状类。|
|模型元素的类由不同的形状上下文显示。|将多个形状类映射到同一个域类。 当你生成解决方案时，请遵循错误报告，并提供所请求的代码以确定要使用的形状。|
|形状颜色或其他功能（如字体）指示当前状态。|请参阅[更新形状和连接线以反映模型](../modeling/updating-shapes-and-connectors-to-reflect-the-model.md)。<br /><br /> 创建更新已公开属性的规则。 请参阅[规则在模型内部传播更改](../modeling/rules-propagate-changes-within-the-model.md)。<br /><br /> 或者，使用 OnAssociatedPropertyChanged() 更新未公开的功能，如链接箭头或字体。|
|形状上的图标更改为指示状态。|在“DSL 详细信息”窗口中设置修饰器映射的可见性。 在同一位置中查找多个图像修饰器。 请参阅[更新形状和连接线以反映模型](../modeling/updating-shapes-and-connectors-to-reflect-the-model.md)。<br /><br /> 或者，重写 `ImageField.GetDisplayImage()`。 请参阅 <xref:Microsoft.VisualStudio.Modeling.Diagrams.ImageField> 中的示例。|
|在任何形状上设置背景图像|重写 InitializeInstanceResources() 以添加定位的 ImageField。|
|将形状嵌套到任何深度|设置递归嵌入树。 定义 BoundsRules 以包含形状。|
|在元素边界上的固定点附加连接线。|定义嵌入的终端元素，由关系图上的小端口表示。 使用 BoundsRules 就地修复端口。 请参阅[可视化和建模 SDK](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db) 中的线路关系图示例。|
|文本字段显示从其他值派生的值。|将文本修饰器映射到计算或自定义存储域属性。 有关详细信息，请参阅[计算和自定义存储属性](../modeling/calculated-and-custom-storage-properties.md)。|
|传播模型元素或形状之间的更改|请参阅[域特定语言中的验证](../modeling/validation-in-a-domain-specific-language.md)。|
|将更改传播到存储外部的资源，如其他 Visual Studio 扩展。|请参阅[事件处理程序在模型外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)。|
|“属性”窗口显示相关元素的属性。|设置属性转发。 请参阅[自定义“属性”窗口](../modeling/customizing-the-properties-window.md)。|
|属性类别|“属性”窗口分为称为“类别”的各个部分。 设置域属性的“类别”。 具有相同类别名称的属性将出现在同一部分中。 还可以设置关系角色的“类别”。|
|控制用户对域属性的访问权限|将“可浏览”设置为“False”，以防止域属性在运行时出现在“属性”窗口中。 你仍可以将其映射到文本修饰器。<br /><br /> “Is UI Read Only”可防止用户更改域属性。<br /><br /> 对域属性的程序访问不受影响。|
|更改 DSL 的模型资源管理器中节点的名称、图标和可见性。|请参阅[自定义模型资源管理器](../modeling/customizing-the-model-explorer.md)。|
|启用复制、剪切和粘贴|在 DSL 资源管理器中设置“编辑器”节点的“启用复制粘贴”属性。|
|每当复制某个元素时，就会复制引用链接及其目标。 例如，复制附加到某一项的注释。|设置源角色的“传播复制”属性（由 DSL 定义关系图中域关系一侧的行表示）。<br /><br /> 编写代码以重写 ProcessOnCopy 来实现更复杂的效果。<br /><br /> 请参阅[自定义复制行为](../modeling/customizing-copy-behavior.md)。|
|删除元素时删除、重新链接相关元素或重新设置其父级。|设置关系角色的“传播删除”值。 为了获得更复杂的效果，请在 DomainModel.cs 中定义的 `MyDslDeleteClosure` 类中重写 `ShouldVisitRelationship` 和 `ShouldVisitRolePlayer` 方法。|
|通过复制和拖放保留形状布局和外观。|将形状和连接线添加到已复制的 `ElementGroupPrototype`。 要重写的最简便方法是 `ElementOperations.CreateElementGroupPrototype()`<br /><br /> 请参阅[自定义复制行为](../modeling/customizing-copy-behavior.md)。|
|在所选位置（例如当前光标位置）粘贴形状。|重写 `ClipboardCommandSet.ProcessOnCopy()` 以使用特定于位置的版本的 `ElementOperations.Merge().` 请参阅[自定义复制行为](../modeling/customizing-copy-behavior.md)。|
|粘贴时创建其他链接|重写 ClipboardCommandSet.ProcessOnPasteCommand()|
|从此关系图、其他 DSL 和 Windows 元素启用拖放操作|请参阅[如何：添加拖放处理程序](../modeling/how-to-add-a-drag-and-drop-handler.md)|
|允许将形状或工具拖到子形状（例如端口）上，就像将其拖动到父级上一样。|在目标对象类上定义元素合并指令，以将已删除的对象转发到父级。 请参阅[自定义元素创建和移动](../modeling/customizing-element-creation-and-movement.md)。|
|允许将形状或工具拖到形状上，并创建其他链接或对象。 例如，允许将注释拖到要链接到的项上。|在目标域类上定义元素合并指令，并定义要生成的链接。 在复杂情况下，可以添加自定义代码。 请参阅[自定义元素创建和移动](../modeling/customizing-element-creation-and-movement.md)。|
|使用一个工具创建一组元素。 例如，具有一组固定端口的组件。|重写 ToolboxHelper.cs 中的工具箱初始化方法。 创建包含元素及其关系链接的元素组原型 (EGP)。 请参阅[自定义工具和工具箱](../modeling/customizing-tools-and-the-toolbox.md)。<br /><br /> 将主体和端口形状包含在 EGP 中，或定义 BoundsRules 以在实例化 EGP 时定位端口形状。|
|使用一个连接工具来实例化多种类型的关系。|将链接连接指令 (LCD) 添加到工具调用的连接生成器中。 LCD 确定两个元素类型的关系的类型。 若要使其依赖于元素的状态，可以添加自定义代码。 请参阅[自定义工具和工具箱](../modeling/customizing-tools-and-the-toolbox.md)。|
|粘滞工具 - 用户可以双击任意工具以连续创建多个形状或连接线。|在 DSL 资源管理器中，选择 `Editor` 节点。 在“属性”窗口中，设置“Uses Sticky Toolbox Items”。|
|定义菜单命令|请参阅[如何：修改标准的菜单命令](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md)|
|用验证规则对模型进行约束|请参阅[域特定语言中的验证](../modeling/validation-in-a-domain-specific-language.md)|
|从 DSL 生成代码、配置文件或文档。|[从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)|
|自定义模型保存到文件的方式。|请参阅[自定义文件存储和 XML 序列化](../modeling/customizing-file-storage-and-xml-serialization.md)|
|将模型保存到数据库或其他介质。|重写 YourLanguageDocData<br /><br /> 请参阅[自定义文件存储和 XML 序列化](../modeling/customizing-file-storage-and-xml-serialization.md)|
|集成多个 DSL，使其作为一个应用程序的一部分工作。|请参阅[使用 Visual Studio Modelbus 集成模型](../modeling/integrating-models-by-using-visual-studio-modelbus.md)。|
|允许第三方扩展 DSL，并控制扩展。|[使用 MEF 扩展 DSL](../modeling/extend-your-dsl-by-using-mef.md)<br /><br /> [使用 DSL 库在 DSL 之间共享类](../modeling/sharing-classes-between-dsls-by-using-a-dsl-library.md)<br /><br /> [定义锁定策略以创建只读段](../modeling/defining-a-locking-policy-to-create-read-only-segments.md)|

## <a name="see-also"></a>另请参阅

- [如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)
- [编写代码以自定义域特定语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)
- [Visual Studio 的建模 SDK - 特定于域的语言](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
