---
title: FxCopCmd 错误
ms.date: 10/19/2016
description: 了解 FxCopCmd 命令返回的错误代码。 查看每个代码表示的错误类型，并了解如何识别致命错误。
ms.custom: SEO-VS-2020
ms.topic: reference
helpviewer_keywords:
- FxCopCmd errors
ms.assetid: bb614ed0-1b7c-4b56-99ae-da50ef6cfef9
ms.author: mikejo
author: mikejo5000
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: c06c996245dfba796d4ab7e71fdbb28ad486f017
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601316"
---
# <a name="fxcopcmd-tool-errors"></a>FxCopCmd 工具错误

FxCopCmd 不会认为所有错误都是严重错误。 如果 FxCopCmd 有足够的信息来执行部分分析，它将执行分析并报告发生的错误。 错误代码是一个 32 位整数，包含与错误相对应的数值的位组合。

下表描述了 FxCopCmd 返回的错误代码：

|错误|数值|
|-----------|-------------------|
|无错误|0x0|
|分析错误|0x1|
|规则例外|0x2|
|Project加载错误|0x4|
|程序集加载错误|0x8|
|规则库加载错误|0x10|
|导入报表加载错误|0x20|
|输出错误|0x40|
|命令行开关错误|0x80|
|初始化错误|0x100|
|程序集引用错误|0x200|
|BuildBreakingMessage|0x400|
|未知错误|0x1000000|

**对于严重** 错误，将返回分析错误。 它指示无法完成分析。 如果适用，错误代码还包含致命错误的根本原因。 以下条件生成严重错误：

- 由于输入不足，无法执行分析。

- 分析引发了 FxCopCmd 未处理的异常。

- 找不到指定的项目文件或该文件已损坏。

- 未指定输出选项或无法写入文件。

> [!NOTE]
> FxCopCmd 返回代码 **程序集引用0x200** 错误本身是警告而不是错误。 此返回代码指示缺少间接引用，但 FxCopCmd 能够处理这些引用。 该警告意味着某些分析结果可能已被泄露。 将 **Assembly 引用错误** 视为与任何其他返回代码结合使用时的错误。

## <a name="see-also"></a>另请参阅

- [Code Analysis应用程序错误](../code-quality/code-analysis-application-errors.md)
