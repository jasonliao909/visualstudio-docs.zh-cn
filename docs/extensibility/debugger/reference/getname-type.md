---
description: 指定要检索的文件的名称类型。
title: GETNAME_TYPE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- GETNAME_TYPE
helpviewer_keywords:
- GETNAME_TYPE enumeration
ms.assetid: 2f9f1679-e9e8-4c9c-ac90-aa07bfe69914
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 358d0301ae0fc3ad0d9c35ede96734288836fb896b755d8c3fa6f128cf3e10e5
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121434251"
---
# <a name="getname_type"></a>GETNAME_TYPE
指定要检索的文件的名称类型。

## <a name="syntax"></a>语法

```cpp
enum enum_GETNAME_TYPE {
    GN_NAME         = 0,
    GN_FILENAME     = 1,
    GN_BASENAME     = 2,
    GN_MONIKERNAME  = 3,
    GN_URL          = 4,
    GN_TITLE        = 5,
    GN_STARTPAGEURL = 6
};
typedef DWORD GETNAME_TYPE;
```

```csharp
public enum enum_GETNAME_TYPE {
    GN_NAME         = 0,
    GN_FILENAME     = 1,
    GN_BASENAME     = 2,
    GN_MONIKERNAME  = 3,
    GN_URL          = 4,
    GN_TITLE        = 5,
    GN_STARTPAGEURL = 6
};
```

## <a name="fields"></a>字段
`GN_NAME`\
指定文档或上下文的友好名称。

`GN_FILENAME`\
指定文档或上下文的完整路径。

`GN_BASENAME`\
指定基文件名，而不是文档或上下文的完整路径。

`GN_MONIKERNAME`\
以名字对象的形式指定文档或上下文的唯一名称。

`GN_URL`\
指定文档或上下文的 URL 名称。

`GN_TITLE`\
指定文档的标题（如果有）。

`GN_STARTPAGEURL`\
获取进程的起始页 URL。

## <a name="remarks"></a>备注
这些值作为参数传递到 [GetName](../../../extensibility/debugger/reference/idebugdocument2-getname.md)、 [GetName](../../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md)和 [GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md) 方法，以指定要返回的名称的类型。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetName](../../../extensibility/debugger/reference/idebugdocument2-getname.md)
- [GetName](../../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md)
- [GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md)
