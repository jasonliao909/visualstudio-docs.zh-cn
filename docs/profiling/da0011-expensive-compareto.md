---
title: DA0011 - 高开销 CompareTo | Microsoft Docs
description: 类型的 CompareTo 方法开销巨大或分配内存。
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.performance.DA0011
- vs.performance.rules.DAExpensiveCompareTo
- vs.performance.11
- vs.performance.rules.DA0011
ms.assetid: 239a381d-0d97-4367-8668-746c93f5af2c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 261327205f0ee8a297ad5fda333394a002dc7e9a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126640787"
---
# <a name="da0011-expensive-compareto"></a>DA0011：高开销 CompareTo

|项|“值”|
|-|-|
|规则 ID|DA0011|
|类别|.NET Framework 使用情况|
|分析方法|采样<br /><br /> .NET 内存|
|消息|CompareTo 函数应该比较便宜，且不应分配任何内存。 如果可能，降低 CompareTo 函数的复杂性。|
|规则类型|警告|

## <a name="cause"></a>原因
 类型的 CompareTo 方法开销巨大或分配内存。

## <a name="rule-description"></a>规则说明
 CompareTo 方法应高效，且不应分配内存。

## <a name="how-to-fix-violations"></a>如何解决冲突
 降低 CompareTo 方法的复杂性。
