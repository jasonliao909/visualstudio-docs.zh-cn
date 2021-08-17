---
title: 托管代码的“托管最少量规则”规则集
ms.date: 11/04/2016
description: 了解集中的托管最低规则规则Visual Studio，该规则侧重于安全性、稳定性和其他关键问题。 请参阅规则说明。
ms.custom: SEO-VS-2020
ms.topic: reference
ms.assetid: 44a50c54-8dd3-42b2-8387-532a150e5a6c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- dotnet
ms.openlocfilehash: 35cc4d2abc0c99afd3d9add98178aea54e5f2367
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122091222"
---
# <a name="managed-minimum-rules-rule-set-for-managed-code"></a>托管代码的“托管最少量规则”规则集

最小托管规则侧重于代码中的最关键问题，包括潜在的安全漏洞、应用程序崩溃以及其他重要的逻辑和设计错误。 在为项目创建的任何自定义规则集中包括此规则集。

|规则|描述|
|----------|-----------------|
|[CA1001](/dotnet/fundamentals/code-analysis/quality-rules/ca1001)|具有可释放字段的类型应该是可释放的|
|[CA1821](/dotnet/fundamentals/code-analysis/quality-rules/ca1821)|移除空终结器|
|[CA2213](/dotnet/fundamentals/code-analysis/quality-rules/ca2213)|应释放可释放的字段|
|[CA2231](/dotnet/fundamentals/code-analysis/quality-rules/ca2231)|重写时重载运算符等于 `ValueType.Equals`|
