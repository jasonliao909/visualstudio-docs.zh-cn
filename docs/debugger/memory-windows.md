---
title: 在调试器中查看变量的内存 | Microsoft Docs
description: 了解如何在调试时使用“内存”窗口来查看应用正在使用的内存空间。 其他窗口显示了变量及其在内存中的位置。
ms.custom: SEO-VS-2020
ms.date: 10/04/2018
ms.topic: how-to
f1_keywords:
- vs.debug.memory
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- Memory window
- strings [Visual Studio], viewing
- debugger [Visual Studio], Memory window
- memory [Visual Studio], debugging
- debugging [Visual Studio], Memory window
- buffers, viewing
ms.assetid: 7f7a0439-10e4-4966-bb2d-51f04cda4fe2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 8a725ced36f886054094cc0ce97da34a1a74d3da
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126736131"
---
# <a name="use-the-memory-windows-in-the-visual-studio-debugger-c-c-visual-basic-f"></a>在 Visual Studio 调试器中使用“内存”窗口（C#、C++、Visual Basic、F#）

在调试期间，“内存”窗口显示应用使用的内存空间。

调试器窗口（如“监视”、“自动”、“局部变量”和“快速监视”对话框   ）会显示存储于内存中特定位置的变量。 “内存”窗口显示总体概况。 内存视图对于检查大片的数据（如缓冲区和大的字符串）很方便，这些内容在其他窗口中显示得不太好。

“内存”窗口并不局限于显示数据。 该窗口可以显示内存空间中的任何内容，包括数据、代码以及未分配内存中的无用随机位。

“内存”窗口对于脚本或 SQL 调试不可用。 这些语言无法识别内存概念。

## <a name="open-a-memory-window"></a>打开“内存”窗口

与其他调试器窗口一样，“内存”窗口仅在调试会话期间可用。

>[!IMPORTANT]
>若要启用“内存”窗口，必须在“工具” > “选项”（或“调试” > “选项”）>“调试” > “常规”中选择“启用地址级调试”。

**打开“内存”窗口**

1. 确保在“工具” > “选项”（或“调试” > “选项”）>“调试” > “常规”中选择“启用地址级调试”。

1. 通过选择绿色箭头，按 F5，或选择“调试” > “启动调试”来启动调试。

2. 在“调试” > “窗口” > “内存”下，选择“内存 1”、“内存 2”、“内存 3”或“内存 4”。 （某些版本的 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 仅提供一个“内存”窗口。）

## <a name="move-around-in-the-memory-window"></a>在“内存”窗口中四处移动

计算机的地址空间很大，在“内存”窗口中滚动可能会轻易地失去位置。

较高的内存地址显示在窗口的底部。 若要查看较高的地址，请向下滚动。 若要查看较低的地址，请向上滚动。

通过使用拖放操作或在“地址”字段中输入地址，可以立即在“内存”窗口中转到指定地址。 “地址”字段接受字母数字地址和计算结果为地址的表达式，如 `e.User.NonroamableId`。

若要强制立即重新计算“地址”字段中的表达式，请选择圆角箭头“ 自动重新计算”图标。

默认情况下，“内存”窗口将“地址”表达式视为实时表达式，它们会在应用运行时重新计算 。 实时表达式可能十分有用，例如，可用于查看指针变量所涉及的内存。

若要使用拖放操作移动到内存位置，请执行以下操作：

1. 在任一调试器窗口中，选择内存地址或选择包含内存地址的指针变量。

2. 将地址或指针拖动到“内存”窗口中。 该地址随后会出现在“地址”字段中，“内存”窗口将调整为在顶部显示该地址。

若要通过在“地址”字段中输入内存位置来移动到该位置，请执行以下操作：

- 在“地址”字段中键入或粘贴地址或表达式，然后按 Enter，或从“地址”字段中的下拉列表中选择它。 “内存”窗口将调整为在顶部显示该地址。

## <a name="customize-the-memory-window"></a>自定义“内存”窗口

默认情况下，内存内容以十六进制格式显示为 1 字节整数，窗口宽度会确定所显示的列数。 可以自定义“内存”窗口显示内存内容的方式。

**更改内存内容的格式：**

- 在“内存”窗口中右键单击，然后从上下文菜单中选择所需的格式。

**更改“内存”窗口中的列数：**

- 选择“列”字段旁的下拉箭头，然后选择要显示的列数，或选择“自动”以基于窗口宽度自动调整。

如果不希望“内存”窗口的内容随着应用运行而更改，则可以关闭实时表达式计算功能。

**切换活动计算：**

- 在“内存”窗口中右键单击，然后在上下文菜单中选择“自动重新计算”。

  >[!NOTE]
  >实时表达式计算是一个开关，默认情况下处于打开状态，因此选择“自动重新计算”会将其关闭。 再次选择“自动重新计算”会重新打开。

可以隐藏或显示“内存”窗口顶部的工具栏。 当工具栏隐藏时，无法访问“地址”字段或其他工具。

切换工具栏显示：

- 在“内存”窗口中右键单击，然后在上下文菜单中选择“显示工具栏”。 工具栏将出现或不出现，具体取决于它先前的状态。

## <a name="follow-a-pointer-through-memory"></a>跟踪内存中的指针

在本机代码应用中，可以将寄存器名称用作实时表达式。 例如，可以使用堆栈指针跟踪堆栈。

**跟踪内存中的指针：**

1. 在“内存”窗口“地址”字段中，输入处于当前范围内的指针表达式。 根据所使用的语言，可能必须取消引用指针。

2. 按 **Enter**。

   当使用调试命令（如“单步执行”）时，“地址”字段中和“内存”窗口顶部显示的内存地址将随指针更改而自动更改。

## <a name="see-also"></a>请参阅
- [查看调试器中的数据](../debugger/viewing-data-in-the-debugger.md)