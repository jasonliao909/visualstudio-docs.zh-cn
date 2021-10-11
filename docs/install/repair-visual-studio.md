---
title: 修复 Visual Studio
titleSuffix: ''
description: 了解如何修复 Visual Studio 2017 的安装
ms.date: 09/14/2021
ms.custom: vs-acquisition
ms.topic: how-to
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: ca36dbefec8ff61a8ba05286f2dd8aa6593cc13b
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128429029"
---
# <a name="repair-visual-studio"></a>修复 Visual Studio

Visual Studio 安装有时会损毁或损坏。 修复功能可用于修复各种安装时问题，包括更新问题。

## <a name="when-to-use-repair"></a>何时使用修复

如果你遇到以下方面的问题，请使用修复功能：

* 安装有效负载。将文件写入磁盘失败并且文件损坏时，可能会发生与此相关的问题。 修复功能可以重新获取所需的文件。
* 客户端下载 - 假设你已修复任何 Internet 连接或代理问题。
* 更新 Visual Studio。 修复可解决许多常见的更新问题。

> [!TIP] 
> 不稳定的 Internet 连接或 Windows 服务（例如 Windows Installer）出现问题可能会导致安装问题。 在这种情况下，修复也可能受到影响。 若要找出根本性问题，请查看 Visual Studio 安装程序生成的错误报告。

> [!NOTE] 
> 修复 Visual Studio 会重置用户设置并重新安装现有的程序集。 如果你遇到产品问题并且修复功能无法修复该问题，请创建 [Visual Studio 反馈票证](https://aka.ms/feedback/suggest?space=8)。 有关详细信息，请参阅[如何报告 Visual Studio 或 Visual Studio 安装程序的问题](../ide/how-to-report-a-problem-with-visual-studio.md)。

## <a name="how-to-repair"></a>如何修复
::: moniker range="vs-2017"

1. 在计算机上找到 Visual Studio 安装程序。

     例如，在运行 Windows 10 周年更新或更高版本的计算机上，选择“开始”，再滚动到字母“V”（其中它被列为“Visual Studio 安装程序”）。

   > [!NOTE]
   > 对于某些计算机，Visual Studio 安装程序可能列在字母 **“M”** 下，即 **Microsoft Visual Studio 安装程序**。
   >
   > 或者，可以在以下位置找到 Visual Studio 安装程序：`C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

1. 打开安装程序，选择“更多”，然后选择“修复”。

    ![显示 Visual Studio 安装程序的“更多”下拉菜单中“修复”选项的屏幕截图。](media/repair-visual-studio.png "从 Visual Studio 安装程序修复 Visual Studio")

   > [!NOTE]
   > 修复 Visual Studio 将重置环境。 将删除无需提升权限即可安装的每用户扩展、用户设置和配置文件等本地自定义项。 将还原主题、颜色、键绑定等同步设置。
   >

   > [!TIP]
   > “修复”选项仅对已安装的 Visual Studio 实例显示。 如果没有看到“修复”选项，很可能是因为选择“更多”时所在的版本在 Visual Studio 安装程序中列为“可用”，而不是“已安装”。

::: moniker-end

::: moniker range="vs-2019"

1. 在计算机上找到 Visual Studio 安装程序。

     在 Windows 的“开始”菜单中，可以搜索“安装程序”。

     ![显示在“开始”菜单中搜索 Visual Studio 安装程序后出现的结果的屏幕截图。](media/vs-2019/visual-studio-installer.png "搜索 Visual Studio 安装程序")

     > [!NOTE]
     > 还可以在以下位置中找到 Visual Studio 安装程序：
     >
     > `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

    可能需要先更新安装程序，然后才能继续操作。 如果是这样，请按照提示操作。

1. 在安装程序中，查找已安装的 Visual Studio 版本。 接下来，选择“更多”，然后选择“修复”。

     ![显示 Visual Studio 安装程序的“更多”下拉菜单中“修复”选项的屏幕截图。](media/vs-2019/vs-installer-repair.png "修复 Visual Studio 2019")

   > [!NOTE]
   > 修复 Visual Studio 会重置其环境。 将删除无需提升权限即可安装的每用户扩展、用户设置和配置文件等本地自定义项。 主题、颜色和键绑定等已同步的设置将会还原。
   >

   > [!TIP]
   > “修复”选项仅对已安装的 Visual Studio 实例显示。 如果没有看到“修复”选项，很可能是因为选择“更多”时所在的版本在 Visual Studio 安装程序中列为“可用”，而不是“已安装”。

::: moniker-end

::: moniker range=">=vs-2022"

1. 在计算机上找到 Visual Studio 安装程序。

     在 Windows 的“开始”菜单中搜索“安装程序”，然后从结果中选择“Visual Studio 安装程序”。

     ![显示在“开始”菜单中搜索 Visual Studio 安装程序后出现的结果的屏幕截图。](media/vs-2022/vs-installer-search.png "搜索 Visual Studio 安装程序")

     > [!NOTE]
     > 还可以在以下位置中找到 Visual Studio 安装程序：
     >
     > `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

    在继续之前，系统可能会提示更新 Visual Studio 安装程序。 如果是这样，请按照提示操作。

1. 在 Visual Studio 安装程序中，找到要修复的 Visual Studio 安装。 然后从“更多”下拉菜单中选择“修复” 。

     ![显示 Visual Studio 安装程序的“更多”下拉菜单中“修复”选项的屏幕截图。](media/vs-2022/vs-installer-repair.png "修复 Visual Studio 2022")

   > [!NOTE]
   > 修复 Visual Studio 会重置其环境。 将删除无需提升权限即可安装的每用户扩展、用户设置和配置文件等本地自定义项。 主题、颜色和键绑定等已同步的设置将会还原。
   >

   > [!TIP]
   > “修复”选项适用于已安装的 Visual Studio 实例。 如果在“更多”下拉菜单中未看到“修复”选项，则你所处的位置可能是 Visual Studio 安装程序的“可用”选项卡而不是“已安装”选项卡   。

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [安装 Visual Studio](install-visual-studio.md)
* [更新 Visual Studio](update-visual-studio.md)
* [卸载 Visual Studio](uninstall-visual-studio.md)
* [Visual Studio 安装和升级问题疑难解答](troubleshooting-installation-issues.md)
