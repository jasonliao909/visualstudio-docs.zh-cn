---
title: 图形事件调用堆栈 | Microsoft Docs
description: 查看 Visual Studio 图形分析器中的图形事件调用堆栈，以映射有问题的图形事件和应用的源代码之间的关系。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.graphics.callstack
ms.assetid: 8a30168d-8b39-4de1-b094-c7356ba101a3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 29bc023dcc4eae885746396f77b27f27188ada61
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126642001"
---
# <a name="graphics-event-call-stack"></a>图形事件调用堆栈
Visual Studio 图形分析器中的图形事件调用堆栈可帮助你映射有问题的图形事件和应用的源代码之间的关系。

 这就是“事件调用堆栈”窗口：

 ![继续 DrawIndexed 事件的调用堆栈。](media/gfx_diag_demo_graphics_event_call_stack_orientation.png "gfx_diag_demo_graphics_event_call_stack_orientation")

## <a name="understanding-the-graphics-event-call-stack"></a>了解图形事件调用堆栈
 你可以使用“事件调用堆栈”来了解导致特定 Direct3D 事件的执行流。 它类似于 Visual Studio 调用堆栈窗口，不同之处在于，它不会显示正在运行的应用中当前线程的当前调用堆栈，而是在选定的 Direct3D 事件发生时显示存在的调用堆栈。 你可以从“事件调用堆栈”跳转到选定的 Direct3D 事件的调用站点，以检查周围的代码。

 通过使用“事件调用堆栈”标识问题事件源自的代码路径，你可以使用你的代码库知识推导出问题可能的来源，或者可以在应用源代码中添加断点，以便使用传统调试技术检查应用或事件参数的状态是如何导致事件错误行为的。 这一检查可以帮助你在源代码中找到问题，这些问题只显示为呈现问题。

### <a name="graphics-event-call-stack-information"></a>图形事件调用堆栈信息
 调用堆栈不支持预框架事件或用户定义的事件。 图形事件的调用堆栈以表格形式显示。

|列|说明|
|------------|-----------------|
|**Name**|包含调用站点的函数的唯一标识符号。 这个函数的调试符号在它可用时显示；否则将显示函数偏移量。|
|**文件**|包含调用站点的源代码文件或库文件的文件名。|
|**位置**|调用站点行号。|

### <a name="links-to-graphics-objects"></a>指向图形对象的链接
 若要了解选定的图形事件，你可能需要了解与它关联的 Direct3D 对象的有关信息。 “图形事件调用堆栈”窗口提供了指向这一信息的链接。

## <a name="see-also"></a>请参阅
- [演练：因顶点着色而缺少对象](walkthrough-missing-objects-due-to-vertex-shading.md)