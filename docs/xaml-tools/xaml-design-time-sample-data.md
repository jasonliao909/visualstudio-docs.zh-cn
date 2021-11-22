---
title: 将设计时示例数据与 Visual Studio 中的 XAML 设计器结合使用
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
# <a name="use-design-time-sample-data-with-the-xaml-designer-in-visual-studio"></a>将设计时示例数据与 Visual Studio 中的 XAML 设计器结合使用

一些依赖于数据的控件（例如，`ListView`、`ListBox` 和 `DataGrid`）在没有数据的情况下很难可视化。 本文将介绍一种新的方法，这种方法让使用 Visual Studio 中的 XAML 设计器处理 Windows Presentation Foundation (WPF) .NET Core 项目或 .NET Framework 项目的开发人员可以启用这些控件中的示例数据。 

## <a name="requirements"></a>要求

示例数据功能需要 Visual Studio 2019 [16.10](/visualstudio/releases/2019/release-notes-v16.10) 或更高版本。

使用新的设计器时，该功能支持面向 WPF for .NET Core 或 .NET Framework 的 Windows 桌面项目。 若要为 .NET Framework 启用新设计器：

1. 请转到“工具” > “选项” > “环境” > “预览功能”。
2. 选择“适用于 .NET Framework 的新的 WPF XAML 设计器”，然后重启 Visual Studio。

## <a name="basics-of-the-sample-data-feature"></a>示例数据功能的基础知识

示例数据功能仅适用于设计时可视化。 它仅出现在 XAML 设计器中，不会出现在正在运行的应用中。 因此，它应用于 `ItemsSource` 属性 `d:ItemsSource` 的设计时版本。 示例数据需要设计时命名空间才能运行。 

> [!NOTE]
> 若要了解有关 XAML 中的设计时属性的详细信息，请参阅 [XAML 设计时属性](../xaml-tools/xaml-designtime-data.md)。

首先，将以下代码行添加到 XAML 文档的标头（如果这些代码行尚不存在）：

```xml
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
```

添加命名空间后，可以使用 `d:ItemsSource="{d:SampleData}"` 来启用 `ListView`、`Listbox` 或 `DataGrid` 控件中的示例数据。 例如：

```xml
<DataGrid d:ItemsSource="{d:SampleData}"/>
```

[![显示数据网格中的示例数据的屏幕截图。](media\xaml-sample-data-empty-datagrid.png "对数据网格启用的示例数据")](media\xaml-sample-data-empty-datagrid.png#lightbox)

在此示例中，如果没有 `d:ItemsSource="{d:SampleData}"`，XAML 设计器将显示空的数据网格。 相反，对于 `d:SampleData`，它现在显示已生成的默认示例数据。

默认情况下，会显示五个项。 但是，可以使用 `ItemCount` 属性指定要显示的项的数目。 例如：`d:ItemsSource="{d:SampleData ItemCount=2}"`。

## <a name="sample-data-with-data-templates"></a>具有数据模板的示例数据

在使用数据模板时，示例数据功能适用于 `ListBox`、`ListView` 或 `DataGrid` 控件。 此功能将分析 `DataTemplate` 控件并尝试为其生成适当的数据。 

将仅为使用绑定的数据模板中的元素生成示例数据。 即使绑定还没有源，也会生成示例数据。 例如：

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

[![显示带有数据模板的列表视图中的示例数据的屏幕截图。](media\xaml-sample-data-templated-listview.png "在具有数据模板的列表视图中使用的示例数据")](media\xaml-sample-data-templated-listview.png#lightbox)

## <a name="sample-data-with-suggested-actions"></a>具有“建议的操作”的示例数据

若要从设计器轻松地为控件启用或禁用示例数据，可以使用“建议的操作”功能。 “建议的操作”是设计器中的灯泡，在选择控件时会显示在右上方。 可以通过选择控件、选择灯泡，然后选择“显示示例数据”来启用示例数据。 例如：

[![显示示例数据以及“建议的操作”的屏幕截图。](media\xaml-sample-data-suggested-actions.png "启用具有“建议的操作”的示例数据")](media\xaml-sample-data-suggested-actions.png#lightbox)

## <a name="sample-data-with-the-ivalueconverter-interface"></a>具有 IValueConverter 接口的示例数据 

“示例数据”功能不完全支持转换器或 `IValueConverter` 接口。 但是，可以通过执行以下一项或两项操作来使其工作：

- 请确保 `Convert` 函数可以处理值已是目标类型的方案。
- 执行将值转换回原始类型的 `ConvertBack` 函数。 

## <a name="troubleshooting"></a>疑难解答

如果示例数据未显示任何内容或无法显示正确的类型，则可以尝试刷新设计器或关闭并重新打开页面。

如果你遇到此部分中未列出的问题或无法通过刷新页面来修复的问题，请使用[报告问题](../ide/how-to-report-a-problem-with-visual-studio.md)工具告知我们。

## <a name="see-also"></a>另请参阅

- [XAML 设计时属性](../xaml-tools/xaml-designtime-data.md)
- [WPF 应用中的 XAML](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [UWP 应用中的 XAML](/windows/uwp/xaml-platform/xaml-overview)
- [Xamarin.Forms 应用中的 XAML](/xamarin/xamarin-forms/xaml/)