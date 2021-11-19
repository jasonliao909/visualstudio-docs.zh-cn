---
title: 域属性的属性
description: 了解域属性是可保留值的模型元素的一项功能，以及如何在关系图上的域类框中列出域属性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, domain properties
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 82fa25201813e6a4380162a11fdcfcf5736c82be
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663923"
---
# <a name="properties-of-domain-properties"></a>域属性的属性
域属性是可保留值的模型元素的一项功能。 例如，`Person` 域类可以具有属性 `Name` 和 `BirthDate`。 在 DSL 定义中，域属性列出在关系图上的域类框中以及 DSL 资源管理器中的域类下。 有关详细信息，请参阅[如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)。

> [!NOTE]
> “属性”一词有两种用法。 域属性是在域类上定义的一项功能。 相反，DSL 的许多元素具有属性，它们列在 DSL 定义的“属性”窗口中。 例如，每个域属性都具有一组属性，本主题对它们进行了描述。

 在运行时，如果用户创建域类的实例，则可以在“属性”窗口中查看域属性的值，并且这些值可显示在形状上。

 大多数域属性都将实现为普通 CLR 属性。 但是，从编程的角度来看，域属性具有比普通程序属性更丰富的功能：

- 可以定义监视属性状态的规则和事件。 有关详细信息，请参阅[响应和传播更改](../modeling/responding-to-and-propagating-changes.md)。

- 事务有助于防止不一致的状态。 有关详细信息，请参阅[在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

  当在关系图或 DSL 资源管理器中选择域属性时，可以在“属性”窗口中查看以下项。 有关如何使用这些项的详细信息，请参阅[自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

|属性|说明|默认值|
|-|-|-|
|**说明**|用于记录已生成设计器的用户界面 (UI) 的说明。|\<none>|
|**显示名称**|将针对此域属性在生成的设计器中显示的名称。 它可以包含空格和标点，例如“Song Title”。|\<none>|
|**元素名称提供程序**|该提供程序仅在已将 `Is Element Name` 设置为 `true` 时才适用。 你可以编写用于为域类的新元素提供名称，从而重写默认行为的代码。<br /><br /> 在 DSL 项目的代码文件中，创建派生自 <xref:Microsoft.VisualStudio.Modeling.ElementNameProvider> 的类。<br /><br /> 然后，在 DSL 资源管理器中，右键单击 DSL 的根，然后单击“添加外部类型”。 输入类的名称。<br /><br /> 再次选择此域属性，然后在下拉列表中选择类的名称。|\<none>|
|**Getter 访问修饰符**|域类的访问级别（`public` 或 `internal`）。 这将控制程序代码可访问属性的范围。|`public`|
|**帮助关键字**|用于针对此域属性索引 F1 帮助的可选关键字。|\<none>|
|**可浏览**|如果为 `True`，则在此 DSL 的模型处于打开状态时在“属性”窗口中向用户显示域属性。<br /><br /> 如果为 `False`，则域属性将隐藏在 UI 中。<br /><br /> 如果想要使域属性可见但只读，则设置“UI 只读”。|`True`|
|**元素名称**|如果为 `True`，则此域属性将在 DSL 资源管理器中显示为其模型元素的名称。<br /><br /> 新模型元素将接收此属性的唯一默认值。 如果想要控制生成这些值的方式，则设置“元素名称提供程序”。|`False`|
|**UI 只读**|如果为 `True`，则无法使用 UI 更改域属性的值。 它仍可通过程序进行设置，并且将在“属性”窗口中可见。<br /><br /> 如果想要向用户隐藏域属性，则设置“可浏览”。 如果想要通过程序控制访问权限，则设置“Setter 访问修饰符”。|`False`|
|**种类**|域属性的类型（`Normal`、`Calculated` 或 `CustomStorage`）。 有关详细信息，请参阅[计算和自定义存储属性](../modeling/calculated-and-custom-storage-properties.md)。|`Normal`|
|**Name**|此域属性的名称。 它必须是有效标识符，例如 SongTitle。|\<none>|
|**备注**|与此域属性相关联的非正式说明。|\<none>|
|**Setter 访问修饰符**|用于 Setter 的访问修饰符。 这将控制程序代码可设置属性的范围。|`public`|
|类型|属性的类型。 若要添加到可用类型的列表，请在 DSL 资源管理器中右键单击 DSL 的根，然后单击“添加外部类型”。|`String`|

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))