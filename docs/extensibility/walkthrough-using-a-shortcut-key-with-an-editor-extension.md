---
title: 将快捷键与编辑器扩展一同使用
description: 了解如何使用快捷键将视图修饰添加到文本视图。 本演练基于视区装饰编辑器模板。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - link keystrokes to commands
ms.assetid: cf6cc6c6-5a65-4f90-8f14-663decf74672
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: e07ed59b6415cc826bc6dc6d5c1e9947b51ec606
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122041511"
---
# <a name="walkthrough-use-a-shortcut-key-with-an-editor-extension"></a>演练：将快捷键与编辑器扩展一同使用
可以响应编辑器扩展中的快捷键。 下面的演练演示如何使用快捷键向文本视图添加视图修饰。 本演练基于视区装饰编辑器模板，并允许使用 + 字符添加修饰。

## <a name="prerequisites"></a>必备条件
 从 Visual Studio 2015 开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="create-a-managed-extensibility-framework-mef-project"></a>创建一Managed Extensibility Framework (MEF) Project

1. 创建 C# VSIX 项目。  ("**新建** Project对话框中，选择 **"Visual C#/** 扩展性"，然后选择 **"VSIX Project**.) 将解决方案命名 `KeyBindingTest` "。

2. 向项目添加编辑器文本修饰项模板，并将其命名 `KeyBindingTest` 。 有关详细信息，请参阅 [使用编辑器项模板 创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 添加以下引用，将 **CopyLocal** 设置为 `false` ：

    Microsoft.VisualStudio.Editor

    Microsoft.VisualStudio.OLE.Interop

    Microsoft.VisualStudio.Shell.14.0

    Microsoft.VisualStudio.TextManager.Interop

   在 KeyBindingTest 类文件中，将类名更改为"PurpleCornerBox"。 使用左边距中出现的灯泡进行其他适当的更改。 在构造函数中，将装饰层的名称从 **KeyBindingTest** 更改为 **PurpleCornerBox**：

```csharp
this.layer = view.GetAdornmentLayer("PurpleCornerBox");
```

在 KeyBindingTestTextViewCreationListener.cs 类文件中，将 AdornmentLayer 的名称从 **KeyBindingTest** 更改为 **PurpleCornerBox：**

```csharp
[Export(typeof(AdornmentLayerDefinition))]
[Name("PurpleCornerBox")]
[Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]
public AdornmentLayerDefinition editorAdornmentLayer;
```

## <a name="handle-typechar-command"></a>处理 TYPECHAR 命令
在 Visual Studio 2017 版本 15.6 之前，在编辑器扩展中处理命令的唯一方法就是实现基于 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 的命令筛选器。 Visual Studio 2017 版本 15.6 引入了基于编辑器命令处理程序的新式简化方法。 接下来的两个部分演示如何使用旧式和新式方法处理命令。

## <a name="define-the-command-filter-prior-to-visual-studio-2017-version-156"></a>在 2017 (15.6 Visual Studio 之前定义命令筛选器) 

 命令筛选器是 的实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ，它通过实例化修饰来处理命令。

1. 添加一个类文件并将其命名为 `KeyBindingCommandFilter`。

2. 添加以下 using 指令。

    ```csharp
    using System;
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio.OLE.Interop;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Text.Editor;

    ```

3. 名为 KeyBindingCommandFilter 的类应继承自 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 。

    ```csharp
    internal class KeyBindingCommandFilter : IOleCommandTarget
    ```

4. 为文本视图添加私有字段，在命令链中添加下一个命令，并添加一个标志来表示是否已添加命令筛选器。

    ```csharp
    private IWpfTextView m_textView;
    internal IOleCommandTarget m_nextTarget;
    internal bool m_added;
    internal bool m_adorned;
    ```

5. 添加用于设置文本视图的构造函数。

    ```csharp
    public KeyBindingCommandFilter(IWpfTextView textView)
    {
        m_textView = textView;
        m_adorned = false;
    }
    ```

6. 按 `QueryStatus()` 如下所示实现 方法。

    ```csharp
    int IOleCommandTarget.QueryStatus(ref Guid pguidCmdGroup, uint cCmds, OLECMD[] prgCmds, IntPtr pCmdText)
    {
        return m_nextTarget.QueryStatus(ref pguidCmdGroup, cCmds, prgCmds, pCmdText);
    }
    ```

7. 实现 方法，以便如果键入了加号或 () `Exec()` **+** 向视图添加紫色框。

    ```csharp
    int IOleCommandTarget.Exec(ref Guid pguidCmdGroup, uint nCmdID, uint nCmdexecopt, IntPtr pvaIn, IntPtr pvaOut)
    {
        if (m_adorned == false)
        {
            char typedChar = char.MinValue;

            if (pguidCmdGroup == VSConstants.VSStd2K && nCmdID == (uint)VSConstants.VSStd2KCmdID.TYPECHAR)
            {
                typedChar = (char)(ushort)Marshal.GetObjectForNativeVariant(pvaIn);
                if (typedChar.Equals('+'))
                {
                    new PurpleCornerBox(m_textView);
                    m_adorned = true;
                }
            }
        }
        return m_nextTarget.Exec(ref pguidCmdGroup, nCmdID, nCmdexecopt, pvaIn, pvaOut);
    }

    ```

## <a name="add-the-command-filter-prior-to-visual-studio-2017-version-156"></a>在 2017 (15.6 Visual Studio 之前添加命令筛选器) 
 装饰提供程序必须将命令筛选器添加到文本视图。 此示例中，提供程序实现 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> 以侦听文本视图创建事件。 此装饰提供程序还导出装饰层，该层定义装饰的 Z 顺序。

1. 在 KeyBindingTestTextViewCreationListener 文件中，添加以下 using 指令：

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.OLE.Interop;
    using Microsoft.VisualStudio.Utilities;
    using Microsoft.VisualStudio.Editor;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.TextManager.Interop;

    ```

2. 若要获取文本视图适配器，必须导入 <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> 。

    ```csharp
    [Import(typeof(IVsEditorAdaptersFactoryService))]
    internal IVsEditorAdaptersFactoryService editorFactory = null;

    ```

3. 更改 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> 方法，以便添加 `KeyBindingCommandFilter` 。

    ```csharp
    public void TextViewCreated(IWpfTextView textView)
    {
        AddCommandFilter(textView, new KeyBindingCommandFilter(textView));
    }
    ```

4. 处理程序 `AddCommandFilter` 获取文本视图适配器并添加命令筛选器。

    ```csharp
    void AddCommandFilter(IWpfTextView textView, KeyBindingCommandFilter commandFilter)
    {
        if (commandFilter.m_added == false)
        {
            //get the view adapter from the editor factory
            IOleCommandTarget next;
            IVsTextView view = editorFactory.GetViewAdapter(textView);

            int hr = view.AddCommandFilter(commandFilter, out next);

            if (hr == VSConstants.S_OK)
            {
                commandFilter.m_added = true;
                 //you'll need the next target for Exec and QueryStatus
                if (next != null)
                commandFilter.m_nextTarget = next;
            }
        }
    }
    ```

## <a name="implement-a-command-handler-starting-in-visual-studio-2017-version-156"></a>从 2017 (15.6 Visual Studio 开始，实现命令处理程序) 

首先，更新项目的 Nuget 引用以引用最新的编辑器 API：

1. 右键单击项目，然后选择"**管理 Nuget 包"。**

2. 在 **Nuget 程序包管理器** 中，选择"更新"选项卡，选中"**选择所有包**"复选框，然后选择"更新 **"。**

命令处理程序是 的实现 <xref:Microsoft.VisualStudio.Commanding.ICommandHandler%601> ，它通过实例化修饰来处理命令。

1. 添加一个类文件并将其命名为 `KeyBindingCommandHandler`。

2. 添加以下 using 指令。

   ```csharp
   using Microsoft.VisualStudio.Commanding;
   using Microsoft.VisualStudio.Text.Editor;
   using Microsoft.VisualStudio.Text.Editor.Commanding.Commands;
   using Microsoft.VisualStudio.Utilities;
   using System.ComponentModel.Composition;
   ```

3. 名为 KeyBindingCommandHandler 的类应继承自 `ICommandHandler<TypeCharCommandArgs>` ，并导出为 <xref:Microsoft.VisualStudio.Commanding.ICommandHandler> ：

   ```csharp
   [Export(typeof(ICommandHandler))]
   [ContentType("text")]
   [Name("KeyBindingTest")]
   internal class KeyBindingCommandHandler : ICommandHandler<TypeCharCommandArgs>
   ```

4. 添加命令处理程序的显示名称：

   ```csharp
   public string DisplayName => "KeyBindingTest";
   ```

5. 按 `GetCommandState()` 如下所示实现 方法。 由于此命令处理程序处理核心编辑器 TYPECHAR 命令，因此它可以将启用该命令委托给核心编辑器。

   ```csharp
   public CommandState GetCommandState(TypeCharCommandArgs args)
   {
       return CommandState.Unspecified;
   }
   ```

6. 实现 方法，以便如果键入了加号或 () `ExecuteCommand()` **+** 向视图添加紫色框。

   ```csharp
   public bool ExecuteCommand(TypeCharCommandArgs args, CommandExecutionContext executionContext)
   {
       if (args.TypedChar == '+')
       {
           bool alreadyAdorned = args.TextView.Properties.TryGetProperty(
               "KeyBindingTextAdorned", out bool adorned) && adorned;
           if (!alreadyAdorned)
           {
               new PurpleCornerBox((IWpfTextView)args.TextView);
               args.TextView.Properties.AddProperty("KeyBindingTextAdorned", true);
           }
       }

       return false;
   }
   ```

   7. 将装饰层定义从 *KeyBindingTestTextViewCreationListener.cs* 文件复制到 *KeyBindingCommandHandler.cs，* 然后删除 *KeyBindingTestTextViewCreationListener.cs* 文件：

   ```csharp
   /// <summary>
   /// Defines the adornment layer for the adornment. This layer is ordered
   /// after the selection layer in the Z-order.
   /// </summary>
   [Export(typeof(AdornmentLayerDefinition))]
   [Name("PurpleCornerBox")]
   [Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]
   private AdornmentLayerDefinition editorAdornmentLayer;
   ```

## <a name="make-the-adornment-appear-on-every-line"></a>使修饰显示在每一行上

原始修饰出现在文本文件中每个字符"a"上。 现在，我们已更改代码以添加修饰以响应字符，它仅在键入字符的行 **+** **+** 上添加修饰。 我们可以更改修饰代码，使修饰再次出现在每个"a"上。

在 *KeyBindingTest.cs* 文件中，更改 方法以在视图中的所有行中进行复用，以修饰 `CreateVisuals()` "a"字符。

```csharp
private void CreateVisuals(ITextViewLine line)
{
    IWpfTextViewLineCollection textViewLines = this.view.TextViewLines;

    foreach (ITextViewLine textViewLine in textViewLines)
    {
        if (textViewLine.ToString().Contains("a"))
        {
            // Loop through each character, and place a box around any 'a'
            for (int charIndex = textViewLine.Start; charIndex < textViewLine.End; charIndex++)
            {
                if (this.view.TextSnapshot[charIndex] == 'a')
                {
                    SnapshotSpan span = new SnapshotSpan(this.view.TextSnapshot, Span.FromBounds(charIndex, charIndex + 1));
                    Geometry geometry = textViewLines.GetMarkerGeometry(span);
                    if (geometry != null)
                    {
                        var drawing = new GeometryDrawing(this.brush, this.pen, geometry);
                        drawing.Freeze();

                        var drawingImage = new DrawingImage(drawing);
                        drawingImage.Freeze();

                        var image = new Image
                        {
                            Source = drawingImage,
                        };

                        // Align the image with the top of the bounds of the text geometry
                        Canvas.SetLeft(image, geometry.Bounds.Left);
                        Canvas.SetTop(image, geometry.Bounds.Top);

                        this.layer.AddAdornment(AdornmentPositioningBehavior.TextRelative, span, null, image, null);
                    }
                }
            }
        }
    }
}
```

## <a name="build-and-test-the-code"></a>生成并测试代码

1. 生成 KeyBindingTest 解决方案，在实验实例中运行它。

2. 创建或打开文本文件。 键入一些包含字符"a"的单词，然后在文本 **+** 视图中的任何位置键入 。

     在文件的每一个"a"字符上都应显示紫色正方形。
