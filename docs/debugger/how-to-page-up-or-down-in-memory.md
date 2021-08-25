---
title: 在内存中向上或向下翻页 | Microsoft Docs
description: 了解在 Visual Studio 中进行调试时，如何在内存中向上或向下翻页，以在“内存”窗口或“反汇编”窗口中查看内存内容。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugger, paging up or down in memory
- memory, paging up or down
- Disassembly window, viewing memory space
- Memory window, paging up or down in memory
ms.assetid: 50b30a68-66f6-43f8-a48b-59ce12c95471
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 9cbf5ddba4244481efe42fe0818989b2a384d092
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122128216"
---
# <a name="how-to-page-up-or-down-in-memory"></a>如何：在内存中向上或向下翻页

在“内存”窗口或“反汇编”窗口中查看内存内容时，可以使用垂直滚动条在内存空间中上下移动 。

### <a name="to-page-up-or-down-in-memory"></a>在内存中向上或向下翻页

1. 若要向下翻页（移动到较高的内存地址），请单击滚动框下方的垂直滚动条。

2. 若要向上翻页（移动到较低的内存地址），请单击滚动块上方的垂直滚动条。

   您还将注意到垂直滚动条以非标准方式工作。 如今的计算机地址空间非常大，抓取滚动条滚动块并将其移动到任意位置，就容易找不到地址。 为此，滚动块就像“装了弹簧”，总是保持在滚动条的中心。 在本机代码应用程序中，可以向上或向下翻页，但不能随便滚动。

   在托管应用程序中，反汇编限于一个函数，因而您可以正常滚动。

   可以注意到，较高的地址出现在窗口的底部。 若要查看较高的地址，必须向下移动而不是向上移动。

#### <a name="to-move-up-or-down-one-instruction"></a>向上或向下移动一个指令

- 单击垂直滚动条顶部或底部的箭头。

## <a name="see-also"></a>请参阅
- [“内存”窗口](../debugger/memory-windows.md)
- [如何：使用“反汇编”窗口](../debugger/how-to-use-the-disassembly-window.md)
- [查看调试器中的数据](../debugger/viewing-data-in-the-debugger.md)