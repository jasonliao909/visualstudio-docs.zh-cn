---
description: 本文介绍 System.Runtime.CompilerServices.AsyncTaskMethodBuilder 类的内部成员。
title: AsyncTaskMethodBuilder 结构 - 内部成员
titleSuffix: ''
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debug engines, AsyncTaskMethodBuilder structure [.NET Framework]
- AsyncTaskMethodBuilder structure [.NET Framework debug engines]
ms.assetid: f32f5857-7ef8-45fd-8b5a-7f644eb98b11
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c5b21045688fc2be555c7a42d6e3b9014b66c761
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903835"
---
# <a name="asynctaskmethodbuilder-structure---internal-members"></a>AsyncTaskMethodBuilder 结构 - 内部成员
本主题介绍 类的内部 <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder> 成员。 有关此类的一般信息，请参阅 <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder> 参考主题。

 **命名空间：** <xref:System.Runtime.CompilerServices?displayProperty=fullName>

 **程序集：mscorlib** (mscorlib.dll) 

 由于无法从 CIL .NET Framework访问这些内部成员，因此在 CIL (中提供了以下) 。

## <a name="syntax"></a>语法

```csharp
.class public sequential ansi sealed beforefieldinit System.Runtime.CompilerServices.AsyncTaskMethodBuilder
       extends System.ValueType
       implements System.Runtime.CompilerServices.IAsyncMethodBuilder
```

## <a name="internal-members"></a>内部成员

|名称|描述|
|----------|-----------------|
|[ObjectIdForDebugger 属性](../../extensibility/debugger/asynctaskmethodbuilder-objectidfordebugger-property.md)|获取一个对象，该对象可用于唯一标识调试器此生成器。|
|[m_builder字段](../../extensibility/debugger/asynctaskmethodbuilder-m-builder-field.md)|表示此非泛型实例委托给的泛型生成器对象。|

## <a name="see-also"></a>另请参阅
- <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder>
- [并行扩展插件的内部.NET Framework](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
