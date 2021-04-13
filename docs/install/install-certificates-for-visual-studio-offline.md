---
title: 安装脱机安装所需的证书
description: 了解如何安装 Visual Studio 脱机安装的证书。
ms.date: 03/29/2021
ms.custom: seodec18, SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 9750A3F3-89C7-4A8F-BA75-B0B06BD772C2
author: ornellaalt
ms.author: ornella
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 0d8441b0a4b8acba3f24f60d5ea8dc7030b79253
ms.sourcegitcommit: 22789927ec8e877b7d2b67a555d6df97d84103e0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2021
ms.locfileid: "105981285"
---
# <a name="install-certificates-required-for-visual-studio-offline-installation"></a>安装 Visual Studio 脱机安装所需的证书

Visual Studio 主要供连接 Internet 的计算机上安装，因为许多组件需要定期更新。 不过，通过额外执行一些步骤，可以在未连接 Internet 的环境中部署 Visual Studio。

Visual Studio 安装程序引擎仅安装受信任的内容。 为此，它会检查正在下载内容的验证码签名，并在安装前验证所有内容是否受信任。 这样可以保证用户环境的安全，在下载位置受到威胁时免受攻击。 因此，Visual Studio 安装程序要求在用户的计算机上安装多个标准的 Microsoft 根证书和中间证书，并保持最新版本。 如果计算机通过 Windows 更新保持最新状态，则签名证书通常是最新状态。 如果计算机连接到 Internet，则在安装过程中，Visual Studio 可能会根据需要刷新证书以验证文件签名。 如果计算机处于脱机状态，则必须采用其他方式刷新证书。

## <a name="how-to-refresh-certificates-when-offline"></a>如何在处于脱机状态时刷新证书

有三个选项可用于在脱机环境中安装或更新证书。

### <a name="option-1---manually-install-certificates-from-a-layout-folder"></a>选项 1 - 从布局文件夹手动安装证书

::: moniker range="vs-2017"

创建[网络布局](../install/create-a-network-installation-of-visual-studio.md)或[本地脱机缓存](../install/create-an-offline-installation-of-visual-studio.md)时，所需证书会下载到 Certificates 文件夹。 然后可以双击每个证书文件，并单击完成证书管理器向导，从而手动安装证书。 如果看到输入密码提示，请将密码留空。

更新：  对于 Visual Studio 2017 版本 15.8 预览版 2 或更高版本，可以通过右键单击每个证书文件，选择“安装证书”，然后单击“证书管理器”向导来手动安装证书。

::: moniker-end

::: moniker range="vs-2019"

创建[网络布局](../install/create-a-network-installation-of-visual-studio.md)或[本地脱机缓存](../install/create-an-offline-installation-of-visual-studio.md)时，所需证书会下载到 Certificates 文件夹。 可以通过右键单击每个证书文件，选择“安装证书”，然后单击“证书管理器”向导来手动安装证书。 如果看到输入密码提示，请将密码留空。

::: moniker-end

### <a name="option-2---distribute-trusted-root-certificates-in-an-enterprise-environment"></a>选项 2 - 在企业环境中分发受信任的根证书

对于企业，如果脱机计算机不具有最新的根证书，管理员可以按照[配置受信任根和不允许的证书](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn265983(v=ws.11))页来更新证书。

### <a name="option-3---install-certificates-as-part-of-a-scripted-deployment-of-visual-studio"></a>选项 3 - 在 Visual Studio 的脚本化部署过程中安装证书

如果正在编写在脱机环境中将 Visual Studio 部署到客户端工作站的脚本，应执行以下步骤：

1. 将[证书管理器工具](/dotnet/framework/tools/certmgr-exe-certificate-manager-tool) (certmgr.exe) 复制到网络布局或本地缓存安装位置。 Windows 自身不附带 Certmgr.exe，但 [Windows SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk) 可以提供。

2. 使用下面的命令创建批处理文件：

   ```cmd
   certmgr.exe -add [layout path]\certificates\manifestRootCertificate.cer -n "Microsoft Root Certificate Authority 2011" -s -r LocalMachine root

   certmgr.exe -add [layout path]\certificates\manifestCounterSignRootCertificate.cer -n "Microsoft Root Certificate Authority 2010" -s -r LocalMachine root

   certmgr.exe -add [layout path]\certificates\vs_installer_opc.RootCertificate.cer -n "Microsoft Root Certificate Authority 2010" -s -r LocalMachine root
   ```
   
   或者，通过以下命令创建批处理文件，该文件使用 Windows 中随附的 certutil.exe：
   
      ```cmd
   certutil.exe -addstore -f "Root" "[layout path]\certificates\manifestRootCertificate.cer"

   certutil.exe -addstore -f "Root" "[layout path]\certificates\manifestCounterSignRootCertificate.cer"

   certutil.exe -addstore -f "Root" "[layout path]\certificates\vs_installer_opc.RootCertificate.cer"
   ```

3. 将批处理文件部署到客户端。 应从提升的进程中运行此命令。

## <a name="what-are-the-certificates-files-in-the-certificates-folder"></a>Certificates 文件夹中的证书文件有哪些？

* manifestRootCertificate.cer 包含：
  * 根证书： Microsoft 根证书颁发机构 2011 
* manifestCounterSignRootCertificate.cer 和 vs_installer_opc.RootCertificate.cer 包含：
  * 根证书： Microsoft 根证书颁发机构 2010 
 
Visual Studio 安装程序只需要在系统上安装根证书。 未安装最新的 Windows 更新的 Windows 7 Service Pack 1 系统需要所有这些证书。

## <a name="why-are-the-certificates-from-the-certificates-folder-not-installed-automatically"></a>为什么无法自动安装 Certificates 文件夹中的证书？

如果是在联机环境中验证签名，Windows API 可用于下载证书并将其添加到系统中。 在此过程中，可通过管理设置验证证书是否受信任且已获允许。 在大多数脱机环境中，无法执行此验证过程。 通过手动安装证书，企业管理员不仅能够确保使用受信任的证书，而且还能够符合组织的安全策略。

## <a name="checking-if-certificates-are-already-installed"></a>检查是否已安装证书

检查安装系统的一种方法是按以下步骤操作：

1. 运行 **mmc.exe**。<br/>
  a. 单击“文件”，然后选择“添加/删除管理单元”   。<br/>
  b. 双击“证书”，选择“计算机帐户”，然后单击“下一步”    。<br/>
  c. 选择“本地计算机”，依次单击“完成”和“确定”    。<br/>
  d. 展开“证书(本地计算机)”  。<br/>
  e. 展开“受信任的根证书颁发机构”，选择“证书”   。<br/>
    * 检查此列表中是否有必需的根证书。<br/>

   f. 展开“中间证书颁发机构”，选择“证书”   。<br/>
    * 检查此列表中是否有需要的中间证书。<br/>

2. 单击“文件”，然后选择“添加/删除管理单元”   。<br/>
  a. 双击“证书”，选择“我的用户帐户”，单击“完成”和“确定”     。<br/>
  b. 展开“证书 - 当前用户”  。<br/>
  c. 展开“中间证书颁发机构”，选择“证书”   。<br/>
    * 检查此列表中是否有需要的中间证书。<br/>

如果证书名称不在“颁发对象”列中，请安装这些证书  。  如果中间证书仅在“当前用户”  中间证书存储中，则仅供已登录的用户使用。 可能需要为其他用户安装它。

## <a name="install-visual-studio"></a>安装 Visual Studio

在客户端计算机上安装证书后，便可以[从本地缓存安装 Visual studio](../install/create-an-offline-installation-of-visual-studio.md#step-3---install-visual-studio-from-the-local-cache)，或[将 Visual Studio 从网络布局共享部署到客户端计算机](create-a-network-installation-of-visual-studio.md#deploy-from-a-network-installation)。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>另请参阅

* [创建 Visual Studio 的网络安装](../install/create-a-network-installation-of-visual-studio.md)
* [创建 Visual Studio 的脱机安装](../install/create-an-offline-installation-of-visual-studio.md)
* [Visual Studio 管理员指南](visual-studio-administrator-guide.md)
* [使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)

