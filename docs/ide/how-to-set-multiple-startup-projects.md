---
title: 如何：设置多个启动项目
description: 了解如何在 Visual Studio 中指定启动调试器时多个项目的运行方式。
ms.custom: SEO-VS-2020
ms.date: 06/21/2017
ms.topic: how-to
helpviewer_keywords:
- startup projects, setting multiple startup projects
ms.assetid: 6131eb80-8745-4eb9-bdab-433e69b41651
ms.technology: vs-ide-compile
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8816ec16e1424ab6b7a27e16c750085a794b3cdf
ms.sourcegitcommit: 99e0146dfe742f6d1955b9415a89c3d1b8afe4e1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2021
ms.locfileid: "134554021"
---
# <a name="how-to-set-multiple-startup-projects"></a>如何：设置多个启动项目

Visual Studio 允许你在按 **f5** (按下 "调试") 时运行多个项目，或按 **Ctrl** + **F5** ("启动但不调试) "，或使用工具栏按钮启动应用程序。 通过这种方式，您可以启动多个相互依赖的站点、应用程序或服务，以便在调试会话期间正常运行，或在本地运行和测试。

## <a name="to-set-multiple-startup-projects"></a>设置多个启动项目

1. 在解决方案资源管理器中，选择解决方案（最高层节点）。

2. 选择解决方案节点的上下文（右键单击）菜单，然后选择“属性”。 “解决方案属性页”对话框随即显示。

3. 展开“通用属性”节点，然后选择“启动项目”。

4. 选择“多个启动项目”选项并设置适当的操作。

:::moniker range=">=vs-2019"

## <a name="example"></a>示例

下面的示例演示了一个解决方案 WebFrontEndA，其中包含三个项目、一个前端网站、一个 Web API 项目和一个 Docker Compose 项目。 以下屏幕截图显示了如何启动三个项目中的两个：一个用于调试，另一个不包含：

![解决方案属性页的屏幕截图。](media/vs-2022/startup-projects.png)

在此示例和任何其他 Docker Compose 情况下，如果选择 `docker-compose` 作为单个启动项目，则将使用另一种方法来指定要启动的项目或服务。 你将使用 Docker Compose 启动配置文件来确定要启动的服务，以及是否附加调试器，以及在 Visual Studio 中是否有不同的对话框用于配置该配置文件。 请参阅 [启动服务的子集](../containers/launch-profiles.md)。 " **解决方案属性页** " 对话框仅用于非容器化解决方案，或在 *不* 使用 Docker Compose 来管理启动时使用。
:::moniker-end

## <a name="see-also"></a>另请参阅

- [编译和生成](../ide/compiling-and-building-in-visual-studio.md)
- [使用解决方案和项目](../ide/creating-solutions-and-projects.md)
- [管理项目和解决方案属性](../ide/managing-project-and-solution-properties.md)
