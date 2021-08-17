---
title: 使用工具窗口创建扩展|Microsoft Docs
description: 了解如何使用 VSIX 项目模板和自定义工具窗口项模板创建具有工具窗口的扩展。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: how-to
ms.assetid: 585b0a3a-f85b-4f92-81bb-9ca499bb8a89
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 2b597f9b84cc4dd6754e48b83adfcef722b9fc352841f579eef1beb07b0f8230
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121434763"
---
# <a name="create-an-extension-with-a-tool-window"></a>使用工具窗口创建扩展

此过程将学习如何使用 VSIX 项目模板和自定义工具 **窗口项模板** 创建具有工具窗口的扩展。

## <a name="prerequisites"></a>先决条件

 从 2015 Visual Studio开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

### <a name="create-a-tool-window"></a>创建工具窗口

1. 创建名为 **FirstWindow** 的 VSIX 项目。 可以通过搜索"vsix"在"新建Project"找到 VSIX 项目模板。 

2. 项目打开时，添加名为 **MyWindow** 的工具窗口项模板。 在“解决方案资源管理器”中，右键单击项目节点并选择“添加” > “新建项”  。 在"**添加新项"对话框中**，转到 **"Visual C#**  >  **扩展性"，** 然后选择"**自定义工具窗口"。** 在 **窗口底部的** "名称"字段中，将工具窗口文件名更改为 *MyWindow.cs*。

3. 生成项目并启动调试。

   将显示该实例Visual Studio实例。 有关实验实例的信息，请参阅 [实验实例](../extensibility/the-experimental-instance.md)。

4. 在实验实例中，转到"**查看**  >  **其他Windows"。**

   应会看到 **MyWindow** 的菜单项。 请单击此按钮。

   应会看到标题为 **MyWindow** 的工具窗口，以及一个显示" **单击我！"的按钮。**
