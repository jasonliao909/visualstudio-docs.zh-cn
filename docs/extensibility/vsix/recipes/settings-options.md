---
title: 设置 & 选项
description: 如何处理自定义设置和选项的食谱。
ms.date: 12/01/2021
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: pchapman
ms.prod: visual-studio-windows
ms.technology: vs-ide-sdk
ms.custom: cookbook
ms.openlocfilehash: 3d51941f729e8a8fda0adadfec6848229543c4a0
ms.sourcegitcommit: a149b3a034bb555ad217656c0ec8bc1672b1e215
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2021
ms.locfileid: "133515848"
---
# <a name="custom-settings-and-options-in-visual-studio-extensions"></a>Visual Studio 扩展中的自定义设置和选项

存储和检索设置对于多个扩展来说是必需的。 让我们来了解如何使用这些目标的设置：

* 提供自定义选项的一种简单方法。
* 公开 " **工具" > 选项** "对话框中的选项。
* 访问和修改设置的线程安全方法。
* 同步和异步支持。
* 无需加载用于初始化设置的包。

以下视频显示了向扩展添加选项的方法。

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RWPmjL]

下面是 " **工具" > 选项** "对话框中的外观。

## <a name="add-an-options-page"></a>添加选项页
右键单击项目，然后选择 " **添加 > 新项 ...** " 以显示可用模板。 然后选择左侧的 "**扩展性**" 类别，然后选择 "**选项" 页 (Community)** 模板 "。 在下面的 " **名称** " 字段中，编写 **General**。

:::image type="content" source="../media/add-new-item-options.png" alt-text="从 &quot;添加新项&quot; 对话框添加 &quot;选项&quot; 页。":::

这将在项目的根中创建 */Options/General.cs* 。

:::image type="content" source="../media/options-folder.png" alt-text="添加到项目的选项页 c # 文件。":::

下面是常规 .cs 文件的内容：

```csharp
internal partial class OptionsProvider
{
    // Register the options with these attributes on your package class:
    // [ProvideOptionPage(typeof(OptionsProvider.GeneralOptions), "MyExtension", "General", 0, 0, true)]
    // [ProvideProfile(typeof(OptionsProvider.GeneralOptions), "MyExtension", "General", 0, 0, true)]
    public class GeneralOptions : BaseOptionPage<General> { }
}

public class General : BaseOptionModel<General>
{
    [Category("My category")]
    [DisplayName("My Option")]
    [Description("An informative description.")]
    [DefaultValue(true)]
    public bool MyOption { get; set; } = true;
}
```

这并不简单，我们将详细介绍详细信息。 但首先，必须注册 "选项" 页面。

## <a name="register-the-options-page"></a>注册选项页
在 *常规 .cs* 文件中的代码注释中，是有关如何注册 "选项" 页的说明。

我们要做的就是将这两个属性复制到包类中。 这可能类似于以下内容：

```csharp
[ProvideOptionPage(typeof(OptionsProvider.GeneralOptions), "MyExtension", "General", 0, 0, true)]
[ProvideProfile(typeof(OptionsProvider.GeneralOptions), "MyExtension", "General", 0, 0, true)]
public sealed class OptionsPackage : ToolkitPackage
{
    ...
}
```

运行扩展后，现在应会看到 "**工具 > 选项**" 对话框中显示的 " **MyExtension"/"常规**" 选项页。

:::image type="content" source="../media/tools-options.png" alt-text="已注册自定义选项页。":::

这两个特性非常相似，但处理不同的方案。

`ProvideOptionsPage`属性是在 "**工具" > 选项**"对话框中显示的" 选项 "页面。 如果你不希望用户看到 "选项" 页面，则可以省略此属性。

`ProvideProfile`在漫游配置文件上注册选项，这意味着各个设置将随用户在实例之间漫游并安装 Visual Studio。 它还启用 Visual Studio 的导入/导出设置功能。 此属性是可选的。

## <a name="the-individual-options"></a>各个选项
在一般的 .cs 文件中，可以看到，单独的选项只是通过属性修饰的简单 c # 属性。

```csharp
    [Category("My category")]
    [DisplayName("My Option")]
    [Description("An informative description.")]
    [DefaultValue(true)]
    public bool MyOption { get; set; } = true;
```

简单的数据类型（如、、、） `string` `bool` `int` 完全受支持，涵盖大多数用例。 对于其他数据类型，必须使用类型转换器。 某些内置于 Visual Studio，如 `EnumConverter` 。

请考虑此枚举：

```csharp
public enum Numbers
{
    First,
    Second,
    Third,
}
```

可以通过以下方式将这些值作为下拉列表中的选项公开 `TypeConverter` ：

```csharp
[Category("My category")]
[DisplayName("My Enum")]
[Description("Select the value you want from the list.")]
[DefaultValue(Numbers.First)]
[TypeConverter(typeof(EnumConverter))]
public Numbers MyEnum { get; set; } = Numbers.First;
```

:::image type="content" source="../media/tools-options-enum.png" alt-text="&quot;选项&quot; 页上的包含枚举值的下拉列表。":::

## <a name="reading-and-writing-options"></a>读取和写入选项
现在，你已注册了允许用户更改其值的选项，可以阅读这些值以在我们的扩展中使用。

您可以使用来自同步和异步上下文的设置。 首先，让我们开始同步：

```csharp
// read settings
var number = General.Instance.MyEnum;

// write settings
General.Instance.MyEnum = Numbers.Second;
General.Instance.Save();
```

用于读取和写入设置的 API 非常简单直接。

在异步上下文中工作时，API 看起来非常相似。

```csharp
// read settings
var general = await General.GetLiveInstanceAsync();
var number = general.MyEnum;

// write settings
general.MyEnum = Numbers.Second;
await general.SaveAsync();
```

## <a name="events"></a>事件
保存设置后，将触发静态事件 `General.Saved` 。 可以像 .NET 中的任何其他事件一样订阅该事件，如下所示：

```csharp
General.Saved += OnSettingsSaved;

...

private void OnSettingsSaved(object sender, General e)
{
   
}
```

## <a name="get-the-source-code"></a>获取源代码
可在 [示例存储库](https://github.com/VsixCommunity/Samples)中找到此扩展的源代码。

## <a name="additional-resources"></a>其他资源
阅读有关这些方案的所有详细信息的文档，但请注意，虽然它们提供了更详细的文档，但并不遵循本示例中概述的最佳实践。 它们也不使用 Community Toolkit 来处理设置。

* [创建选项页](../../creating-an-options-page.md)
* [使用设置存储](../../using-the-settings-store.md)
* [写入用户设置存储](../../writing-to-the-user-settings-store.md)
