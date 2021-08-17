---
description: 将此文档上下文与给定的文档上下文数组进行比较。
title: IDebugDocumentContext2：： Compare |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::Compare
helpviewer_keywords:
- IDebugDocumentContext2::Compare
ms.assetid: 2327b1ba-52d0-42fb-a01e-63cb4b332d2f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 320dd75e43f9c2fd9cfc7b81cba4e6f89407acf6e61d36edbc018f7c3e9e8278
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121292684"
---
# <a name="idebugdocumentcontext2compare"></a>IDebugDocumentContext2::Compare
将此文档上下文与给定的文档上下文数组进行比较。

## <a name="syntax"></a>语法

```cpp
HRESULT Compare( 
   DOCCONTEXT_COMPARE       compare,
   IDebugDocumentContext2** rgpDocContextSet,
   DWORD                    dwDocContextSetLen,
   DWORD*                   pdwDocContext
);
```

```csharp
int Compare( 
   enum_ DOCCONTEXT_COMPARE compare,
   IDebugDocumentContext2[] rgpDocContextSet,
   uint                     dwDocContextSetLen,
   out uint                 pdwDocContext
);
```

## <a name="parameters"></a>参数
`compare`\
中 [DOCCONTEXT_COMPARE](../../../extensibility/debugger/reference/doccontext-compare.md) 枚举中的一个值，该值指定比较的类型。

`rgpDocContextSet`\
中 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) 对象的数组，这些对象表示要进行比较的文档上下文。

`dwDocContextSetLen`\
中要比较的文档上下文数组的长度。

`pdwDocContext`\
弄将索引返回到 `rgpDocContextSet` 满足比较的第一个文档上下文的数组中。

## <a name="return-value"></a>返回值
 `S_OK`如果找到匹配项，则返回。 `S_FALSE`如果未找到匹配项，则返回。 否则，返回错误代码。

## <a name="remarks"></a>备注
 在数组中传递的 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) 对象必须由实现在其上调用的对象的相同调试引擎实现 `IDebugDocumentContext2` ; 否则，比较无效。

## <a name="see-also"></a>请参阅
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [DOCCONTEXT_COMPARE](../../../extensibility/debugger/reference/doccontext-compare.md)
