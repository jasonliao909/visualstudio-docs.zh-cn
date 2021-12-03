---
title: 错误处理
description: 说明如何最好地处理扩展中发生的错误和异常
ms.date: 12/01/2021
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: pchapman
ms.prod: visual-studio-windows
ms.technology: vs-ide-sdk
ms.custom: cookbook
ms.openlocfilehash: 25e6701f0b8702b976181020b1e5a3f6544a9ca7
ms.sourcegitcommit: a149b3a034bb555ad217656c0ec8bc1672b1e215
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2021
ms.locfileid: "133515861"
---
# <a name="error-handling-in-visual-studio-extensions"></a>Visual Studio 扩展中的错误处理

任何程序（包括 Visual Studio 扩展）都可能出现异常。 接下来，请确保以优化用户体验的方式正确处理它们。

如果异常是不应发生的异常，则您希望以一种可以修复异常的方式记录异常的详细信息。 根据问题的严重性，你可能还希望让用户了解相关信息。

## <a name="include-the-symbols"></a>包括符号
若要确保具有有关发生的异常的最准确的信息，请确保在扩展名中包含 .pdb 文件。 默认情况下启用此功能，但请确保通过显示项目 (F4) 的属性进行检查。

:::image type="content" source="../media/include-pdb.png" alt-text="将 PDB 文件包括在 VSIX 容器中。":::

请确保将属性 " **包含调试符号** " 设置为 " **True**"。

这会使你收集所需的信息。 让我们看看一些用于执行此操作的策略。

## <a name="automated-telemetry"></a>自动遥测
你可以使用任何可在任何 .NET 应用程序中通过扩展使用的遥测机制。 常用选项有[Application Insights](/powerapps/maker/canvas-apps/application-insights)、 [Raygun](https://raygun.com/)、 [Google Analytics](https://analytics.google.com/)等。

你将手动使用其 Api 通过这些遥测系统报告异常详细信息。 使用此选项可以很好地解决用户计算机上出现的任何问题，并使你能够及早提前解决问题。

使用此选项时，请务必在隐私声明中提及，因为某些用户不喜欢报告遥测。

## <a name="log-to-output-window"></a>记录到输出窗口
当使用 `try/catch` 块处理异常时，让用户了解发生了什么问题可能是有益的。 这样，他们就可以轻松地将问题报告给你，这种方法很容易修复。

最佳方法之一是将异常详细信息输出到输出窗口。 这样，用户就可以看到发生了异常，并向他们提供 stacktrace 来向你发送 bug 报告。

Community Toolkit 使其变得非常容易。 在同步上下文中，只需 `Log()` 在任何上使用扩展方法 `Exception` 。

```csharp
try
{
    // Do work;
}
catch (Exception ex)
{
    ex.Log();
}
```

对于异步上下文，也可以通过等待扩展方法来完成此操作 `LogAsync()` 。

```csharp
try
{
    // Do work;
}
catch (Exception ex)
{
    await ex.LogAsync();
}
```

## <a name="notify-the-user"></a>通知用户
如果异常对用户严重性较低，则没有理由中断它们。 请考虑使用状态栏来表明发生了错误。

如果异常严重并导致用户流中断，请考虑使用消息框让用户了解该错误。 请确保仍通过遥测和/或输出窗口记录异常，如前文所述。

若要了解有关如何使用状态栏和消息框的详细信息，请参阅 [通知食谱](notifications.md)。
