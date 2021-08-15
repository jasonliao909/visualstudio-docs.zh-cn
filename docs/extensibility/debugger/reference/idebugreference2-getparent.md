---
description: 获取引用的父引用。
title: IDebugReference2：： GetParent |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::GetParent
helpviewer_keywords:
- IDebugReference2::GetParent
ms.assetid: e3061665-ad3e-4c1b-b33f-82755fa21be3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e5b73eb8d83b3a09b9eae5710d43585ad49758f4bcfa6f6c9b67bac6bfdab628
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121338574"
---
# <a name="idebugreference2getparent"></a>IDebugReference2::GetParent
获取引用的父引用。 保留供将来使用。

## <a name="syntax"></a>语法

```cpp
HRESULT GetParent ( 
   IDebugReference2** ppParent
);
```

```csharp
int GetParent ( 
   out IDebugReference2 ppParent
);
```

## <a name="parameters"></a>参数
`ppParent`\
弄返回一个 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) 对象，该对象表示此属性的父级。

## <a name="return-value"></a>返回值
 始终返回 `E_NOTIMPL`。

## <a name="see-also"></a>另请参阅
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
