---
title: 显示进度
description: 介绍不同类型的进度栏以及何时使用它们
ms.date: 12/01/2021
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: pchapman
ms.prod: visual-studio-windows
ms.technology: vs-ide-sdk
ms.custom: cookbook
ms.openlocfilehash: 872876dd0a2785b991abf846399f3519193409f6
ms.sourcegitcommit: a149b3a034bb555ad217656c0ec8bc1672b1e215
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2021
ms.locfileid: "133515817"
---
# <a name="progress-bars-for-backgrounds-tasks-in-visual-studio-extensions"></a>Visual Studio 扩展中的背景任务的进度栏

可以通过多种方式在 Visual Studio 中显示正在运行的后台任务的进度。 下面介绍如何使用自己的扩展中的进度栏。

## <a name="status-bar"></a>状态栏
状态栏有自己的进度指示器，它是向用户显示进度的最简单位置。 它可见，但不需要用户注意或阻止其当前任务。 对于大多数后台任务，状态栏是一个不错的选择。

:::image type="content" source="../media/status-bar-progress.gif" alt-text="正在使用的状态栏进度指示器的动画。":::

使用 API 来显示状态栏进度相当简单：

```csharp
await Task.Delay(1000); // long running task
await VS.StatusBar.ShowProgressAsync("Step 1/3", 1, 3);

await Task.Delay(1000); // long running task
await VS.StatusBar.ShowProgressAsync("Step 2/3", 2, 3);

await Task.Delay(1000); // long running task
await VS.StatusBar.ShowProgressAsync("Step 3/3", 3, 3);

// Progress ends as current step (3) and total steps (3) are equal
```

## <a name="threaded-wait-dialog"></a>线程等待对话框
线程等待对话框 (台币) 是一个进度指示器对话框，该对话框仅在后台任务所用时间超过 x 个扩展程序指定的秒数时才会出现。 它将进度全部写入状态栏，但会在运行 x 秒数后显示此对话框。

:::image type="content" source="../media/threaded-wait-dialog.gif" alt-text="显示进度的线程等待对话框。":::

不能在需要时显示台币。 它通过 Visual Studio 进行管理，使其不会过于频繁地影响最终用户。 使用它所需的代码比只使用状态栏更多，但它仍是一个相对简单的 API，可供使用：  

```csharp
var fac = await VS.Services.GetThreadedWaitDialogAsync() as IVsThreadedWaitDialogFactory;
IVsThreadedWaitDialog4 twd = fac.CreateInstance();

twd.StartWaitDialog("Demo", "Working on it...", "", null, "", 1, true, true);

var totalSteps = 3;

for (var currentStep = 1; currentStep <= totalSteps; currentStep++)
{
    var text = $"Step {currentStep}/{totalSteps}";
    twd.UpdateProgress("In progress", text, text, currentStep, totalSteps, true, out _);

    await Task.Delay(1000); // long running task

    if (currentStep == totalSteps)
    {
        // Dismisses the dialog
        (twd as IDisposable).Dispose();
    }
}
```

## <a name="task-status-center"></a>任务状态中心
在状态栏的左下角是任务状态中心 (TSC) 。 它用于报告长时间运行的后台任务的进度，并由 Visual Studio 中的许多服务使用。

:::image type="content" source="../media/task-status-center.gif" alt-text="显示正在运行的后台任务的任务状态中心。":::

API 的概念比使用其他显示进度的方法更多。

```csharp
private async Task StartAsync()
{
    IVsTaskStatusCenterService tsc = await VS.Services.GetTaskStatusCenterAsync();

    var options = default(TaskHandlerOptions);
    options.Title = "My long running task";
    options.ActionsAfterCompletion = CompletionActions.None;

    TaskProgressData data = default;
    data.CanBeCanceled = true;

    ITaskHandler handler = tsc.PreRegister(options, data);
    Task task = LongRunningTaskAsync(data, handler);
    handler.RegisterTask(task);
}

private async Task LongRunningTaskAsync(TaskProgressData data, ITaskHandler handler)
{
    float totalSteps = 3;

    for (float currentStep = 1; currentStep <= totalSteps; currentStep++)
    {
        await Task.Delay(1000);

        data.PercentComplete = (int)(currentStep / totalSteps * 100);
        data.ProgressText = $"Step {currentStep} of {totalSteps} completed";
        handler.Progress.Report(data);
    }
}
```

## <a name="other-resources"></a>其他资源

* [任务状态中心 API 参考](/dotnet/api/microsoft.visualstudio.taskstatuscenter)
