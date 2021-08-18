---
description: 包含 System.Threading.Tasks.Task 对象的其他属性。
title: ContingentProperties 类 - 内部成员|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- ContingentProperties class [.NET Framework debug engines]
- debug engines, ContingentProperties class [.NET Framework]
ms.assetid: c49d1362-ab1c-4b6d-9950-fcae40e0e66b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 7486f1328aea816e4442def2d7df7133149f3a68
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122043630"
---
# <a name="contingentproperties-class---internal-members"></a>ContingentProperties 类 - 内部成员
包含 对象的其他 <xref:System.Threading.Tasks.Task> 属性。

 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集：mscorlib** (mscorlib.dll) 

 由于无法从 CIL .NET Framework访问这些内部成员，因此在 CIL (中提供了以下) 。

## <a name="syntax"></a>语法

```csharp
.class auto ansi nested assembly beforefieldinit ContingentProperties
       extends System.Object
```

## <a name="members"></a>成员

### <a name="fields"></a>字段

|名称|说明|
|----------|-----------------|
|[m_children](../../extensibility/debugger/m-children-field.md)|向此任务注册的子任务的列表。|

## <a name="remarks"></a>备注
 这些.NET Framework仅在需要时初始化此类的字段。

## <a name="see-also"></a>请参阅
- [并行扩展插件的内部.NET Framework](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
