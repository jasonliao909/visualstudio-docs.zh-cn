---
title: 导出和保存代码图
description: 了解如何将代码图另存为 Visual Studio 项目、图像或 XPS 文件的一部分。
ms.custom: SEO-VS-2020
ms.date: 05/16/2018
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: d6efe3f860749ac24e35af944122ec8a9d121f6039270117e7eb52eb57fcf6f7
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121410928"
---
# <a name="share-code-maps"></a>共享代码图

可以将代码图另存为作为 Visual Studio 项目的一部分、作为图像或 XPS 文件。

## <a name="share-a-code-map-with-other-visual-studio-users"></a>与其他 Visual Studio 用户共享代码图

使用“文件”  菜单保存代码图。

-或-

若要将地图保存为特定项目的一部分，请在地图工具栏上选择 "  >  **将" 移动 \<CodeMapName> 到**"" 共享 "，然后选择要在其中保存地图的项目。

![将映射移动到另一个项目中](../modeling/media/codemapsmovemapmenu.png)

Visual Studio 将映射保存为可与 Visual Studio Enterprise 和 Visual Studio Professional 的其他用户共享的 *.dgml* 文件。

> [!NOTE]
> 在与使用 Visual Studio Professional 的用户共享代码图之前，请确保展开所有组、显示隐藏节点和跨组链接，并检索希望其他人在你的代码图上查看的所有已删除的节点。 否则，其他用户将无法查看这些项目。
>
> 保存建模项目中的代码图或从建模项目复制到其他位置的代码图时，可能会出现以下错误：
>
> “无法在项目目录外保存 *fileName* 。 不支持链接的项。”
>
> Visual Studio 将显示错误，但还是会创建保存的版本。 若要避免错误，请在建模项目外创建代码图。 然后，可将图形保存到所需的位置。 若只是将文件复制到解决方案中的其他位置，那么尝试保存图形将不起作用。

## <a name="export-a-code-map-as-an-image"></a>将代码图导出为图像

将代码图导出为图像时，可以将其复制到其他应用程序，如 Microsoft Word 或 PowerPoint。

1. 在代码图工具栏上，选择 "**共享**  >  **电子邮件" 作为图像** 或 **复制图像**。

2. 将该图像粘贴到另一个应用程序中。

## <a name="export-the-map-as-an-xps-file"></a>将地图作为 XPS 文件导出

将代码图导出为 XPS 文件时，可以在 XML 或 XAML 查看器（如 Internet Explorer）中查看它。

1. 在代码图工具栏上，选择"  >  **以便携式 xps 共享电子邮件**" 或 "**另存为可移植 xps**"。

2. 浏览到你要保存文件的位置。

3. 对代码图命名。 请确保将 " **保存类型** " 框设置为 " **xps 文件 (.xps \*)**。 选择 **“保存”** 。

## <a name="see-also"></a>请参阅

- [使用代码图映射依赖关系](../modeling/map-dependencies-across-your-solutions.md)
