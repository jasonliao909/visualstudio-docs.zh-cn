---
description: 获取线程的名称。
title: IDebugThread2：：GetName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::GetName
helpviewer_keywords:
- IDebugThread2::GetName
ms.assetid: eec54b8f-4a0e-4919-b0f9-81d4bd1e0b6f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6a7f3d867b48fea5ed32679b1584f60d88ceb1a5b2c7a6ece1cbadf1d1b48f50
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121338405"
---
# <a name="idebugthread2getname"></a>IDebugThread2::GetName
获取线程的名称。

## <a name="syntax"></a>语法

```cpp
HRESULT GetName ( 
   BSTR* pbstrName
);
```

```csharp
int GetName ( 
   out string pbstrName
);
```

## <a name="parameters"></a>参数
`pbstrName`\
[out]返回线程的名称。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 检索到的名称始终是可显示的名称，此名称描述线程。 线程名称可能派生自支持命名线程的运行时体系结构，或者可能是派生自调试引擎的名称。 或者，可以通过调用 [SetThreadName](../../../extensibility/debugger/reference/idebugthread2-setthreadname.md) 方法来设置线程的名称。

## <a name="see-also"></a>另请参阅
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [SetThreadName](../../../extensibility/debugger/reference/idebugthread2-setthreadname.md)
