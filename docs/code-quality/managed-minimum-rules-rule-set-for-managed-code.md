---
title: 托管代码的“托管最少量规则”规则集
ms.date: 11/04/2016
description: 了解 Visual Studio 中的 "托管最低规则" 规则集，其中重点介绍安全性、可靠性和其他关键问题。 请参阅规则说明。
ms.custom: SEO-VS-2020
ms.topic: reference
ms.assetid: 44a50c54-8dd3-42b2-8387-532a150e5a6c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 8711fd0a265618a5aaf4f84edcf7dd2b081b16a3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99859809"
---
# <a name="managed-minimum-rules-rule-set-for-managed-code"></a>托管代码的“托管最少量规则”规则集

托管的最小规则侧重于代码中最关键的问题，包括潜在的安全漏洞、应用程序崩溃和其他重要的逻辑和设计错误。 在为项目创建的任何自定义规则集中包含此规则集。

|规则|描述|
|----------|-----------------|
|[CA1001](/dotnet/fundamentals/code-analysis/quality-rules/ca1001)|具有可释放字段的类型应该是可释放的|
|[CA1821](/dotnet/fundamentals/code-analysis/quality-rules/ca1821)|移除空终结器|
|[CA2213](/dotnet/fundamentals/code-analysis/quality-rules/ca2213)|应释放可释放的字段|
|[CA2231](/dotnet/fundamentals/code-analysis/quality-rules/ca2231)|重写时重载相等运算符 `ValueType.Equals`|
