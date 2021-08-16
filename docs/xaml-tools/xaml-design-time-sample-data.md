---
title: 将设计时示例数据与XAML 设计器一Visual Studio
description: 了解如何在 XAML 中使用设计时示例数据。
ms.date: 06/01/2021
ms.topic: conceptual
author: alihamie
ms.author: tglee
manager: jmartens
ms.technology: vs-xaml-tools
monikerRange: '>=vs-2019'
ms.openlocfilehash: e129875a4ac4c5d66e72e7180c58131c48cd486ddc24e24923556d2261dc094e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121296302"
---
# <a name="use-design-time-sample-data-with-the-xaml-designer-in-visual-studio"></a>将设计时示例数据与XAML 设计器一Visual Studio

如果没有数据，某些数据依赖控件（如 ListView、ListBox 或 DataGrid）难以可视化。 本文档将介绍一种新方法，使使用新设计器处理 **WPF .NET Core** 项目或 **WPF .NET Framework** 项目的开发人员能够在这些控件中启用示例数据。 

## <a name="sample-data-feature-basics"></a>示例数据功能基础知识

示例数据仅适用于设计时可视化，这意味着它只出现在 XAML 设计器中，而不是显示在正在运行的应用中。 因此，它应用于 ItemsSource 属性 的设计时版本 `d:ItemsSource` 。 示例数据需要设计时命名空间来工作。 首先，将以下代码行添加到 XAML 文档的标头（如果这些代码行尚不存在）：

> [!NOTE]
> 若要 [详细了解 XAML 中的](../xaml-tools/xaml-designtime-data.md) 设计时属性，请访问 XAML 设计时属性。

```xml
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
```

添加命名空间后，可以使用 在 `d:ItemsSource="{d:SampleData}"` ListView、Listbox 或 DataGrid 中启用示例数据。 例如：

```xml
<DataGrid d:ItemsSource="{d:SampleData}"/>
```

[![使用 DataGrid 的示例数据](media\xaml-sample-data-empty-datagrid.png "在 DataGrid 上启用的示例数据")](media\xaml-sample-data-empty-datagrid.png#lightbox)

此示例中，如果没有 `d:ItemsSource="{d:SampleData}"` XAML 设计器会显示一个空的 DataGrid。 相反， `d:SampleData` 它现在显示生成的默认示例数据。

默认情况下，会显示 5 个项。 但是，可以使用 **ItemCount 属性** 指定要显示的项数。 例如：`d:ItemsSource="{d:SampleData ItemCount=2}"`

## <a name="sample-data-works-with-datatemplates"></a>示例数据适用于 datatemplate

使用数据模板时，示例数据适用于 ListBox、ListView 或 DataGrid 控件。 "示例数据"功能将分析 DataTemplate，并尝试生成相应的数据。 只会为使用绑定的 DataTemplates 中的元素生成示例数据。 即使绑定还没有源，也会生成示例数据。
例如：

```xml
<ListView d:ItemsSource="{d:SampleData ItemCount=3}">
     <ListView.ItemTemplate>
        <DataTemplate>
            <StackPanel Orientation="Horizontal">
                <Image Width="50" Source="{Binding ProfilePicture}"/>
                <StackPanel Orientation="Vertical">
                    <TextBlock Text="{Binding FirstName}" Margin="5"/>
                    <Label Content="{Binding LastName}"/>
                </StackPanel>
            </StackPanel>
        </DataTemplate>
    </ListView.ItemTemplate>
</ListView>
```

[![包含 DataTemplate 的示例数据 ListView](media\xaml-sample-data-templated-listview.png "在包含 DataTemplate 的 ListView 中使用的示例数据")](media\xaml-sample-data-templated-listview.png#lightbox)

## <a name="enable-sample-data-with-suggested-actions"></a>使用建议的操作启用示例数据

若要从设计器轻松启用或禁用控件的示例数据，可以使用"建议的操作"功能。 建议的操作是设计器上的灯泡，在选择控件时显示在右上方。 可以通过选择控件、单击灯泡并单击 来启用示例数据 `Show Sample Data` 。 例如：

[![示例数据建议的操作](media\xaml-sample-data-suggested-actions.png "使用建议的操作启用示例数据")](media\xaml-sample-data-suggested-actions.png#lightbox)

## <a name="sample-data-with-ivalueconverters"></a>使用 IValueConverters 的示例数据 

示例数据功能并不完全支持转换器。 但是，可以通过执行以下一项或两项操作来使它正常工作：
- 确保函数 `Convert` 可以处理值已是 targetType 的方案。

- 实现 `ConvertBack` 将值转换回原始类型的函数。 

## <a name="troubleshooting"></a>疑难解答

如果示例数据未显示任何内容或无法显示正确的类型，可以尝试刷新设计器或关闭并重新打开页面。

如果遇到本部分未列出的问题，或者无法通过刷新页面进行修复，请使用"报告问题"工具 [告知](../ide/how-to-report-a-problem-with-visual-studio.md) 我们。

### <a name="requirements"></a>要求

- 示例数据Visual Studio 2019 版本[16.10](/visualstudio/releases/2019/release-notes-v16.10)或更高版本。

- 支持Windows面向 .NET Core Windows Presentation Foundation (WPF) ，或者.NET Framework设计器时面向的桌面项目。 若要为 .NET Framework启用新设计器，请转到"工具>选项"> 环境 > 预览功能"，为 .NET Framework 选择"新建 WPF XAML 设计器"，然后Visual Studio。

## <a name="see-also"></a>另请参阅

- [XAML 设计时属性](../xaml-tools/xaml-designtime-data.md)
- [WPF 应用中的 XAML](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [UWP 应用中的 XAML](/windows/uwp/xaml-platform/xaml-overview)
- [Xamarin.Forms 应用中的 XAML](/xamarin/xamarin-forms/xaml/)