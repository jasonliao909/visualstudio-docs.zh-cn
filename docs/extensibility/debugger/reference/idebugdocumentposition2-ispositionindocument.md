---
description: 确定文档位置是否包含在给定文档中。
title: IDebugDocumentPosition2：：IsPositionInDocument |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentPosition2::IsPositionInDocument
helpviewer_keywords:
- IDebugDocumentPosition2::IsPositionInDocument
ms.assetid: d5cf57cb-b93b-4e1d-bec9-185f4fe8668d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 849b6989f4e777e00d262019bb5fc5159e55a80fa2b4cc037e70e9eaffe9bd82
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121342279"
---
# <a name="idebugdocumentposition2ispositionindocument"></a>IDebugDocumentPosition2::IsPositionInDocument
确定文档位置是否包含在给定文档中。

## <a name="syntax"></a>语法

```cpp
HRESULT IsPositionInDocument( 
   IDebugDocument2* pDoc
);
```

```csharp
int IsPositionInDocument( 
   IDebugDocument2 pDoc
);
```

## <a name="parameters"></a>参数
`pDoc`\
[in]表示 [包含文档候选项的 IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 此方法主要用于在 [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) 接口中设置断点。 加载文档时，将调用断点位置以确定文档是否包含此位置。

## <a name="see-also"></a>另请参阅
- [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
