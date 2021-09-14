---
title: 终止和分离|Microsoft Docs
description: 正常终止意味着正在调试的程序在运行到完成时没有断点、异常、运行时错误或无限循环。
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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 40a559a110792e5c010d37164ab1db96277ca544
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600808"
---
# <a name="termination-and-detaching"></a>终止和分离
以下部分介绍正常终止。

## <a name="discussion"></a>讨论 (Discussion)
 在 [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) 或 [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) 接口继续后，如果应用程序中没有要调试的断点、异常、运行时错误或无限循环，则正在调试的程序将运行到完成。 此过程是正常终止。

 必须发送 [IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) 来实现正常终止。 正常终止需要运行 [IDebugProgramDestroyEvent2：：GetExitCode](../../extensibility/debugger/reference/idebugprogramdestroyevent2-getexitcode.md) 方法。

## <a name="see-also"></a>另请参阅
- [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)
