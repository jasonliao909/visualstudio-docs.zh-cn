---
description: 指定表达式计算器中的对象的类型。
title: OBJECT_TYPE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- OBJECT_TYPE
helpviewer_keywords:
- OBJECT_TYPE enumeration
ms.assetid: c4d246f9-8a98-44ec-b2bb-ff5c684f668e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fa8720b86771cf2dfd0a46213ff493a3319c9a9a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122103086"
---
# <a name="object_type"></a>Object_Type
指定表达式计算器中的对象的类型。

## <a name="syntax"></a>语法

```cpp
enum enum_OBJECT_TYPE { 
   OBJECT_TYPE_BOOLEAN = 0x0,
   OBJECT_TYPE_CHAR    = 0x1,
   OBJECT_TYPE_I1      = 0x2,
   OBJECT_TYPE_U1      = 0x3,
   OBJECT_TYPE_I2      = 0x4,
   OBJECT_TYPE_U2      = 0x5,
   OBJECT_TYPE_I4      = 0x6,
   OBJECT_TYPE_U4      = 0x7,
   OBJECT_TYPE_I8      = 0x8,
   OBJECT_TYPE_U8      = 0x9,
   OBJECT_TYPE_R4      = 0xa,
   OBJECT_TYPE_R8      = 0xb,
   OBJECT_TYPE_OBJECT  = 0xc,
   OBJECT_TYPE_NULL    = 0xd,
   OBJECT_TYPE_CLASS   = 0xe
};
typedef DWORD OBJECT_TYPE;
```

```csharp
public enum enum_OBJECT_TYPE { 
   OBJECT_TYPE_BOOLEAN = 0x0,
   OBJECT_TYPE_CHAR    = 0x1,
   OBJECT_TYPE_I1      = 0x2,
   OBJECT_TYPE_U1      = 0x3,
   OBJECT_TYPE_I2      = 0x4,
   OBJECT_TYPE_U2      = 0x5,
   OBJECT_TYPE_I4      = 0x6,
   OBJECT_TYPE_U4      = 0x7,
   OBJECT_TYPE_I8      = 0x8,
   OBJECT_TYPE_U8      = 0x9,
   OBJECT_TYPE_R4      = 0xa,
   OBJECT_TYPE_R8      = 0xb,
   OBJECT_TYPE_OBJECT  = 0xc,
   OBJECT_TYPE_NULL    = 0xd,
   OBJECT_TYPE_CLASS   = 0xe
};
```

## <a name="fields"></a>字段
 `OBJECT_TYPE_BOOLEAN`\
 指示对象是布尔值。

 `OBJECT_TYPE_CHAR`\
 指示对象是字符。

 `OBJECT_TYPE_I1`\
 指示对象是一个单字节有符号整数。

 `OBJECT_TYPE_U1`\
 指示对象是一个单字节无符号整数。

 `OBJECT_TYPE_I2`\
 指示对象是一个双字节有符号整数。

 `OBJECT_TYPE_U2`\
 指示对象是一个双字节无符号整数。

 `OBJECT_TYPE_I4`\
 指示对象是一个四字节有符号整数。

 `OBJECT_TYPE_U4`\
 指示对象是一个四字节无符号整数。

 `OBJECT_TYPE_I8`\
 指示对象是一个八字节有符号整数。

 `OBJECT_TYPE_U8`\
 指示对象是一个八字节无符号整数。

 `OBJECT_TYPE_R4`\
 指示对象是一个四字节浮点数。

 `OBJECT_TYPE_R8`\
 指示对象是一个八字节浮点数。

 `OBJECT_TYPE_OBJECT`\
 指示对象是对象。

 `OBJECT_TYPE_NULL`\
 指示对象为 NULL。

 `OBJECT_TYPE_CLASS`\
 指示对象是类。

## <a name="remarks"></a>备注
 作为参数传递给 [CreatePrimitiveObject](../../../extensibility/debugger/reference/idebugfunctionobject-createprimitiveobject.md) 和 [CreateArrayObject](../../../extensibility/debugger/reference/idebugfunctionobject-createarrayobject.md) 方法。

## <a name="requirements"></a>要求
 标头：ee.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [CreatePrimitiveObject](../../../extensibility/debugger/reference/idebugfunctionobject-createprimitiveobject.md)
- [CreateArrayObject](../../../extensibility/debugger/reference/idebugfunctionobject-createarrayobject.md)
