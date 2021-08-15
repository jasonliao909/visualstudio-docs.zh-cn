---
description: 本主题介绍 System.Runtime.CompilerServices.AsyncTaskMethodBuilder 类的内部成员。
title: AsyncTaskMethodBuilder &lt; TResult &gt; 结构 - 内部成员|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- AsyncTaskMethodBuilder<TResult> structure [.NET Framework debug engines]
- debug engines, AsyncTaskMethodBuilder<TResult> structure [.NET Framework]
ms.assetid: 17ebc340-8170-4aff-bf54-dc4548c83632
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 7864f45aaed3d16784a451ce5a0161218650246806da3debce2ef8ea1d3ab4e0
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121434668"
---
# <a name="asynctaskmethodbuilderlttresultgt-structure---internal-members"></a>AsyncTaskMethodBuilder &lt; TResult &gt; 结构 - 内部成员
本主题介绍 类的内部 <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601> 成员。 有关此类的一般信息，请参阅 <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601> 参考主题。

 **命名空间：** <xref:System.Runtime.CompilerServices?displayProperty=fullName>

 **程序集：mscorlib** (mscorlib.dll) 

 由于无法从 CIL .NET Framework访问这些内部成员，因此在公共中间语言 (CIL) 。

## <a name="syntax"></a>语法

```csharp
.class public sequential ansi sealed beforefieldinit System.Runtime.CompilerServices.AsyncTaskMethodBuilder`1<TResult>
       extends System.ValueType
       implements System.Runtime.CompilerServices.IAsyncMethodBuilder
```

## <a name="internal-members"></a>内部成员

|名称|说明|
|----------|-----------------|
|[ObjectIdForDebugger 属性](../../extensibility/debugger/asynctaskmethodbuilder-tresult-objectidfordebugger-property.md)|获取一个对象，该对象可用于唯一标识调试器此生成器。|
|[m_task字段](../../extensibility/debugger/asynctaskmethodbuilder-tresult-m-task-field.md)|表示延迟初始化的生成任务。|

## <a name="see-also"></a>另请参阅
- <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601>
- [并行扩展插件的内部.NET Framework](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
