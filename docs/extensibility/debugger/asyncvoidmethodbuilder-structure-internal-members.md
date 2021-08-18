---
description: 本主题介绍 System.runtime.compilerservices. AsyncVoidMethodBuilder 类的内部成员。
title: AsyncVoidMethodBuilder 结构-内部成员 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debug engines, AsyncVoidMethodBuilder structure [.NET Framework]
- AsyncVoidMethodBuilder structure [.NET Framework debug engines]
ms.assetid: fe2970ab-d4c5-4355-a8e4-772ee0a57178
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 4cb6118600587d634adc5bf648901949eb27ff128908b021e94a62b956eaae6f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121293399"
---
# <a name="asyncvoidmethodbuilder-structure---internal-members"></a>AsyncVoidMethodBuilder 结构-内部成员
本主题介绍类的内部成员 <xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder> 。 有关此类的常规信息，请参阅 <xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder> 参考主题。

 **命名空间：** <xref:System.Runtime.CompilerServices?displayProperty=fullName>

 **Assembly：** mscorlib (mscorlib.dll) 

 由于无法从 .NET Framework 访问这些内部成员，因此在公共中间语言 (CIL) 中提供了以下语法。

## <a name="syntax"></a>语法

```csharp
.class public sequential ansi sealed beforefieldinit System.Runtime.CompilerServices.AsyncVoidMethodBuilder
       extends System.ValueType
       implements System.Runtime.CompilerServices.IAsyncMethodBuilder
```

## <a name="internal-members"></a>内部成员

|名称|说明|
|----------|-----------------|
|[ObjectIdForDebugger 属性](../../extensibility/debugger/asyncvoidmethodbuilder-objectidfordebugger-property.md)|获取一个对象，该对象可用于将此生成器唯一标识到调试器。|
|[m_objectIdForDebugger 字段](../../extensibility/debugger/asyncvoidmethodbuilder-m-objectidfordebugger-field.md)|表示调试器用来唯一标识此生成器的延迟初始化的对象。|

## <a name="see-also"></a>请参阅
- <xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder>
- [.NET Framework 的并行扩展内部机制](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
