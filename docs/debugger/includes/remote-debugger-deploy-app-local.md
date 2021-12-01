---
title: 部署到本地文件夹
description: 将应用部署到本地文件夹
services: ''
author: mikejo5000
ms.service: ''
ms.topic: include
ms.date: 05/23/2018
ms.author: mikejo
ms.custom: include file
ms.openlocfilehash: 36effcf08969c5233eaee54578c9f5e3101528b96e41cb7cbf6c0025c1f7c56b
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "122058379"
---
1. 在“解决方案资源管理器”  中，右键单击项目节点并选择“发布”  （对于 Web Forms，选择“发布 Web 应用”  ）。

    如果先前配置了任何发布配置文件，则“发布”窗格会显示  。 单击“新建配置文件”  。

1. 在“发布”  对话框中，选择“文件夹”  ，单击“浏览”  ，然后创建一个新文件夹“C:\Publish”  。

   ::: moniker range=">=vs-2019"

   :::image type="content" source="../media/vs-2019/remotedbg-publish-local.png" alt-text="Visual Studio 中“选取发布目标”对话框的屏幕截图，其中选择了文件夹“C:\Publish”作为发布目标。":::

   单击“完成”保存发布配置文件。
   ::: moniker-end
   ::: moniker range="vs-2017"
   ![Visual Studio 中“选取发布目标”对话框的屏幕截图，其中选择了文件夹“bin\Release\Publish”作为发布目标。](../media/remotedbg_publish_local.png)
   对于 Web Forms 应用，请在“发布”对话框中选择“自定义”  ，输入配置文件名称，然后选择“确定”  。

   单击下拉列表中的“创建配置文件”  （默认值为“发布”  ）。
   ::: moniker-end

1. 切换到调试配置。

   ::: moniker range=">=vs-2019"
   选择“编辑”以编辑配置文件，然后选择“设置”。 选择“调试”配置，然后在“文件发布”选项下选择“删除目标处的其他文件”。
   ::: moniker-end
   ::: moniker range="vs-2017"
   在“设置”对话框中，单击“下一步”启用调试，选择“调试”配置，然后在“文件发布”选项下选择“删除目标处的其他文件”    。
   ::: moniker-end

   > [!NOTE]
   > 如果使用发布生成，则在发布时，需要在 web.config 文件中禁用调试。

1. 单击“发布”  。

    ![“发布”对话框中“设置”选项卡的屏幕截图。 “配置”设置为“调试”，并选中了“发布”按钮。](../media/remotedbg_publish_debug_config.png)

    应用程序将项目的“调试”  配置发布到本地文件夹。 “输出”窗口中将显示进度。

1. 将 ASP.NET 项目目录从 Visual Studio 计算机复制到 Windows Server 计算机上为 ASP.NET 应用配置的本地目录中（本例中为 C:\Publish  ）。 在本教程中，我们假设你进行手动复制，不过，你也可以使用其他工具，例如 PowerShell、Xcopy 或 Robocopy。

    > [!CAUTION]
    > 如果需要更改代码或重新生成，则必须重新发布并重复此步骤。 复制到远程计算机的可执行文件必须与你的本地源和符号完全匹配。 如果没有这样做，则在尝试调试进程时，你会在 Visual Studio 中收到 `cannot find or open the PDB file` 警告。

1. 在 Windows Server 上，通过在浏览器中打开应用来验证是否可以正常运行应用。

    如果应用无法正常运行，则说明服务器和 Visual Studio 计算机上安装的 ASP.NET 版本可能不匹配，或者 IIS 或网站配置可能有问题。 请重新检查前面的步骤。
