---
title: 托管代码的“全球化规则”规则集
ms.date: 11/04/2016
description: 了解 Visual Studio 中的“全球化规则”规则集，该规则集主要关注与语言、区域设置和区域性相关的问题。 请参阅规则说明。
ms.custom: SEO-VS-2020
ms.topic: reference
ms.assetid: 3c4032ee-0805-4581-8c48-b1827cd6b213
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- dotnet
ms.openlocfilehash: 74c0740faaf016e27a1a3824e728821f5d3c6d73
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601314"
---
# <a name="globalization-rules-rule-set-for-managed-code"></a>托管代码的“全球化规则”规则集

使用“Microsoft 全球化规则”规则集，关注可能导致应用程序中的数据无法在不同语言、区域设置和区域性中正确显示的问题。 如果应用程序经过了本地化和/或全球化，应包含此规则集。

|规则|描述|
|----------|-----------------|
|[CA1303](/dotnet/fundamentals/code-analysis/quality-rules/ca1303)|请不要将文本作为本地化参数传递|
|[CA1304](/dotnet/fundamentals/code-analysis/quality-rules/ca1304)|指定 CultureInfo|
|[CA1305](/dotnet/fundamentals/code-analysis/quality-rules/ca1305)|指定 IFormatProvider|
|[CA1307](/dotnet/fundamentals/code-analysis/quality-rules/ca1307)|为了清晰起见，请指定 StringComparison|
|[CA1308](/dotnet/fundamentals/code-analysis/quality-rules/ca1308)|将字符串规范化为大写|
|[CA1309](/dotnet/fundamentals/code-analysis/quality-rules/ca1309)|使用按顺序的 StringComparison|
|[CA1310](/dotnet/fundamentals/code-analysis/quality-rules/ca1310)|为了确保正确，请指定 StringComparison|
|[CA2101](/dotnet/fundamentals/code-analysis/quality-rules/ca2101)|指定对 P/Invoke 字符串参数进行封送处理|
