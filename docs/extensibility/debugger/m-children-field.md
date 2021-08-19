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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 17f009c25ce6de66a6ac4ce0ac2b1f304dd22a72
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122160551"
---
# <a name="m_children-field"></a>m_children字段
向此任务注册的子任务的列表。

 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集：mscorlib** (*mscorlib.dll*) 

 由于无法从 CIL 访问此内部成员.NET Framework，因此在 CIL (中提供了以下) 。

## <a name="syntax"></a>语法

```csharp
.field public class System.Collections.Generic.List`1<class System.Threading.Tasks.Task> m_children
```

## <a name="remarks"></a>备注
 在任务运行时，只有执行任务的线程才应访问此数组。

 如果任务已完成，则其他线程可以访问此字段，只要它们不向该字段添加任何内容或删除任何内容。

## <a name="see-also"></a>请参阅
- [ContingentProperties 类](../../extensibility/debugger/contingentproperties-class-internal-members.md)
