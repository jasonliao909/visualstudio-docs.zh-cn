---
description: Microsoft 调试接口访问软件开发工具包 (DIA SDK) 提供对存储在由 Microsoft 后编译器工具生成的程序数据库 (.pdb) 文件中的调试信息的访问。
title: 调试接口访问 SDK | Microsoft Docs
ms.date: 07/24/2018
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- debugging [DIA SDK]
- debugger [DIA SDK]
- DIA SDK
ms.assetid: 4c0abe53-11d3-4b7a-bdc7-b054f85aaf40
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 8cf60e03894f2a2a4c79e0242ef4e7b53d24deba
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832384"
---
# <a name="debug-interface-access-sdk"></a>调试接口访问 SDK

Microsoft 调试接口访问软件开发工具包 (DIA SDK) 提供对存储在由 Microsoft 后编译器工具生成的程序数据库 (.pdb) 文件中的调试信息的访问。 由于后编译器工具生成的 .pdb 文件的格式会不断修订，因此公开该格式是不切实际的。 使用 DIA API，可以开发搜索和浏览存储在 .pdb 文件中的调试信息的应用程序。 例如，此类应用程序可以报告堆栈追溯信息和分析性能数据。

## <a name="in-this-section"></a>本节内容

[入门](../../debugger/debug-interface-access/getting-started-debug-interface-access-sdk.md)

概述 DIA SDK 功能并指定 DIA SDK 的安装位置以及所需的头文件和库文件。

[查询 .Pdb 文件](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)

说明如何使用 DIA API 查询 .pdb 文件。

[符号和符号标记](../../debugger/debug-interface-access/symbols-and-symbol-tags.md)

讨论如何在 DIA API 中使用符号和符号标记。

[引用](../../debugger/debug-interface-access/debug-interface-access-sdk-reference.md)

包含 DIA API 的接口、方法、枚举和结构。

[Dia2dump 示例](../../debugger/debug-interface-access/dia2dump-sample.md)

说明如何使用 DIA API 搜索和浏览调试信息。
