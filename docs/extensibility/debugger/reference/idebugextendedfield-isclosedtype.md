---
description: 确定字段是否表示闭合类型。
title: IDebugExtendedField：： IsClosedType |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IsClosedType
- IDebugExtendedField::IsClosedType
ms.assetid: 9136fc57-74ff-4fe4-a6e2-b137cb9d5b08
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 00cb69073f3e975d170578c8b026d40440341502
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122138427"
---
# <a name="idebugextendedfieldisclosedtype"></a>IDebugExtendedField::IsClosedType
确定字段是否表示闭合类型。

## <a name="syntax"></a>语法

```cpp
HRESULT IsClosedType(
   void
);
```

```csharp
int IsClosedType();
```

## <a name="return-value"></a>返回值
 如果该字段为关闭类型，则返回 `S_OK` ; 否则返回 `S_FALSE` 。

## <a name="see-also"></a>请参阅
- [IDebugExtendedField](../../../extensibility/debugger/reference/idebugextendedfield.md)
