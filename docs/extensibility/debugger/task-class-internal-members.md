---
title: 任务类 - 内部成员|Microsoft Docs
description: 了解 System.Threading.Tasks.Task 类的内部成员，这些成员可帮助你实现自定义调试器。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debug engines, Task class [.NET Framework]
- Task class [.NET Framework debug engines]
ms.assetid: 28e47c3b-9323-424a-80ac-6cc3bf19e09b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: c552a4069af343ea45721edc9abb841526124163
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122095161"
---
# <a name="task-class---internal-members"></a>任务类 - 内部成员
本文介绍 类的内部成员 <xref:System.Threading.Tasks.Task?displayProperty=fullName> ，这些成员可帮助你实现自定义调试器。 有关此类的一般信息，请参阅 <xref:System.Threading.Tasks.Task> 参考文章。

 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集：mscorlib** (*mscorlib.dll*) 

 由于无法从 CIL 访问这些内部成员，因此.NET Framework CIL 语言语言 (语法) 。

## <a name="syntax"></a>语法

```csharp
.class public auto ansi System.Threading.Tasks.Task
       extends System.Object
       implements System.Threading.IThreadPoolWorkItem,
                  System.IAsyncResult,
                  System.IDisposable,
                  System.Threading.ICancelableOperation
```

## <a name="members"></a>成员

### <a name="methods"></a>方法

|名称|说明|
|----------|-----------------|
|[SetNotificationForWaitCompletion 方法](../../extensibility/debugger/setnotificationforwaitcompletion-method.md)|设置或清除TASK_STATE_WAIT_COMPLETION_NOTIFICATION位。|
|[NotifyDebuggerOfWaitCompletion 方法](../../extensibility/debugger/notifydebuggerofwaitcompletion-method.md)|调试器用作断点目标的占位符方法。|

### <a name="fields"></a>字段

|名称|说明|
|----------|-----------------|
|[m_action](../../extensibility/debugger/m-action-field.md)|表示在 对象中执行的代码的 <xref:System.Threading.Tasks.Task> 委托。|
|[m_contingentProperties](../../extensibility/debugger/m-contingentproperties-field.md)|存储 对象的其他 <xref:System.Threading.Tasks.Task> 属性。|
|[m_parent](../../extensibility/debugger/m-parent-field.md)|父属性的支持 <xref:System.Threading.Tasks.Task?displayProperty=fullName> 字段。|
|[m_stateFlags](../../extensibility/debugger/m-stateflags-field.md)|存储有关对象的当前状态 <xref:System.Threading.Tasks.Task> 的信息。|
|[m_stateObject](../../extensibility/debugger/m-stateobject-field.md)|一个 对象，该对象表示操作将使用的数据。|
|[m_taskId](../../extensibility/debugger/m-taskid-field.md)|属性的支持 <xref:System.Threading.Tasks.Task.Id%2A?displayProperty=fullName> 字段。|
|[s_taskIdCounter](../../extensibility/debugger/s-taskidcounter-field.md)|对象的下一个可用 <xref:System.Threading.Tasks.Task> 标识符。|
|[TASK_STATE_CANCELED](../../extensibility/debugger/task-state-canceled-field.md)|指示任务在达到运行状态之前已取消，或者任务已确认其取消并完成且没有异常。|
|[TASK_STATE_EXECUTED](../../extensibility/debugger/task-state-executed-field.md)|指示任务正在运行。|
|[TASK_STATE_FAULTED](../../extensibility/debugger/task-state-faulted-field.md)|指示任务由于未处理异常而完成。|
|[TASK_STATE_RAN_TO_COMPLETION](../../extensibility/debugger/task-state-ran-to-completion-field.md)|指示任务已成功完成执行。|
|[TASK_STATE_WAITING_ON_CHILDREN](../../extensibility/debugger/task-state-waiting-on-children-field.md)|指示任务已完成执行其委托，并隐式等待附加的子任务完成。|

## <a name="remarks"></a>备注
 以下内部方法对调试器引擎很有用，因为它们将进入代码 <xref:System.Threading.Tasks.Task> 执行标记：

- `Execute`

- `ExecuteEntry`

- `ExecuteWithThreadLocal`

- `Finish`

- `InnerInvoke`

- `InternalWait`

## <a name="see-also"></a>请参阅
- <xref:System.Threading.Tasks.Task?displayProperty=fullName>
- [并行扩展插件的内部.NET Framework](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
