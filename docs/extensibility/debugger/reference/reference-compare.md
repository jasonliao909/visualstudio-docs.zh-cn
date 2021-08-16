---
description: 指定引用的比较类型。
title: REFERENCE_COMPARE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- REFERENCE_COMPARE
helpviewer_keywords:
- REFERENCE_COMPARE enumeration
ms.assetid: e31cdc78-f621-498b-9ca4-aefa790b9f6f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4db5f1189340e93799fc83bfb9f38e7ac1aa92c5222de6da78e27d2aa487c7cf
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121276160"
---
# <a name="reference_compare"></a>REFERENCE_COMPARE
指定引用的比较类型。

## <a name="syntax"></a>语法

```cpp
enum enum_REFERENCE_COMPARE { 
   REF_COMPARE_EQUAL        = 0x0001,
   REF_COMPARE_LESS_THAN    = 0x0002,
   REF_COMPARE_GREATER_THAN = 0x0003
};
typedef DWORD REFERENCE_COMPARE;
```

```csharp
public enum enum_REFERENCE_COMPARE { 
   REF_COMPARE_EQUAL        = 0x0001,
   REF_COMPARE_LESS_THAN    = 0x0002,
   REF_COMPARE_GREATER_THAN = 0x0003
};
```

## <a name="fields"></a>字段
 `REF_COMPARE_EQUAL`\
 指定一个等于比较。

 `REF_COMPARE_LESS_THAN`\
 指定小于比较。

 `REF_COMPARE_GREATER_THAN`\
 指定大于比较。

## <a name="remarks"></a>备注
 作为参数传递给 [Compare](../../../extensibility/debugger/reference/idebugreference2-compare.md) 方法。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [比较](../../../extensibility/debugger/reference/idebugreference2-compare.md)
