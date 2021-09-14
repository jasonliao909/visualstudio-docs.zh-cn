---
title: 并行扩展插件.NET Framework |Microsoft Docs
description: 这些资源描述类的内部类型、方法和字段，这些类用于实现并行扩展的自定义调试.NET Framework。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debug engines, internals [.NET Framework]
ms.assetid: 93e07cfa-91fa-464c-b866-8bf5570411df
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 12588d5c9fb3957ce83202afa856a08436facb48
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664853"
---
# <a name="parallel-extension-internals-for-the-net-framework"></a>并行扩展插件的内部.NET Framework
本部分介绍类的内部类型、方法和字段，这些类型、方法和字段可帮助你为并行扩展插件实现.NET Framework。

## <a name="in-this-section"></a>本节内容
 [Task 类](../../extensibility/debugger/task-class-internal-members.md) 描述 类的内部数据 <xref:System.Threading.Tasks.Task?displayProperty=fullName> 成员。

 [TaskScheduler 类](../../extensibility/debugger/taskscheduler-class-internal-members.md) 描述 类的内部数据 <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName> 成员。

 [ContingentProperties 类](../../extensibility/debugger/contingentproperties-class-internal-members.md) 描述 类的内部数据 `System.Threading.Tasks.ContingentProperties` 成员。

 [AsyncTaskMethodBuilder 结构](../../extensibility/debugger/asynctaskmethodbuilder-structure-internal-members.md) 描述 结构的内部 <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder> 成员。

 [AsyncTaskMethodBuilder \<TResult> 结构](../../extensibility/debugger/asynctaskmethodbuilder-tresult-structure-internal-members.md) 描述结构的内部 <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601> 成员。

 [AsyncVoidMethodBuilder 结构](../../extensibility/debugger/asyncvoidmethodbuilder-structure-internal-members.md) 描述 结构的内部 <xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder> 成员。

## <a name="see-also"></a>另请参阅
- <xref:System.Threading.Tasks.Task?displayProperty=fullName>
- <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>
- [Visual Studio调试器扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
- [并行编程](/dotnet/standard/parallel-programming/index)
