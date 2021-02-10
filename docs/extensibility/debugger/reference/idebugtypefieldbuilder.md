---
title: IDebugTypeFieldBuilder |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugTypeFieldBuilder interface
ms.assetid: 2dfed0be-6972-4bec-baec-f0b78df9ef97
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 67a94f3f88d85d1e74ce7b1d67e1ef3d44546132
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99965689"
---
# <a name="idebugtypefieldbuilder"></a>IDebugTypeFieldBuilder
表示创建表示类型的字段的功能。

## <a name="syntax"></a>语法

```
IDebugTypeFieldBuilder : IUnknown
```

## <a name="notes-for-callers"></a>调用方说明
 此接口是从符号提供程序获取的。

## <a name="methods"></a>方法
 此接口实现以下方法：

|方法|说明|
|------------|-----------------|
|[CreatePrimitive](../../../extensibility/debugger/reference/idebugtypefieldbuilder-createprimitive.md)|创建一个表示基元类型的对象。|
|[CreatePointerToType](../../../extensibility/debugger/reference/idebugtypefieldbuilder-createpointertotype.md)|创建指向指定类型的指针。|

## <a name="requirements"></a>要求
 标头： Sh。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
