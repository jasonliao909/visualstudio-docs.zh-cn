---
title: 设置多个启动项目
description: 本文介绍如何设置多个要在运行或调试时启动的项目。
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 11/09/2020
ms.topic: how-to
ms.prod: visual-studio-mac
ms.assetid: fd354fff-ce6b-4505-a815-84a2311e39ba
ms.openlocfilehash: d219d8aca5c9af49ff8f4f0e0490f0bd794b56d9
ms.sourcegitcommit: 965372ad0d75f015403c1af508080bf799914ce3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2022
ms.locfileid: "135805502"
---
# <a name="set-multiple-startup-projects"></a>设置多个启动项目

通过 Visual Studio for Mac 可指定在调试或运行解决方案时应启动多个项目。

## <a name="to-set-multiple-startup-projects"></a>设置多个启动项目

1. 在解决方案窗口中，选择解决方案（最高层节点）。

2. 右键单击解决方案节点，然后选择“设置启动项目”：

   ![选择设置启动项目](media/startup-proj-ctx-menu.png)

3. 随即打开“创建解决方案运行配置”对话框。 通过此对话框，可为解决方案创建新的命名解决方案运行配置。 可以使用任何喜欢的名称。 默认名称为 `Multiple Projects`。

   ![“创建解决方案运行配置”对话框](media/create-sln-run-config.png)

4. 选择“创建运行配置”。 “解决方案选项”对话框将与所选的新“解决方案运行配置”一起打开：

   ![“解决方案选项”对话框](media/sln-options-run-config-multi-projects.png)

5. 选择从 Visual Studio for Mac 调试或运行应用时要启动的项目：

   ![包含所选项目的“解决方案选项”对话框](media/sln-options-run-config-multi-projects-configured.png)

6. 选择“确定”。 新的“解决方案运行配置”将设置为可用的运行配置：

   ![将带有多个项目的解决方案配置为在调试或运行时启动](media/startup-project-configured.png)

   现在两个项目已配置为启动，这通过两个项目在解决方案窗口中显示为粗体来表示。 在工具栏中，将新的运行配置设置为当前的“解决方案运行配置”。

## <a name="next-steps"></a>后续步骤

- [在 Visual Studio for Mac 中编译和生成](compiling-and-building.md)
- [了解生成配置](configurations.md)
