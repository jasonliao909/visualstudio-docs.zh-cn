---
description: 获取文档的名称，格式为多个窗体中的一种。
title: IDebugDocument2：： GetName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocument2::GetName
helpviewer_keywords:
- IDebugDocument2::GetName
ms.assetid: 6f09ff09-b0cf-4472-8fc8-143991f0ceb1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 214bd95d1dec9917e89c9f3cf284599ca4115c78
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122096435"
---
# <a name="idebugdocument2getname"></a>IDebugDocument2::GetName
获取文档的名称，格式为多个窗体中的一种。

## <a name="syntax"></a>语法

```cpp
HRESULT GetName( 
   GETNAME_TYPE gnType,
   BSTR*        pbstrFileName
);
```

```csharp
int GetName( 
   enum_GETNAME_TYPE gnType,
   out string        pbstrFileName
);
```

## <a name="parameters"></a>参数
`gnType`\
中 [GETNAME_TYPE](../../../extensibility/debugger/reference/getname-type.md) 枚举中的一个值，该值确定要返回的名称的类型。

`pbstrFileName`\
弄返回一个包含文档名称的字符串。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 例如，此方法可以将文档名称作为标题返回，或以文件名或文件名称的一部分形式返回。

## <a name="see-also"></a>请参阅
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
- [GETNAME_TYPE](../../../extensibility/debugger/reference/getname-type.md)
