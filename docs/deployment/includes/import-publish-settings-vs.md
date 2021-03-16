---
ms.openlocfilehash: 94c2c733b631ef5e727c79a6e093bb224aec38c4
ms.sourcegitcommit: 79a6be815244f1cfc7b4123afff29983fce0555c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249860"
---

1. 如果计算机上的 Visual Studio 中打开有 ASP.NET 项目，则在该计算机的解决方案资源管理器中右键单击该项目，然后选择“发布”。

   如果先前配置了任何发布配置文件，则“发布”窗格会显示。 单击“新建”或“创建新配置文件”。

1. 选择该选项以导入配置文件。

   ::: moniker range=">=vs-2019"
   在“发布”对话框中，单击“导入配置文件”。
   ::: moniker-end
   ::: moniker range="vs-2017"
   在“选取发布目标”对话框中，点击“导入配置文件” 。
   ::: moniker-end

   ![选择发布](../../deployment/media/tutorial-publish-tool-import-profile.png)

1. 导航到上一节中创建的发布设置文件的位置。

1. 在“导入发布设置文件”对话框中，导航到在上一部分创建的配置文件并选择该文件，然后单击“打开” 。

   ::: moniker range=">=vs-2019"
   单击“完成”保存发布配置文件，然后单击“发布”。

   Visual Studio 开始执行部署过程，并且输出窗口将显示进度和结果。

   如果出现任何部署错误，请单击“编辑”以编辑设置。 修改设置，然后单击“验证”以测试新设置。 如果找不到主机名，请尝试“服务器”和“目标 URL”字段中的 IP 地址而不是主机名 。
   ::: moniker-end
   ::: moniker range="vs-2017"
   Visual Studio 开始执行部署过程，并且输出窗口将显示进度和结果。

   如果出现任何部署错误，请单击“设置”以编辑设置。 修改设置，然后单击“验证”以测试新设置。 如果找不到主机名，请尝试“服务器”和“目标 URL”字段中的 IP 地址而不是主机名 。
   ::: moniker-end

   ![编辑发布工具中的设置](../../deployment/media/tutorial-configure-publish-settings-in-tool.png)
