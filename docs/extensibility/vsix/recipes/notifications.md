---
title: 通知
description: 用于向用户显示通知的各种不同方式的配方。
ms.date: 12/01/2021
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: pchapman
ms.prod: visual-studio-windows
ms.technology: vs-ide-sdk
ms.custom: cookbook
ms.openlocfilehash: d0b38d963bb3a0c80aee1f43b06afb5fa142d1a3
ms.sourcegitcommit: a149b3a034bb555ad217656c0ec8bc1672b1e215
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2021
ms.locfileid: "133515839"
---
# <a name="displaying-notifications-in-visual-studio-extensions"></a>在扩展Visual Studio通知

有几种机制可以向扩展的用户显示通知。 选择适当的选项可能很有挑战性，让我们看一下选项。

* 状态栏
* 信息栏
* 消息框
* “输出”窗口

它们用于不同的目的，并且对用户的关注有不同的需求级别。

使用 **状态** 栏通知用户不需要用户执行任何操作或输入的事件。 如果他们未在状态栏中看到通知，则这一点正常 - 查看通知并不重要。

若要吸引用户的注意，并让他们执行一些操作，请使用信息 **栏**。 他们不必执行任何操作，可以等到完成所执行的工作。 通知很重要，但不是关键。

当通知必须阻止当前用户继续其操作时，请使用消息 **框**。 这是一条阻止和关键通知。

若要通知用户非严重错误，请使用 **输出窗口。** 如果希望确保用户看到输出窗口，可以重点关注问题，但建议不要这样做。

## <a name="status-bar"></a>状态栏
状态栏是主窗口底部的区域，它显示有关当前窗口状态 (的信息，例如正在查看哪些内容以及如何查看) 、后台任务 (（如打印、扫描和格式设置) ）或其他上下文信息 (例如选择和键盘状态) 。

:::image type="content" source="../media/status-bar.png" alt-text="显示自定义文本的状态栏。":::

如果不需要完全关注用户，但仍要向用户提供信息，请使用状态栏。

### <a name="set-the-text"></a>设置文本
这会将状态栏中的文本设置为任何字符串。

```csharp
// call it from an async context
await VS.StatusBar.ShowMessageAsync("My text");

// or from a synchronous method:
VS.StatusBar.ShowMessageAsync("My text").FireAndForget();
```

### <a name="animation-icon"></a>“动画”图标
向状态栏添加动画图标非常简单。

:::image type="content" source="../media/status-bar-animation.gif" alt-text="使用 StatusAnimation.Sync 图标对状态栏进行动画显示。":::

只需指定要使用哪个动画图标。

```csharp
// call it from an async context
await VS.StatusBar.StartAnimationAsync(StatusAnimation.Sync);

// or from a synchronous method:
VS.StatusBar.StartAnimationAsync(StatusAnimation.Sync).FireAndForget();
```

通过调用 再次停止动画 `EndStatusbarAnimationAsync` 。

```csharp
// call it from an async context
await VS.StatusBar.EndAnimationAsync(StatusAnimation.Sync);

// or from a synchronous method:
VS.StatusBar.EndAnimationAsync(StatusAnimation.Sync).FireAndForget();
```

## <a name="info-bar"></a>信息栏
信息栏是工具窗口或文档窗口顶部的黄色栏。 它可用于在不阻止用户的情况下吸引用户的注意。 信息栏可以包含图标、文本和多个超链接。

:::image type="content" source="../media/info-bar-solution-explorer.png" alt-text="信息栏，显示在解决方案资源管理器。":::

下面将了解如何将信息栏添加到解决方案资源管理器窗口。

```csharp
var model = new InfoBarModel(
    new[] {
        new InfoBarTextSpan("The text in the Info Bar. "),
        new InfoBarHyperlink("Click me")
    },
    KnownMonikers.PlayStepGroup,
    true);

InfoBar infoBar = VS.InfoBar.CreateInfoBar(ToolWindowGuids80.SolutionExplorer, model);
infoBar.ActionItemClicked += InfoBar_ActionItemClicked;
await infoBar.TryShowInfoBarUIAsync();

...

private void InfoBar_ActionItemClicked(object sender, InfoBarActionItemEventArgs e)
{
    ThreadHelper.ThrowIfNotOnUIThread();

    if (e.ActionItem.Text == "Click me")
    {
        // do something
    }
}
```

若要将信息栏添加到文档窗口，只需将打开的文档的文件名传递给 `VS.Notifications.CreateInfoBar(fileName, model)` 方法。

:::image type="content" source="../media/info-bar-document.png" alt-text="显示在文档顶部的信息栏。":::

如果要将信息栏直接连接到 ，可以使用以下 `ITextView` 便捷扩展方法实现此操作：

```csharp
InfoBar infoBar = textView.CreateInfoBar(model);
```

## <a name="message-box"></a>消息框
有多种方式使用 .NET 显示消息框。 例如，通过 Windows 窗体或 WPF。 它们会导致Visual Studio窗口正确设置父级的扩展中出现一些问题，因此建议使用Visual Studio消息框。

:::image type="content" source="../media/message-box.png" alt-text="本机Visual Studio消息框。":::

需要阻止 UI 以获得用户的完全关注时，请使用消息框。

```csharp
// Simple text box
VS.MessageBox.Show("Title", "The message");

// Async and with buttons defined
await VS.MessageBox.ShowAsync("Title", "The message", OLEMSGICON.OLEMSGICON_INFO, OLEMSGBUTTON.OLEMSGBUTTON_OKCANCEL);   
```

## <a name="output-window"></a>输出窗口
使用输出窗口显示有关异常和其他文本信息的信息。

:::image type="content" source="../media/output-window.png" alt-text="写入自定义自定义输出窗口的文本。":::

使用 方法输出窗口创建自定义对象窗格并写入 `VS.Windows.CreateOutputWindowPaneAsync` 到该窗格。

```csharp
OutputWindowPane pane = await VS.Windows.CreateOutputWindowPaneAsync("Name of pane");
await pane.WriteLineAsync("Line 1");
await pane.WriteLineAsync("Line 2");
await pane.WriteLineAsync("Line 3");

```

有关 [记录异常的详细信息](handle-errors.md) ，请参阅错误处理方案。
