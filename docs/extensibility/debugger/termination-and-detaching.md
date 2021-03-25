---
title: 终止和分离 |Microsoft Docs
description: 正常终止意味着正在调试的程序运行到完成，但没有断点、异常、运行时错误或无限循环。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- programs, termination events
- debug engines, detaching from programs
ms.assetid: 268c1e51-6363-45d1-964c-1ab99bdfa4f9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8662809b50dbfec3046af1d0d6b6fa151c3a33e0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057827"
---
# <a name="termination-and-detaching"></a>终止和分离
以下部分介绍了正常终止。

## <a name="discussion"></a>讨论 (Discussion)
 在 [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) 或 [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) 接口继续后，如果要调试的应用程序中没有断点、异常、运行时错误或无限循环，则正在调试的程序将运行到完成。 此过程是正常终止。

 必须发送 [IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) 以实现正常终止。 正常终止要求运行 [IDebugProgramDestroyEvent2：： GetExitCode](../../extensibility/debugger/reference/idebugprogramdestroyevent2-getexitcode.md) 方法。

## <a name="see-also"></a>另请参阅
- [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)
