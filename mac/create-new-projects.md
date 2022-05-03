---
title: 创建新项目和解决方案
description: 本文介绍如何在 Visual Studio for Mac 中创建项目和解决方案
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 02/28/2022
ms.custom: devdivchpfy22
ms.topic: how-to
ms.assetid: 5880BB10-0A12-47E2-8A82-7A2D59C4D579
ms.openlocfilehash: c1fc6f8f4c02dc450c79da0e8a33c1a9952871d6
ms.sourcegitcommit: fcf47a9c356df7e9636bcab92186923e5c9b8892
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2022
ms.locfileid: "144495867"
---
# <a name="create-a-new-project"></a>创建新项目

 [!INCLUDE [Visual Studio for Mac](~/includes/applies-to-version/vs-mac-only.md)]

## <a name="opening-the-project-creation-dialog"></a>打开项目创建对话框

可通过多种方式在 Visual Studio for Mac 中创建新项目。 首次打开 Visual Studio for Mac 时，将显示启动窗口。 在此处，可以选择“ **新建** ”，转到项目创建屏幕。

> [!TIP]
> 此外，在启动窗口中，还可以打开并搜索最近的项目和解决方案。 还可以通过转到菜单栏并依次选择“文件”、“最近使用的解决方案”来打开最近使用的项目

![带有“创建新项目“的启动窗口](media/first-run-project.png)

如果 Visual Studio for Mac 已打开，并且已加载解决方案，可以通过转到菜单栏并依次选择“文件”、“新建解决方案”来创建新解决方案。 通过此方法创建新解决方案将关闭已加载的解决方案。

## <a name="creating-a-new-project"></a>创建新项目

默认情况下，“新建项目”对话框将按“最近使用”排序显示最近使用的模板。

如果不想使用最近的模板，可以从对话框左侧的类别中进行选择。 每个类别包含多个项目模板，你可以随意选择。 单击项目类型可查看屏幕右侧的描述。

![“新建项目”屏幕](media/project-creation-screen.png)

## <a name="configuring-your-new-project"></a>配置新项目

选择项目模板后，以下屏幕将引导你完成设置项目所需的任何配置步骤：可能会因项目类型而异。

所有项目都需要一个新项目以及存储文件的位置。 如果项目属于新解决方案，而不是将添加到现有解决方案，则还需要提供解决方案名称。

在此阶段，还可以选择配置 Git 源代码管理选项。 下图是配置 .NET Core 项目的最终步骤示例：

![配置新项目](media/configure-new-project.png)

## <a name="adding-additional-projects-to-a-solution"></a>将其他项目添加到解决方案

可通过右键单击解决方案窗口中的解决方案并依次选择“添加”、“添加新项目”，或者依次选择“添加”、“添加现有项目”，向解决方案添加其他项目  。

添加新项目将引导你完成项目创建步骤，如[配置新项目](#configuring-your-new-project)中所示。

选择添加现有项目，你将能浏览计算机上的现有项目并将其添加到解决方案。

## <a name="see-also"></a>请参阅

- [创建解决方案和项目（Windows 上的 Visual Studio）](/visualstudio/ide/creating-solutions-and-projects)
