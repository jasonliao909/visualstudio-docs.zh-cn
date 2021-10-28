---
title: “行”视图 - 采样数据 | Microsoft Docs
description: 了解采样数据的“行”视图如何列出分析运行期间收集样本时所执行语句的性能数据。
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Lines view
ms.assetid: 46497249-c797-42c5-a02c-3e4bb3b4ee60
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: bc344c640a2b075b3795fb694ab076555a8b4083
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126736860"
---
# <a name="lines-view---sampling-data"></a>“行”视图 - 采样数据
采样数据的“行”视图列出分析运行期间收集样本时所执行语句的性能数据。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。

 在源文件中，一个语句可分散在多行中，而一行也可包括多个语句。 语句由以下数据标识：

- 包含函数语句的源文件。

- 包含该语句的函数。

- 该语句的起始源代码行。

- 该语句的起始源代码行中的字符。

- 该语句的结束源代码行。

- 该语句的结束源代码行中的字符。

  “行名”列提供一串可排序的标识符数据。

  根据定义，语句不调用其他函数。 因此，仅列出独占值。

|列|说明|
|------------|-----------------|
|**进程 ID**|分析运行的进程 ID (PID)。|
|**进程名**|进程的名称。|
|**模块名**|函数行所在模块的名称。|
|**模块路径**|函数行所在模块的路径。|
|**源文件**|包含函数行的源文件。|
|**函数名**|函数名。|
|**函数行号**|此函数在源文件中的起始行号。|
|**函数地址**|函数的起始地址。|
|**源行开始**|源文件中收集此样本的的起始行号。|
|**源行结束**|源文件中收集此样本的的结束行号。|
|**源字符开始**|源文件行中收集此样本的起始字符的偏移量。|
|**源字符结束**|源文件行中收集此样本的结束字符的偏移量。|
|**行名**|由探查器生成的行标识符，语法为：`Source File` **;[** `Line Number Start` **,** `Character Start` **]->;[** `Line Number End` **,** `Character End` **]**|
|**独占样本数**|执行函数行时收集的样本总数。|
|**独占样本数百分比**|执行函数行时在分析运行期间收集的所有样本数的百分比。|

## <a name="see-also"></a>另请参阅
- [“行”视图 - 采样](../profiling/lines-view-dotnet-memory-sampling-data.md)
