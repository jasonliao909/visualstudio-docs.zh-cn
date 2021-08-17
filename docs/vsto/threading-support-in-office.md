---
title: 中的线程Office
description: 在对象模型中支持Microsoft Office线程。 对象Office不是线程安全的，但可以在一个解决方案中使用多个Office线程。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- multiple threads [Office development in Visual Studio]
- threading [Office development in Visual Studio]
- Office applications [Office development in Visual Studio], threading support
- object models [Office development in Visual Studio], threading support
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 0313a6c0b263cfb47cbde84524682db446fc29050fa42b639e2fed407d33b9ee
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121423808"
---
# <a name="threading-support-in-office"></a>中的线程Office
  本文提供有关如何在对象模型中支持线程Microsoft Office的信息。 对象Office不是线程安全的，但可以与一个解决方案中的多个线程Office。 Office是 COM 服务器 (组件) 模型。 COM 允许客户端在任意线程上调用 COM 服务器。 对于非线程安全的 COM 服务器，COM 提供了一种机制来序列化并发调用，以便随时只有一个逻辑线程在服务器上执行。 此机制称为 STA 模型 (单元) 单元。 由于调用是序列化的，因此当服务器繁忙或正在后台线程上处理其他调用时，调用方可能会阻塞一段时间。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="knowledge-required-when-using-multiple-threads"></a>使用多个线程时所需的知识
 若要使用多个线程，必须至少对多线程处理以下方面有基本的了解：

- WindowsApi

- COM 多线程概念

- 并发

- 同步

- 封送

  有关多线程的常规信息，请参阅 [托管线程](/dotnet/standard/threading/)。

  Office STA 中运行。 通过了解这一点的含义，可以了解如何将多个线程用于Office。

## <a name="basic-multithreading-scenario"></a>基本多线程方案
 解决方案中的Office始终在主 UI 线程上运行。 你可能想要通过在后台线程上运行单独的任务来优化应用程序性能。 目标是一次似乎完成两个任务，而不是一个任务后跟另一个任务，这应使执行更顺畅 (使用多个线程) 。 例如，你可能在 Excel UI 主线程上具有事件代码，并且在后台线程上，可以运行一个任务，该任务从服务器收集数据，然后使用服务器的数据更新 Excel UI 中的单元格。

## <a name="background-threads-that-call-into-the-office-object-model"></a>调用对象模型的后台Office线程
 当后台线程调用 Office时，该调用会自动跨 STA 边界封送。 但是，无法保证应用程序Office后台线程执行调用时处理调用。 有几种可能的情况：

1. 应用程序Office必须发送消息才能让调用有机会输入。 如果它正在执行大量处理而不产生这种结果，则这可能需要一些时间。

2. 如果单元中已存在另一个逻辑线程，则新线程无法进入。 当逻辑线程进入应用程序Office，然后重新调用调用方的单元时，通常会发生这种情况。 应用程序被阻止，等待该调用返回。

3. Excel可能状态，因此无法立即处理传入调用。 例如，Office应用程序可能正在显示模式对话框。

   对于可能性 2 和 3，COM 提供了 [IMessageFilter](/windows/desktop/api/objidl/nn-objidl-imessagefilter) 接口。 如果服务器实现它，则所有调用都通过 [HandleIncomingCall](/windows/desktop/api/objidl/nf-objidl-imessagefilter-handleincomingcall) 方法进入。 对于可能 2，会自动拒绝调用。 对于可能性 3，服务器可以拒绝调用，具体取决于情况。 如果调用被拒绝，调用方必须决定要执行什么。 通常，调用方实现 [IMessageFilter](/windows/desktop/api/objidl/nn-objidl-imessagefilter)，在这种情况下 [，RetryRejectedCall](/windows/desktop/api/objidl/nf-objidl-imessagefilter-retryrejectedcall) 方法会通知其拒绝。

   但是，对于使用 Visual Studio 中的 Office 开发工具创建的解决方案，COM 互操作会将所有被拒绝的调用转换为 ("消息筛选器指示应用程序 <xref:System.Runtime.InteropServices.COMException> 正忙") 。 每当在后台线程上调用对象模型时，都必须准备好处理此异常。 通常，这涉及到重试一段时间，然后显示对话框。 但是，也可以将后台线程创建为 STA，然后注册该线程的消息筛选器来处理这种情况。

## <a name="start-the-thread-correctly"></a>正确启动线程
 创建新的 STA 线程时，在启动线程之前将单元状态设置为 STA。 下面的代码示例演示如何执行此操作。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/ThisWorkbook.cs" id="Snippet5":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/ThisWorkbook.vb" id="Snippet5":::

 有关详细信息，请参阅 [托管线程处理最佳做法](/dotnet/standard/threading/managed-threading-best-practices)。

## <a name="modeless-forms"></a>无模式窗体
 无模式窗体允许在显示窗体时与应用程序进行某种类型的交互。 用户与窗体交互，窗体无需关闭即可与应用程序交互。 对象Office支持托管无模式窗体;但是，不应在后台线程上使用它们。

## <a name="see-also"></a>请参阅
- [线程处理 (C#)](/dotnet/csharp/programming-guide/concepts/threading/index)
- [线程处理 (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/threading/index)
- [使用线程和线程处理](/dotnet/standard/threading/using-threads-and-threading)
- [设计和创建Office解决方案](../vsto/designing-and-creating-office-solutions.md)
