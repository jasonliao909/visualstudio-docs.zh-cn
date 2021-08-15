---
description: 检索当前文档位置的范围。
title: IDebugDocumentPositionOffset2：：GetRange |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentPositionOffset2::GetRange
ms.assetid: 27da7130-0932-4f97-abde-05e6fb018606
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1f62d00ef9abb422132da27c0f7eb2112477d79ca8b4939c5dd10ceb6344de39
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121261991"
---
# <a name="idebugdocumentpositionoffset2getrange"></a>IDebugDocumentPositionOffset2::GetRange
检索当前文档位置的范围。

## <a name="syntax"></a>语法

```cpp
HRESULT GetRange(
   DWORD* pdwBegOffset,
   DWORD* pdwEndOffset
);
```

```csharp
public int GetRange(
   ref uint pdwBegOffset,
   ref uint pdwEndOffset
);
```

## <a name="parameters"></a>参数
`pdwBegOffset`\
[in， out]范围的起始位置的偏移量。 如果不需要此信息，则此参数设置为 null 值。

`pdwEndOffset`\
[in， out]范围的结束位置的偏移量。 如果不需要此信息，则此参数设置为 null 值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 在文档位置中为位置断点指定的范围由调试引擎 (DE) 用于提前搜索实际提供代码的语句。 例如，考虑以下代码：

```
Line 5: // comment
Line 6: x = 1;
```

 第 5 行不向正在调试的程序提供代码。 如果第 5 行上设置断点的调试器希望 DE 为提供代码的第一行向前搜索一定数量的内容，则调试器将指定一个范围，其中包含可能正确放置断点的其他候选行。 然后，DE 会向前搜索这些行，直到找到可以接受断点的行。

## <a name="see-also"></a>另请参阅
- [IDebugDocumentPositionOffset2](../../../extensibility/debugger/reference/idebugdocumentpositionoffset2.md)
- [GetRange](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md)
