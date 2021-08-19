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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: fb9897fd4a15b78a6130d68ddcaf3c1089def8ab
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122133284"
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

|名称|说明|
|----------|-----------------|
|[ObjectIdForDebugger 属性](../../extensibility/debugger/asynctaskmethodbuilder-objectidfordebugger-property.md)|获取一个对象，该对象可用于唯一标识调试器此生成器。|
|[m_builder字段](../../extensibility/debugger/asynctaskmethodbuilder-m-builder-field.md)|表示此非泛型实例委托给的泛型生成器对象。|

## <a name="see-also"></a>请参阅
- <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder>
- [并行扩展插件的内部.NET Framework](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
