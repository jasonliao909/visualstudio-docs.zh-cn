---
description: IDebugProgram2：：Execute 继续从已停止状态运行此程序。 任何以前的执行状态 (如步骤) 清除，程序将再次开始执行。
title: IDebugProgram2：：Execute |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Execute
helpviewer_keywords:
- IDebugProgram2::Execute
ms.assetid: f7205ce8-0ac6-4fcd-b6ec-b720b4fcaccf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e79fcde5a554abedc030861004b8117a54a2366a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122057442"
---
# <a name="idebugprogram2execute"></a>IDebugProgram2::Execute
继续从已停止状态运行此程序。 任何以前的执行状态 (如步骤) 清除，程序将再次开始执行。

> [!NOTE]
> 不推荐使用此方法。 请 [改为使用 Execute](../../../extensibility/debugger/reference/idebugprocess3-execute.md) 方法。

## <a name="syntax"></a>语法

```cpp
HRESULT Execute(
   void
);
```

```csharp
int Execute();
```

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 当用户从其他程序线程中的停止状态开始执行时，将对此程序调用此方法。 当用户从 IDE 的"调试"菜单中选择"开始"命令时，也会调用此方法。 此方法的实现可能与在程序中的当前线程上调用 [Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md) 方法一样简单。

> [!WARNING]
> 在处理此调用时，不要将停止事件 (同步) 事件发送到 Event; [](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)否则调试器可能会停止响应。

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [恢复](../../../extensibility/debugger/reference/idebugthread2-resume.md)
