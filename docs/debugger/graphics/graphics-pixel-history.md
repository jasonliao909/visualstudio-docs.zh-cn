---
title: 图形像素历史记录 | Microsoft Docs
description: 通过查看特定像素的历史记录来故障排除呈现问题。 图形像素历史记录显示 Direct3D 事件的效果。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.graphics.pixelhistory
ms.assetid: 0a2cbde5-1ad9-487e-857c-a3664158c268
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: ed00f0616cc18ce9f2bc73ebbae0927e0c79e990
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126735600"
---
# <a name="graphics-pixel-history"></a>图形像素历史记录
Visual Studio 中的“图形像素历史记录”窗口可以帮助你了解，在游戏或应用的某个帧期间，Direct3D 事件如何对某一特定像素产生影响。

 下面是“像素历史记录”窗口：

 ![一个像素的历史记录中具有三个 Direct3D 事件。](media/gfx_diag_demo_pixel_history_orientation.png "gfx_diag_demo_pixel_history_orientation")

## <a name="understanding-the-pixel-history-window"></a>了解“像素历史记录”窗口
 通过使用“像素历史纪录”，你可以分析在某个帧期间，Direct3D 事件如何对呈现器目标的某一特定像素产生影响。 你可以将呈现问题准确定位到特定的 Direct3D 事件，即使后续事件 - 或同一个事件的后续基元 - 继续更改像素的最终颜色值。 例如，一个像素可能被错误呈现，然后被另一个半透明的像素遮盖，这样它们的颜色就会在帧缓冲区中相融合。 如果可用于指导你的只有呈现器目标的最终内容，这种问题将会很难诊断。

 “像素历史”窗口显示像素在所选帧过程中的完整历史记录。 窗口顶部的“最终帧缓存器”会显示出在帧的末尾写入帧缓冲区的颜色以及其他像素信息（例如像素所属的帧以及像素屏幕坐标。 该区域还包含“呈现 Alpha”复选框。 选中此复选框后，“最终帧缓存器”颜色和中间颜色值将会以一定的透明度呈现为棋盘样式。 如果清除复选框，颜色值的 Alpha 通道将被忽略。

 窗口的底部会显示可能影响像素颜色的事件，以及代表帧缓冲区中像素的初始和最终颜色值的“初始”和“最终”伪事件 。 初始颜色值由更改像素颜色的第一个事件确定（通常为 `Clear` 事件）。 像素的历史记录中始终存在这两个伪事件，即使没有其他事件影响到它。 当其他事件有可能影响到像素时，这些事件会显示在“初始”和“最终”事件之间 。 可将这些事件展开以查看它们的详细信息。 对于如清除呈现器目标之类的简单事件，事件的效果只是一个颜色值。 更复杂的事件，例如绘制调用，则生成可能会参与像素颜色构成的一个或多个基元。

 事件绘制的基元由它们的基元类型和索引以及对象的基元总计数来标识。 例如，标识符“(6214) 中的三角形 (1456)”表示该基元对应 6214 个三角形组成的对象中的第 1456 个三角形。 每个基元标识符的左侧的是一个图标，总结基元对像素产生的效果。 影响像素颜色的基元由填充了生成颜色的圆角矩形表示。 代表不可能对像素颜色产生影响的基元的图标指示了像素被排除的原因。 这些图标将在本文后面的[基元排除](#exclusion)一节中进行说明。

 你可以展开每个基元来检查像素着色器输出是如何与现有的像素颜色合并产生最后生成的颜色的。 你也可以从这里检查或调试与基元相关的像素着色器代码，也可以进一步展开顶点着色器节点来检查顶点着色器输入。

### <a name="primitive-exclusion"></a><a name="exclusion"></a> 基元排除
 如果基元被排除了影响像素颜色的可能性，造成这一排除的原因可能是多种的。 这个表格中所述的图标各代表一个原因：

|图标|排除原因|
|----------|--------------------------|
|![“深度测试失败”图标。](media/vsg_hist_icon_failed_depth.png "vsg_hist_icon_failed_depth")|由于没有通过深度测试，像素被排除。|
|![“剪式测试失败”图标。](media/vsg_hist_icon_failed_scissor.png "vsg_hist_icon_failed_scissor")|由于未通过剪式测试，像素被排除。|
|![“模具测试失败”图标。](media/vsg_hist_icon_failed_stencil.png "vsg_hist_icon_failed_stencil")|由于未通过模具测试，像素被排除。|

### <a name="draw-call-exclusion"></a>绘图调用排除
 如果绘图调用中的所有基元因未通过测试而不再影响呈现目标，则绘图调用将无法进行扩展，并且对应于排除原因的图标将显示在它的旁边。 绘图调用排除的原因与基元排除的原因类似，并且它们的图标也相似。

### <a name="viewing-and-debugging-shader-code"></a>查看和调试着色器代码
 你可以使用与着色器关联的基元下方的控件检查顶点着色器、外壳着色器、域着色器、几何着色器和像素着色器的代码，并对其进行调试。

##### <a name="to-view-a-shaders-source-code"></a>查看着色器源代码

1. 在“图形像素历史记录”窗口中，找到与要检查的着色器对应的绘图调用，并将其展开。

2. 在刚刚展开的绘图调用下面，选择一个演示你感兴趣的问题的基元，并将其展开。

3. 在感兴趣的基元下，点击着色器标题链接 - 例如，点击链接“顶点着色器 obj:30”查看顶点着色器源代码。

    > [!TIP]
    > 对象编号“obj:30”用于在整个图形分析器界面中（如对象表和“管道阶段”窗口中）标识此着色器。

##### <a name="to-debug-a-shader"></a>调试着色器

1. 在“图形像素历史记录”窗口中，找到与要检查的着色器对应的绘图调用，并将其展开。

2. 然后，在刚刚展开的绘图调用下面，选择一个演示你感兴趣的问题的基元，并将其展开。

3. 在感兴趣的基元下，选择“启动调试”。 进入 HLSL 调试器的此入口点默认为着色器对相应基元的首个调用 — 即着色器处理的第一个像素或顶点。 与基元关联的像素只有一个，而对折线和三角形的顶点着色器调用则有多个。

     要调试某一特定顶点的顶点着色器调用，请展开 VertexShader 标题链接并找到感兴趣的顶点，然后选择它旁边的“启动调试”。

### <a name="links-to-graphics-objects"></a>指向图形对象的链接
 如果要了解像素历史记录中的图形事件，你可能需要了解事件发生时设备状态的有关信息或事件所引用的 Direct3D 对象的有关信息。 对于像素历史记录中的各个事件，“图形像素历史记录”提供了指向当时设备状态和相关对象的链接。

## <a name="see-also"></a>请参阅
- [演练：因设备状态而缺少对象](walkthrough-missing-objects-due-to-device-state.md)
- [演练：调试因着色引起的呈现错误](walkthrough-debugging-rendering-errors-due-to-shading.md)