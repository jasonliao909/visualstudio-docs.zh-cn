---
description: 返回对 属性的值的引用。
title: IDebugProperty2：：GetReference |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetReference
helpviewer_keywords:
- IDebugProperty2::GetReference method
ms.assetid: 2fa97d9b-c3d7-478e-ba5a-a933f40a0103
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: be8e0b73ec8fe11a5fc5ad2eff5c1f38b2511d4a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122159589"
---
# <a name="idebugproperty2getreference"></a>IDebugProperty2::GetReference
返回对 属性的值的引用。

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

## <a name="parameters"></a>参数
`ppRererence`\
[out]返回 [一个 IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) 对象，该对象表示对 属性值的引用。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码，通常为 `E_NOTIMPL` 或 `E_GETREFERENCE_NO_REFERENCE` 。

## <a name="see-also"></a>请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
