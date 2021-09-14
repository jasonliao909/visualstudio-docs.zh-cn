---
description: 包含针对 System.object 对象的其他属性。
title: ContingentProperties 类-内部成员 |Microsoft Docs
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600975"
---
# <a name="contingentproperties-class---internal-members"></a>ContingentProperties 类-内部成员
包含对象的其他属性 <xref:System.Threading.Tasks.Task> 。

 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>

 **Assembly：** mscorlib (mscorlib.dll) 

 由于无法从 .NET Framework 访问这些内部成员，因此在公共中间语言 (CIL) 中提供了以下语法。

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
 仅当需要此类的字段时，.NET Framework 才初始化此类的字段。

## <a name="see-also"></a>另请参阅
- [.NET Framework 的并行扩展内部机制](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
