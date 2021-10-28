---
title: 关于“寄存器”窗口 | Microsoft Docs
description: 了解 Visual Studio 中的“寄存器”窗口，该窗口仅在“选项”对话框的“调试”节点中启用了地址级调试后才可用。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- Registers window, about Registers window
- debugging [Visual Studio], Registers window
ms.assetid: ab354047-053e-4f94-8ac1-26e761442b6f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 0ae8733c30a299123e1f0d21a43be943a24a5277
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126737188"
---
# <a name="about-the-registers-window-in-visual-studio-c-c-visual-basic-f"></a>关于 Visual Studio 中的“寄存器”窗口 (C#、C++、Visual Basic、F#)

只有在“选项”对话框中的“调试”节点下启用了地址级调试后，“寄存器”窗口才可用。

 寄存器是处理器（CPU）中的特殊区域，用于存储处理器需要当前处理的少量数据。 编译或解释源代码时会生成一些指令，这些指令根据需要将数据从内存移动到寄存器或反之。 相对于访问内存数据，访问寄存器数据非常快。那些允许处理器将数据保留在寄存器并多次访问的代码，比起那些需要处理器不断加载和卸载寄存器的代码执行速度快得多。 为了方便编译器将数据保存在寄存器中并实现其他优化，应避免使用全局变量而尽可能地依靠局部变量。 称以此方式编写的代码具有良好的引用局部性。 在某些语言中，如 C/C++ 中，程序员可以声明寄存器变量，它告诉编译器在所有时间尽可能地将该变量保留在寄存器中。 有关更多信息，请参阅 [Register 关键字](/previous-versions/482s4fy9(v=vs.140))。

 寄存器可分为两类：通用寄存器和专用寄存器。 通用寄存器保存用于一般操作（如将两数相加或引用数组中的元素）的数据。 专用寄存器具有特定用途和专门的意义。 堆栈指针寄存器是一个好例子，处理器利用它跟踪程序的调用堆栈。 程序员可能不会直接处理堆栈指针，但它对于程序正确运行至关重要。 没有堆栈指针，处理器在函数调用完成后将不知道返回何处。

 大多数通用寄存器只保存一个数据元素。 例如单个整数、浮点数或某一数组元素。 一些新的处理器具有较大的寄存器，称为向量寄存器，可以保存一个小的数组。 由于它们可以保存较多数据，向量寄存器对于涉及数组的运算处理得非常快。 向量寄存器最初是用在昂贵的、高性能超级计算机上，但现在也用于微处理器，它们在密集的图形操作中具有很大优势。

 一个处理器通常有两组通用寄存器，一组针对浮点运算进行优化，一组针对整数运算进行优化。 因此，它们被称为浮点寄存器和整数寄存器。

 托管代码在运行时被编译为用来访问微处理器的物理寄存器的本机代码。 对于公共语言运行时或本机代码，“寄存器”窗口可以显示这些物理寄存器信息。 而对于脚本或 SQL 应用程序，“寄存器”窗口不会显示寄存器信息，因为脚本或 SQL 都是不支持寄存器概念的语言。

 有关显示“寄存器”窗口的更多信息，请参阅[使用寄存器窗口](../debugger/how-to-use-the-registers-window.md)。

 当查看“寄存器”窗口时，会看到 `EAX = 003110D8` 等条目。

 `=` 号左边的符号是寄存器名称（这里是 `EAX`）。 符号“`=`”右边的数字表示寄存器内容。

 通过“寄存器”窗口不仅可以看到寄存器的内容，还可以完成更多任务。 当本机代码处于中断模式时，可以单击寄存器内容并更改其值。 这不是可以随意做的事。 除非理解正在编辑的寄存器和它所包含的内容，草率编辑很可能导致程序崩溃或其他不良后果。 很遗憾，详细介绍各种 Intel 和 Intel 兼容处理器的寄存器组超出了本文的范围。

## <a name="register-groups"></a>寄存器组

为避免杂乱，“寄存器”窗口中的寄存器按组显示。 右键单击“寄存器”窗口，可以看到一个包含组列表的快捷菜单，可根据需要显示或隐藏它。

## <a name="register-flags"></a>寄存器标志

对于 Intel x86 处理器，你可能会在“寄存器”窗口中看到以下标志。 调试会话期间，你还可以编辑这些标志。

|Flag|设置值|
|-|-|
|溢出|OV = 1|
|方向|UP = 1|
|中断|EI = 1|
|Sign|PL = 1|
|零|ZR = 1|
|辅助 Carry|AC = 1|
|Parity|PE = 1|
|Carry|CY = 1|

## <a name="see-also"></a>请参阅
- [如何：使用“寄存器”窗口](../debugger/how-to-use-the-registers-window.md)
- [初探调试器](../debugger/debugger-feature-tour.md)