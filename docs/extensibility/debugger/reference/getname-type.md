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
ms.openlocfilehash: b95c08ab5adc5140bfcfc21b9e9fa7cc9f46c78a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122064989"
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
指定基本文件名，而不是文档或上下文的完整路径。

`GN_MONIKERNAME`\
以名字对象的形式指定文档或上下文的唯一名称。

`GN_URL`\
指定文档或上下文的 URL 名称。

`GN_TITLE`\
指定文档的标题（如果存在）。

`GN_STARTPAGEURL`\
获取进程起始页 URL。

## <a name="remarks"></a>备注
这些值作为参数传递给[GetName、GetName](../../../extensibility/debugger/reference/idebugdocument2-getname.md)和[](../../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md) [GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md)方法，以指定要返回的名称类型。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetName](../../../extensibility/debugger/reference/idebugdocument2-getname.md)
- [GetName](../../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md)
- [GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md)
