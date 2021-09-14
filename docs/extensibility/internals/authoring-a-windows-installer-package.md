---
title: 创作 Windows Installer 包 |Microsoft Docs
description: 了解如何为包含文件和注册表数据的数据库表的 Visual Studio 创作 Windows Installer 包。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- .msi files, VSPackages
- msi files, VSPackages
ms.assetid: 0ce7c21d-0d3f-47fe-a0bb-eed506e32609
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 9b2a279b178a7158db8bde117c3aa1e97ad2925f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665336"
---
# <a name="author-a-windows-installer-package"></a>创作 Windows Installer 包
数据驱动 Windows Installer 模型。 例如，您可以在数据库表中创作包含文件和注册表数据的行和列，而不是编写过程脚本来复制文件和写入注册表项。

## <a name="database-entries"></a>数据库条目
若要安装 VSPackage，Windows Installer 包必须包含用于执行以下任务的数据库条目：

- [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]使用包括 AppSearch、CompLocator、RegLocator、DrLocator 和签名) 的 Windows Installer 表，搜索系统以查找 VSPackage (支持的版本。

- 如果未安装支持的版本 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，或者如果不 (满足 VSPackage 的其他系统要求，则取消安装，) 使用 LaunchCondition 表。

- 使用) 的目录、组件和文件表 (安装 VSPackage 和相关文件。

- 使用注册表)  (将 VSPackage 的相应信息添加到注册表中。

- [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]通过使用 CustomAction 表) 调用 **devenv.exe/setup** (来集成中的 VSPackage。

有关详细信息，请参阅[Windows Installer](/windows/desktop/Msi/windows-installer-portal)。

## <a name="setup-tools"></a>安装工具
许多第三方安装工具为 Windows Installer 包提供了一个开发环境。 提供以下免费工具：

- InstallShield 受限版本

   可以通过 Visual Studio 的 "**新建 Project** " 对话框获取有限版本的 InstallShield。 展开 **其他 Project 类型**，然后选择 "**安装和部署**"。 选择 InstallShield 模板。

- Windows安装程序 XML 工具集

   Windows Installer xml (WiX) 工具集生成 xml 源文件 Windows Installer 包。 WiX 工具集是一个 Microsoft 开源项目。 可以从 [Wix 工具集](https://sourceforge.net/projects/wix/)下载源代码和可执行文件。

   有关使用集成到的商业产品 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] ，请参阅[Visual Studio Marketplace](https://marketplace.visualstudio.com/)。

## <a name="see-also"></a>另请参阅
- [安装 vspackage 与 Windows Installer](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
