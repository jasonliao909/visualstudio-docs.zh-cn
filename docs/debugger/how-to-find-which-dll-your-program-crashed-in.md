---
title: 查找导致程序崩溃的 DLL | Microsoft Docs
description: 使用“模块”窗口标识当应用程序故障时哪个外部 DLL 处于活动状态。 可针对系统 DLL 或其他人的代码执行此操作。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.debug.dll
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, DLL crashes
- Module List dialog box
- errors [debugger], DLL crashes
- Modules window
- debugging [Visual Studio], DLL crashes
- DLLs, load order of
ms.assetid: ecf62568-8b65-4a41-b8a4-e962ff2dfb71
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: a1a76976dc630074768bb14bc39fc480278962fa
ms.sourcegitcommit: 541871db9065c4fb1b21c24f980c563991b183c7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2021
ms.locfileid: "129431349"
---
# <a name="how-to-find-which-dll-your-program-crashed-in-c-c-visual-basic-f"></a>如何：查找导致程序崩溃的 DLL（C#、C++、Visual Basic、F#）

 如果应用程序在调用系统 DLL 或别人的代码时出现崩溃，则需要找出在崩溃发生时哪个 DLL 是活动的。 如果在自己的程序外部的 DLL 中出现崩溃，可以使用“模块”窗口标识该位置。

### <a name="to-find-where-a-crash-occurred-using-the-modules-window"></a>使用“模块”窗口查找崩溃发生的位置

1. 记下崩溃发生的地址。

    如果错误消息中未显示地址，则可能需要使用其他方法来标识 DLL。 如果怀疑是系统 DLL，则可以在调试时从 Microsoft 符号服务器[加载符号](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。 否则，可能需要使用堆信息[创建转储文件](../debugger/using-dump-files.md)。 可以使用各种工具来创建转储文件。

2. 在“调试”菜单上选择“窗口”，再单击“模块”  。

3. 在“模块”窗口中，查找“地址”列 。 可能需要使用滚动条来查看。

4. 单击列顶部的“地址”按钮按地址对 DLL 进行排序。

5. 细查排序的列表，找到其地址包含崩溃位置的 DLL。

6. 查看“名称”和“路径”列，查看 DLL 的名称和路径 。

## <a name="see-also"></a>请参阅
- [调试 DLL 项目](../debugger/debugging-dll-projects.md)
- [如何：使用“模块”窗口](../debugger/how-to-use-the-modules-window.md)