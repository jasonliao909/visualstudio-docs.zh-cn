---
title: diagnostic 命名空间 | Microsoft Docs
description: 使用诊断命名空间发出并行可视化工具标记。 诊断命名空间隶属于并行命名空间。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkersobj/Concurrency, diagnostic
helpviewer_keywords:
- Concurrency, diagnostic namespace
ms.assetid: ad786b19-7c4c-46ee-bfb6-c4752b373a09
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 9e9d976983b534081926795ff1754fe7047f2f42
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126735511"
---
# <a name="diagnostic-namespace"></a>diagnostic 命名空间
`diagnostics` 命名空间提供用于发出并行可视化工具标记的功能。

## <a name="syntax"></a>语法

```cpp
namespace diagnostic;
```

## <a name="members"></a>成员

### <a name="classes"></a>类

|“属性”|说明|
|----------|-----------------|
|[marker_series 类](../profiling/marker-series-class.md)|表示由单个提供程序生成的一系列事件通道。|
|[span 类](../profiling/span-class.md)|定义应用程序的一个阶段。|

### <a name="enumerations"></a>枚举

|名称|说明|
|----------|-----------------|
|[marker_importance 枚举](../profiling/marker-importance-enumeration.md)|表示并发可视化工具标记的重要性级别。|

## <a name="requirements"></a>要求
 **标头：cvmarkersobj.h** 

 **命名空间：** 并发

## <a name="see-also"></a>另请参阅
- [Concurrency 命名空间（并发可视化工具）](../profiling/concurrency-namespace-concurrency-visualizer.md)