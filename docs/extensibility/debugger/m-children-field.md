---
description: 向此任务注册的子任务的列表。
title: m_children字段|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- m_children field, ContingentProperties class [.NET Framework debug engines]
ms.assetid: 0a3b5653-7bc0-4a7a-8963-9020bc52b9cb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 311ab164551e46fbe1c30b5a6045a7993a900a67
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901365"
---
# <a name="m_children-field"></a>m_children字段
向此任务注册的子任务的列表。

 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集：mscorlib** (*mscorlib.dll*) 

 由于无法从 CIL 访问此内部成员，因此.NET Framework CIL 语言中的公共中间语言 (语法) 。

## <a name="syntax"></a>语法

```csharp
.field public class System.Collections.Generic.List`1<class System.Threading.Tasks.Task> m_children
```

## <a name="remarks"></a>备注
 在任务运行时，只有执行任务的线程才应访问此数组。

 如果任务已完成，则其他线程可以访问此字段，只要它们不向该字段添加任何内容或删除任何内容。

## <a name="see-also"></a>另请参阅
- [ContingentProperties 类](../../extensibility/debugger/contingentproperties-class-internal-members.md)
