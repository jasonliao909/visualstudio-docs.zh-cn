---
ms.openlocfilehash: 09f6e03fa38c8f953ea5d70aedf81cd09c065a08
ms.sourcegitcommit: 3d1143b007bf0ead80bf4cb3867bf89ab0ab5b53
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2021
ms.locfileid: "123397852"
---
用于托管服务器的 Web 部署 3.6 提供额外的配置功能，可实现从 UI 创建发布设置文件。

IIS 的Web 平台安装程序允许安装版本 3.6 而不是 4.0，因此这是本文中建议的版本。

1. 如果已在 Windows Server 上安装 Web 部署，请使用“控制面板” > “程序” > “卸载程序”将其卸载。

2. 接下来，在 Windows 服务器上安装用于托管服务器的 Web 部署 3.6。

    要安装用于托管服务器的 Web 部署，请使用 Web 平台安装程序 (WebPI)。 （要从 IIS 查找 Web 平台安装程序链接，请选择服务器管理器左侧窗格中的“IIS”。 在服务器窗格中，右键单击服务器并选择“Internet Information Services (IIS)管理器”。 然后，在“操作”窗口中，使用“获取新的 Web 平台组件”连接 。）你还可以从[下载](https://www.microsoft.com/web/downloads/platform.aspx)获取 Web 平台安装程序 (WebPI)。

    在 Web 平台安装程序中，在“应用程序”选项卡中查找“用于托管服务器的 Web 部署 3.6”。

3. 如果尚未安装“IIS 管理脚本和工具”，请立即安装。

    转到“选择服务器角色” > “Web 服务器(IIS)” > “管理工具”，然后选择“IIS 管理脚本和工具”角色，点击“下一步”，然后安装角色    。

    ![安装 IIS 管理脚本和工具](../../deployment/media/tutorial-iis-management-scripts-and-tools.png)

    需要脚本和工具来生成发布设置文件。

4. 根据需要，打开“控制面板”>“系统和安全”>“管理工具”>“服务”来验证 Web 部署是否正确运行，然后确保：

    * “Web 部署代理服务”正在运行（旧版本中的服务名称不同）。

    * “Web 管理服务”正在运行。

    如果某个代理服务未运行，请重新启动“Web 部署代理服务”。

    如果 Web 部署代理服务不存在，请转到“控制面板”>“程序”>“卸载程序”，查找“Microsoft Web 部署 \<version>。 选择“更改”安装，并确保对 Web 部署组件选择“将安装到本地驱动器” 。 完成更改安装步骤。