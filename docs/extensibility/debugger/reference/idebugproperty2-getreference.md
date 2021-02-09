---
title: IDebugProperty2：： GetReference |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetReference
helpviewer_keywords:
- IDebugProperty2::GetReference method
ms.assetid: 2fa97d9b-c3d7-478e-ba5a-a933f40a0103
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 270a8cc755318578f680e4266ca01e35dee20bb9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99850889"
---
# <a name="idebugproperty2getreference"></a>IDebugProperty2::GetReference
返回对该属性值的引用。

## <a name="syntax"></a>语法

```cpp
HRESULT GetReference(
   IDebugReference2** ppReference
);
```

```csharp
int GetReference(
   out IDebugReference2 ppReference
);
```

## <a name="parameters"></a>parameters
`ppRererence`\
弄返回一个 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) 对象，该对象表示对属性值的引用。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码，通常为 `E_NOTIMPL` 或 `E_GETREFERENCE_NO_REFERENCE` 。

## <a name="see-also"></a>另请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
