---
description: 检索当前文档位置的范围。
title: IDebugDocumentPositionOffset2：： GetRange |Microsoft Docs
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
ms.openlocfilehash: 5a262287e6dc84316686f1132ed0ac496eee35e0
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122111237"
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
[in，out]范围起始位置的偏移量。 如果不需要此信息，请将此参数设置为 null 值。

`pdwEndOffset`\
[in，out]范围结束位置的偏移量。 如果不需要此信息，请将此参数设置为 null 值。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 调试引擎 (DE) 为某个位置断点指定的文档位置中指定的范围，以便向前搜索实际提供代码的语句。 例如，考虑以下代码：

```
Line 5: // comment
Line 6: x = 1;
```

 第5行对正在调试的程序不提供任何代码。 如果在第5行设置断点的调试器希望在第一行中向前搜索分配代码的时间，则调试器将指定一个范围，其中包含可正确放置断点的其他候选行。 然后，取消搜索这些行，直到找到可接受断点的行。

## <a name="see-also"></a>请参阅
- [IDebugDocumentPositionOffset2](../../../extensibility/debugger/reference/idebugdocumentpositionoffset2.md)
- [GetRange](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md)
