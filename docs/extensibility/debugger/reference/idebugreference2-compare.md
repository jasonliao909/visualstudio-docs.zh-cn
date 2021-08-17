---
description: 将一个引用与另一个引用进行比较。
title: IDebugReference2：：Compare |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::Compare
helpviewer_keywords:
- IDebugReference2::Compare
ms.assetid: 3361c495-2673-4b7c-82e3-dee74e1fa58d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e56b2d5883e1c26fbfaa8657b8fed3c5236db348
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122087556"
---
# <a name="idebugreference2compare"></a>IDebugReference2::Compare
将一个引用与另一个引用进行比较。 保留供将来使用。

## <a name="syntax"></a>语法

```cpp
HRESULT Compare ( 
   REFERENCE_COMPARE dwCompare,
   IDebugReference2* pReference
);
```

```csharp
int Compare ( 
   enum_REFERENCE_COMPARE dwCompare,
   IDebugReference2       pReference
);
```

## <a name="parameters"></a>参数
`dwCompare`\
[in]指定比较 [REFERENCE_COMPARE（](../../../extensibility/debugger/reference/reference-compare.md) 例如，等于、小于或大于）的枚举中的值。

`pReference`\
[in]表示 [要比较的引用的 IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) 对象。

## <a name="return-value"></a>返回值
 始终返回 `E_NOTIMPL`。

## <a name="see-also"></a>请参阅
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [REFERENCE_COMPARE](../../../extensibility/debugger/reference/reference-compare.md)
