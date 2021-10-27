---
title: DA0010 - 高开销 GetHashCode | Microsoft Docs
description: 对该类型的 GetHashCode 方法的调用在分析数据中占很大比例或此方法分配内存。
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.performance.rules.DAExpensiveGetHashCode
- vs.performance.DA0010
- vs.performance.rules.DA0010
- vs.performance.10
ms.assetid: 3987e21a-5b4f-45e4-8a33-6b3f0a472c08
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 1347b390c5d70478f2c7311746e6282fa344ba98
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126640790"
---
# <a name="da0010-expensive-gethashcode"></a>DA0010：高开销 GetHashCode

|项|“值”|
|-|-|
|规则 ID|DA0010|
|类别|.NET Framework 使用情况|
|分析方法|采样<br /><br /> .NET 内存|
|消息|GetHashCode 函数成本应较低，且不应分配任何内存。 如果可能，降低哈希代码函数的复杂性。|
|消息类型|警告|

## <a name="cause"></a>原因
 对该类型的 GetHashCode 方法的调用在分析数据中占很大比例或此方法分配内存。

## <a name="rule-description"></a>规则说明
 哈希是一项用于快速定位大型集合中的某个特定项的技术。 因为哈希表很大，且必须支持极高的访问速率，所以哈希表应该很有效。 此要求的含义是 .NET Framework 中的 GetHashCode 方法不应分配内存。 分配内存会增加垃圾回收器上的负载，并向潜在延迟公开该方法（如果因分配请求而需要运行垃圾回收）。

## <a name="how-to-fix-violations"></a>如何解决冲突
 降低方法的复杂性。
