---
description: 介绍 IDebugProperty2 或 IDebugReference2 接口的各种属性。
title: DBG_ATTRIB_FLAGS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DBG_ATTRIB_FLAGS
helpviewer_keywords:
- DBGPROP_ATTRIB_FLAGS enumerations
ms.assetid: 2f13e601-dadc-476e-a8ec-01c4515082e7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7cf9ae3908b2edf6fbaf65c5e67ff428eb999afe
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122065119"
---
# <a name="dbg_attrib_flags"></a>DBG_ATTRIB_FLAGS
介绍 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 或 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) 接口的各种属性。 结构 [DEBUG_PROPERTY_INFO成员](../../../extensibility/debugger/reference/debug-property-info.md) 。

## <a name="syntax"></a>语法

```cpp
#define DBG_ATTRIB_NONE                 0x0000000000000000,
#define DBG_ATTRIB_ALL                  0x00000000ffffffff,

// Attributes about the object itself

#define DBG_ATTRIB_OBJ_IS_EXPANDABLE    0x0000000000000001,
#define DBG_ATTRIB_OBJ_HAS_ID           0x0000000000000002,
#define DBG_ATTRIB_OBJ_CAN_HAVE_ID      0x0000000000000004,

// Attributes about the value of the object

#define DBG_ATTRIB_VALUE_READONLY       0x0000000000000010,
#define DBG_ATTRIB_VALUE_ERROR          0x0000000000000020,
#define DBG_ATTRIB_VALUE_SIDE_EFFECT    0x0000000000000040,
#define DBG_ATTRIB_OVERLOADED_CONTAINER 0x0000000000000080,
#define DBG_ATTRIB_VALUE_BOOLEAN        0x0000000000000100,
#define DBG_ATTRIB_VALUE_BOOLEAN_TRUE   0x0000000000000200,
#define DBG_ATTRIB_VALUE_INVALID        0x0000000000000400,
#define DBG_ATTRIB_VALUE_NAT            0x0000000000000800,
#define DBG_ATTRIB_VALUE_AUTOEXPANDED   0x0000000000001000,
#define DBG_ATTRIB_VALUE_TIMEOUT        0x0000000000002000,
#define DBG_ATTRIB_VALUE_RAW_STRING     0x0000000000004000,
#define DBG_ATTRIB_VALUE_CUSTOM_VIEWER  0x0000000000008000,

// Attributes about field access types for the object

#define DBG_ATTRIB_ACCESS_NONE          0x0000000000010000,
#define DBG_ATTRIB_ACCESS_PUBLIC        0x0000000000020000,
#define DBG_ATTRIB_ACCESS_PRIVATE       0x0000000000040000,
#define DBG_ATTRIB_ACCESS_PROTECTED     0x0000000000080000,
#define DBG_ATTRIB_ACCESS_FINAL         0x0000000000100000,
#define DBG_ATTRIB_ACCESS_ALL           0x00000000001f0000,

// Attributes for the storage types of the object

#define DBG_ATTRIB_STORAGE_NONE         0x0000000001000000,
#define DBG_ATTRIB_STORAGE_GLOBAL       0x0000000002000000,
#define DBG_ATTRIB_STORAGE_STATIC       0x0000000004000000,
#define DBG_ATTRIB_STORAGE_REGISTER     0x0000000008000000,
#define DBG_ATTRIB_STORAGE_ALL          0x000000000f000000,

// Attributes for the type modifiers on the object

#define DBG_ATTRIB_TYPE_NONE            0x0000000100000000,
#define DBG_ATTRIB_TYPE_VIRTUAL         0x0000000200000000,
#define DBG_ATTRIB_TYPE_CONSTANT        0x0000000400000000,
#define DBG_ATTRIB_TYPE_SYNCHRONIZED    0x0000000800000000,
#define DBG_ATTRIB_TYPE_VOLATILE        0x0000001000000000,
#define DBG_ATTRIB_TYPE_ALL             0x0000001f00000000,

// Attributes that describe the type of object

#define DBG_ATTRIB_DATA                 0x0000010000000000,
#define DBG_ATTRIB_METHOD               0x0000020000000000,
#define DBG_ATTRIB_PROPERTY             0x0000040000000000,
#define DBG_ATTRIB_CLASS                0x0000080000000000,
#define DBG_ATTRIB_BASECLASS            0x0000100000000000,
#define DBG_ATTRIB_INTERFACE            0x0000200000000000,
#define DBG_ATTRIB_INNERCLASS           0x0000400000000000,
#define DBG_ATTRIB_MOSTDERIVED          0x0000800000000000,
#define DBG_ATTRIB_CHILD_ALL            0x0000ff0000000000,

// Miscellaneous attributes

#define DBG_ATTRIB_MULTI_CUSTOM_VIEWERS 0x0001000000000000

typedef UINT64 DBG_ATTRIB_FLAGS;
```

```csharp
public const int DBG_ATTRIB_NONE                 = 0x0000000000000000,
public const int DBG_ATTRIB_ALL                  = 0x00000000ffffffff,

// Attributes about the object itself

public const int DBG_ATTRIB_OBJ_IS_EXPANDABLE    = 0x0000000000000001,
public const int DBG_ATTRIB_OBJ_HAS_ID           = 0x0000000000000002,
public const int DBG_ATTRIB_OBJ_CAN_HAVE_ID      = 0x0000000000000004,

// Attributes about the value of the object

public const int DBG_ATTRIB_VALUE_READONLY       = 0x0000000000000010,
public const int DBG_ATTRIB_VALUE_ERROR          = 0x0000000000000020,
public const int DBG_ATTRIB_VALUE_SIDE_EFFECT    = 0x0000000000000040,
public const int DBG_ATTRIB_OVERLOADED_CONTAINER = 0x0000000000000080,
public const int DBG_ATTRIB_VALUE_BOOLEAN        = 0x0000000000000100,
public const int DBG_ATTRIB_VALUE_BOOLEAN_TRUE   = 0x0000000000000200,
public const int DBG_ATTRIB_VALUE_INVALID        = 0x0000000000000400,
public const int DBG_ATTRIB_VALUE_NAT            = 0x0000000000000800,
public const int DBG_ATTRIB_VALUE_AUTOEXPANDED   = 0x0000000000001000,
public const int DBG_ATTRIB_VALUE_TIMEOUT        = 0x0000000000002000,
public const int DBG_ATTRIB_VALUE_RAW_STRING     = 0x0000000000004000,
public const int DBG_ATTRIB_VALUE_CUSTOM_VIEWER  = 0x0000000000008000,

// Attributes about field access types for the object

public const int DBG_ATTRIB_ACCESS_NONE          = 0x0000000000010000,
public const int DBG_ATTRIB_ACCESS_PUBLIC        = 0x0000000000020000,
public const int DBG_ATTRIB_ACCESS_PRIVATE       = 0x0000000000040000,
public const int DBG_ATTRIB_ACCESS_PROTECTED     = 0x0000000000080000,
public const int DBG_ATTRIB_ACCESS_FINAL         = 0x0000000000100000,
public const int DBG_ATTRIB_ACCESS_ALL           = 0x00000000001f0000,

// Attributes for the storage types of the object

public const int DBG_ATTRIB_STORAGE_NONE         = 0x0000000001000000,
public const int DBG_ATTRIB_STORAGE_GLOBAL       = 0x0000000002000000,
public const int DBG_ATTRIB_STORAGE_STATIC       = 0x0000000004000000,
public const int DBG_ATTRIB_STORAGE_REGISTER     = 0x0000000008000000,
public const int DBG_ATTRIB_STORAGE_ALL          = 0x000000000f000000,

// Attributes for the type modifiers on the object

public const int DBG_ATTRIB_TYPE_NONE            = 0x0000000100000000,
public const int DBG_ATTRIB_TYPE_VIRTUAL         = 0x0000000200000000,
public const int DBG_ATTRIB_TYPE_CONSTANT        = 0x0000000400000000,
public const int DBG_ATTRIB_TYPE_SYNCHRONIZED    = 0x0000000800000000,
public const int DBG_ATTRIB_TYPE_VOLATILE        = 0x0000001000000000,
public const int DBG_ATTRIB_TYPE_ALL             = 0x0000001f00000000,

// Attributes that describe the type of object

public const int DBG_ATTRIB_DATA                 = 0x0000010000000000,
public const int DBG_ATTRIB_METHOD               = 0x0000020000000000,
public const int DBG_ATTRIB_PROPERTY             = 0x0000040000000000,
public const int DBG_ATTRIB_CLASS                = 0x0000080000000000,
public const int DBG_ATTRIB_BASECLASS            = 0x0000100000000000,
public const int DBG_ATTRIB_INTERFACE            = 0x0000200000000000,
public const int DBG_ATTRIB_INNERCLASS           = 0x0000400000000000,
public const int DBG_ATTRIB_MOSTDERIVED          = 0x0000800000000000,
public const int DBG_ATTRIB_CHILD_ALL            = 0x0000ff0000000000,

// Miscellaneous attributes

public const int DBG_ATTRIB_MULTI_CUSTOM_VIEWERS = 0x0001000000000000
```

## <a name="members"></a>成员
 `DBG_ATTRIB_NONE`\
 表示没有特性。

 `DBG_ATTRIB_ALL`\
 指示所有属性。

 `DBG_ATTRIB_OBJ_IS_EXPANDABLE`\
 表示引用或属性具有子级。

 `DBG_ATTRIB_OBJ_HAS_ID`\
 指示已创建此对象的 ID。

 `DBG_ATTRIB_OBJ_CAN_HAVE_ID`\
 指示可创建此对象的 ID。

 `DBG_ATTRIB_VALUE_READONLY`\
 表示值是只读的。

 `DBG_ATTRIB_VALUE_ERROR`\
 指示该值为错误。

 `DBG_ATTRIB_VALUE_SIDE_EFFECT`\
 指示评估有副作用。

 `DBG_ATTRIB_OVERLOADED_CONTAINER`\
 指示此属性确实是重载的容器。

 `DBG_ATTRIB_VALUE_BOOLEAN`\
 指示 中的值为 `DEBUG_PROPERTY_INFO::bstrValue` 布尔值。

 `DBG_ATTRIB_VALUE_BOOLEAN_TRUE`\
 指示 中的值为 `DEBUG_PROPERTY_INFO::bstrValue` 布尔值和 `TRUE` 。

 `DBG_ATTRIB_VALUE_INVALID`\
 表示 `DEBUG_PROPERTY_INFO::bstrValue` 中的值无效。

 `DBG_ATTRIB_VALUE_NAT`\
 指示 中的值为 `DEBUG_PROPERTY_INFO::bstrValue` NAT *("* 不是) 。 NAT 描述 Intel 64 位处理器中指示延迟推理异常的寄存器标志。

 `DBG_ATTRIB_VALUE_AUTOEXPANDED`\
 指示 中的值 `DEBUG_PROPERTY_INFO::bstrValue` 可能已自动展开。

 `DBG_ATTRIB_VALUE_TIMEOUT`\
 指示评估已过时。

 `DBG_ATTRIB_VALUE_RAW_STRING`\
 指示 中的值 `DEBUG_PROPERTY_INFO::bstrValue` 可以通过原始字符串表示。

 `DBG_ATTRIB_VALUE_CUSTOM_VIEWER`\
 指示此属性至少有一个与之关联的自定义查看器。

 `DBG_ATTRIB_ACCESS_NONE`\
 指示一个对象，该对象既不 `public` 具有 、 `private` ，也不 `protected` 具有类型访问权限。

 `DBG_ATTRIB_ACCESS_PUBLIC`\
 表示对象具有公共访问。

 `DBG_ATTRIB_ACCESS_PRIVATE`\
 表示对象具有私有访问。

 `DBG_ATTRIB_ACCESS_PROTECTED`\
 表示对象具有受保护的访问。

 `DBG_ATTRIB_ACCESS_FINAL`\
 表示对象具有最终访问。

 `DBG_ATTRIB_ACCESS_ALL`\
 用于从 中提取访问属性的掩码 `DBG_ATTRIB_FLAGS` 。

 `DBG_ATTRIB_STORAGE_NONE`\
 指示未指定存储类型。

 `DBG_ATTRIB_STORAGE_GLOBAL`\
 表示全局存储。

 `DBG_ATTRIB_STORAGE_STATIC`\
 表示静态存储。

 `DBG_ATTRIB_STORAGE_REGISTER`\
 指示寄存器中的存储。

 `DBG_ATTRIB_STORAGE_ALL`\
 用于从 中提取存储属性的掩码 `DBG_ATTRIB_FLAGS` 。

 `DBG_ATTRIB_TYPE_NONE`\
 指示没有类型修饰符。

 `DBG_ATTRIB_TYPE_VIRTUAL`\
 指示对象的类型是虚拟的。

 `DBG_ATTRIB_TYPE_CONSTANT`\
 表示对象的类型是常量。

 `DBG_ATTRIB_TYPE_SYNCHRONIZED`\
 指示对象的类型已同步。

 `DBG_ATTRIB_TYPE_VOLATILE`\
 指示对象的类型是可变的。

 `DBG_ATTRIB_TYPE_ALL`\
 用于从 中提取类型属性的掩码 `DBG_ATTRIB_FLAGS` 。

 `DBG_ATTRIB_DATA`\
 指示此对象是数据字段。

 `DBG_ATTRIB_METHOD`\
 指示此对象是方法。

 `DBG_ATTRIB_PROPERTY`\
 指示此对象是属性。

 `DBG_ATTRIB_CLASS`\
 指示此对象是一个类。

 `DBG_ATTRIB_BASECLASS`\
 指示此对象是基类。

 `DBG_ATTRIB_INTERFACE`\
 指示此对象是接口。

 `DBG_ATTRIB_INNERCLASS`\
 指示此对象是内部类。

 `DBG_ATTRIB_MOSTDERIVED`\
 指示此对象是"*最派生的*"。 术语"*最派生*"是指对象的实际类型，而不是其引用的类型。

 `DBG_ATTRIB_CHILD_ALL`\
 指示通过 的 `DBG_ATTRIB_DATA` 掩码 `DBG_ATTRIB_MOSTDERIVED` 。

 `DBG_ATTRIB_MULTI_CUSTOM_VIEWERS`\
 指示对象有多个与之关联的自定义查看器。

## <a name="remarks"></a>备注

> [!NOTE]
> 此枚举中的值实际上未在 C# 的程序集中定义。 相反，必须将定义复制到源文件。

 这些标志还用于筛选对象的子项，例如，作为参数传递给 [EnumChildren 时](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)。 这些值可以与位 合并 `OR` 。

 标志 `DBG_ATTRIB_VALUE_CUSTOM_VIEWER` 指示从 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] [IDebugProperty2 接口获取 IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty2.md)接口，并调用[GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)以获取自定义查看器列表。 [](../../../extensibility/debugger/reference/idebugproperty3.md)

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
