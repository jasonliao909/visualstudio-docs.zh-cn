---
ms.openlocfilehash: 6e9650a10a193947f11172d717481f8221a66ccf
ms.sourcegitcommit: 3d1143b007bf0ead80bf4cb3867bf89ab0ab5b53
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2021
ms.locfileid: "123397854"
---

1. 关闭并重新打开 IIS 管理控制台以在 UI 中显示更新的配置选项。

2. 在 IIS 中，右键单击“默认网站”，选择“部署” > “配置 Web 部署发布”  。

    ![配置 Web 部署配置](../../deployment/media/tutorial-configure-web-deploy-publishing.png)

   如果看不到“部署”菜单，请参阅前面的部分来验证 Web 部署是否正在运行。

3. 在“配置 Web 部署发布”对话框中，检查设置。

4. 单击“设置”。

    在“结果”面板中，输出显示已为指定用户授予访问权限，并且已在对话框中显示的位置生成了具有 .publishsettings 文件扩展名的文件。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <publishData>
      <publishProfile
        publishUrl="https://myhostname:8172/msdeploy.axd"
        msdeploySite="Default Web Site"
        destinationAppUrl="http://myhostname:80/"
        mySQLDBConnectionString=""
        SQLServerDBConnectionString=""
        profileName="Default Settings"
        publishMethod="MSDeploy"
        userName="myhostname\myusername" />
    </publishData>
    ```

    根据 Windows Server 和 IIS 配置，可以在 XML 文件看到不同的值。 下面是有关所看到的值的一些详细信息：

   * `publishUrl` 属性中引用的 msdeploy.axd 文件是 Web 部署动态生成的 HTTP 处理程序文件。 （用于测试目的，`http://myhostname:8172` 通常也适用。）
   * `publishUrl` 端口设置为端口 8172，这是 Web 部署的默认端口。
   * `destinationAppUrl` 端口设置为端口 80，这是 IIS 部署的默认端口。
   * 如果在后续步骤中，无法使用主机名从 Visual Studio 连接到远程主机，请测试服务器的 IP 地址，用它来代替主机名。

     > [!NOTE]
     > 如果要发布到在 Azure VM 上运行的 IIS，必须在网络安全组中打开 Web 部署和 IIS 的入站端口。 有关详细信息，请参阅[打开虚拟机的端口](/azure/virtual-machines/windows/nsg-quickstart-portal)。

5. 将此文件复制到运行 Visual Studio 的计算机上。
