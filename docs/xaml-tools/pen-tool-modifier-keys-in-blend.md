---
title: “笔”工具修改键
titleSuffix: Blend for Visual Studio
description: 了解使用 Pen 工具创建路径时Blend for Visual Studio中的 Pen 工具修饰符键，以访问用于修改路径的命令。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: c3ab14c6-a320-46db-a6b3-7fd1ca261587
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-xaml-tools
ms.workload:
- multiple
ms.openlocfilehash: 01e861e21540fdfba9ac869838c3f080e2fe2422
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122037806"
---
# <a name="pen-tool-modifier-keys-in-blend-for-visual-studio"></a>Blend for Visual Studio 中的“笔”工具修改键

下表列出了在使用“笔”工具 ![笔工具](../designers/media/d514358f-185a-412f-a55d-36633b25dc8a.png) 创建路径时可用于修改此路径的快捷方式。 “笔”工具还可用于在现有路径上添加或删除点，或联接两个现有路径。

|为了执行此操作|操作|指针|
| - |-------------|-------------|
|创建一个点来开始绘制直线线段|单击以创建新点|![创建一个点来开始绘制直线线段](../designers/media/0bfb1b71-80ac-4ad4-aed8-40e09f8b7ab8.png)<br /><br /> “钢笔”指针|
|创建一个点来开始绘制曲线线段|单击以创建新点，然后在松开鼠标按钮前拖动以调整切线图柄|![创建一个点来开始绘制曲线线段](../designers/media/0bfb1b71-80ac-4ad4-aed8-40e09f8b7ab8.png)<br /><br /> “钢笔”指针|
|在没有平滑限制的情况下调整最后的切线，使您生成尖锐的角|单击以创建新点，然后在松开鼠标按钮之前按 **Alt**|![在没有平滑限制的情况下调整最后一根切线](../designers/media/317e5475-b70c-489f-9477-110a98639ade.png)<br /><br /> “钢笔”调整指针|
|拆分最后一个切线，以便切线终结点独立操作，使您生成尖锐的角|单击以创建新点，然后按住 **Alt** 并拖动，然后松开鼠标按钮|![拆分最后一根切线，使切线终点独立存在](../designers/media/317e5475-b70c-489f-9477-110a98639ade.png)<br /><br /> “钢笔”调整指针|
|以 15 度的增量将切线终结点绕新点移动|单击以创建新点，然后按住 **Shift** Alt 并拖动 + ，然后松开鼠标按钮|![以 15 度的增量将切线终结点绕新点移动](../designers/media/317e5475-b70c-489f-9477-110a98639ade.png)<br /><br /> “钢笔”调整指针|
|将一个终结点处的切线减小为零长度|单击该终结点|![将一个终结点处的切线减小为零长度](../designers/media/317e5475-b70c-489f-9477-110a98639ade.png)<br /><br /> “钢笔”调整指针|
|向现有路径添加新点|单击您需要新点的位置处的路径|![向现有路径添加新点](../designers/media/b004ad5a-33a4-46ae-81c0-20be0d819332.png)<br /><br /> “钢笔”插入指针|
|从路径删除一个点|悬浮在现有点上并单击|![删除路径中的点](../designers/media/08a64b78-f3df-4730-8169-c56b5631b071.png)<br /><br /> “钢笔”删除指针|
|结束具有尖锐角的路径|单击起始点|![结束具有尖角的路径](../designers/media/a12fd3b4-a553-4762-b01c-c35efa594362.png)<br /><br /> “钢笔”结束指针|
|结束边角处具有平滑曲线的路径|单击起始点并在松开鼠标按钮前拖动以修改切线图柄|![结束边角处具有平滑曲线的路径](../designers/media/a12fd3b4-a553-4762-b01c-c35efa594362.png)<br /><br /> “钢笔”结束指针|
|在联接两个路径时创建尖锐的角|选择两个路径，单击“笔”工具，并单击其中一个路径的终结点，然后单击另一路径的终结点|![在联接两个路径时创建尖锐的角](../designers/media/bd12dfa4-112e-4f37-9765-3479e6b69894.png)<br /><br /> “钢笔”联接指针|
|在联接两个路径时创建平滑的角|选择两个路径，单击“笔”工具，并单击其中一个路径的终结点，然后拖动另一路径的终结点|![在联接两个路径时创建平滑的角](../designers/media/bd12dfa4-112e-4f37-9765-3479e6b69894.png)<br /><br /> “钢笔”联接指针|
|创建一个新路径|按住 **Ctrl** 并单击上一路径之外以停止向上一路径添加点，然后单击或拖动希望新路径开始的地方|![创建一个新路径](../designers/media/69758176-5f53-465b-808c-f13fd1a0b3f2.png)<br /><br /> “钢笔”开始指针|

## <a name="see-also"></a>请参阅

- [“美工板”修改键](artboard-modifier-keys-in-blend.md)
- [路径选择工具修饰符键](direct-selection-tool-modifier-keys-in-blend.md)
- [绘制形状和路径](draw-shapes-and-paths.md)