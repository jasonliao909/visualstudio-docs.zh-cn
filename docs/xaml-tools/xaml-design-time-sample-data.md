---
title: 在 Visual Studio 中使用 XAML 设计器的设计时示例数据
description: 了解如何在 XAML 中使用设计时示例数据。
ms.date: 06/01/2021
ms.topic: conceptual
author: alihamie
ms.author: tglee
manager: jmartens
ms.technology: vs-xaml-tools
monikerRange: '>=vs-2019'
ms.openlocfilehash: b12ab7e93fbd7c7adab188492853ec4a9230cc7d
ms.sourcegitcommit: 2eb12954b7b0ac9508fff11a86c54e880f3d104f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2021
ms.locfileid: "129439803"
---
# <a name="use-design-time-sample-data-with-the-xaml-designer-in-visual-studio"></a>在 Visual Studio 中使用 XAML 设计器的设计时示例数据

某些数据相关的控件（如 `ListView` 、 `ListBox` 和 `DataGrid` ）难以直观显示，无需数据。 在本文中，我们将回顾一种新方法，该方法允许使用 XAML 设计器中的 Visual Studio 来处理 Windows Presentation Foundation (WPF) .net Core 项目或 wpf .NET Framework 项目的开发人员，以便在这些控件中启用示例数据。 

## <a name="requirements"></a>要求

示例数据功能需要 Visual Studio 2019 [16.10](/visualstudio/releases/2019/release-notes-v16.10)或更高版本。

使用新设计器时，此功能支持面向适用于 .net Core 的 WPF 或 .NET Framework 的 Windows 桌面项目。 若要为 .NET Framework 启用新设计器：

1. 请参阅 "**工具**" "选项" "  >    >  **环境**  >  **预览功能**"。
2. **为 .NET Framework 选择 "新建 WPF XAML 设计器**，然后重新启动 Visual Studio"。

## <a name="basics-of-the-sample-data-feature"></a>示例数据功能的基础知识

示例数据功能仅用于设计时可视化。 它仅出现在 XAML 设计器中，不出现在正在运行的应用程序中。 因此，它将应用于属性的设计时版本 `ItemsSource` `d:ItemsSource` 。 示例数据需要设计时命名空间才能工作。 

> [!NOTE]
> 若要了解有关 XAML 中的设计时属性的详细信息，请参阅 [xaml 设计时属性](../xaml-tools/xaml-designtime-data.md)。

首先，将以下代码行添加到 XAML 文档的标头（如果这些代码行尚不存在）：

```xml
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
```

添加命名空间后，可以使用 `d:ItemsSource="{d:SampleData}"` 在 `ListView` 、或控件中启用示例数据 `Listbox` `DataGrid` 。 例如：

```xml
<DataGrid d:ItemsSource="{d:SampleData}"/>
```

[![显示数据网格中的示例数据的屏幕截图。](media\xaml-sample-data-empty-datagrid.png "数据网格上启用的示例数据")](media\xaml-sample-data-empty-datagrid.png#lightbox)

在此示例中，如果没有 `d:ItemsSource="{d:SampleData}"` ，XAML 设计器会显示空的数据网格。 相反，对于 `d:SampleData` ，它现在会显示生成的默认示例数据。

默认情况下，会显示五个项目。 但是，可以使用 `ItemCount` 属性指定要显示的项的数目。 例如：`d:ItemsSource="{d:SampleData ItemCount=2}"`。

## <a name="sample-data-with-data-templates"></a>数据模板示例数据

`ListBox`使用数据模板时，示例数据功能适用于、 `ListView` 或 `DataGrid` 控件。 此功能将分析 `DataTemplate` 控件并尝试为其生成适当的数据。 

示例数据将仅为使用绑定的数据模板中的元素生成。 即使绑定还没有源，也会生成示例数据。 例如：

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

[![在带有数据模板的列表视图中显示示例数据的屏幕截图。](media\xaml-sample-data-templated-listview.png "使用数据模板的列表视图中使用的示例数据")](media\xaml-sample-data-templated-listview.png#lightbox)

## <a name="sample-data-with-suggested-actions"></a>带建议操作的示例数据

若要从设计器中轻松启用或禁用控件的示例数据，可以使用建议的操作功能。 建议的操作是在选择控件时显示在右上角的设计器上的灯泡。 您可以通过选择控件，选择灯泡，然后选择 " **显示示例数据**" 来启用示例数据。 例如：

[![用建议的操作显示示例数据的屏幕截图。](media\xaml-sample-data-suggested-actions.png "使用建议的操作启用示例数据")](media\xaml-sample-data-suggested-actions.png#lightbox)

## <a name="sample-data-with-the-ivalueconverter-interface"></a>示例数据与 IValueConverter 接口 

示例数据功能不完全支持转换器或 `IValueConverter` 接口。 但是，可以通过执行以下一项或两项操作来使其正常工作：

- 请确保 `Convert` 函数可以处理值已是目标类型的方案。
- 实现 `ConvertBack` 将值转换回原始类型的函数。 

## <a name="troubleshooting"></a>疑难解答

如果您的示例数据未显示任何内容，或者无法显示正确的类型，则可以尝试刷新设计器或关闭并重新打开该页。

如果你遇到本部分中未列出的问题或无法通过刷新页面修复的问题，请通过使用 [报告问题](../ide/how-to-report-a-problem-with-visual-studio.md) 工具告诉我们。

## <a name="see-also"></a>另请参阅

- [XAML 设计时属性](../xaml-tools/xaml-designtime-data.md)
- [WPF 应用中的 XAML](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [UWP 应用中的 XAML](/windows/uwp/xaml-platform/xaml-overview)
- [Xamarin.Forms 应用中的 XAML](/xamarin/xamarin-forms/xaml/)