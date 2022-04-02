---
title: XAML 数据绑定诊断
description: 使用 Visual Studio 中的新工具来检测和解决 XAML 项目中的数据绑定错误。
ms.date: 03/28/2022
ms.topic: conceptual
helpviewer_keywords:
- xaml data binding
- xaml diagnostics
author: spadapet
ms.author: tglee
manager: jmartens
ms.technology: vs-xaml-tools
ms.workload:
- multiple
monikerRange: '>=vs-2019'
ms.openlocfilehash: 615e3d64625c3a67cb0e5ed1ab785688ee9ca5ff
ms.sourcegitcommit: 1ed233bb3afc5ae1f52aff8e41f7e650342033ad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2022
ms.locfileid: "141274188"
---
# <a name="xaml-data-binding-diagnostics"></a>XAML 数据绑定诊断

处理 XAML 项目的开发人员通常需要在其应用程序中检测并解决 XAML 数据绑定失败。 现在，在 Visual Studio 2019[版本16.8 或更高版本](/visualstudio/releases/2019/history)中提供了一些工具，并且 Visual Studio 2022 帮助你在调试应用程序时发现这些恼人的数据绑定失败。 常见绑定故障的示例如下所示：

- 绑定到不存在的属性名称： `{Binding Wrong.Name}`
- 绑定到错误类型的值，例如在需要枚举时绑定到布尔值： `Visibility="{Binding IsVisible}"`

由于这些绑定是使用反射在运行时计算的，因此 XAML 编辑器并不总是能捕获它们，并且生成仍将成功。 只有在运行时才会发生失败。

以下文章介绍了 XAML 数据绑定：

- 对于 WPF： [数据绑定概述-WPF .net](/dotnet/desktop/wpf/data/)
- 对于 UWP： [数据绑定概述-UWP 应用程序](/windows/uwp/data-binding/data-binding-quickstart/)
- 对于 Xamarin. Forms： [xamarin。窗体数据绑定-xamarin](/xamarin/xamarin-forms/app-fundamentals/data-binding/)

绑定失败始终写入到 Visual Studio 中的 "调试输出" 窗口。 但这很容易错过调试输出中的绑定故障，因为它包含将绑定失败滚动到视图之外的其他调试信息。 下面是调试输出窗口内 WPF 绑定失败的示例：

:::image type="content" source="media/xaml-binding-failures-output-window-inline.png" alt-text="包含绑定失败的输出窗口的屏幕截图。" lightbox="media/xaml-binding-failures-output-window-expanded.png":::

绑定失败可能是窗口顶部之外的几百行，并且文本不会准确地告诉您哪个绑定发生了故障，因此您需要考虑它并进行搜索。

现在，使用 "XAML 绑定故障" 工具窗口，可以清楚地查看哪些绑定已失败，以及每个失败的相关数据，如 XAML 内的文件位置。 此外，还提供了许多有用的功能，可用于通过搜索、排序，甚至打开在失败绑定上设置了焦点的 XAML 编辑器。

:::image type="content" source="media/xaml-binding-failures-window-inline.png" alt-text="XAML 绑定失败工具窗口的屏幕截图。" lightbox="media/xaml-binding-failures-window-expanded.png":::

双击这些行将打开绑定的源 XAML，如下图所示：

:::image type="content" source="media/xaml-binding-failures-example-inline.png" alt-text="XAML 编辑器中的示例绑定屏幕截图。" lightbox="media/xaml-binding-failures-example-expanded.png":::

## <a name="xaml-binding-failures-tool-window"></a>XAML 绑定失败工具窗口

在调试期间，可以使用 "XAML 绑定失败" 工具窗口。 若要打开它，请参阅 **调试**  >  **Windows**  >  **XAML 绑定失败**。

:::image type="content" source="media/xaml-binding-failures-menu.png" alt-text="&quot;调试&quot; 菜单中的 &quot;XAML 绑定失败&quot; 选项的屏幕截图。":::

或者，在 "应用程序" 工具栏中选择 " **绑定失败** " 按钮。 图标旁边的数字显示了工具窗口中显示的绑定失败数。

:::image type="content" source="media/xaml-binding-failures-in-app.png" alt-text="显示 &quot;绑定失败&quot; 按钮的应用内工具栏屏幕截图。":::

如果工具窗口中没有任何绑定失败，则图标将显示为灰色，而不会在其旁边显示数字。 运行应用程序时，这会很有帮助。 如果你看到图标变为红色，其中包含数字，请单击它以快速跳转到工具窗口，查看发生了哪些绑定失败。 无需密切关注 Visual Studio 工具窗口。 绑定失败时，图标会立即通知你。

:::image type="content" source="media/xaml-binding-failures-in-app-2.png" alt-text="应用内工具栏的屏幕截图，显示 &quot;绑定失败&quot; 按钮且无故障。":::

" [实时可视化树工具" 窗口](inspect-xaml-properties-while-debugging.md)中也会显示类似图标。

:::image type="content" source="media/xaml-binding-failures-live-visual-tree.png" alt-text="实时可视化树工具窗口中的 &quot;绑定失败&quot; 按钮的屏幕截图。":::

下面是对 "XAML 绑定故障" 工具窗口的所有组件的说明。

:::image type="content" source="media/xaml-binding-failures-callouts-inline.png" alt-text="XAML 绑定失败工具窗口的屏幕截图。" lightbox="media/xaml-binding-failures-callouts-expanded.png":::

* 顶部的工具栏包含以下按钮：
  * **清除失败列表**：如果你要在应用中显示新页面并想要查看是否显示任何绑定故障，这会很有用。 当你启动新的调试会话时，将自动清除此列表。
  * **删除所选行**：如果故障已修复或不相关，可以从列表中将其删除。 如果绑定再次失败，则会再次显示已删除的行。
  * **清除所有筛选器**：如果列表中有任何筛选器（如搜索文本），则此按钮将清除这些筛选器并显示完整列表。
  * **合并重复项**：当行位于项模板中时，在行中多次出现相同的绑定。 如果选择了 " **合并重复项** " 按钮， (它周围有轮廓) 则所有重复失败都显示为单个行。 " **计数** " 列将显示发生失败的次数。
* 在顶部的 " **搜索绑定失败** " 框中，可以将故障筛选为仅包含特定文本的故障。
* 表中的列按顺序显示：
  * 显示行是否用于错误或警告的图标。
  * 如果支持在 XAML 中导航到失败 `{Binding}` ，则显示尖括号 `<>` 。 请参阅 [支持的平台](#supported-platforms) 部分。
  * **数据上下文**：这是绑定源对象的类型名称
    * 请参阅 [绑定。源](/dotnet/api/system.windows.data.binding.source)
  * **绑定路径**：这是绑定的属性路径
    * 请参阅 [Binding。路径](/dotnet/api/system.windows.data.binding.path)
  * **Target**：这是将设置绑定值的类型和属性名称。
    * 请参阅 [BindingExpressionBase](/dotnet/api/system.windows.data.bindingexpressionbase.target) 和 [BindingExpressionBase。 system.windows.media.animation.storyboard.targetproperty](/dotnet/api/system.windows.data.bindingexpressionbase.targetproperty)
  * **目标类型**：这是绑定的目标属性的期望类型。
    * 请参阅 [BindingExpressionBase. system.windows.media.animation.storyboard.targetproperty](/dotnet/api/system.windows.data.bindingexpressionbase.targetproperty)
  * **说明**：此列包含绑定失败的具体信息。
  * **文件**、**行** 和 **Project**：如果已知，则这是在 XAML 中定义绑定的位置。
* 右键单击某一行或多个选定行会显示一个上下文菜单，其中包含用于显示/隐藏列或对列进行分组的标准选项。 其他选项如下所示：
  * 将一行或只是单个列中的所有文本复制到剪贴板。
  * 复制原始错误将复制 "调试输出" 窗口中显示的文本。
  * 对于选定的行，视图源将跳到 XAML 中的绑定源。
  * 重置列将撤消对列可见性和排序的所有更改，使你能够快速恢复到最初显示的内容。

若要对列表进行排序，请单击任一列标题。 若要按额外的列进行排序，请按住 **Shift** 键并单击其他列标题。 若要选择显示哪些列和隐藏哪些列，请从快捷菜单中选择“显示列”。 若要更改列显示的顺序，请将任一列标题向左或向右拖动。

双击行或按 **enter** 键导航到源后，可以按 **F8** 或 **Shift + F8** 在绑定失败列表中向下或向上移动。 这与 Visual Studio 中显示列表的其他窗格类似。

## <a name="supported-platforms"></a>受支持的平台

如果绑定失败写入调试输出，则支持大多数 XAML 平台。 某些平台向调试器提供额外的源信息，允许导航到源。

|**平台**|**支持**|**导航到支持的源**|
|---|---|---|
|**WPF .NET Framework**|是|否|
|**WPF .NET 5.0 RC2 +**|是|是|
|**UWP**|是|否|
|**WinUI3 桌面**|是|否|
|**MAUI (多平台应用 UI)**|是|否|
|**Xamarin 4.5.0.266-pre3 +**|是|是|
|**Xamarin 4.5.0.266-pre3 之前**|否|否|

必须在 热重载 中启用 XAML Visual Studio选项，以导航到源以正常工作。 此选项位于"工具 > **""选项** > **""删除"对话框中**：

:::image type="content" source="media/xaml-binding-failures-hot-reload-option.png" alt-text="XAML 选项对话框热重载屏幕截图。":::

导航到源仅适用于 XAML 源文件中定义的绑定，而不是通过代码创建的绑定。 可以清楚地了解哪些行支持导航到源。 如果第二列中没有尖括号图标，则不支持导航到源，如以下屏幕截图中突出显示的行：

:::image type="content" source="media/xaml-binding-failures-no-go-to-code.png" alt-text="显示没有源位置的 XAML 绑定失败的屏幕截图。":::

对于 .NET Framework 中的 WPF，数据绑定失败必须显示在"XAML 绑定失败"窗格的调试输出中，以检测和显示它们。 此选项位于"工具""选项"" >  >  >  > 跟踪输出窗口 **WPF 跟踪设置** 对话框中。 如果设置为"关闭"或"严重"，则数据绑定错误不会写入调试输出，并且无法检测到。 使用 .NET 5、.NET 6 及更高版本中的 WPF 时，数据绑定输出设置不会影响失败列表。

:::image type="content" source="media/xaml-binding-failures-wpf-output-options.png" alt-text="WPF 输出选项的屏幕截图。":::

## <a name="see-also"></a>请参阅

* [XAML 热重载](xaml-hot-reload.md)
