---
title: 内存和分页性能规则 | Microsoft Docs
description: 了解内存和分页类别中的性能规则如何确定在分析运行期间能影响应用程序性能和响应能力的分页活动。
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: f37972b2-efe4-4a1c-a5d1-a246ccd76817
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 7e8606ea4d44d374a6d0c8b59905038b352aceaa
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122054621"
---
# <a name="memory-and-paging-performance-rules"></a>内存和分页性能规则
内存和分页类别中的性能规则确定在分析运行期间能影响应用程序性能和响应能力的分页活动。

|规则|描述|
|-|-|
|[DA0014：以分页方式将活动内存移到磁盘的发生率极高](../profiling/da0014-extremely-high-rates-of-paging-active-memory-to-disk.md)|在整个分析运行期间出现了超高比率的分页活动内存进出磁盘的情况。 此级别的分页速率通常会影响应用程序性能和响应能力。 请考虑通过修改算法来减少内存分配。 可能还需要考虑应用程序的内存要求。 尝试在拥有更多内存的计算机上重新运行分析。 当分页活动数超过规则 D0017 的上限阈值时，将引发此规则。|
|[DA0017：以分页方式将活动内存移到磁盘的发生率高](../profiling/da0017-high-rates-of-paging-active-memory-to-disk.md)|在整个分析运行期间出现了相对高比率的分页活动内存进出磁盘的情况。 此级别的分页速率通常会影响应用程序性能和响应能力。 请考虑通过修改算法来减少内存分配。 可能还需要考虑应用程序的内存要求。 尝试在拥有更多内存的计算机上重新运行分析。|
