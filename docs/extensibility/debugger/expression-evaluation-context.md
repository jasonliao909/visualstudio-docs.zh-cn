---
title: 表达式计算上下文|Microsoft Docs
description: 了解表达式计算上下文，它表示表达式计算上下文，当程序在断点处停止时存在。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- expression evaluation, context
ms.assetid: a2fd3758-09bd-45ae-8ecc-2d276c0036ba
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 4555cf1431b23766085a4174223d3f880d08df45
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602510"
---
# <a name="expression-evaluation-context"></a>表达式计算上下文
在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试中，表达式 **计算上下文：**

- 表示表达式计算上下文。 通常，计算上下文对应于用于计算变量、参数、函数和方法的词法范围。 例如，与堆栈帧关联的表达式计算上下文将为计算局部变量、方法参数和类成员提供上下文 (（如果适用) ）。

- 当程序在断点处停止时存在。 表达式本身是表示已分析表达式的数据结构，该表达式已准备好在给定上下文中进行绑定和计算。

     有关详细信息，使用 [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 方法创建表达式。 计算表达式时，它将生成一个可打印字符串，其中包含变量或参数的名称和类型及其值。 此字符串显示在 IDE 监视窗口或"局部设置"窗口中。

     给定 `BSTR` 和 [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) 接口后，调试引擎 (DE) 可以通过分析表达式来创建 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 接口。 给定 `IDebugExpression2` 接口后，DE 可以通过同步或异步表达式计算获取值。 此值以及变量或参数的名称和类型将发送到 IDE 进行显示。

## <a name="see-also"></a>另请参阅
- [表达式计算接口](../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [调试器上下文](../../extensibility/debugger/debugger-contexts.md)
