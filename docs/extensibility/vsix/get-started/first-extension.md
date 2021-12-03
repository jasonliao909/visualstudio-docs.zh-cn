---
title: 第一个扩展
description: 显示启动并运行第一个扩展Visual Studio几个简单步骤。
ms.date: 12/01/2021
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: pchapman
ms.prod: visual-studio-windows
ms.technology: vs-ide-sdk
ms.custom: cookbook
ms.openlocfilehash: f9fabafbc1bf99e07827e02618b5c3e267265860
ms.sourcegitcommit: a149b3a034bb555ad217656c0ec8bc1672b1e215
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2021
ms.locfileid: "133515869"
---
# <a name="your-first-visual-studio-extension"></a>第一Visual Studio扩展

本文将指导你完成一些简单的步骤，使第一个Visual Studio扩展启动并运行。 使用 Visual Studio 和 C# 编写.NET Framework扩展。 如果你是 .NET 开发人员，你会发现编写扩展类似于编写大多数其他 .NET 程序和库。

今天要写入的扩展将添加一个命令，该命令在执行时向文本编辑器中插入新的 guid。 它简单、有用，并且对扩展开发的各个方面提供了很好的介绍。

如果你是视觉学习者，请查看本教程中某人的这段简短视频。

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RWPmjK]

在开始编写第一Visual Studio扩展 (，我承诺！) ，请确保你已获得[所需的工具](get-tools.md)。

## <a name="create-the-project"></a>创建项目
有几个项目模板可供选择，因此你想要做出正确的选择。 此社区工具包中使用的模板均在名称 **(Community)** 名字对象。

VSIX **Project/Command (Community)** 模板附带了一个挂接的命令，因此可以轻松从该模板开始。 对于大多数扩展来说，这是一个很好的起点。 如果知道需要工具窗口，请使用 **VSIX Project/工具窗口 (Community)** 模板。 它还具有用于打开工具窗口的命令。

将 **空 VSIX Project (Community)** 或 **VSIX** Project (Community) 模板用于仅 MEF 扩展或其他高级方案。

这一次，你将选择 VSIX Project **w/Command (Community)** 模板，如以下屏幕截图所示。

:::image type="content" source="../media/new-project-dialog.png" alt-text="&quot;新建Project显示 VSIX 项目模板的对话框。":::

选择项目模板后，需要为项目命名。 将其称为 **InsertGuid**。

:::image type="content" source="../media/configure-new-project.png" alt-text="配置新项目。":::

点击"创建 **"** 按钮后，最终应看到如下所示Project VSIX 设备：

:::image type="content" source="../media/new-project-files.png" alt-text="新项目文件和文件夹。":::

## <a name="overview-of-the-files"></a>文件概述
让我们看一下最重要的文件。

**InsertGuidPackage.cs** 是指 Package 类。 它 `InitializeAsync(...)` 的方法由 Visual Studio来初始化扩展。 在此处添加事件侦听器并注册命令、工具窗口、设置和其他内容。

**source.extension.vsixmanifest** 是扩展的清单文件。 它包含元数据（如标题和说明）以及扩展包含的信息。

**VSCommandTable.vsct** 是一个 XML 文件，其中以声明的方式定义了命令和键绑定，因此它们可以通过Visual Studio。

**Commands/MyCommand.cs** 是 *VSCommandTable.vsct* 文件中定义的命令的命令处理程序。 它通过单击按钮控制执行命令时发生的情况。

## <a name="modifying-the-command"></a>修改命令
首先，需要确保命令在菜单系统中具有正确的名称、图标Visual Studio位置。

打开 *VSCommandTable.vsct* 文件，找到 `<Group>` 和 `<Button>` 。 请注意按钮如何将组指定为其父级，而组的父级是内置的 *VSMainMenu/Tools* 菜单。

对于扩展，需要将"*插入 GUID"* 命令按钮设置在"编辑"主菜单下，以便将组重新父级设置到"编辑"菜单。 将 *"工具**"替换为"* 编辑"，如以下代码片段所示：

```xml
<Group guid="InsertGuid" id="MyMenuGroup" priority="0x0600">
  <Parent guid="VSMainMenu" id="Edit"/>
</Group>
```

你可获取完整的 IntelliSense 位置，方便查找正确的位置。

:::image type="content" source="../media/vsct-parent-intellisense.png" alt-text="VSCT 父 IntelliSense。":::

`<Button>`还需要更新 。 将 元素的 属性更新为 PasteAppend ，为此图标 `id` `<Icon>` *提供一个新图标*。 使用良好的描述性名称更新文本，使用命令的技术名称更新 > - 这是用户在"工具""选项"> 环境">"键盘"对话框中向命令分配自定义键盘快捷方式时显示 `<ButtonText>` `<LocCanonicalName>` 的名称。

```xml
<Button guid="InsertGuid" id="MyCommand" priority="0x0100" type="Button">
  <Parent guid="InsertGuid" id="MyMenuGroup" />
  <Icon guid="ImageCatalogGuid" id="PasteAppend" />
  <CommandFlag>IconIsMoniker</CommandFlag>
  <Strings>
    <ButtonText>Insert GUID</ButtonText>
    <LocCanonicalName>.Edit.InsertGuid</LocCanonicalName>
  </Strings>
</Button>
```

>[!NOTE]
> 始终以 `<LocCanonicalName>` 点字符启动 。 它确保不会自动预绘制其他文本，并且不会显示点。  

可以使用映像库中提供的数千个Visual Studio，甚至可以获取 IntelliSense 中显示的预览：

:::image type="content" source="../media/vsct-icon-intellisense.png" alt-text="VSCT 图标 IntelliSense。":::

现在，你已更新了命令的名称、图标和位置，现在可以编写一些代码以将 guid 插入文本编辑器中。

打开 */Commands/MyCommand.cs* 文件，并修改该文件，以在执行时插入新的 guid：

```csharp
using System;
using Community.VisualStudio.Toolkit;
using EnvDTE;
using Microsoft.VisualStudio.Shell;
using Task = System.Threading.Tasks.Task;

namespace InsertGuid
{
    [Command(PackageIds.MyCommand)]
    internal sealed class MyCommand : BaseCommand<MyCommand>
    {
        protected override async Task ExecuteAsync(OleMenuCmdEventArgs e)
        {
            await Package.JoinableTaskFactory.SwitchToMainThreadAsync();
            DocumentView docView = await VS.Documents.GetActiveDocumentViewAsync();
            if (docView?.TextView == null) return;
            SnapshotPoint position = docView.TextView.Caret.Position.BufferPosition;
            docView.TextBuffer?.Insert(position, Guid.NewGuid().ToString()); 
        }
    }
}
```

使用 对象获取活动编辑器文本视图，然后将 guid 插入其文本缓冲区 `VS` 的插入点位置。

>[!NOTE]
> 你将在此 `await JoinableTaskFactory.SwitchToMainThreadAsync()` 社区 `ThreadHelper.ThrowIfNotOnUIThread()` 工具包中的许多位置看到 和 。 它们处理线程切换最佳做法，此时你无需知道何时以及如何使用它们 - 编译器警告和代码修补程序 (灯泡) 使这变得非常简单。

扩展的第一个草稿现已完成，现在可以进行测试。

## <a name="running-and-debugging"></a>运行和调试
运行扩展与运行任何其他 .NET 项目一样简单。 只需点击 *F5* 以在附加调试器的情况下运行，或 *单击 Ctrl+F5* 即可运行而不运行。

这样做将启动安装了扩展的 Visual Studio试验实例。 实验实例是常规版本的 Visual Studio，但安装了单独的设置和扩展。 它有助于将内容分开。

启动实验实例时，应在"编辑"主菜单中看到"插入 *GUID"* 命令。 

:::image type="content" source="../media/insert-guid-command.png" alt-text="&quot;编辑&quot;主菜单中的&quot;插入 GUID&quot;命令。":::

打开任何基于文本的文件并执行 命令以插入新的 guid。 就这么简单！

## <a name="summary"></a>总结
现已创建第一个扩展，该扩展将命令按钮添加到主菜单，在执行时与文本编辑器进行交互。

祝贺！！

可以在示例存储库中找到此扩展 [的代码](https://github.com/VsixCommunity/Samples)。

## <a name="additional-resources"></a>其他资源

* [扩展剖析](extension-anatomy.md)
* [菜单&命令](../recipes/menus-buttons-commands.md)
* [最佳做法清单](../publish/checklist.md)
