---
description: 检索端口供应商的说明和说明元数据。
title: IDebugPortSupplierDescription2：：GetDescription |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortSupplierDescription2::GetDescription
ms.assetid: bff5f536-1cd1-4313-8856-db7b05818305
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e83c0232087edf417435cfaf03f9a832d5d0b4d0f4f5f1193aa56c3bda963d6e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121416711"
---
# <a name="idebugportsupplierdescription2getdescription"></a>IDebugPortSupplierDescription2::GetDescription
检索端口供应商的说明和说明元数据。

## <a name="syntax"></a>语法

```cpp
HRESULT GetDescription(
   PORT_SUPPLIER_DESCRIPTION_FLAGS *pdwFlags,
   BSTR *pbstrText
);
```

```csharp
public int GetDescription(
   out enum_PORT_SUPPLIER_DESCRIPTION_FLAGS pdwFlags,
   out string pbstrText
);
```

## <a name="parameters"></a>参数
`pdwFlags`\
[out]说明的元数据标志。

`pbstrText`\
[out]端口供应商的说明。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugPortSupplierDescription2](../../../extensibility/debugger/reference/idebugportsupplierdescription2.md)
