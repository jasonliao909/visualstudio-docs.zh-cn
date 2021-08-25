---
title: 调试 COM 和 ActiveX | Microsoft Docs
description: 了解有关在 Visual Studio 中调试 COM 应用程序和 ActiveX 控件的提示。 了解有关 COM 服务器和容器调试的信息。 查找 COM 调试工具。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.com
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- COM, debugging
- debugging ActiveX applications
- debugging [Visual Studio], COM
- debugging COM containers
- ActiveX controls, debugging
ms.assetid: 3260b2a7-3239-493d-9271-aedf705c13c7
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: b44c0e7e7f9d128a204819ec964f45c264d4d715
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122081784"
---
# <a name="com-and-activex-debugging"></a>调试 COM 和 ActiveX
本节提供有关调试 COM 应用程序和 ActiveX 控件的提示。

## <a name="in-this-section"></a>本节内容
 [调试 COM 服务器和容器](../debugger/com-server-and-container-debugging.md) 叙述调试 COM 应用程序时的特殊注意事项。 问题包括：使用同一解决方案中的两个项目来调试 COM 服务器和容器，跟踪到跨越进程边界的调用中，在回调函数中设置断点，以及单步通过和单步执行容器和服务器。

 [如何：调试 ActiveX 控件](../debugger/how-to-debug-an-activex-control.md) 包含有关如何调试 ActiveX 控件的信息。 这包括：为调试会话指定容器以查看 ActiveX 控件中的代码的执行方式，调试数据绑定 ActiveX 控件，模拟特定容器，以及单步执行容器的代码。

 [COM 调试工具](../debugger/com-debugging-tools.md) 列出在调试 COM 应用程序时可能会用到的查看器和示例应用程序。

## <a name="related-sections"></a>相关章节
 [初探调试器](../debugger/debugger-feature-tour.md) 提供指向调试文档的较大章节的链接。 涉及的信息包括：调试器的新增功能、设置和准备、断点、处理异常、编辑并继续、调试托管代码、调试 C++ 项目、调试 COM 和 ActiveX、调试 DLL、调试 SQL，以及用户界面参考。

## <a name="see-also"></a>请参阅

- [调试器安全](../debugger/debugger-security.md)
- [COM 简介](/cpp/atl/introduction-to-com)
- [ActiveX 控件](/cpp/mfc/activex-controls)
- [SDI 服务器应用程序](com-server-and-container-debugging.md)