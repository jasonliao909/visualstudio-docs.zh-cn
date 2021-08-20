---
title: 创作安装程序Windows包|Microsoft Docs
description: 了解如何为包含Windows注册表Visual Studio的数据库表创建一个安装程序包。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122086908"
---
# <a name="author-a-windows-installer-package"></a>创作Windows安装程序包
数据驱动Windows安装程序模型。 例如，不是编写过程脚本来复制文件和写入注册表项，而是在包含文件和注册表数据的数据库表中创作行和列。

## <a name="database-entries"></a>数据库条目
若要安装 VSPackage，Windows安装程序包必须包含数据库条目才能执行以下任务：

- 搜索系统以使用 Windows Installer 表查找 VSPackage 支持 (的版本，这些表包括 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] AppSearch、CompLocator、RegLocator、DrLocator 和 Signature) 。

- 如果未安装受支持的 版本，或者未满足 VSPackage 的另一个系统要求，则取消安装 ([!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] LaunchCondition 表) 。

- 使用目录、组件和文件表 (安装 VSPackage 和依赖) 。

- 使用注册表表文件将 VSPackage 的适当 (添加到注册表) 。

- 通过使用 CustomAction 表 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]devenv.exe **/setup** (集成 VSPackage) 。

有关详细信息，请参阅 Windows[安装程序](/windows/desktop/Msi/windows-installer-portal)。

## <a name="setup-tools"></a>安装工具
各种第三方安装工具为安装程序包Windows环境。 以下免费工具可用：

- InstallShield Limited Edition

   可以通过"新建"对话框获取 InstallShield **Visual Studio Project** 版本。 展开 **"其他Project类型**"，然后选择"**设置和部署"。** 选择 InstallShield 模板。

- Windows安装程序 XML 工具集

   Windows安装程序 XML (WiX) 工具集Windows XML 源文件中的安装程序包。 WiX 工具集是一个 Microsoft 开源项目。 可以从 Wix 工具集 下载 [源代码和可执行文件](https://sourceforge.net/projects/wix/)。

   有关使用 集成到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中的商业产品， [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 请参阅 Visual Studio[市场](https://marketplace.visualstudio.com/)。

## <a name="see-also"></a>请参阅
- [使用安装程序安装 VSPackages Windows安装程序](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
