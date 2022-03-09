---
title: 创建视图修饰、命令和设置 |Microsoft Docs
description: 了解如何使用此演练Visual Studio使用列指南扩展代码编辑器。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 4a2df0a3-42da-4f7b-996f-ee16a35ac922
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 855fa3db4f81b29099d75ea95522f19cff7f7476
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139552247"
---
# <a name="walkthrough-create-a-view-adornment-commands-and-settings-column-guides"></a>演练：使用列指南创建视图修饰、命令和 (设置) 
可以使用命令和Visual Studio扩展文本/代码编辑器。 本文演示如何开始使用常用扩展功能列指南。 列指南是文本编辑器视图上绘制的浅色线条，可帮助你管理特定列宽的代码。 具体而言，格式化代码对于包括在文档、博客文章或 bug 报告中的示例非常重要。

本演练中的操作：
- 创建 VSIX 项目
- 添加编辑器视图修饰
- 添加了对保存和获取设置的支持 (在何处绘制列指南及其颜色) 
- 添加命令 (/删除列指南，更改其颜色) 
- 将命令放在"编辑"菜单和文本文档上下文菜单上
- 添加对从命令窗口调用Visual Studio的支持

  可以使用此库[extension 来试用Visual Studio指南功能的版本](https://marketplace.visualstudio.com/items?itemName=PaulHarrington.EditorGuidelines)。

  > [!NOTE]
  > 本演练将大量代码粘贴到扩展模板生成的Visual Studio文件中。 但是，本演练很快将参考一个已完成的解决方案，GitHub其他扩展示例。 完成的代码略有不同，因为它具有真正的命令图标，而不是使用泛型模板图标。

## <a name="get-started"></a>开始使用
从 2015 Visual Studio开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装 [Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="set-up-the-solution"></a>设置解决方案
首先，创建 VSIX 项目，添加编辑器视图修饰，然后添加命令 (添加 VSPackage 来拥有命令) 。 基本体系结构如下所示：
- 你有一个文本视图创建侦听器，用于为每个视图 `ColumnGuideAdornment` 创建对象。 此对象侦听有关视图更改或设置更改、更新或重绘列指南的事件（如有必要）。
- 有一个 `GuidesSettingsManager` ，用于处理从设置存储的Visual Studio写入。 设置管理器还具有更新支持用户命令的设置的操作， (列、删除列、更改颜色) 。
- 如果有用户命令，则有必要使用 VSIP 包，但它只是初始化命令实现对象的样板代码。
- 有一个 `ColumnGuideCommands` 对象运行用户命令，并挂钩 *.vsct* 文件中声明的命令的命令处理程序。

  **VSIX**。 使用 **"&#124;新建...** "命令创建项目。 在左侧 **导航窗格中的** **C#** 下选择"扩展性"节点，然后选择 **Project窗格中的 VSIX** 扩展节点。 输入名称 **ColumnGuides，然后选择****"确定**"以创建项目。

  **视图修饰**。 按项目节点上的右指针按钮解决方案资源管理器。 选择" **添加新&#124;...** "命令以添加新的视图装饰项。 在 **左侧导航&#124;** 选择"扩展性"和"编辑器"，然后选择右侧窗格中的 **"编辑器视** 区修饰"。 输入名称 **ColumnGuideAdornment** 作为项名称，然后选择" **添加** "以添加它。

  可以看到，此项目模板向项目 () 添加了两个文件以及引用，等等： **ColumnGuideAdornment.cs** 和 **ColumnGuideAdornmentTextViewCreationListener.cs**。 模板在视图上绘制紫色矩形。 下一部分将更改视图创建侦听器中的几行，并替换 **ColumnGuideAdornment.cs 的内容**。

  **命令**。 在 **解决方案资源管理器**，按项目节点上的右指针按钮。 选择" **添加新&#124;...** "命令以添加新的视图装饰项。 在 **左侧导航&#124; VSPackage** 中选择"扩展性"，然后选择右侧 **窗格中** 的"自定义命令"。 输入名称 **ColumnGuideCommands** 作为项名称，然后选择"添加 **"**。 除了多个引用，添加命令和包还添加了 **ColumnGuideCommands.cs**、 **ColumnGuideCommandsPackage.cs** 和 **ColumnGuideCommandsPackage.vsct**。 在下面的部分中，将替换第一个文件和最后一个文件的内容，以定义和实现命令。

## <a name="set-up-the-text-view-creation-listener"></a>设置文本视图创建侦听器
在 *编辑器中打开 ColumnGuideAdornmentTextViewCreationListener.cs* 。 每当用户创建文本视图时，此代码Visual Studio处理程序。 有一些属性可控制何时调用处理程序，具体取决于视图的特征。

代码还必须声明装饰层。 当编辑器更新视图时，它会获取视图的装饰层，以及从 获取装饰元素的 修饰层。 可以使用属性声明层相对于其他层的顺序。 替换以下行：

```csharp
[Order(After = PredefinedAdornmentLayers.Caret)]
```

这两行代码：

```csharp
[Order(Before = PredefinedAdornmentLayers.Text)]
[TextViewRole(PredefinedTextViewRoles.Document)]
```

替换的行位于声明装饰层的一组属性中。 更改的第一行只会更改列指南行的显示位置。 在视图中"之前"绘制文本行意味着它们显示在文本后面或下方。 第二行声明列指南修饰适用于符合文档概念的文本实体，但你可以声明修饰，例如，只能用于可编辑文本。 语言服务和编辑器扩展 [点中提供详细信息](../extensibility/language-service-and-editor-extension-points.md)

## <a name="implement-the-settings-manager"></a>实现设置管理器
将 *GuidesSettingsManager.cs* 的内容替换为以下 (说明) ：

```csharp
using Microsoft.VisualStudio.Settings;
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.Shell.Settings;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Windows.Media;

namespace ColumnGuides
{
    internal static class GuidesSettingsManager
    {
        // Because my code is always called from the UI thred, this succeeds.
        internal static SettingsManager VsManagedSettingsManager =
            new ShellSettingsManager(ServiceProvider.GlobalProvider);

        private const int _maxGuides = 5;
        private const string _collectionSettingsName = "Text Editor";
        private const string _settingName = "Guides";
        // 1000 seems reasonable since primary scenario is long lines of code
        private const int _maxColumn = 1000;

        static internal bool AddGuideline(int column)
        {
            if (! IsValidColumn(column))
                throw new ArgumentOutOfRangeException(
                    "column",
                    "The paramenter must be between 1 and " + _maxGuides.ToString());
            var offsets = GuidesSettingsManager.GetColumnOffsets();
            if (offsets.Count() >= _maxGuides)
                return false;
            // Check for duplicates
            if (offsets.Contains(column))
                return false;
            offsets.Add(column);
            WriteSettings(GuidesSettingsManager.GuidelinesColor, offsets);
            return true;
        }

        static internal bool RemoveGuideline(int column)
        {
            if (!IsValidColumn(column))
                throw new ArgumentOutOfRangeException(
                    "column", "The paramenter must be between 1 and 10,000");
            var columns = GuidesSettingsManager.GetColumnOffsets();
            if (! columns.Remove(column))
            {
                // Not present.  Allow user to remove the last column
                // even if they're not on the right column.
                if (columns.Count != 1)
                    return false;

                columns.Clear();
            }
            WriteSettings(GuidesSettingsManager.GuidelinesColor, columns);
            return true;
        }

        static internal bool CanAddGuideline(int column)
        {
            if (!IsValidColumn(column))
                return false;
            var offsets = GetColumnOffsets();
            if (offsets.Count >= _maxGuides)
                return false;
            return ! offsets.Contains(column);
        }

        static internal bool CanRemoveGuideline(int column)
        {
            if (! IsValidColumn(column))
                return false;
            // Allow user to remove the last guideline regardless of the column.
            // Okay to call count, we limit the number of guides.
            var offsets = GuidesSettingsManager.GetColumnOffsets();
            return offsets.Contains(column) || offsets.Count() == 1;
        }

        static internal void RemoveAllGuidelines()
        {
            WriteSettings(GuidesSettingsManager.GuidelinesColor, new int[0]);
        }

        private static bool IsValidColumn(int column)
        {
            // zero is allowed (per user request)
            return 0 <= column && column <= _maxColumn;
        }

        // This has format "RGB(<int>, <int>, <int>) <int> <int>...".
        // There can be any number of ints following the RGB part,
        // and each int is a column (char offset into line) where to draw.
        static private string _guidelinesConfiguration;
        static private string GuidelinesConfiguration
        {
            get
            {
                if (_guidelinesConfiguration == null)
                {
                    _guidelinesConfiguration =
                        GetUserSettingsString(
                            GuidesSettingsManager._collectionSettingsName,
                            GuidesSettingsManager._settingName)
                        .Trim();
                }
                return _guidelinesConfiguration;
            }

            set
            {
                if (value != _guidelinesConfiguration)
                {
                    _guidelinesConfiguration = value;
                    WriteUserSettingsString(
                        GuidesSettingsManager._collectionSettingsName,
                        GuidesSettingsManager._settingName, value);
                    // Notify ColumnGuideAdornments to update adornments in views.
                    var handler = GuidesSettingsManager.SettingsChanged;
                    if (handler != null)
                        handler();
                }
            }
        }

        internal static string GetUserSettingsString(string collection, string setting)
        {
            var store = GuidesSettingsManager
                            .VsManagedSettingsManager
                            .GetReadOnlySettingsStore(SettingsScope.UserSettings);
            return store.GetString(collection, setting, "RGB(255,0,0) 80");
        }

        internal static void WriteUserSettingsString(string key, string propertyName,
                                                     string value)
        {
            var store = GuidesSettingsManager
                            .VsManagedSettingsManager
                            .GetWritableSettingsStore(SettingsScope.UserSettings);
            store.CreateCollection(key);
            store.SetString(key, propertyName, value);
        }

        // Persists settings and sets property with side effect of signaling
        // ColumnGuideAdornments to update.
        static private void WriteSettings(Color color, IEnumerable<int> columns)
        {
            string value = ComposeSettingsString(color, columns);
            GuidelinesConfiguration = value;
        }

        private static string ComposeSettingsString(Color color,
                                                    IEnumerable<int> columns)
        {
            StringBuilder sb = new StringBuilder();
            sb.AppendFormat("RGB({0},{1},{2})", color.R, color.G, color.B);
            IEnumerator<int> columnsEnumerator = columns.GetEnumerator();
            if (columnsEnumerator.MoveNext())
            {
                sb.AppendFormat(" {0}", columnsEnumerator.Current);
                while (columnsEnumerator.MoveNext())
                {
                    sb.AppendFormat(", {0}", columnsEnumerator.Current);
                }
            }
            return sb.ToString();
        }

        // Parse a color out of a string that begins like "RGB(255,0,0)"
        static internal Color GuidelinesColor
        {
            get
            {
                string config = GuidelinesConfiguration;
                if (!String.IsNullOrEmpty(config) && config.StartsWith("RGB("))
                {
                    int lastParen = config.IndexOf(')');
                    if (lastParen > 4)
                    {
                        string[] rgbs = config.Substring(4, lastParen - 4).Split(',');

                        if (rgbs.Length >= 3)
                        {
                            byte r, g, b;
                            if (byte.TryParse(rgbs[0], out r) &&
                                byte.TryParse(rgbs[1], out g) &&
                                byte.TryParse(rgbs[2], out b))
                            {
                                return Color.FromRgb(r, g, b);
                            }
                        }
                    }
                }
                return Colors.DarkRed;
            }

            set
            {
                WriteSettings(value, GetColumnOffsets());
            }
        }

        // Parse a list of integer values out of a string that looks like
        // "RGB(255,0,0) 1, 5, 10, 80"
        static internal List<int> GetColumnOffsets()
        {
            var result = new List<int>();
            string settings = GuidesSettingsManager.GuidelinesConfiguration;
            if (String.IsNullOrEmpty(settings))
                return new List<int>();

            if (!settings.StartsWith("RGB("))
                return new List<int>();

            int lastParen = settings.IndexOf(')');
            if (lastParen <= 4)
                return new List<int>();

            string[] columns = settings.Substring(lastParen + 1).Split(',');

            int columnCount = 0;
            foreach (string columnText in columns)
            {
                int column = -1;
                // VS 2008 gallery extension didn't allow zero, so per user request ...
                if (int.TryParse(columnText, out column) && column >= 0)
                {
                    columnCount++;
                    result.Add(column);
                    if (columnCount >= _maxGuides)
                        break;
                }
            }
            return result;
        }

        // Delegate and Event to fire when settings change so that ColumnGuideAdornments
        // can update.  We need nothing special in this event since the settings manager
        // is statically available.
        //
        internal delegate void SettingsChangedHandler();
        static internal event SettingsChangedHandler SettingsChanged;

    }
}

```

大多数此代码创建和分析设置格式："RGB \<int> (，\<int>) \<int> \<int>、 \<int>、..."。  末尾的整数是需要列指南的从 1 开始列。 列指南扩展在单个设置值字符串中捕获其所有设置。

代码的某些部分值得突出显示。 以下代码行获取Visual Studio存储的托管包装器。 大多数情况下，这会抽象化Windows注册表，但此 API 独立于存储机制。

```csharp
internal static SettingsManager VsManagedSettingsManager =
    new ShellSettingsManager(ServiceProvider.GlobalProvider);
```

该Visual Studio设置存储使用类别标识符和设置标识符来唯一标识所有设置：

```csharp
private const string _collectionSettingsName = "Text Editor";
private const string _settingName = "Guides";
```

不需要使用 作为 `"Text Editor"` 类别名称。 可以选取任何喜欢的。

前几个函数是更改设置的入口点。 它们检查高级约束，例如允许的最大指南数。  然后，调用 `WriteSettings`，它组成设置字符串并设置属性 `GuideLinesConfiguration`。 设置此属性会将设置值保存到Visual Studio存储`SettingsChanged``ColumnGuideAdornment`中，并触发 事件以更新所有对象，每个对象都与文本视图相关联。

有几个入口点函数 `CanAddGuideline`（如 ）用于实现更改设置的命令。 当Visual Studio菜单时，它会查询命令实现，以查看命令当前是否已启用、其名称是什么等。  下面将了解如何挂接命令实现中的这些入口点。 有关命令详细信息，请参阅 [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)。

## <a name="implement-the-columnguideadornment-class"></a>实现 ColumnGuideAdornment 类
对于 `ColumnGuideAdornment` 可以具有修饰的每个文本视图，将实例化 类。 此类侦听有关视图更改或设置更改的事件，并在必要时侦听更新或重绘列指南。

将 *ColumnGuideAdornment.cs* 的内容替换为以下 (代码) ：

```csharp
using System;
using System.Windows.Media;
using Microsoft.VisualStudio.Text.Editor;
using System.Collections.Generic;
using System.Windows.Shapes;
using Microsoft.VisualStudio.Text.Formatting;
using System.Windows;

namespace ColumnGuides
{
    /// <summary>
    /// Adornment class, one instance per text view that draws a guides on the viewport
    /// </summary>
    internal sealed class ColumnGuideAdornment
    {
        private const double _lineThickness = 1.0;
        private IList<Line> _guidelines;
        private IWpfTextView _view;
        private double _baseIndentation;
        private double _columnWidth;

        /// <summary>
        /// Creates editor column guidelines
        /// </summary>
        /// <param name="view">The <see cref="IWpfTextView"/> upon
        /// which the adornment will be drawn</param>
        public ColumnGuideAdornment(IWpfTextView view)
        {
            _view = view;
            _guidelines = CreateGuidelines();
            GuidesSettingsManager.SettingsChanged +=
                new GuidesSettingsManager.SettingsChangedHandler(SettingsChanged);
            view.LayoutChanged +=
                new EventHandler<TextViewLayoutChangedEventArgs>(OnViewLayoutChanged);
            _view.Closed += new EventHandler(OnViewClosed);
        }

        void SettingsChanged()
        {
            _guidelines = CreateGuidelines();
            UpdatePositions();
            AddGuidelinesToAdornmentLayer();
        }

        void OnViewClosed(object sender, EventArgs e)
        {
            _view.LayoutChanged -= OnViewLayoutChanged;
            _view.Closed -= OnViewClosed;
            GuidesSettingsManager.SettingsChanged -= SettingsChanged;
        }

        private bool _firstLayoutDone;

        void OnViewLayoutChanged(object sender, TextViewLayoutChangedEventArgs e)
        {
            bool fUpdatePositions = false;

            IFormattedLineSource lineSource = _view.FormattedLineSource;
            if (lineSource == null)
            {
                return;
            }
            if (_columnWidth != lineSource.ColumnWidth)
            {
                _columnWidth = lineSource.ColumnWidth;
                fUpdatePositions = true;
            }
            if (_baseIndentation != lineSource.BaseIndentation)
            {
                _baseIndentation = lineSource.BaseIndentation;
                fUpdatePositions = true;
            }
            if (fUpdatePositions ||
                e.VerticalTranslation ||
                e.NewViewState.ViewportTop != e.OldViewState.ViewportTop ||
                e.NewViewState.ViewportBottom != e.OldViewState.ViewportBottom)
            {
                UpdatePositions();
            }
            if (!_firstLayoutDone)
            {
                AddGuidelinesToAdornmentLayer();
                _firstLayoutDone = true;
            }
        }

        private static IList<Line> CreateGuidelines()
        {
            Brush lineBrush = new SolidColorBrush(GuidesSettingsManager.GuidelinesColor);
            DoubleCollection dashArray = new DoubleCollection(new double[] { 1.0, 3.0 });
            IList<Line> result = new List<Line>();
            foreach (int column in GuidesSettingsManager.GetColumnOffsets())
            {
                Line line = new Line()
                {
                    // Use the DataContext slot as a cookie to hold the column
                    DataContext = column,
                    Stroke = lineBrush,
                    StrokeThickness = _lineThickness,
                    StrokeDashArray = dashArray
                };
                result.Add(line);
            }
            return result;
        }

        void UpdatePositions()
        {
            foreach (Line line in _guidelines)
            {
                int column = (int)line.DataContext;
                line.X2 = _baseIndentation + 0.5 + column * _columnWidth;
                line.X1 = line.X2;
                line.Y1 = _view.ViewportTop;
                line.Y2 = _view.ViewportBottom;
            }
        }

        void AddGuidelinesToAdornmentLayer()
        {
            // Grab a reference to the adornment layer that this adornment
            // should be added to
            // Must match exported name in ColumnGuideAdornmentTextViewCreationListener
            IAdornmentLayer adornmentLayer =
                _view.GetAdornmentLayer("ColumnGuideAdornment");
            if (adornmentLayer == null)
                return;
            adornmentLayer.RemoveAllAdornments();
            // Add the guidelines to the adornment layer and make them relative
            // to the viewport
            foreach (UIElement element in _guidelines)
                adornmentLayer.AddAdornment(AdornmentPositioningBehavior.OwnerControlled,
                                            null, null, element, null);
        }
    }

}
```

此类的实例保留视图上绘制的 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView> 关联的 `Line` 和 对象的列表。

构造函数 (创建列`ColumnGuideAdornmentTextViewCreationListener`Visual Studio对象时从) 调用`Line`。  构造函数还添加事件处理程序，用于`SettingsChanged` (和`GuidesSettingsManager`视图) 和 中定义的事件`LayoutChanged``Closed`。

事件`LayoutChanged`由于视图中的多种更改而触发，包括Visual Studio视图时。 处理程序 `OnViewLayoutChanged` 调用 以 `AddGuidelinesToAdornmentLayer` 执行。 中的代码 `OnViewLayoutChanged` 根据字号更改、视图滚动条、水平滚动等更改确定是否需要更新行位置。 中的代码 `UpdatePositions` 会导致参考线在字符之间绘制，或绘制在文本行中指定字符偏移量中的文本列之后。

每当设置更改 `SettingsChanged` 时，函数只需 `Line` 使用任何新设置重新创建所有对象。 设置行位置后，代码会从`Line``ColumnGuideAdornment`装饰层中删除所有以前的对象，并添加新对象。

## <a name="define-the-commands-menus-and-menu-placements"></a>定义命令、菜单和菜单位置
声明命令和菜单、将命令组或菜单放置在各种其他菜单上以及挂接命令处理程序可能有很多。 本演练重点介绍命令在此扩展中如何工作，但有关更深入的信息，请参阅 [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)。

### <a name="introduction-to-the-code"></a>代码简介
列指南扩展显示声明一组命令 (添加列、删除列、更改行颜色) ，然后将该组放置在编辑器上下文菜单的子菜单上。  列指南扩展还会将命令添加到主"编辑 **"** 菜单，但使命令不可见，下面将介绍为常见模式。

命令实现有三个部分：ColumnGuideCommandsPackage.cs、ColumnGuideCommandsPackage.vsct 和 ColumnGuideCommands.cs。 模板生成的代码在"工具"菜单上添加一个命令，该命令将弹出一个对话框作为实现。 你可以查看在 *.vsct* 和 *ColumnGuideCommands.cs* 文件中实现的方式，因为它非常简单。 替换以下这些文件中的代码。

包代码包含发现扩展提供命令Visual Studio查找命令放置位置所需的样本声明。 当包初始化时，它会实例化命令实现类。 有关与命令相关的包详细信息，请参阅 [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)。

### <a name="a-common-commands-pattern"></a>常见命令模式
列指南扩展中的命令是列指南中非常常见的模式Visual Studio。 将相关命令放在组中，将`<CommandFlag>CommandWellOnly</CommandFlag>`该组放在主菜单上，通常将""设置为使命令不可见。  将命令放在主菜单上 (如"编辑) "会为它们提供很好的名称 (例如 **Edit.AddColumnGuide**) ，这可用于在"工具选项"中重新分配键绑定时查找 **命令**。 从命令窗口调用命令时，它对于完成 **也很有用**。

然后，将命令组添加到希望用户使用命令的上下文菜单或子菜单。 Visual Studio仅`CommandWellOnly`视为主菜单的不显示标志。 将同一组命令放在上下文菜单或子菜单上时，这些命令可见。

作为通用模式的一部分，列指南扩展将创建包含单个子菜单的第二个组。 子菜单又包含包含四列指南命令的第一个组。 保存子菜单的第二个组是放置于各种上下文菜单上的可重用资产，该资源将子菜单置于这些上下文菜单上。

### <a name="the-vsct-file"></a>.vsct 文件
*.vsct* 文件声明命令及其位置，以及图标等。 将 *.vsct* 文件的内容替换为以下代码 (以下) ：

```xml
<?xml version="1.0" encoding="utf-8"?>
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema">

  <!--  This is the file that defines the actual layout and type of the commands.
        It is divided in different sections (e.g. command definition, command
        placement, ...), with each defining a specific set of properties.
        See the comment before each section for more details about how to
        use it. -->

  <!--  The VSCT compiler (the tool that translates this file into the binary
        format that VisualStudio will consume) has the ability to run a preprocessor
        on the vsct file; this preprocessor is (usually) the C++ preprocessor, so
        it is possible to define includes and macros with the same syntax used
        in C++ files. Using this ability of the compiler here, we include some files
        defining some of the constants that we will use inside the file. -->

  <!--This is the file that defines the IDs for all the commands exposed by
      VisualStudio. -->
  <Extern href="stdidcmd.h"/>

  <!--This header contains the command ids for the menus provided by the shell. -->
  <Extern href="vsshlids.h"/>

  <!--The Commands section is where commands, menus, and menu groups are defined.
      This section uses a Guid to identify the package that provides the command
      defined inside it. -->
  <Commands package="guidColumnGuideCommandsPkg">
    <!-- Inside this section we have different sub-sections: one for the menus, another
    for the menu groups, one for the buttons (the actual commands), one for the combos
    and the last one for the bitmaps used. Each element is identified by a command id
    that is a unique pair of guid and numeric identifier; the guid part of the identifier
    is usually called "command set" and is used to group different command inside a
    logically related group; your package should define its own command set in order to
    avoid collisions with command ids defined by other packages. -->

    <!-- In this section you can define new menu groups. A menu group is a container for
         other menus or buttons (commands); from a visual point of view you can see the
         group as the part of a menu contained between two lines. The parent of a group
         must be a menu. -->
    <Groups>

      <!-- The main group is parented to the edit menu. All the buttons within the group
           have the "CommandWellOnly" flag, so they're actually invisible, but it means
           they get canonical names that begin with "Edit". Using placements, the group
           is also placed in the GuidesSubMenu group. -->
      <!-- The priority 0xB801 is chosen so it goes just after
           IDG_VS_EDIT_COMMANDWELL -->
      <Group guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"
             priority="0xB801">
        <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_EDIT" />
      </Group>

      <!-- Group for holding the "Guidelines" sub-menu anchor (the item on the menu that
           drops the sub menu). The group is parented to
           the context menu for code windows. That takes care of most editors, but it's
           also placed in a couple of other windows using Placements -->
      <Group guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
             priority="0x0600">
        <Parent guid="guidSHLMainMenu" id="IDM_VS_CTXT_CODEWIN" />
      </Group>

    </Groups>

    <Menus>
      <Menu guid="guidColumnGuidesCommandSet" id="GuidesSubMenu" priority="0x1000"
            type="Menu">
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup" />
        <Strings>
          <ButtonText>&Column Guides</ButtonText>
        </Strings>
      </Menu>
    </Menus>

    <!--Buttons section. -->
    <!--This section defines the elements the user can interact with, like a menu command or a button
        or combo box in a toolbar. -->
    <Buttons>
      <!--To define a menu group you have to specify its ID, the parent menu and its
          display priority.
          The command is visible and enabled by default. If you need to change the
          visibility, status, etc, you can use the CommandFlag node.
          You can add more than one CommandFlag node e.g.:
              <CommandFlag>DefaultInvisible</CommandFlag>
              <CommandFlag>DynamicVisibility</CommandFlag>
          If you do not want an image next to your command, remove the Icon node or
          set it to <Icon guid="guidOfficeIcon" id="msotcidNoIcon" /> -->

      <Button guid="guidColumnGuidesCommandSet" id="cmdidAddColumnGuide"
              priority="0x0100" type="Button">
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />
        <Icon guid="guidImages" id="bmpPicAddGuide" />
        <CommandFlag>CommandWellOnly</CommandFlag>
        <CommandFlag>AllowParams</CommandFlag>
        <Strings>
          <ButtonText>&Add Column Guide</ButtonText>
        </Strings>
      </Button>

      <Button guid="guidColumnGuidesCommandSet" id="cmdidRemoveColumnGuide"
              priority="0x0101" type="Button">
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />
        <Icon guid="guidImages" id="bmpPicRemoveGuide" />
        <CommandFlag>CommandWellOnly</CommandFlag>
        <CommandFlag>AllowParams</CommandFlag>
        <Strings>
          <ButtonText>&Remove Column Guide</ButtonText>
        </Strings>
      </Button>

      <Button guid="guidColumnGuidesCommandSet" id="cmdidChooseGuideColor"
              priority="0x0103" type="Button">
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />
        <Icon guid="guidImages" id="bmpPicChooseColor" />
        <CommandFlag>CommandWellOnly</CommandFlag>
        <Strings>
          <ButtonText>Column Guide &Color...</ButtonText>
        </Strings>
      </Button>

      <Button guid="guidColumnGuidesCommandSet" id="cmdidRemoveAllColumnGuides"
              priority="0x0102" type="Button">
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />
        <CommandFlag>CommandWellOnly</CommandFlag>
        <Strings>
          <ButtonText>Remove A&ll Columns</ButtonText>
        </Strings>
      </Button>
    </Buttons>

    <!--The bitmaps section is used to define the bitmaps that are used for the
        commands.-->
    <Bitmaps>
      <!--  The bitmap id is defined in a way that is a little bit different from the
            others:
            the declaration starts with a guid for the bitmap strip, then there is the
            resource id of the bitmap strip containing the bitmaps and then there are
            the numeric ids of the elements used inside a button definition. An important
            aspect of this declaration is that the element id
            must be the actual index (1-based) of the bitmap inside the bitmap strip. -->
      <Bitmap guid="guidImages" href="Resources\ColumnGuideCommands.png"
              usedList="bmpPicAddGuide, bmpPicRemoveGuide, bmpPicChooseColor" />
    </Bitmaps>

  </Commands>

  <CommandPlacements>

    <!-- Define secondary placements for our groups -->

    <!-- Place the group containing the three commands in the sub-menu -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"
                      priority="0x0100">
      <Parent guid="guidColumnGuidesCommandSet" id="GuidesSubMenu" />
    </CommandPlacement>

    <!-- The HTML editor context menu, for some reason, redefines its own groups
         so we need to place a copy of our context menu there too. -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
                      priority="0x1001">
      <Parent guid="CMDSETID_HtmEdGrp" id="IDMX_HTM_SOURCE_HTML" />
    </CommandPlacement>

    <!-- The HTML context menu in Dev12 changed. -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
                      priority="0x1001">
      <Parent guid="CMDSETID_HtmEdGrp_Dev12" id="IDMX_HTM_SOURCE_HTML_Dev12" />
    </CommandPlacement>

    <!-- Similarly for Script -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
                      priority="0x1001">
      <Parent guid="CMDSETID_HtmEdGrp" id="IDMX_HTM_SOURCE_SCRIPT" />
    </CommandPlacement>

    <!-- Similarly for ASPX  -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
                      priority="0x1001">
      <Parent guid="CMDSETID_HtmEdGrp" id="IDMX_HTM_SOURCE_ASPX" />
    </CommandPlacement>

    <!-- Similarly for the XAML editor context menu -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
                      priority="0x0600">
      <Parent guid="guidXamlUiCmds" id="IDM_XAML_EDITOR" />
    </CommandPlacement>

  </CommandPlacements>

  <!-- This defines the identifiers and their values used above to index resources
       and specify commands. -->
  <Symbols>
    <!-- This is the package guid. -->
    <GuidSymbol name="guidColumnGuideCommandsPkg"
                value="{e914e5de-0851-4904-b361-1a3a9d449704}" />

    <!-- This is the guid used to group the menu commands together -->
    <GuidSymbol name="guidColumnGuidesCommandSet"
                value="{c2bc0047-8bfa-4e5a-b5dc-45af8c274d8e}">
      <IDSymbol name="GuidesContextMenuGroup" value="0x1020" />
      <IDSymbol name="GuidesMenuItemsGroup" value="0x1021" />
      <IDSymbol name="GuidesSubMenu" value="0x1022" />
      <IDSymbol name="cmdidAddColumnGuide" value="0x0100" />
      <IDSymbol name="cmdidRemoveColumnGuide" value="0x0101" />
      <IDSymbol name="cmdidChooseGuideColor" value="0x0102" />
      <IDSymbol name="cmdidRemoveAllColumnGuides" value="0x0103" />
    </GuidSymbol>

    <GuidSymbol name="guidImages" value="{2C99F852-587C-43AF-AA2D-F605DE2E46EF}">
      <IDSymbol name="bmpPicAddGuide" value="1" />
      <IDSymbol name="bmpPicRemoveGuide" value="2" />
      <IDSymbol name="bmpPicChooseColor" value="3" />
    </GuidSymbol>

    <GuidSymbol name="CMDSETID_HtmEdGrp_Dev12"
                value="{78F03954-2FB8-4087-8CE7-59D71710B3BB}">
      <IDSymbol name="IDMX_HTM_SOURCE_HTML_Dev12" value="0x1" />
    </GuidSymbol>

    <GuidSymbol name="CMDSETID_HtmEdGrp" value="{d7e8c5e1-bdb8-11d0-9c88-0000f8040a53}">
      <IDSymbol name="IDMX_HTM_SOURCE_HTML" value="0x33" />
      <IDSymbol name="IDMX_HTM_SOURCE_SCRIPT" value="0x34" />
      <IDSymbol name="IDMX_HTM_SOURCE_ASPX" value="0x35" />
    </GuidSymbol>

    <GuidSymbol name="guidXamlUiCmds" value="{4c87b692-1202-46aa-b64c-ef01faec53da}">
      <IDSymbol name="IDM_XAML_EDITOR" value="0x103" />
    </GuidSymbol>
  </Symbols>

</CommandTable>

```

**GUID。** 若要Visual Studio查找并调用命令处理程序，需要确保在从项目项模板 () 生成的 *ColumnGuideCommandsPackage.cs* 文件中声明的包 GUID 与从上述) 复制的 *.vsct* 文件 (中声明的包 GUID 相匹配。 如果重新使用此示例代码，应确保具有不同的 GUID，这样你将不会与可能复制了此代码的其他人发生冲突。

在 *ColumnGuideCommandsPackage.cs* 中查找此行，并复制引号之间的 GUID：

```csharp
public const string PackageGuidString = "ef726849-5447-4f73-8de5-01b9e930f7cd";
```

然后，将 GUID 粘贴 *到 .vsct* 文件中，以便声明中包含以下 `Symbols` 行：

```xml
<GuidSymbol name="guidColumnGuideCommandsPkg"
            value="{ef726849-5447-4f73-8de5-01b9e930f7cd}" />
```

对于扩展，命令集和位图图像文件的 GUID 也应是唯一的：

```xml
<GuidSymbol name="guidColumnGuidesCommandSet"
            value="{c2bc0047-8bfa-4e5a-b5dc-45af8c274d8e}">
<GuidSymbol name="guidImages" value="{2C99F852-587C-43AF-AA2D-F605DE2E46EF}">
```

但是，无需更改本演练中的命令集和位图图像 GUID 即可使代码正常工作。 命令集 GUID 需要匹配 *ColumnGuideCommands.cs* 文件中的声明，但也需要替换该文件的内容;因此，GUID 将匹配。

*.vsct* 文件的其他 GUID 标识将列指南命令添加到的预先存在的菜单，因此它们永远不会更改。

**文件部分**。 *.vsct* 有三个外部部分：命令、位置和符号。 命令部分定义命令组、菜单、按钮或菜单项以及图标的位图。 "放置"部分声明组在菜单上的位置或预先存在的菜单上的其他位置。 symbols 节声明 *.vsct* 文件中其他位置使用的标识符，这使得 *.vsct* 代码比所有位置都有 GUID 和十六进制数字更具可读性。

**"命令"部分，"组定义"**。 命令部分首先定义命令组。 命令组是菜单上看到的命令，这些命令的灰色线条略微分隔了组。 如本示例所示，组也可以填充整个子菜单，在这种情况下，看不到灰色分隔线。 *.vsct* `GuidesMenuItemsGroup`  `GuidesContextMenuGroup` `IDM_VS_MENU_EDIT` `IDM_VS_CTXT_CODEWIN` 文件声明两个组，一个组是 (主"编辑"菜单) 的父级为 (代码编辑器的上下文菜单) 。

第二个组声明具有优先级 `0x0600` ：

```xml
<Group guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
             priority="0x0600">
```

其思路是，将列指南子菜单放在要添加子菜单组的任何上下文菜单的末尾。 但是，不应假定你最了解 ，而是使用 的优先级强制子菜单始终为最后一个 `0xFFFF`。 必须试验数字，以查看子菜单位于放置它的上下文菜单上的位置。 在这种情况下， `0x0600` 足够高，可以尽可能放在菜单的末尾，但它为其他人设计其扩展名留有空间，以低于列指南扩展名（如果需要）。

**"命令"部分，菜单定义**。 接下来，命令部分定义子菜单， `GuidesSubMenu`其父级为 `GuidesContextMenuGroup`。 是 `GuidesContextMenuGroup` 添加到所有相关上下文菜单的组。 在 placements 部分中，代码将包含四列指南命令的组放在此子菜单上。

**"命令"部分，按钮定义**。 然后，命令部分定义作为四列指南命令的菜单项或按钮。 `CommandWellOnly`（如上所述）表示命令在放置在主菜单上时不可见。 添加指南和删除 (的两个菜单项按钮) 也具有 标志 `AllowParams` ：

```xml
<CommandFlag>AllowParams</CommandFlag>
```

此标志允许命令在调用命令处理程序时接收Visual Studio菜单位置。  如果用户从命令窗口运行命令，则参数将传递到事件参数中的命令处理程序。

**命令节、位图定义**。 最后，命令部分声明用于命令的位图或图标。 本部分是一个简单的声明，用于标识项目资源并列出已用图标的基于一的索引。 *.vsct 文件的 symbols* 节声明用作索引的标识符的值。 本演练使用随添加到项目的自定义命令项模板一起提供的位图条。

**Placements 节**。 命令部分之后是 placements 节。 第一个字段是代码将上面讨论的第一个组添加到显示命令的子菜单中，该组包含四列指南命令：

```xml
<CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"
                  priority="0x0100">
  <Parent guid="guidColumnGuidesCommandSet" id="GuidesSubMenu" />
</CommandPlacement>
```

所有其他位置均将包含 `GuidesContextMenuGroup` (的 `GuidesSubMenu`) 添加到其他编辑器上下文菜单。 当代码声明 时， `GuidesContextMenuGroup`它是代码编辑器的上下文菜单的父级。 这就是看不到代码编辑器上下文菜单的位置的原因。

**符号部分**。 如上所述，symbols 节声明 *.vsct* 文件中其他位置使用的标识符，这使得 *.vsct* 代码比所有位置都有 GUID 和十六进制数字更具可读性。 本部分的要点是包 GUID 必须与包类中的声明一致。 而且，命令集 GUID 必须与命令实现类中的声明一致。

## <a name="implement-the-commands"></a>实现命令
*ColumnGuideCommands.cs* 文件实现命令并挂钩处理程序。 当Visual Studio加载并初始化包时，包将调用`Initialize`命令实现类。 命令初始化只是实例化 类，构造函数会挂接所有命令处理程序。

将 *ColumnGuideCommands.cs* 文件的内容替换为以下 (说明) ：

```csharp
using System;
using System.ComponentModel.Design;
using System.Globalization;
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.Shell.Interop;
using Microsoft.VisualStudio.TextManager.Interop;
using Microsoft.VisualStudio.Text.Editor;
using Microsoft.VisualStudio;

namespace ColumnGuides
{
    /// <summary>
    /// Command handler
    /// </summary>
    internal sealed class ColumnGuideCommands
    {

        const int cmdidAddColumnGuide = 0x0100;
        const int cmdidRemoveColumnGuide = 0x0101;
        const int cmdidChooseGuideColor = 0x0102;
        const int cmdidRemoveAllColumnGuides = 0x0103;

        /// <summary>
        /// Command menu group (command set GUID).
        /// </summary>
        static readonly Guid CommandSet =
            new Guid("c2bc0047-8bfa-4e5a-b5dc-45af8c274d8e");

        /// <summary>
        /// VS Package that provides this command, not null.
        /// </summary>
        private readonly Package package;

        OleMenuCommand _addGuidelineCommand;
        OleMenuCommand _removeGuidelineCommand;

        /// <summary>
        /// Initializes the singleton instance of the command.
        /// </summary>
        /// <param name="package">Owner package, not null.</param>
        public static void Initialize(Package package)
        {
            Instance = new ColumnGuideCommands(package);
        }

        /// <summary>
        /// Gets the instance of the command.
        /// </summary>
        public static ColumnGuideCommands Instance
        {
            get;
            private set;
        }

        /// <summary>
        /// Initializes a new instance of the <see cref="ColumnGuideCommands"/> class.
        /// Adds our command handlers for menu (commands must exist in the command
        /// table file)
        /// </summary>
        /// <param name="package">Owner package, not null.</param>
        private ColumnGuideCommands(Package package)
        {
            if (package == null)
            {
                throw new ArgumentNullException("package");
            }

            this.package = package;

            // Add our command handlers for menu (commands must exist in the .vsct file)

            OleMenuCommandService commandService =
                this.ServiceProvider.GetService(typeof(IMenuCommandService))
                    as OleMenuCommandService;
            if (commandService != null)
            {
                // Add guide
                _addGuidelineCommand =
                    new OleMenuCommand(AddColumnGuideExecuted, null,
                                       AddColumnGuideBeforeQueryStatus,
                                       new CommandID(ColumnGuideCommands.CommandSet,
                                                     cmdidAddColumnGuide));
                _addGuidelineCommand.ParametersDescription = "<column>";
                commandService.AddCommand(_addGuidelineCommand);
                // Remove guide
                _removeGuidelineCommand =
                    new OleMenuCommand(RemoveColumnGuideExecuted, null,
                                       RemoveColumnGuideBeforeQueryStatus,
                                       new CommandID(ColumnGuideCommands.CommandSet,
                                                     cmdidRemoveColumnGuide));
                _removeGuidelineCommand.ParametersDescription = "<column>";
                commandService.AddCommand(_removeGuidelineCommand);
                // Choose color
                commandService.AddCommand(
                    new MenuCommand(ChooseGuideColorExecuted,
                                    new CommandID(ColumnGuideCommands.CommandSet,
                                                  cmdidChooseGuideColor)));
                // Remove all
                commandService.AddCommand(
                    new MenuCommand(RemoveAllGuidelinesExecuted,
                                    new CommandID(ColumnGuideCommands.CommandSet,
                                                  cmdidRemoveAllColumnGuides)));
            }
        }

        /// <summary>
        /// Gets the service provider from the owner package.
        /// </summary>
        private IServiceProvider ServiceProvider
        {
            get
            {
                return this.package;
            }
        }

        private void AddColumnGuideBeforeQueryStatus(object sender, EventArgs e)
        {
            int currentColumn = GetCurrentEditorColumn();
            _addGuidelineCommand.Enabled =
                GuidesSettingsManager.CanAddGuideline(currentColumn);
        }

        private void RemoveColumnGuideBeforeQueryStatus(object sender, EventArgs e)
        {
            int currentColumn = GetCurrentEditorColumn();
            _removeGuidelineCommand.Enabled =
                GuidesSettingsManager.CanRemoveGuideline(currentColumn);
        }

        private int GetCurrentEditorColumn()
        {
            IVsTextView view = GetActiveTextView();
            if (view == null)
            {
                return -1;
            }

            try
            {
                IWpfTextView textView = GetTextViewFromVsTextView(view);
                int column = GetCaretColumn(textView);

                // Note: GetCaretColumn returns 0-based positions. Guidelines are 1-based
                // positions.
                // However, do not subtract one here since the caret is positioned to the
                // left of
                // the given column and the guidelines are positioned to the right. We
                // want the
                // guideline to line up with the current caret position. e.g. When the
                // caret is
                // at position 1 (zero-based), the status bar says column 2. We want to
                // add a
                // guideline for column 1 since that will place the guideline where the
                // caret is.
                return column;
            }
            catch (InvalidOperationException)
            {
                return -1;
            }
        }

        /// <summary>
        /// Find the active text view (if any) in the active document.
        /// </summary>
        /// <returns>The IVsTextView of the active view, or null if there is no active
        /// document or the
        /// active view in the active document is not a text view.</returns>
        private IVsTextView GetActiveTextView()
        {
            IVsMonitorSelection selection =
                this.ServiceProvider.GetService(typeof(IVsMonitorSelection))
                                                    as IVsMonitorSelection;
            object frameObj = null;
            ErrorHandler.ThrowOnFailure(
                selection.GetCurrentElementValue(
                    (uint)VSConstants.VSSELELEMID.SEID_DocumentFrame, out frameObj));

            IVsWindowFrame frame = frameObj as IVsWindowFrame;
            if (frame == null)
            {
                return null;
            }

            return GetActiveView(frame);
        }

        private static IVsTextView GetActiveView(IVsWindowFrame windowFrame)
        {
            if (windowFrame == null)
            {
                throw new ArgumentException("windowFrame");
            }

            object pvar;
            ErrorHandler.ThrowOnFailure(
                windowFrame.GetProperty((int)__VSFPROPID.VSFPROPID_DocView, out pvar));

            IVsTextView textView = pvar as IVsTextView;
            if (textView == null)
            {
                IVsCodeWindow codeWin = pvar as IVsCodeWindow;
                if (codeWin != null)
                {
                    ErrorHandler.ThrowOnFailure(codeWin.GetLastActiveView(out textView));
                }
            }
            return textView;
        }

        private static IWpfTextView GetTextViewFromVsTextView(IVsTextView view)
        {

            if (view == null)
            {
                throw new ArgumentNullException("view");
            }

            IVsUserData userData = view as IVsUserData;
            if (userData == null)
            {
                throw new InvalidOperationException();
            }

            object objTextViewHost;
            if (VSConstants.S_OK
                   != userData.GetData(Microsoft.VisualStudio
                                                .Editor
                                                .DefGuidList.guidIWpfTextViewHost,
                                       out objTextViewHost))
            {
                throw new InvalidOperationException();
            }

            IWpfTextViewHost textViewHost = objTextViewHost as IWpfTextViewHost;
            if (textViewHost == null)
            {
                throw new InvalidOperationException();
            }

            return textViewHost.TextView;
        }

        /// <summary>
        /// Given an IWpfTextView, find the position of the caret and report its column
        /// number. The column number is 0-based
        /// </summary>
        /// <param name="textView">The text view containing the caret</param>
        /// <returns>The column number of the caret's position. When the caret is at the
        /// leftmost column, the return value is zero.</returns>
        private static int GetCaretColumn(IWpfTextView textView)
        {
            // This is the code the editor uses to populate the status bar.
            Microsoft.VisualStudio.Text.Formatting.ITextViewLine caretViewLine =
                textView.Caret.ContainingTextViewLine;
            double columnWidth = textView.FormattedLineSource.ColumnWidth;
            return (int)(Math.Round((textView.Caret.Left - caretViewLine.Left)
                                       / columnWidth));
        }

        /// <summary>
        /// Determine the applicable column number for an add or remove command.
        /// The column is parsed from command arguments, if present. Otherwise
        /// the current position of the caret is used to determine the column.
        /// </summary>
        /// <param name="e">Event args passed to the command handler.</param>
        /// <returns>The column number. May be negative to indicate the column number is
        /// unavailable.</returns>
        /// <exception cref="ArgumentException">The column number parsed from event args
        /// was not a valid integer.</exception>
        private int GetApplicableColumn(EventArgs e)
        {
            var inValue = ((OleMenuCmdEventArgs)e).InValue as string;
            if (!string.IsNullOrEmpty(inValue))
            {
                int column;
                if (!int.TryParse(inValue, out column) || column < 0)
                    throw new ArgumentException("Invalid column");
                return column;
            }

            return GetCurrentEditorColumn();
        }

        /// <summary>
        /// This function is the callback used to execute a command when the a menu item
        /// is clicked. See the Initialize method to see how the menu item is associated
        /// to this function using the OleMenuCommandService service and the MenuCommand
        /// class.
        /// </summary>
        private void AddColumnGuideExecuted(object sender, EventArgs e)
        {
            int column = GetApplicableColumn(e);
            if (column >= 0)
            {
                GuidesSettingsManager.AddGuideline(column);
            }
        }

        private void RemoveColumnGuideExecuted(object sender, EventArgs e)
        {
            int column = GetApplicableColumn(e);
            if (column >= 0)
            {
                GuidesSettingsManager.RemoveGuideline(column);
            }
        }

        private void RemoveAllGuidelinesExecuted(object sender, EventArgs e)
        {
            GuidesSettingsManager.RemoveAllGuidelines();
        }

        private void ChooseGuideColorExecuted(object sender, EventArgs e)
        {
            System.Windows.Media.Color color = GuidesSettingsManager.GuidelinesColor;

            using (System.Windows.Forms.ColorDialog picker =
                new System.Windows.Forms.ColorDialog())
            {
                picker.Color = System.Drawing.Color.FromArgb(255, color.R, color.G,
                                                             color.B);
                if (picker.ShowDialog() == System.Windows.Forms.DialogResult.OK)
                {
                    GuidesSettingsManager.GuidelinesColor =
                        System.Windows.Media.Color.FromRgb(picker.Color.R,
                                                           picker.Color.G,
                                                           picker.Color.B);
                }
            }
        }

    }
}

```

**修复引用**。 此时缺少引用。 按"引用"节点上的右指针按钮解决方案资源管理器。 选择" **添加..."** 命令。 " **添加** 引用"对话框的右上角有一个搜索框。 输入不带双引号 ("editor") 。 选择 **"Microsoft.VisualStudio.Editor**"项 (必须选中该项左侧的框，而不只是选择该项) 并选择"确定"以添加引用。

**初始化**。  当包类初始化时，它会对 `Initialize` 命令实现类调用 。 初始化 `ColumnGuideCommands` 实例化类，将类实例和包引用保存在类成员中。

让我们看看类构造函数中的命令处理程序挂钩之一：

```csharp
_addGuidelineCommand =
    new OleMenuCommand(AddColumnGuideExecuted, null,
                       AddColumnGuideBeforeQueryStatus,
                       new CommandID(ColumnGuideCommands.CommandSet,
                                     cmdidAddColumnGuide));

```

创建 。`OleMenuCommand` Visual Studio使用 Microsoft Office 命令系统。 `OleMenuCommand`实例化 时的关键参数是实现命令 () 的函数，当 Visual Studio 显示包含命令 (`AddColumnGuideExecuted` `AddColumnGuideBeforeQueryStatus`) 和命令 ID 的菜单时要调用的函数。 Visual Studio 在菜单上显示命令之前调用查询状态函数，以便该命令可以使自身不可见或灰显以用于菜单的特定显示 (例如，如果没有选择) ，请禁用复制，更改其图标，甚至更改其名称 (例如，从"添加内容"更改为"删除内容") ， 等等。 命令 ID 必须与 . *vsct* 文件中声明的命令 ID 匹配。 命令集和列指南 add 命令的字符串必须在 *.vsct* 文件和 *ColumnGuideCommands.cs 之间匹配*。

以下行提供有关用户通过命令窗口调用命令时 (以下) ：

```csharp
_addGuidelineCommand.ParametersDescription = "<column>";
```

 **查询状态**。 查询状态函数和`AddColumnGuideBeforeQueryStatus``RemoveColumnGuideBeforeQueryStatus`检查某些设置 (如最大参考线数或最大列数) 或者是否有要删除的列指南。 如果条件正确，则启用命令。  查询状态函数需要高效，因为它们每次运行时Visual Studio菜单和菜单上的每个命令。

 **AddColumnGuideExecuted 函数**。 添加指南的有趣部分是找出当前编辑器视图和点线位置。  首先，此 `GetApplicableColumn`函数调用 ，用于检查命令处理程序的事件参数中是否有用户提供的参数，如果没有 ，该函数将检查编辑器的视图：

```csharp
private int GetApplicableColumn(EventArgs e)
{
    var inValue = ((OleMenuCmdEventArgs)e).InValue as string;
    if (!string.IsNullOrEmpty(inValue))
    {
        int column;
        if (!int.TryParse(inValue, out column) || column < 0)
            throw new ArgumentException("Invalid column");
        return column;
    }

    return GetCurrentEditorColumn();
}

```

`GetCurrentEditorColumn` 必须稍微挖掘一下才能获取 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView> 代码视图。  如果跟踪 、 `GetActiveTextView``GetActiveView`和 `GetTextViewFromVsTextView`，则可以看到如何这样做。 以下代码是抽象的相关代码，从当前选择开始，然后获取所选内容的框架，然后将帧的 DocView <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView><xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData> 作为 获取，然后从 IVsTextView 获取 ，然后获取视图主机，最后获取 IWpfTextView：

```csharp
   IVsMonitorSelection selection =
       this.ServiceProvider.GetService(typeof(IVsMonitorSelection))
           as IVsMonitorSelection;
   object frameObj = null;

ErrorHandler.ThrowOnFailure(selection.GetCurrentElementValue(
                                (uint)VSConstants.VSSELELEMID.SEID_DocumentFrame,
                                out frameObj));

   IVsWindowFrame frame = frameObj as IVsWindowFrame;
   if (frame == null)
       <<do nothing>>;

...
   object pvar;
   ErrorHandler.ThrowOnFailure(frame.GetProperty((int)__VSFPROPID.VSFPROPID_DocView,
                                                  out pvar));

   IVsTextView textView = pvar as IVsTextView;
   if (textView == null)
   {
       IVsCodeWindow codeWin = pvar as IVsCodeWindow;
       if (codeWin != null)
       {
           ErrorHandler.ThrowOnFailure(codeWin.GetLastActiveView(out textView));
       }
   }

...
   if (textView == null)
       <<do nothing>>

   IVsUserData userData = textView as IVsUserData;
   if (userData == null)
       <<do nothing>>

   object objTextViewHost;
   if (VSConstants.S_OK
           != userData.GetData(Microsoft.VisualStudio.Editor.DefGuidList
                                                            .guidIWpfTextViewHost,
                                out objTextViewHost))
   {
       <<do nothing>>
   }

   IWpfTextViewHost textViewHost = objTextViewHost as IWpfTextViewHost;
   if (textViewHost == null)
       <<do nothing>>

   IWpfTextView textView = textViewHost.TextView;

```

拥有 IWpfTextView 后，可以获取 caret 所在的列：

```csharp
private static int GetCaretColumn(IWpfTextView textView)
{
    // This is the code the editor uses to populate the status bar.
    Microsoft.VisualStudio.Text.Formatting.ITextViewLine caretViewLine =
        textView.Caret.ContainingTextViewLine;
    double columnWidth = textView.FormattedLineSource.ColumnWidth;
    return (int)(Math.Round((textView.Caret.Left - caretViewLine.Left)
                                / columnWidth));
}

```

用户单击当前列时，代码只需调用设置管理器来添加或删除列。 设置管理器触发所有对象侦听 `ColumnGuideAdornment` 的事件。 当事件触发时，这些对象使用新的列指南设置更新其关联的文本视图。

## <a name="invoke-command-from-the-command-window"></a>从命令窗口调用命令
列指南示例使用户能够从命令窗口中以扩展性的形式调用两个命令。 如果使用"视图"**&#124;"Windows &#124;命令窗口"** 命令，则可以看到命令窗口。 可以通过输入"edit."与命令窗口交互，在命令名称完成并提供参数 120 后，结果如下：

```csharp
> Edit.AddColumnGuide 120
>
```

启用此行为的示例片段在 *.vsct* `ColumnGuideCommands` 文件声明中、类构造函数（当它挂钩命令处理程序时）和用于检查事件参数的命令处理程序实现中。

虽然命令`<CommandFlag>CommandWellOnly</CommandFlag>`未显示在"编辑"菜单 UI 中，但 .*vsct* 文件以及"编辑"主菜单中的位置 **都显示"**"。 在主"编辑" **菜单上显示** 它们的名称，例如 **Edit.AddColumnGuide**。 保存四个命令的命令组声明将该组直接放置在"编辑 **"** 菜单上：

```xml
<Group guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"
             priority="0xB801">
        <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_EDIT" />
      </Group>

```

然后，"按钮"部分声明了命令 `CommandWellOnly` ，使它们在主菜单上不可见，然后使用 声明它们 `AllowParams`：

```xml
<Button guid="guidColumnGuidesCommandSet" id="cmdidAddColumnGuide"
        priority="0x0100" type="Button">
  <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />
  <Icon guid="guidImages" id="bmpPicAddGuide" />
  <CommandFlag>CommandWellOnly</CommandFlag>
  <CommandFlag>AllowParams</CommandFlag>

```

你看到了命令处理程序挂钩类构造函数 `ColumnGuideCommands` 中的代码，其中提供了允许参数的说明：

```csharp
_addGuidelineCommand.ParametersDescription = "<column>";

```

在检查 `GetApplicableColumn` 编辑器的 `OleMenuCmdEventArgs` 视图以查看当前列之前，你已看到函数检查了值：

```csharp
private int GetApplicableColumn(EventArgs e)
{
    var inValue = ((OleMenuCmdEventArgs)e).InValue as string;
    if (!string.IsNullOrEmpty(inValue))
    {
        int column;
        if (!int.TryParse(inValue, out column) || column < 0)
            throw new ArgumentException("Invalid column");
        return column;
    }

```

## <a name="try-your-extension"></a>试用扩展
现在可以按 **F5** 执行列指南扩展。 打开文本文件，并使用编辑器的上下文菜单添加指南行、删除它们并更改其颜色。 单击文本" (未空格传递行尾) 添加列指南，或者编辑器将其添加到行的最后一列。 如果使用命令窗口并使用参数调用命令，可以在任意位置添加列指南。

如果要尝试不同的命令放置、更改名称、更改图标等，并且对在菜单中显示最新代码的 Visual Studio 存在任何问题，可以重置正在调试的实验性配置单元。 打开"开始 **Windows菜单，** 然后键入"重置"。 查找并运行命令"重置下一Visual Studio **实例"**。 此命令将清理所有扩展组件的实验性注册表配置单元。 它不会从组件中清除设置，因此，当你的代码下次启动时读取设置存储时，关闭Visual Studio实验性配置单元时，你拥有的任何指南都仍然存在。

## <a name="finished-code-project"></a>已完成的代码项目
即将有一个GitHub扩展性Visual Studio项目，已完成的项目将在那里。 本文将更新为在发生这种情况时指向该位置。 完成的示例项目可能具有不同的 GUID，并且命令图标具有不同的位图条。

可以使用此库[extension 来试用Visual Studio指南功能的版本](https://marketplace.visualstudio.com/items?itemName=PaulHarrington.EditorGuidelines)。

## <a name="see-also"></a>另请参阅
- [在编辑器中](../extensibility/inside-the-editor.md)
- [扩展编辑器和语言服务](../extensibility/extending-the-editor-and-language-services.md)
- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
- [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)
- [向菜单添加子菜单](../extensibility/adding-a-submenu-to-a-menu.md)
- [使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)
