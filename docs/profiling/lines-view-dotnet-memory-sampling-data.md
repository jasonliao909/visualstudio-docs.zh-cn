---
title: “行”视图 - .NET 内存采样数据 | Microsoft Docs
description: 了解 .NET 内存分配分析数据的“行”视图如何列出分析运行期间分配内存的语句。
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Lines view
ms.assetid: 6631ab87-0e62-4c76-a063-4ea7222b07da
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: 3e04f70f412b234d49c2fe51aaf6a22229ce90f1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122038716"
---
# <a name="lines-view---net-memory-sampling-data"></a>“行”视图 - .NET 内存采样数据
使用采样方法的 .NET 内存分配分析数据的“行”视图列出分析运行期间分配内存的语句。 这些列还包括分配的大小和数量。

 在源文件中，一个语句可分散在多行中，而一行也可包括多个语句。

 语句由以下数据标识：

- 包含函数语句的源文件。

- 包含该语句的函数。

- 该语句的起始源代码行。

- 该语句的起始源代码行中的字符。

- 该语句的结束源代码行。

- 该语句的结束源代码行中的字符。

  “行名”列提供一串可排序的标识符数据。

  根据定义，语句不调用其他函数。 因此，仅列出独占值。

|列|描述|
|------------|-----------------|
|**进程 ID**|分析运行的进程 ID (PID)。|
|**进程名**|进程的名称。|
|**模块名**|语句所在模块的名称。|
|**模块路径**|语句所在模块的路径。|
|**源文件**|语句所在的源文件。|
|**函数名**|语句所在函数的名称。|
|**函数行号**|此函数在源文件中的起始行号。|
|**函数地址**|函数的起始地址。|
|**源行开始**|源文件中发生分配的起始行号。|
|**源行结束**|源文件中发生分配的结束行号。|
|**源字符开始**|发生分配的源文件行中起始字符的偏移量。|
|**源字符结束**|发生分配的源文件行中结束字符的偏移量。|
|**行名**|由探查器生成的行标识符，语法为：`Source File` **;[** `Line Number Start` **,** `Character Start` **]->;[** `Line Number Start,Character Start` **]**|
|**独占分配数**|此行中创建的对象总数。|
|**独占分配数百分比**|在分析运行期间创建的，此行中分配的所有对象数的百分比。|
|**独占字节数**|在分析运行期间分配的，此行中分配的所有内存字节数的百分比。|
|**独占字节数百分比**|在分析运行期间分配的，此行中分配的所有内存字节数的百分比。|

## <a name="see-also"></a>另请参阅
- [“行”视图](../profiling/lines-view-sampling-data.md)
