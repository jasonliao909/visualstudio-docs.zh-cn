---
title: 自动功能挂起
ms.date: 11/04/2016
description: 了解 Visual Studio 如何减少分析范围，关闭垃圾回收低延迟模式，以及在系统内存受到限制时刷新缓存。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- live code analysis
- background analysis
- analysis scope
- full solution analysis
- performance
- low-memory
ms.assetid: 572c15aa-1fd0-468c-b6be-9fa50e170914
author: Mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: 0a1791f02264a4e6a32976ef8975375196054b2a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602102"
---
# <a name="automatic-feature-suspension"></a>自动功能挂起

如果可用系统内存降至 200 MB 或更低，则 Visual Studio 在代码编辑器中显示以下消息：

![挂起完整解决方案分析的警报文本](../code-quality/media/fsa_alert.png)

当 Visual Studio 检测到内存不足的情况时，它会自动挂起某些高级功能，以帮助其保持稳定。 Visual Studio 继续像过去一样运行，但其性能会下降。

在内存不足的情况下，将执行以下操作：

- Visual C# 和 Visual Basic 的实时代码分析减少到最小范围。

- Visual C# 和 Visual Basic 的[垃圾回收](/dotnet/standard/garbage-collection/index) (GC) 低延迟模式已禁用。

- Visual Studio 缓存已刷新。

## <a name="improve-visual-studio-performance"></a>提高 Visual Studio 性能

有关如何在处理大型解决方案或内存不足的情况时提高 Visual Studio 性能的提示和技巧，请参阅[大型解决方案的性能注意事项](https://github.com/dotnet/roslyn/blob/master/docs/wiki/Performance-considerations-for-large-solutions.md)。

## <a name="live-code-analysis-is-reduced-to-minimal-scope"></a>实时代码分析减少到最小范围

默认情况下，对打开的文档和项目执行实时代码分析。 可以自定义此分析范围，使其减少到当前文档或增加到整个解决方案。 有关详细信息，请参阅[如何：配置托管代码的实时代码分析范围](./configure-live-code-analysis-scope-managed-code.md)。 在内存不足的情况下，Visual Studio 将实时分析范围强制减少到当前文档。 但是，可以通过在出现信息栏中的“重新启用”按钮时选择它或重新启动 Visual Studio 来重新启用首选分析范围。 “选项”对话框始终显示当前实时代码分析范围设置。

## <a name="gc-low-latency-disabled"></a>GC 低延迟已禁用

若要重新启用 GC 低延迟模式，请重新启动 Visual Studio。 默认情况下，Visual Studio 会在键入时启用 GC 低延迟模式，以确保键入内容不会阻止任何 GC 操作。 但是，如果内存不足的情况导致 Visual Studio 显示自动挂起警告，则会为该会话禁用 GC 低延迟模式。 重新启动 Visual Studio 会重新启用默认 GC 行为。 有关详细信息，请参阅 <xref:System.Runtime.GCLatencyMode>。

## <a name="visual-studio-caches-flushed"></a>Visual Studio 缓存已刷新

如果继续你的当前开发会话或重新启动 Visual Studio，则所有 Visual Studio 缓存都会立即清空，但会开始重新填充。 已刷新的缓存包括以下功能的缓存：

- 查找所有引用

- 定位到

- 添加 Using

此外，还会清除用于内部 Visual Studio 操作的缓存。

> [!NOTE]
> 自动功能挂起警告只会在每个解决方案的基础上出现一次，而不会在每个会话的基础上出现。 这意味着，如果从 Visual Basic 切换到 Visual C#（反之亦然）并遇到另一个内存不足的情况，则可能会出现另一个自动功能挂起警告。

## <a name="see-also"></a>另请参阅

- [如何：配置托管代码的实时代码分析范围](./configure-live-code-analysis-scope-managed-code.md)
- [垃圾回收基础](/dotnet/standard/garbage-collection/fundamentals)
- [大型解决方案的性能注意事项](https://github.com/dotnet/roslyn/blob/master/docs/wiki/Performance-considerations-for-large-solutions.md)
