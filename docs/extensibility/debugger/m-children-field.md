---
description: 向此任务注册的子任务的列表。
title: m_children 字段 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- m_children field, ContingentProperties class [.NET Framework debug engines]
ms.assetid: 0a3b5653-7bc0-4a7a-8963-9020bc52b9cb
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5aaf29d76a7bbd81a416c86360f315bc5c09b76c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158864"
---
# <a name="m_children-field"></a>m_children 字段
向此任务注册的子任务的列表。

 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>

 **Assembly：** mscorlib (*mscorlib.dll*) 

 由于无法从 .NET Framework 访问此内部成员，因此在公共中间语言 (CIL) 中提供了以下语法。

## <a name="syntax"></a>语法

```csharp
.field public class System.Collections.Generic.List`1<class System.Threading.Tasks.Task> m_children
```

## <a name="remarks"></a>备注
 当任务正在运行时，只有执行任务的线程才能访问此数组。

 如果任务已完成，则其他线程可以访问此字段，只要它们不向其添加任何内容或从中删除任何内容。

## <a name="see-also"></a>另请参阅
- [ContingentProperties 类](../../extensibility/debugger/contingentproperties-class-internal-members.md)
