---
title: 如何：打开多个解决方案
description: 了解如何打开 Visual Studio for Mac 的多个解决方案，以及如何打开应用程序的多个实例。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 07/19/2018
ms.assetid: 592BA4E3-8DEF-4FCD-8BA0-519A4CEEE03E
ms.custom: video
ms.topic: how-to
ms.openlocfilehash: 346c695cf5c0fe9781dfad026811a87add2e0002
ms.sourcegitcommit: 0841d3f610bd2af4af1cf07dd9d31d1e0629b193
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2021
ms.locfileid: "123961759"
---
# <a name="open-multiple-solutions-or-instances-of-visual-studio-for-mac"></a>打开 Visual Studio for Mac 的多个解决方案或实例

默认情况下，Mac 上的所有应用程序（包括 Visual Studio for Mac）都是单实例应用。 也就是说，如果要使用的应用程序已经打开（由停靠栏中图标下方的点指明），再次选择此图标会打开正在运行的实例，而不是新实例。 如果需要应用程序的其他实例，可提示系统打开，如[下一部分](#open-a-second-instance-of-visual-studio-for-mac)中所述。

此外，打开解决方案时，默认行为是在新工作区中打开解决方案并关闭当前工作区（如有必要）。 可通过保持当前工作区打开来替代此默认行为，如[打开第二个解决方案](#open-a-second-solution-inside-a-single-instance)部分中所述。

## <a name="open-a-second-instance-of-visual-studio-for-mac"></a>打开 Visual Studio for Mac 的第二个实例

若要打开集成开发环境 (IDE) 的第二个实例，请打开“终端”应用程序，并输入下面的代码行：

```bash
open -n "/Applications/Visual Studio.app"
```

## <a name="open-a-second-solution-inside-a-single-instance"></a>在单实例中打开第二个解决方案

要在第一个解决方案旁边打开第二个解决方案，请使用以下步骤：

1. 在第一个解决方案已打开后，依次选择“文件” > “打开”。
2. 浏览文件系统，查找现有解决方案。
3. 依次选择 .sln 文件和“选项”：

    ![突出显示 .sln 文件和“选项”的 Visual Studio for Mac 屏幕截图](media/open-multiple-solutions-image3.png)

4. 取消选中“关闭当前工作区”框：

    ![已清除“关闭当前工作区”框的“选项”对话框屏幕截图](media/open-multiple-solutions-image1.png)

5. 选择“打开”，在 Solution Pad 中打开第二个解决方案。

或者，如果最近打开过解决方案，可按照以下步骤操作：

1. 依次转到“文件” > “最近打开的解决方案”。

    ![“最近打开的解决方案”菜单屏幕截图](media/open-multiple-solutions-image2.png)

1. 按住 Ctrl 键并选择解决方案。 此组合操作会在 Solution Pad 中打开第二个解决方案。

## <a name="related-video"></a>相关视频

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Work-With-Multiple-Solutions/player]
