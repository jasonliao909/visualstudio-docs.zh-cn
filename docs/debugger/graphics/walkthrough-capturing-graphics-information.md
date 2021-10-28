---
title: 演练：捕获图形信息 | Microsoft Docs
description: 了解如何使用 Visual Studio 图形诊断从 Direct3D 应用中手动捕获图形信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 48f12f6e-57b4-48ec-a145-89fa71a42424
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: fd22f1e5f2cdd8cc01df164b654691b2fd8ca167
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126736739"
---
# <a name="walkthrough-capturing-graphics-information"></a>演练：捕获图形信息
本演练演示了如何使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 图形诊断从 Direct3D 应用手动捕获图形信息。

 此演练阐释了以下任务：

- 将图形诊断挂接到你的应用

- 捕获图形信息

## <a name="capturing-graphics-information"></a>捕获图形信息
 若要使用图形诊断工具，首先，你必须捕获它所依赖的图形信息。 若要启用捕获，请使用“启动诊断”  命令将图形诊断在启动时挂接到你的应用。

#### <a name="to-enable-the-capture-of-graphics-information-after-a-project-or-solution-is-loaded"></a>在加载项目或解决方案后启用图形信息捕获

1. 在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]中，为你希望从中捕获图形信息的应用加载项目或解决方案文件。

2. 在“图形诊断”工具栏上，选择“启动诊断” 。

#### <a name="to-enable-the-capture-of-graphics-information-without-loading-a-project-or-solution"></a>不加载项目或解决方案而启用图形信息捕获

1. 在菜单栏上，依次选择 **“文件”** 、 **“打开”** 和 **“项目/解决方案”** 。 此时将出现“打开项目”  对话框。

2. 不为应用指定项目或解决方案文件，而是为其指定你希望从中捕获图形信息的可执行文件，然后选择“打开” 。

3. 在菜单栏上，依次选择 **“调试”** 、 **“图形”** 、 **“启动诊断”** 。

   在启动应用并且它呈现帧之后，您可捕获图形信息。

#### <a name="to-capture-graphics-information"></a>捕获图形信息

- 在“图形诊断”工具栏上，选择“捕获”  按钮。 ![图形捕获按钮图标](media/debuggingdirectxgraphics.png "DebuggingDirectXGraphics")

   \- 或 -

   当焦点位于应用上时，按 **Print Screen**。

  每次捕获有关帧的信息时，图形诊断都将记录 Direct3D 事件和关联的状态，并将该数据添加到图形日志。 将为每个图形诊断会话创建一个新图形日志。 有关图形日志的信息，请参阅[概述](overview-of-visual-studio-graphics-diagnostics.md)。

## <a name="next-steps"></a>后续步骤
 本演练演示了如何手动捕获图形信息。 下一步，请考虑此选项：

- 了解如何使用图形诊断工具分析捕获的图形信息。 请参阅[概述](overview-of-visual-studio-graphics-diagnostics.md)。

## <a name="see-also"></a>请参阅
- [Capturing Graphics Information](capturing-graphics-information.md)