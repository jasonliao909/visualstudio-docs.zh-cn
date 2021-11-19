---
description: " (DIA) SDK 的 \"调试接口访问\" 提供了说明文档和说明如何使用 DIA API 的示例。"
title: " (调试接口访问 SDK 入门) |Microsoft Docs"
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- .dbg files
- DBG files
ms.assetid: cb3d040a-2846-40d7-bdbc-8a5beb5dd2f6
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 4e74262594e23af3819851bcf23d69692fd7d64c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832357"
---
# <a name="getting-started-debug-interface-access-sdk"></a>入门（调试接口访问 SDK）
 (DIA) SDK 的 "调试接口访问" 提供了说明文档和说明如何使用 DIA API 的示例。 使用 DIA SDK 中的接口和方法开发自定义应用程序，这些应用程序打开 .pdb 和 dbg 文件，然后在其内容中搜索符号、值、属性、地址和其他调试信息。 此 SDK 还为与 c + + 应用程序中的符号关联的属性提供引用表。

 为了最好地使用 DIA SDK，你应熟悉以下内容：

- C + + 编程语言

- COM 编程

- Visual Studio 集成开发环境 (IDE) 用于编译示例

  DIA SDK 通常与 Visual Studio 一起安装，其默认位置为 *[drive]* \Program Files \ Microsoft Visual Studio 9.0 \ DIA SDK。 作为安装的一部分，将自动注册用于实现 DIA SDK 的 msdia90.dll，因此，你需要做的就是将其包含 `dia2.h` 在你的程序中并链接到 `diaguids.lib` 。

  标头： include\dia2。h

  库： lib\diaguids.lib

  DLL: bin\msdia80.dll

  IDL: idl\dia2.idl

## <a name="in-this-section"></a>本节内容

[概述](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)

查看 DIA 的基本体系结构。

[查询 .Pdb 文件](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)

提供有关如何使用 DIA API 查询 .pdb 文件的分步说明。

## <a name="see-also"></a>另请参阅

- [调试接口访问 SDK](../../debugger/debug-interface-access/debug-interface-access-sdk.md)
