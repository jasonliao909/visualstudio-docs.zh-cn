---
title: .NET Framework 的并行扩展内部机制 |Microsoft Docs
description: 这些资源描述了类的内部类型、方法和字段，这些类用于实现到 .NET Framework 并行扩展的自定义调试器。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, internals [.NET Framework]
ms.assetid: 93e07cfa-91fa-464c-b866-8bf5570411df
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b3c17c36112d383528e97c1eb04c858b89406c36
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99900317"
---
# <a name="parallel-extension-internals-for-the-net-framework"></a>.NET Framework 的并行扩展内部机制
本节介绍类的内部类型、方法和字段，这些类可帮助您为 .NET Framework 的并行扩展实现自定义调试器。

## <a name="in-this-section"></a>本节内容
 [Task 类](../../extensibility/debugger/task-class-internal-members.md) 描述类的内部数据成员 <xref:System.Threading.Tasks.Task?displayProperty=fullName> 。

 [TaskScheduler 类](../../extensibility/debugger/taskscheduler-class-internal-members.md) 描述类的内部数据成员 <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName> 。

 [ContingentProperties 类](../../extensibility/debugger/contingentproperties-class-internal-members.md) 描述类的内部数据成员 `System.Threading.Tasks.ContingentProperties` 。

 [AsyncTaskMethodBuilder 结构](../../extensibility/debugger/asynctaskmethodbuilder-structure-internal-members.md) 描述结构的内部成员 <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder> 。

 [AsyncTaskMethodBuilder \<TResult> 结构](../../extensibility/debugger/asynctaskmethodbuilder-tresult-structure-internal-members.md) 描述了结构的内部成员 <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601> 。

 [AsyncVoidMethodBuilder 结构](../../extensibility/debugger/asyncvoidmethodbuilder-structure-internal-members.md) 描述结构的内部成员 <xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder> 。

## <a name="see-also"></a>另请参阅
- <xref:System.Threading.Tasks.Task?displayProperty=fullName>
- <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>
- [Visual Studio 调试器扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
- [并行编程](/dotnet/standard/parallel-programming/index)
