---
title: 生成和清理项目和解决方案
description: 本文介绍如何在 Visual Studio for Mac 中生成项目
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 02/28/2022
ms.custom: devdivchpfy22
ms.assetid: E4B6CB42-9FE2-43B9-93B7-BD4BD50518B1
ms.topic: how-to
ms.openlocfilehash: 75a09a9a3961162ebfe5affa1ca613b60b66d4bb
ms.sourcegitcommit: fcf47a9c356df7e9636bcab92186923e5c9b8892
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2022
ms.locfileid: "144502908"
---
# <a name="building-and-cleaning-projects-and-solutions"></a>生成和清理项目和解决方案

 [!INCLUDE [Visual Studio for Mac](~/includes/applies-to-version/vs-mac-only.md)]

按照本文的步骤了解如何生成、重新生成或清理解决方案中所有或部分项目。

> [!NOTE]
> 本主题适用于 Visual Studio for Mac。 对于 Windows 上的 Visual Studio，请参阅[在 Visual Studio 中生成和清除项目和解决方案](/visualstudio/ide/building-and-cleaning-projects-and-solutions-in-visual-studio)。

## <a name="to-build-rebuild-or-clean-an-entire-solution"></a>生成、重新生成或清理整个解决方案

1. 在“解决方案窗口”中选择“解决方案”节点：

    ![选择选择“解决方案”节点](media/compiling-and-building-image1.png)

2. 在菜单栏中选择“生成”菜单，然后选择以下选项之一：

    ![选择“生成所有菜单项”](media/compiling-and-building-image2.png)

    * 选择“全部生成”，编译自最近生成以来更改过的项目中的文件和组件。

    * 选择“全部重新生成”清理解决方案，然后创建所有项目文件和组件。

    * 选择“全部清理”，删除任何中间文件和输出文件。 仅剩下项目和组件文件后，可生成中间文件和输出文件的新实例。

## <a name="to-build-or-rebuild-a-single-project"></a>生成或重新生成单个项目

1. 在“解决方案窗口”中选择项目。

2. 从菜单栏中选择“生成”菜单。

3. 选择“生成[ProjectName]”、“重新生成[ProjectName]”或“清理[ProjectName]”。

## <a name="to-stop-a-build"></a>停止生成

若要停止生成，使用以下选项之一：

* 按状态区域中的红色方块：

    ![按红色方块停止生成](media/compiling-and-building-image3.png)

* 使用“生成”菜单中的“停止”项。

* 按 command+shift+return。

## <a name="see-also"></a>请参阅

- [生成和清除项目和解决方案（Windows 上的 Visual Studio）](/visualstudio/ide/building-and-cleaning-projects-and-solutions-in-visual-studio)