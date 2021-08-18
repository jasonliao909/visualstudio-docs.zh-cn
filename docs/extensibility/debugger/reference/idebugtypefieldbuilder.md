---
description: 表示创建表示类型的字段的功能。
title: IDebugTypeFieldBuilder |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugTypeFieldBuilder interface
ms.assetid: 2dfed0be-6972-4bec-baec-f0b78df9ef97
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: d3bd84eff7b52c48ad9f419e3d69e3a57fed485c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122103619"
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
