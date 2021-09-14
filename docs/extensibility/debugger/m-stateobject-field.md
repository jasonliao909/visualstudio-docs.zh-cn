---
description: 一个 对象，该对象表示操作将使用的数据。
title: m_stateObject字段|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- m_stateObject field, Task class [.NET Framework debug engines]
ms.assetid: 68c54b22-3e1c-4031-b9c7-b972c519d8a0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: fad86acc86043e58bfa68f0cf8687b7c439b7ad6
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602508"
---
# <a name="m_stateobject-field"></a>m_stateObject字段
一个 对象，该对象表示操作将使用的数据。

 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集：mscorlib** (*mscorlib.dll*) 

 由于无法从 CIL 访问此内部成员，因此.NET Framework CIL 语言中的公共中间语言 (语法) 。

## <a name="syntax"></a>语法

```
.field assembly object m_stateObject
```

## <a name="remarks"></a>备注
 这是 `state` 构造函数中的 <xref:System.Threading.Tasks.Task.%23ctor%2A> 参数。 它还是 属性的支持 <xref:System.Threading.Tasks.Task.AsyncState%2A?displayProperty=fullName> 字段。

## <a name="see-also"></a>另请参阅
- [Task 类](../../extensibility/debugger/task-class-internal-members.md)
