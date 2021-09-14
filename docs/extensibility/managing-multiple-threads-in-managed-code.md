---
title: 如何：管理托管代码中的多个线程|Microsoft Docs
description: 了解如何在托管的 VSPackage 扩展调用异步方法或具有与 UI 线程Visual Studio线程。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 59730063-cc29-4dae-baff-2234ad8d0c8f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 8bc6cdae2ac2fca16467bdbeee2333e7d7189ee9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664275"
---
# <a name="how-to-manage-multiple-threads-in-managed-code"></a>如何：在托管代码中管理多个线程
如果你有一个托管的 VSPackage 扩展，该扩展调用异步方法，或者具有对除 Visual Studio UI 线程外的其他线程执行的操作，则应遵循下面给出的准则。 你可以使 UI 线程保持响应，因为它不需要等待另一个线程上的工作完成。 可以使代码更高效，因为你没有占用堆栈空间的额外线程，并且可以使它更可靠且更易于调试，因为可以避免死锁和无响应的代码。

 通常，你可以从 UI 线程切换到其他线程，反之亦然。 当方法返回时，当前线程是最初调用它的线程。

> [!IMPORTANT]
> 以下准则使用 命名空间中的 <xref:Microsoft.VisualStudio.Threading> API，特别是 <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory> 类。 此命名空间中的 API 是 中的新增功能 [!INCLUDE[vs_dev12](../extensibility/includes/vs_dev12_md.md)] 。 可以从属性 获取 <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory> 的实例 <xref:Microsoft.VisualStudio.Shell.ThreadHelper> `ThreadHelper.JoinableTaskFactory` 。

## <a name="switch-from-the-ui-thread-to-a-background-thread"></a>从 UI 线程切换到后台线程

1. 如果位于 UI 线程上，并且想要在后台线程上执行异步工作，请使用 `Task.Run()` ：

    ```csharp
    await Task.Run(async delegate{
        // Now you're on a separate thread.
    });
    // Now you're back on the UI thread.

    ```

2. 如果位于 UI 线程上，并且想要在后台线程上执行工作时同步阻止，请使用 <xref:System.Threading.Tasks.TaskScheduler> 中的 `TaskScheduler.Default` 属性 <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.Run%2A> ：

    ```csharp
    // using Microsoft.VisualStudio.Threading;
    ThreadHelper.JoinableTaskFactory.Run(async delegate {
        await TaskScheduler.Default;
        // You're now on a separate thread.
        DoSomethingSynchronous();
        await OrSomethingAsynchronous();
    });
    ```

## <a name="switch-from-a-background-thread-to-the-ui-thread"></a>从后台线程切换到 UI 线程

1. 如果位于后台线程上，并且想要在 UI 线程上执行某些操作，请使用 <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> ：

    ```csharp
    // Switch to main thread
    await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync();
    ```

     可以使用 方法 <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> 切换到 UI 线程。 此方法使用当前异步方法的延续将消息发送到 UI 线程，并与线程框架的其余部分通信，以设置正确的优先级并避免死锁。

     如果后台线程方法不是异步的，并且无法使其异步，则仍可以使用 语法通过包装工作来切换到 UI 线程， `await` <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.Run%2A> 如以下示例所示：

    ```csharp
    ThreadHelper.JoinableTaskFactory.Run(async delegate {
        // Switch to main thread
        await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync();
        // Do your work on the main thread here.
    });
    ```
