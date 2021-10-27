---
title: “调试会话的可执行文件”对话框 | Microsoft Docs
description: 若要调试 DLL，必须指定可执行文件以调用 DLL。 了解未指定可执行文件时显示的对话框。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.exefordebug
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- executable files, specifying when debugging
- DLLs, debugging
- debugger, Executable for Debugging Session dialog box
- Executable for Debugging Session dialog box
ms.assetid: c0ddbe32-b99f-4425-acf1-f48842804f56
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 528a34c6f9d7ecbe4ab3254e779441a4bc307239
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126735608"
---
# <a name="executable-for-debugging-session-dialog-box"></a>“调试会话的可执行文件”对话框

当您尝试调试没有指定可执行文件的 DLL 时，将出现该对话框。 Visual Studio 不能直接启动 DLL。 相反，Visual Studio 会启动指定的可执行文件。 在可执行文件调用 DLL 时，可以调试该 DLL。

 可执行文件名称 输入调用正在调试的 DLL 的可执行文件的路径名。

 可访问项目的 URL (仅限 ATL Server) 如果正在调试 ATL Server DLL，则输入可以找到项目的 URL。

 输入后，这些设置存储在“属性页”项目中，因此，在后续调试会话中，不必再输入这些设置。 如果需要更改设置，您可以打开“属性页”并更改值。 有关为调试会话指定可执行文件的详细信息，请参阅[调试 DLL](../debugger/how-to-debug-from-a-dll-project.md)。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中进行调试](../debugger/index.yml)
- [初探调试器](../debugger/debugger-feature-tour.md)