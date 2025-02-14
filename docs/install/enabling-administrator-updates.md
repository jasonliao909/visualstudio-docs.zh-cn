---
title: 启用使用 Microsoft Endpoint Configuration Manager 的 Visual Studio 管理员更新
titleSuffix: ''
description: 详细了解如何部署 Visual Studio 的管理员更新。
ms.date: 04/06/2022
ms.topic: overview
ms.assetid: 546fbad6-f12b-49cf-bccc-f2e63e051a18
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: ea70733536a0bfd0cf3a60ecc839047301f2df2d
ms.sourcegitcommit: 015d0bf8295f48d687c91aacc4ec2747063fe9ca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2022
ms.locfileid: "141533275"
---
# <a name="enabling-administrator-updates-to-visual-studio-with-microsoft-endpoint-configuration-manager"></a>启用使用 Microsoft Endpoint Configuration Manager 的 Visual Studio 管理员更新

Microsoft Endpoint Configuration Manager (SCCM) 可以使用软件更新管理工作流管理Visual Studio管理员更新。 为使文档简洁，下面的内容将 Visual Studio 2017、Visual Studio 2019 和 Visual Studio 2022 产品统称为“Visual Studio”。

当 Microsoft 将新的 Visual Studio 更新发布到内容分发网络 (CDN) 时，Microsoft 会将相应的管理员更新包同时发布到 Microsoft 更新服务器。 这样，管理员便可通过 [Microsoft 更新目录](https://www.catalog.update.microsoft.com/Home.aspx) (MUC) 或 [Windows Server Update Services](/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus) (WSUS) 分发 Visual Studio 更新。 可设置 Configuration Manager，将 Visual Studio 管理员更新从 WSUS 目录同步到站点服务器，然后它可以下载该更新，并将其分发到组织内的 Visual Studio 客户端计算机。 有关每个版本的Visual Studio中存在哪些修补程序的详细信息，请参阅Visual Studio发行说明。

若要通过 Configuration Manager 分发 Visual Studio 管理员更新，需要执行以下两个初始准备步骤：
1. 启用 Configuration Manager 以接收 Visual Studio 管理员更新通知。 
2. 启用（或禁用）客户端计算机以从 Configuration Manager 接收 Visual Studio 管理员更新。

执行这些步骤后，可使用 Configuration Manager 的软件更新管理功能来部署 Visual Studio 管理员更新。 [应用管理员更新](../install/applying-administrator-updates.md)中介绍了 Visual Studio 管理员更新的不同类型和特征，其中提供了有关如何以及何时在整个组织中分发管理员更新的指导。 有关 Configuration Manager 功能和选项的详细信息，请参阅[在 Microsoft Endpoint Configuration Manager 中部署软件更新](/mem/configmgr/sum/deploy-use/deploy-software-updates)。

## <a name="enable-configuration-manager-to-receive-visual-studio-administrator-update-notifications"></a>启用 Configuration Manager 以接收 Visual Studio 管理员更新通知

若要启用 Configuration Manager 来管理 Visual Studio 管理员更新，你需要：

* 运行 Microsoft Endpoint Configuration Manager（当前分支）和 Windows Server Update Services (WSUS) 的 Windows Server 的当前许可版本。 不能单独使用 WSUS 来部署这些更新；它必须与 Configuration Manager 结合使用。

* Microsoft Endpoint Configuration Manager 必须配置为在 Visual Studio 管理员更新包可用时接收通知。  为此，请使用以下步骤；有关详细信息，请参阅 [ Microsoft Endpoint Configuration Manager 中的软件更新简介](/mem/configmgr/sum/understand/software-updates-introduction)。

  1. 在 Configuration Manager 控制台中，依次选择“管理”（左下角）、“站点配置”（左中部）和“站点”，然后选择你的站点服务器  。

  2. 在顶部的“主页”选项卡功能区中的“设置”组按钮中，选择“配置站点组件”，然后选择“软件更新点”   。

  3. 在“软件更新点组件属性”对话框中：

        * 在“产品”选项卡上的“开发人员工具、运行时和可再发行组件”层次结构中，选择要同步的 Visual Studio 版本 。

        * 在“分类”选项卡上，确保选中“安全更新”、“功能包”和“更新”。

  4. 接下来，选择“软件库”（左下方），将软件更新与 WSUS 服务器同步，然后在顶部的“主页”选项卡上，选择“同步软件更新”按钮  。 “同步软件更新”将使可用的 Visual Studio 管理员更新在 Configuration Manager 控制台中可见，并可以从该控制台进行部署。

## <a name="enable-or-disable-client-machines-ability-to-receive-visual-studio-administrator-updates-from-configuration-manager"></a>启用（或禁用）客户端计算机从 Configuration Manager 接收 Visual Studio 管理员更新的功能

若要使客户端计算机能够接受Visual Studio管理员更新，需要确保正确安装Visual Studio客户端检测器实用工具，需要设置注册表项以允许客户端接收管理员更新，并且需要确保执行管理员更新的帐户对计算机具有管理权限并访问源 产品更新的位置。 

### <a name="visual-studio-client-detector-utility"></a>Visual Studio 客户端检测程序实用工具

必须在客户端计算机上安装 [Visual Studio 客户端检测程序实用工具](https://support.microsoft.com/help/5001148)，才能正确识别和接收管理员更新。 此实用工具包含在 2020 年 5 月 12 日或 2020 年 5 月 12 日发布的所有Visual Studio产品更新中，它作为所有Visual Studio管理员更新的先决条件包含在内，并且也可以在 [Microsoft 更新目录中](https://catalog.update.microsoft.com)独立安装。

### <a name="encoding-administrator-intent-on-the-client-machines"></a>在客户端计算机上对管理员意向进行编码

必须使客户端计算机能够接收管理员更新。 此步骤是必需步骤，以确保不会无意或意外地将更新推送到毫无准备的客户端计算机。

AdministratorUpdatesEnabled 项专为管理员而设计，用于对管理员意向进行编码 **** 。 此键可以位于任何[标准Visual Studio注册表位置](set-defaults-for-enterprise-deployments.md)。 需要对客户端计算机具有管理员访问权限才能创建并设置此项的值。

* 若要将客户端计算机配置为接受管理员更新，请将 AdministratorUpdatesEnabled REG_DWORD 项设置为 1 ****  **** 。
* 如果 AdministratorUpdatesEnabled REG_DWORD 项缺失或设置为 0，则将阻止管理员更新应用于客户端计算机 **** 。

### <a name="ensuring-the-account-has-the-right-privileges-and-permissions"></a>确保帐户具有正确的特权和权限
默认情况下，客户端计算机的 SYSTEM 帐户将下载并安装Visual Studio管理员更新。 这意味着 SYSTEM 帐户必须对计算机具有管理权限。 此外，根据[客户端配置为从何处获取产品源](/visualstudio/install/update-visual-studio#configure-source-location-of-updates-1)，SYSTEM 帐户还必须至少有权访问 Internet 上的[Visual Studio终结点](/visualstudio/install/install-and-use-visual-studio-behind-a-firewall-or-proxy-server)或从网络布局位置读取权限才能下载更新的产品位。 注意：为客户端计算机的 SYSTEM 帐户集合授予对网络共享的权限的一种简单方法是向"域计算机"AD 组授予权限。

## <a name="feedback-and-support"></a>反馈和支持

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

可使用以下方法，提供有关 Visual Studio 管理员更新的反馈或报告影响更新的问题：

* 请参阅 [Visual Studio 安装和升级问题疑难解答](../install/troubleshooting-installation-issues.md)指南。
* 在 [Visual Studio 安装常见问题解答论坛](/answers/topics/vs-setup.html)上向社区提问。
* 请转到 [Visual Studio 支持页面](https://visualstudio.microsoft.com/vs/support/)，检查你的问题是否在常见问题解答中列出。  你也可以选择[支持链接](https://visualstudio.microsoft.com/vs/support/#talktous)按钮以获取聊天帮助。
* 向 Visual Studio 团队[提供功能反馈或报告有关此启用管理员更新体验的问题](https://aka.ms/vs/wsus/feedback)。
* 与你组织的 Microsoft 技术部客户经理联系。

## <a name="see-also"></a>另请参阅

* [应用管理员更新](../install/applying-administrator-updates.md)
* [Visual Studio 管理员指南](../install/visual-studio-administrator-guide.md)
* [Visual Studio 产品生命周期和维护](/visualstudio/productinfo/vs-servicing-vs)
* [安装 Visual Studio](../install/install-visual-studio.md)
* [更新 Visual Studio](../install/update-visual-studio.md)
* [Microsoft 更新目录常见问题解答](https://www.catalog.update.microsoft.com/faq.aspx)
* [Microsoft Endpoint Configuration Manager (SCCM) 文档](/mem/configmgr)
* [将 Microsoft 目录中的更新导入 Configuration Manager](/mem/configmgr/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog)
* [Windows Server Update Services (WSUS) 文档](/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus)
