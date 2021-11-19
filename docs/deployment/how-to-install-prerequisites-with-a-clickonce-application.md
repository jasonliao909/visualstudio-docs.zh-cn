---
title: 将必备组件与 ClickOnce 应用一起安装
description: 了解如何在安装 ClickOnce 应用程序时选择要一起打包的必备组件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], prerequisites
- prerequisites, ClickOnce
- components, bootstrapping
ms.assetid: e964fca5-fdfd-47cf-a1c9-7fb96b1c88b5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 9f319505fa0d17722e79274c993c1ccd54a8f5ce
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666950"
---
# <a name="how-to-install-prerequisites-with-a-clickonce-application"></a>如何：与 ClickOnce 应用程序一起安装系统必备组件
所有 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序都需要在计算机上安装正确版本的 .NET Framework 才能运行；许多应用程序还有其他必备组件。 发布 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时，可选择一组要与应用程序一起打包的必备组件。 在安装时，将检查每个必备组件，确定其是否存在；如果不存在，则将在安装 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序之前对其进行安装。

 除了打包和发布必备组件外，还可指定组件的下载位置。 例如，不在发布的每个应用程序中包含必备组件，而是可使用一个集中的文件共享或 Web 位置，其中包含所有必备组件的安装程序 - 在安装时，将从该位置下载和安装组件。

> [!IMPORTANT]
> 发布你的第一个 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序之前，应先将必备组件安装程序包添加到开发计算机中。 有关详细信息，请参阅[如何：将必备组件添加到 ClickOnce 应用程序中](../deployment/how-to-include-prerequisites-with-a-clickonce-application.md)。

 必备组件在“必备组件”对话框中进行管理，可通过项目设计器的“发布”窗格访问该对话框  。

> [!NOTE]
> 除了预先确定的必备组件列表外，还可将自己的组件添加到列表中。 有关详细信息，请参阅[创建引导程序包](../deployment/creating-bootstrapper-packages.md)。

### <a name="to-specify-prerequisites-to-install-with-a-clickonce-application"></a>指定与 ClickOnce 应用程序一起安装必备组件

1. 在“解决方案资源管理器” 中选择一个项目，然后在“项目”  菜单上单击“属性” 。

2. 选择“发布”窗格。

3. 单击“必备组件”按钮打开“必备组件”对话框 。

4. 在 **“系统必备”** 对话框中，确保选中 **“创建用于安装系统必备组件的安装程序”** 复选框。

5. 在“必备组件”列表中，检查要安装的组件，然后单击“确定” 。

     所选组件将随应用程序一起打包和发布。

### <a name="to-specify-a-different-download-location-for-prerequisites"></a>为必备组件指定其他下载位置

1. 在“解决方案资源管理器” 中选择一个项目，然后在“项目”  菜单上单击“属性” 。

2. 选择“发布”窗格。

3. 单击“必备组件”按钮打开“必备组件”对话框 。

4. 在 **“系统必备”** 对话框中，确保选中 **“创建用于安装系统必备组件的安装程序”** 复选框。

5. 在“指定必备组件的安装位置”部分，选择“从以下位置下载必备组件” 。

6. 从下拉列表中选择一个位置，或输入 URL、文件路径或 FTP 位置，然后单击“确定”。

    > [!NOTE]
    > 必须确保指定位置存在指定组件的安装程序。

## <a name="see-also"></a>另请参阅
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)