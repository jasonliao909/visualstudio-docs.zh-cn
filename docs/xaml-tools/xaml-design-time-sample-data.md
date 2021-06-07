---
title: 在 Visual Studio 中使用 XAML 设计器的设计时示例数据
description: 了解如何在 XAML 中使用设计时示例数据。
ms.date: 06/01/2021
ms.topic: conceptual
author: alihamie
ms.author: tglee
manager: jmartens
monikerRange: vs-2019
ms.openlocfilehash: 8303e1150db7c12c404e8f67bce52418fbd05b9d
ms.sourcegitcommit: ab5735d64a6ad7aecabf5d6df159888e3246bff5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2021
ms.locfileid: "111433787"
---
# <a name="use-design-time-sample-data-with-the-xaml-designer-in-visual-studio"></a>在 Visual Studio 中使用 XAML 设计器的设计时示例数据

某些数据依赖控件（例如 ListView、ListBox 或 DataGrid）难以直观显示，无需数据。 在本文档中，我们将回顾一种新方法，该方法允许开发人员使用新的设计器在这些控件中启用示例数据，从而使用 **wpf .Net Core** 项目或 **wpf .NET Framework** 项目。 

## <a name="sample-data-feature-basics"></a>示例数据功能基础知识

示例数据仅用于设计时可视化，这意味着它仅出现在 XAML 设计器中，而不显示在运行的应用程序中。 因此，它将应用于 System.windows.controls.itemscontrol.itemssource 属性的设计时版本 `d:ItemsSource` 。 示例数据需要设计时命名空间才能工作。 首先，将以下代码行添加到 XAML 文档的标头（如果这些代码行尚不存在）：

> [!NOTE]
> 若要深入了解 XAML 中的设计时属性，请访问 [xaml 设计时属性](../xaml-tools/xaml-designtime-data.md) 。

```xml
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
```

添加命名空间后，可以使用 `d:ItemsSource="{d:SampleData}"` 在 ListView、Listbox 或 DataGrid 中启用示例数据。 例如：

```xml
<DataGrid d:ItemsSource="{d:SampleData}"/>
```

[![数据网格示例](media\xaml-sample-data-empty-datagrid.png "DataGrid 上启用的示例数据")](media\xaml-sample-data-empty-datagrid.png#lightbox)

在此示例中，没有 `d:ItemsSource="{d:SampleData}"` XAML 设计器会显示空的 DataGrid。 `d:SampleData`现在，它会显示生成的默认示例数据。

默认情况下，将显示5个项目。 但是，可以使用 **ItemCount** 属性来指定要显示的项目数。 例如：`d:ItemsSource="{d:SampleData ItemCount=2}"`

## <a name="sample-data-works-with-datatemplates"></a>示例数据适用于 datatemplates

使用数据模板时，示例数据适用于 ListBox、ListView 或 DataGrid 控件。 示例数据功能将分析 System.windows.datatemplate> 并尝试为其生成适当的数据。 只会为使用绑定的 DataTemplates 中的元素生成示例数据。 即使绑定还没有源，也会生成示例数据。
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

[![使用 System.windows.datatemplate> 的示例数据 ListView](media\xaml-sample-data-templated-listview.png "包含 System.windows.datatemplate> 的 ListView 中使用的示例数据")](media\xaml-sample-data-templated-listview.png#lightbox)

## <a name="enable-sample-data-with-suggested-actions"></a>使用建议的操作启用示例数据

若要从设计器中轻松启用或禁用控件的示例数据，可以使用建议的操作功能。 建议的操作是设计器上的一个灯泡，在选择控件时显示在右上方。 您可以通过选择控件，单击灯泡，然后单击 "打开" 来启用示例数据 `Show Sample Data` 。 例如：

[![示例数据建议的操作](media\xaml-sample-data-suggested-actions.png "使用建议的操作启用示例数据")](media\xaml-sample-data-suggested-actions.png#lightbox)

## <a name="sample-data-with-ivalueconverters"></a>示例数据与 IValueConverters 

示例数据功能不完全支持转换器。 但是，可以通过执行以下一项或两项操作来使其正常工作：
- 请确保您的 `Convert` 函数可以处理某个方案，其中值已是 targetType。

- 实现 `ConvertBack` 将值转换回原始类型的函数。 

## <a name="troubleshooting"></a>疑难解答

如果您的示例数据未显示任何内容，或者无法显示正确的类型，则可以尝试刷新设计器或关闭并重新打开该页。

如果你遇到本部分中未列出的问题，或者无法通过刷新页面修复此问题，请通过使用 [报告问题](../ide/how-to-report-a-problem-with-visual-studio.md) 工具告诉我们。

### <a name="requirements"></a>要求

- 示例数据需要 Visual Studio 2019 版本 [16.10](/visualstudio/releases/2019/release-notes-v16.10) 或更高版本。

- 使用新的设计器时，支持面向 .NET Core 或 .NET Framework 的 Windows Presentation Foundation (WPF) 的 Windows 桌面项目。 若要为 .NET Framework 启用新设计器，请 > 选项 > 环境 > 预览功能中选择 "新建 WPF XAML 设计器"，然后重新启动 Visual Studio。

## <a name="see-also"></a>另请参阅

- [XAML 设计时属性](../xaml-tools/xaml-designtime-data.md)
- [WPF 应用中的 XAML](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [UWP 应用中的 XAML](/windows/uwp/xaml-platform/xaml-overview)
- [Xamarin.Forms 应用中的 XAML](/xamarin/xamarin-forms/xaml/)