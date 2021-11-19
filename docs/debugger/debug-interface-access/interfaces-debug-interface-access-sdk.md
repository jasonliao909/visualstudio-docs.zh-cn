---
description: 方法按字母顺序在目录的每个接口下列出，在接口页上按 Vtable 顺序列出。
title: 调试 (访问 SDK) |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- interfaces [DIA SDK]
- DIA SDK, interfaces
ms.assetid: 62aee7c3-d314-4272-a32b-b2818f32fab8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: a225edc9d357f93b76cff7eb4c8c2daef4b4bdda
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832775"
---
# <a name="interfaces-debug-interface-access-sdk"></a>接口（调试接口访问 SDK）
方法按字母顺序在目录的每个接口下列出，在接口页上按 Vtable 顺序列出。

## <a name="in-this-section"></a>本节内容

[IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)

提供对调试DIA SDK虚拟地址和相对虚拟地址的计算方式的控制。

[IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)

启动对调试符号源的访问。

[IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)

提供对调试数据流中的记录的访问。

[IDiaEnumDebugStreams](../../debugger/debug-interface-access/idiaenumdebugstreams.md)

枚举数据源中包含的各种调试流。

[IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)

枚举数据源中包含的各种帧数据元素。

[IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)

枚举数据源中包含的各种注入源。

[IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)

枚举数据源中包含的各种行号。

[IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)

枚举数据源中包含的各种节贡献。

[IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)

枚举数据源中包含的各种段。

[IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)

枚举数据源中包含的各种源文件。

[IDiaEnumStackFrames](../../debugger/debug-interface-access/idiaenumstackframes.md)

枚举可用的各种堆栈帧。

[IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)

枚举数据源中包含的各种符号。

[IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)

按 对数据源中包含的各种符号进行枚举。

[IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)

枚举数据源中包含的各种表。

[IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)

公开堆栈帧的详细信息。

[IDiaImageData](../../debugger/debug-interface-access/idiaimagedata.md)

公开模块或图像的基位置和内存偏移量的详细信息。

[IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)

访问存储在 DIA 数据源中的程序源代码。

[IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)

访问描述从图像文本的字节块映射到源文件行号的过程的信息。

[IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)

从 DIA 符号定位过程接收回调，从而使用户界面能够报告位置尝试的进度。

[IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)

从 DIA 符号定位过程接收回调，从而允许对定位过程施加限制。

[IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)

允许读取 DIA 属性集的持久属性。

[IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)

使客户端应用程序能够按文件位置指定提供可执行文件的字节。

[IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)

使客户端应用程序能够提供由相对虚拟地址指定的可执行文件的字节。

[IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)

检索描述节贡献的数据，即由编译器向图像贡献的连续内存块。

[IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)

地图区号到地址空间段的数据。

[IDiaSession](../../debugger/debug-interface-access/idiasession.md)

为调试符号提供查询上下文。

[IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)

表示源文件。

[IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)

公开堆栈帧的属性。

[IDiaStackWalker](../../debugger/debug-interface-access/idiastackwalker.md)

提供使用 PDB 文件执行堆栈演练的方法。

[IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)

维护 [IDiaFrameData：：execute](../../debugger/debug-interface-access/idiaframedata-execute.md) 方法调用之间的堆栈上下文。

[IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)

使用 PDB 中的程序调试数据库和 PDB (帮助) 堆栈。

[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

描述符号实例的属性。

[IDiaTable](../../debugger/debug-interface-access/idiatable.md)

枚举 DIA 数据源表。

## <a name="related-sections"></a>相关章节
[枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)

描述集合的各个接口使用的枚举和DIA SDK。

[常量（调试接口访问 SDK）](../../debugger/debug-interface-access/constants-debug-interface-access-sdk.md)

描述中可用的常量DIA SDK。

## <a name="see-also"></a>另请参阅

- [引用](../../debugger/debug-interface-access/debug-interface-access-sdk-reference.md)
