---
description: 此方法使程序可用于 (DEs) 和会话调试管理器的调试引擎。
title: IDebugProgramPublisher2：:P ublishProgram |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramPublisher2::PublishProgram
helpviewer_keywords:
- IDebugProgramPublisher2::PublishProgram
ms.assetid: 92ff63f0-e869-4040-b3ae-b2c899e708ff
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 167514d361ee3119d63682f3edf37b7ae0db193a4bd1db00c596057f9ca26419
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121449139"
---
# <a name="idebugprogrampublisher2publishprogram"></a>IDebugProgramPublisher2::PublishProgram
此方法使程序可用于 (DEs) 和会话调试管理器的调试引擎。

## <a name="syntax"></a>语法

```cpp
HRESULT PublishProgram(
   CONST_GUID_ARRAY Engines,
   LPCOLESTR        szFriendlyName,
   IUnknown*        pDebuggeeInterface
);
```

```csharp
int PublishProgram(
   CONST_GUID_ARRAY Engines,
   string           szFriendlyName,
   object           pDebuggeeInterface
);
```

## <a name="parameters"></a>参数
`Engines`\
中可以启动或附加到此程序的 DEs Guid 数组。

`szFriendlyName`\
中程序 (的友好名称显示在显示给用户) 的菜单或对话框中。

`pDebuggeeInterface`\
[in] `IUnknown` 程序的接口 (此值用作唯一标识程序的 cookie;此相同的值用于 "取消发布" 程序) 

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 若要使程序不再可用于调试，请调用 [UnpublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogram.md)。

## <a name="see-also"></a>另请参阅
- [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)
- [UnpublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogram.md)
