---
title: 如何：设置多个启动项目
description: 了解如何在 Visual Studio 中指定启动调试器时多个项目的运行方式。
ms.custom: SEO-VS-2020
ms.date: 12/21/2021
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
ms.openlocfilehash: b143a145360cd79f7ee4b2703776386e542e4b24
ms.sourcegitcommit: 00af065ac27d41339b31d96a630705509b70b6fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2022
ms.locfileid: "140764462"
---
# <a name="how-to-set-multiple-startup-projects"></a>如何：设置多个启动项目

Visual Studio，可以指定在按 **F5** (开始调试) 或 **CtrlF5**+ (启动而不调试) 时运行多个项目，或使用工具栏按钮启动应用程序。 这样，就可以启动多个站点、应用或服务，这些站点、应用或服务在调试会话期间可以正常工作，或者只是在本地运行和测试。

## <a name="to-set-multiple-startup-projects"></a>设置多个启动项目

1. 在解决方案资源管理器中，选择解决方案（最高层节点）。

2. 选择解决方案节点的上下文（右键单击）菜单，然后选择“属性”。 “解决方案属性页”对话框随即显示。

   ![解决方案属性页](media/vs-2022/solution-properties-startup-projects.png)

3. 展开“通用属性”节点，然后选择“启动项目”。

4. 选择“多个启动项目”选项并设置适当的操作。

:::moniker range=">=vs-2019"

## <a name="example"></a>示例

以下示例演示一个解决方案 WebFrontEndA，该解决方案包含三个项目、一个前端网站、一个 Web API 项目和一Docker Compose项目。 以下屏幕截图显示如何启动三个项目中的两个项目，一个使用调试，另一个不带调试：

![解决方案属性页的屏幕截图。](media/vs-2022/startup-projects.png)

在此示例和任何其他 `docker-compose` Docker Compose，如果选择 作为单个启动项目，但随后你将使用不同的方法指定要启动的项目或服务。 你将使用一Docker Compose启动配置文件来确定要启动的服务，以及是否附加调试器，并且该配置文件中Visual Studio不同的对话框。 请参阅 [启动服务的子集](../containers/launch-profiles.md)。 "**解决方案属性页**"对话框仅用于非容器化解决方案，或者未使用 Docker Compose管理启动。
:::moniker-end

## <a name="see-also"></a>另请参阅

- [编译和生成](../ide/compiling-and-building-in-visual-studio.md)
- [使用解决方案和项目](../ide/creating-solutions-and-projects.md)
- [管理项目和解决方案属性](../ide/managing-project-and-solution-properties.md)
