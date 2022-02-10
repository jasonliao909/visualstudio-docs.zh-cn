---
title: 应用使用 Microsoft Endpoint Configuration Manager 的 Visual Studio 管理员更新
titleSuffix: ''
description: 了解如何应用 Visual Studio 的管理员更新。
ms.date: 02/04/2022
ms.topic: overview
ms.assetid: 9a3fdb28-db3d-4970-bc17-7417a985f0fb
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: f81d8ad7bd8ade46ac0af190843ca107409f5834
ms.sourcegitcommit: b9c5ca58f380ee102153b69656cb062b3d2dab8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/10/2022
ms.locfileid: "138427760"
---
# <a name="applying-administrator-updates-that-use-microsoft-endpoint-configuration-manager"></a>应用使用 Microsoft Endpoint Configuration Manager 的管理员更新

本文档介绍 Visual Studio 管理员更新的不同类型和特征。 在下方，可找到有关应如何以及何时在整个组织中分配这些更新、哪些配置选项可用以及如何查看报表并进行故障排除的信息。 若要详细了解使用管理员更新的先决条件，请参阅[启用管理员更新](../install/enabling-administrator-updates.md)。 管理员更新会假定计算机上已安装 Visual Studio。 应用管理员更新时不会启动全新安装。

## <a name="understanding-visual-studio-administrator-updates"></a>了解 Visual Studio 管理员更新

发布到 Microsoft 更新以供 Microsoft 目录和 WSUS 使用的 Visual Studio 管理员更新包内含有 Configuration Manager 所需的使其能够下载 Visual Studio 更新并将其分发到客户端计算机的信息。 它还包含 IT 管理员所需的用于确定要在整个组织中分配哪些更新的信息。 使用它还能让网络布局的维护更便捷。 Visual Studio 管理员更新包中包含的信息不足以执行产品的全新安装，也不包含发布到内容分发网络的任何实际产品二进制文件。 Visual Studio 管理员更新是累积更新，就像常规 Visual Studio 更新一样。 你可以假设任何具有较高产品版本号和较晚发布日期的 Visual Studio 更新都是较旧、较低版本的超集。

Visual Studio 管理员更新适用于受支持的 Visual Studio 服务版本。 若要详细了解在特定时间范围内仍处于支持状态的 Visual Studio 服务基线，请参阅 [Visual Studio 产品生命周期和服务](/visualstudio/productinfo/vs-servicing-vs)。 所有受支持的 Visual Studio 服务基线都将保持安全。  

> [!NOTE]
> Visual Studio管理员更新会导致客户端计算机从客户端配置为从 Internet 或网络布局下载更新的任何位置下载产品[](/visualstudio/install/update-visual-studio#configure-source-location-of-updates-1)文件。 因此，管理员更新可用于客户端未连接到 Internet 的情况。 例如，如果将客户端配置为从网络布局获取更新，则管理员更新可用于触发客户端自行更新。  

## <a name="types-and-characteristics-of-administrator-updates"></a>管理员更新的类型和特征

有三种类型的 Visual Studio 管理员更新：

* 安全更新适用于所有 Visual Studio 版本（例如 Enterprise、Professional、Community 等），且这些更新包含有限、高针对性且兼容的服务级别更改。 安全更新不会将客户端提升到更高的次要版本；它们旨在向已经处于特定次要版本级别的客户端提供对安全漏洞的修补程序。 安全更新中至少有一个安全修补程序，但安全修补程序可能位于/可能不位于客户端计算机上安装的组件或工作负载中。 例如，可修复 .NET 组件中的安全漏洞，并将更新标记为安全更新，但它对仅安装了 C++ 组件的客户端计算机没有任何有意义的影响。 安全更新可能还包含其他可靠性修补程序或其他必要的组件更新。 安全更新将发布到 [Microsoft 更新目录](https://www.catalog.update.microsoft.com/Home.aspx) (MUC) 和 [Windows Server Update Services](/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus)，它们在其中被归类为“安全更新”。
* 功能更新使 IT 管理员能够将其组织中的计算机提升到较新的 Visual Studio 次要版本。 功能更新仅适用于在企业中常见的 Visual Studio 版本，例如 Enterprise、Professional 和生成工具 SKU。 所有功能更新将作为“功能包”发布到 Microsoft 更新目录中，可选择将它们[从 Microsoft 更新目录中手动导入 Configuration Manager](/mem/configmgr/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog)。 功能更新是累积更新，将包含其他质量修补程序和先前的安全修补程序。 请参阅下面的[配置选项部分](#understanding-configuration-options)，了解如何将客户端计算机配置为保持在服务基线上并防止功能更新被传递给特定客户端。
* 质量更新仅适用于那些在企业中常见的 Visual Studio 版本，并包含有限、高针对性且兼容的服务级别更改。 质量更新不会将客户端提升到更高的次要版本；它们旨在向已经处于特定次要版本级别的客户端提供性能和可靠性修补程序或其他必要的组件更新。 质量更新与安全更新一起累积，因此只有在安全修补程序已独立发布时，质量更新才会包含安全修补程序。 质量更新作为“更新”发布到 Microsoft 更新目录中，也可选择将它们手动[导入 Configuration Manager](/mem/configmgr/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog)。

### <a name="decoding-the-titles-of-administrator-updates"></a>对管理员更新的标题进行解码

每个管理员更新的标题描述了更新的适用版本范围和所最终版本。例如，

::: moniker range="vs-2017"

* 分类为“安全更新”的 Visual Studio 2017 版本 15.9.0 到 15.9.35 更新将适用于版本 15.9.0 到 15.9.35 之间的任何 Visual Studio 2017 客户端版本，并将这些客户端版本更新至 15.9.35。
* 分类为“功能包”的 Visual Studio 2017 版本 15.0.0 到 15.9.0 更新将适用于授权企业使用的整个产品版本范围 15.0.0 到 15.9.0 的 Visual Studio 2017 客户端版本，并将这些客户端版本更新至 15.9.0。 应用此功能包基本上使客户端可以接收安全更新。 
* 简单地分类为“更新”的 Visual Studio 2017 版本 15.9.0 至 15.9.37 更新将适用于授权企业使用的版本 15.9.0 至 15.9.37 之间的 Visual Studio 2017 客户端版本，并将这些客户端版本更新至 15.9.37。

::: moniker-end

::: moniker range="vs-2019"

* 分类为“安全更新”的 Visual Studio 2019 版本 16.7.0 至 16.7.12 更新将适用于版本 16.7.0 至 16.7.12 之间的任何 Visual Studio 2019 客户端版本，并将这些客户端版本更新至 16.7.12。  
* 分类为“功能包”的 Visual Studio 2019 版本 16.0.0 到 16.9.0 更新将适用于授权企业使用的整个产品版本范围 16.0.0 到 16.9.0 的 Visual Studio 2019 客户端版本，并将这些客户端版本（未配置为保持在早期服务基线上的版本）更新至 16.9.0。 
* 简单地分类为“更新”的 Visual Studio 2019 版本 16.8.0 到 16.8.7 更新将适用于授权企业使用的版本 16.8.0 到 16.8.7 之间的 Visual Studio 2019 客户端版本，并将这些客户端版本更新至 16.8.7。

::: moniker-end

::: moniker range=">=vs-2022"
* **Visual Studio 2022 版本 17.0.3** 更新分类为"安全更新"，将应用于客户端上当前通道或 [17.0 LTSC](/visualstudio/install/update-visual-studio?view=vs-2022&preserve-view=true#configure-source-location-of-updates-1) 通道上的任何 Visual Studio 2022 版本，并更新到 17.0.3 版。  
* **Visual Studio 2022 版本 17.1.0** 更新（分类为"功能包"）将应用于 Visual Studio 2022 版本，这些版本在当前通道上的客户端上获得企业使用许可，并更新到 17.1.0 版本。 
* **Visual Studio 2022 版本 17.1.2** 更新仅归类为"更新"，将应用于在当前通道上的客户端上授予企业使用的 Visual Studio 2022 版本，并更新到 17.1.2 版本。 
* **Visual Studio 2022 版本 17.2.7** 更新分类为"安全更新"，将应用于客户端上当前通道或 17.2 LTSC 通道上的任何 Visual Studio 2022 版本，并更新到 17.2.7 版。 

如果客户端实例大于要应用的管理员更新版本，则管理员更新将不起作用。
::: moniker-end

## <a name="using-configuration-manager-to-deploy-visual-studio-updates"></a>使用 Configuration Manager 部署 Visual Studio 更新

### <a name="understanding-configuration-options"></a>了解配置选项

有几个配置选项可用于定制 Visual Studio 管理员更新，使它们与你的组织的部署首选项和要求兼容并保持一致。 最常见的配置选项如下所示。 有关所有受支持的管理员更新行为的详尽列表，请参阅[使用命令行参数安装 Visual Studio](../install/use-command-line-parameters-to-install-visual-studio.md) 并仅注意与“更新”操作相关的内容。

* [管理员更新选择加入](../install/enabling-administrator-updates.md#encoding-administrator-intent-on-the-client-machines)：需要此注册表项以使客户端计算机能够接收管理员更新。 它是一种计算机范围的项，意味着它适用于安装在计算机上的所有 Visual Studio 实例。
* Visual studio 用户选择退出：Visual Studio 用户可以使用单独的计算机范围内的 AdministratorUpdatesOptOut 注册表项来选择退出接收 Visual Studio 管理员更新。 此项的目的是允许 Visual Studio 用户控制自动将更新应用到计算机的过程。 若要将客户端计算机配置为阻止管理员更新，请将 AdministratorUpdatesOptOut REG_DWORD 项设置为 1 ****  **** 。 若缺少该项或设置的值为 0，这意味着 Visual Studio 用户希望接收 Visual Studio 管理员更新 **** 。
    请注意，AdministratorUpdatesOptOut  项（用于对用户首选项进行编码）优先于 AdministratorUpdatesEnabled  项（用于对 IT 管理员意向进行编码） ****  **** 。 如果 AdministratorUpdatesOptOut 设置为 1，则即使 AdministratorUpdatesEnabled 项也设置为 1，也会在客户端上阻止更新 ****  ****  ****  **** 。此操作假定 IT 管理员可访问和监视哪些开发人员选择退出，然后双方可以讨论谁的需求更重要。IT 管理员始终可以随时更改任意一个项。
* 更新的产品位的位置：大多数情况下，客户端计算机通过 Microsoft CDN 从 Internet 下载更新的产品位。 在此场景下，要求客户端计算机具有 Internet 访问权限。 但是，某些企业会将客户端计算机限制为仅从内部网络布局位置安装和更新位。 若要确保可以使用内部网络位置的更新位来应用管理员更新，必须满足以下条件，然后才能成功部署管理员更新： 
  * 在某些情况下，客户端计算机必须已从该网络布局位置运行引导程序。 理想情况下，初始客户端安装将从网络布局使用引导程序执行，但也可以使用同一网络位置的更新的引导程序安装更新。 其中任一操作将在客户端计算机上嵌入与该特定布局位置的连接。
  * 必须更新（客户端连接的）网络布局位置，以[获取管理员更新要部署的更新的产品位](../install/update-a-network-installation-of-visual-studio.md)。

::: moniker range=">=vs-2019"

* 服务基线粘性：如上所述，管理员功能更新会将 Visual Studio 安装提升到更新的产品次要版本。 但有时，Visual Studio 用户需要保持在稳定且安全的特定服务基线级别，并想控制其计算机何时提升到更新的次要版本。 若要将客户端计算机配置为保持在某个服务基线上，并忽略发送给它的不需要的管理员功能更新，则需要创建 BaselineStickinessVersions2019 Reg_SZ 数据值并将其设置为一个字符串，该字符串表示客户端计算机须对齐和保持的优选基线。 字符串可以包含允许的服务基线版本，例如 **16.9.0**。  
     如果 `BaselineStickinessVersions2019` 注册表值的格式不正确，则将阻止在计算机上安装所有管理员功能更新。 请务必关注[支持的 Visual Studio 功能更新时间范围](/visualstudio/productinfo/vs-servicing-vs)。 另外，不管 `BaselineStickinessVersions2019` 键是否存在或值为多少，虽然从技术上讲是可以应用已达到生存期终点的功能更新，但不建议这样做，因为它们将不再受支持，可能不安全。

::: moniker-end

* 即使正在使用 Visual Studio，也强制进行更新：安装更新之前，必须关闭 visual Studio。 如果 Visual Studio 已打开或正在使用，则更新安装将被中止。 若要确保 Visual Studio 已关闭，一种简单的方法是将 Configuration Manager 配置为在计算机重启后立即应用更新。 你也可以使用 `--force` 参数强制关闭 Visual Studio。 强制 Visual Studio 关闭可能会导致工作丢失，因此请谨慎使用。 在默认系统上下文中运行管理员更新将忽略 `–-force` 标志，因此你需要将管理员更新配置为在用户上下文中运行。

### <a name="methods-for-configuring-an-administrator-update"></a>配置管理员更新的方法

有三种主要方法可用于配置管理员更新：注册表项、客户端计算机上的配置文件或对 Configuration Manager 部署包本身的修改。   

* 注册表项：管理员更新会在任何标准 Visual Studio 位置查找特定的注册表项，如[为企业部署设置默认值](../install/set-defaults-for-enterprise-deployments.md)中所述。 注册表项控制的选项包括 **AdministratorUpdatesEnabled** Reg_DWORD **AdministratorUpdatesOptOut**  Reg_DWORD。 需要对客户端计算机具有管理员访问权限才能创建并设置注册表项的值。

* 配置文件：某些设置可保留在客户端计算机上的可选配置文件中，这样做的好处是只需设置该文件一次，就可以将它应用于以后的所有管理员更新。 配置文件方法的行为类似于注册表项，并且作用于计算机范围内，这意味着它将适用于客户端计算机上安装的所有 Visual Studio 安装。 配置文件的标准位置位于 `C:\ProgramData\Microsoft\VisualStudio\updates.config`。 但是，如果你想要使用另一个位置来存储该文件，则可创建一个名为 UpdateConfigurationFile 的 Reg_SZ 注册表项，并将此项的值设置为你的配置文件的路径。 此注册表项可放置在任何 Visual Studio 注册表位置中，如[为企业部署设置默认值](../install/set-defaults-for-enterprise-deployments.md)中所述。 如果你选择为自定义配置文件位置添加注册表值，则它将查找该文件；如果文件不存在，则会引发异常，并且更新将失败。

     配置文件采用 JSON 格式，它支持选项 `installerUpdateArgs`，这是一个由逗号分隔的字符串数组，用于指定可传递到 Visual Studio 安装程序中的更多开关。 如果该文件的内容包含无效字段或不受支持的选项，则更新将失败。 有关详细信息，请参阅[使用命令行参数安装 Visual Studio](../install/use-command-line-parameters-to-install-visual-studio.md)。

   下面是一个示例配置文件：

  ```json
  "installerUpdateArgs" : ["--quiet", "--noWeb"], 
  "checkPendingReboot" :  "true" 
  ```

* 手动更新 SCCM 中的管理员更新包：还可以手动修改 SCCM 中单个管理员更新包的命令行参数。

## <a name="verification-reports-and-troubleshooting-error-codes"></a>验证、报表和疑难解答错误代码

### <a name="determining-that-visual-studio-was-updated"></a>确定是否已更新 Visual Studio

可使用以下一种方法来验证是否已正确安装管理员更新：

* 在客户端计算机上，启动 Visual Studio，选择“帮助” >“关于”，验证版本号是否与预期更新标题中的最后一个数字匹配 ****  **** 。
* 使用客户端计算机上的 vswhere 工具标识计算机上各种版本的 Visual Studio。 有关详细信息，请参阅 [用于检测和管理 Visual Studio 实例的工具](../install/tools-for-managing-visual-studio-instances.md)。
* 每个管理更新尝试会在客户端计算机的 `%temp%` 目录中生成几个日志文件，该目录用于捕获更新操作的进度。按日期对文件夹进行排序，并分别为管理更新、引导程序、Visual Studio 安装程序和安装引擎查找以  `dd_updatedriver`、 `dd_bootstrapper`、 `dd_client` 和  `dd_setup` 开头的文件。验证这些日志文件是否包含一个 0，指示已成功应用更新。 请注意，这些日志文件还可用于验证配置文件是否正在使用。 有关更多详细信息，请参阅 [Visual Studio 日志收集工具](https://www.microsoft.com/download/details.aspx?id=12493)。

### <a name="error-codes-and-conditions"></a>错误代码和条件

>[!IMPORTANT]
> 请记住，在安装更新之前，必须关闭 Visual Studio。 如果 Visual Studio 已打开或正在使用，则更新安装将被取消。

管理更新可能返回以下返回代码：  

| 错误代码 | 定义                                                                                                    |
|------------|---------------------------------------------------------------------------------------------------------------|
| 0          | 已成功安装管理更新。                                                         |
| 1001       | Visual Studio 安装程序或相关安装过程正在运行。 未应用更新。                     |
| 1002       | Visual Studio 安装程序已暂停。 未应用更新。                                                 |
| 1003       | Visual Studio 正在运行。 未应用更新。 使用 `--force` 标志可否决此条件。 |
| 1004       | 未检测到 Internet。更新无法与保存更新文件的 Internet 位置联系。 未应用更新。 |
| 1005       | AdministratorUpdatesEnabled 注册表值设置为 0 或根本未设置 **** 。 未应用更新。 |
| 1006       | AdministratorUpdatesOptOut 注册表值设置为 1 **** 。 未应用更新。 此项适用于不应由管理员更新的客户端计算机。 |
| 1007       | 未安装 Visual Studio 安装程序。                                                                 |
| 1008       | BaselineStickinessVersions2019 注册表值的格式不可读。                            |
| 1009       | 该Visual Studio实例配置为使用布局，但该布局缺少执行更新的包。 |
| 3010       | 系统需要重启。更新可能已应用，也可能未应用。 重启计算机，然后重试更新。 |
| 862968     | 更新成功，建议重启，但不要求重启。                                     |
| 其他      | 尝试应用更新时出错。未应用更新。                                     |

有关客户端错误代码的详尽列表，请参阅 [使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)。

## <a name="feedback-and-support"></a>反馈和支持

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

可使用以下方法，提供有关 Visual Studio 管理员更新的反馈或报告影响更新的问题：

* 请参阅 [Visual Studio 安装和升级问题疑难解答](../install/troubleshooting-installation-issues.md)指南。
* 在 [Visual Studio 安装常见问题解答论坛](/answers/topics/vs-setup.html)上向社区提问。
* 请转到 [Visual Studio 支持页面](https://visualstudio.microsoft.com/vs/support/)，检查你的问题是否在常见问题解答中列出。  你也可以选择[支持链接](https://visualstudio.microsoft.com/vs/support/#talktous)按钮以获取聊天帮助。
* 向 Visual Studio 团队[提供功能反馈或报告有关此应用管理员更新体验的问题](https://aka.ms/vs/wsus/feedback)。
* 与你组织的 Microsoft 技术部客户经理联系。

## <a name="see-also"></a>另请参阅

* [启用管理员更新](../install/enabling-administrator-updates.md)
* [Visual Studio 管理员指南](../install/visual-studio-administrator-guide.md)
* [Visual Studio 产品生命周期和维护](/visualstudio/productinfo/vs-servicing-vs)
* [Visual Studio 2019 发行说明](/visualstudio/releases/2019/release-notes)
* [Visual Studio 2017 发行说明](/visualstudio/releasenotes/vs2017-relnotes)
* [安装 Visual Studio](../install/install-visual-studio.md)
* [使用命令行参数安装 Visual Studio](../install/use-command-line-parameters-to-install-visual-studio.md)
* [用于检测和管理 Visual Studio 实例的工具](../install/tools-for-managing-visual-studio-instances.md)
* [创建 Visual Studio 的网络安装](../install/create-a-network-installation-of-visual-studio.md)
* [如何在响应文件中定义设置](../install/automated-installation-with-response-file.md)
* [控制对基于网络的 Visual Studio 部署的更新](../install/controlling-updates-to-visual-studio-deployments.md)
* [Microsoft 更新目录常见问题解答](https://www.catalog.update.microsoft.com/faq.aspx)
* [Microsoft Endpoint Configuration Manager (SCCM) 文档](/mem/configmgr)
* [将 Microsoft 目录中的更新导入 Configuration Manager](/mem/configmgr/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog)
* [Windows Server Update Services (WSUS) 文档](/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus)
