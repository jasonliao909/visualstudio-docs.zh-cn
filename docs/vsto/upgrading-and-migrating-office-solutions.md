---
title: 升级和迁移Office解决方案
description: 如果具有在早期版本的 Visual Studio 中创建的 Offince 项目，则必须升级项目，以在当前版本的 Visual Studio 中使用它。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], upgrading
- Office projects [Office development in Visual Studio], upgrading
- upgrading applications [Office development in Visual Studio]
- upgrading Office solutions in Visual Studio
- migrating Office solutions in Visual Studio
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: af09d705ddeb0fdbf01244ee085d93fb54d52ac7969c8e1e6de9917abc32b431
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121384140"
---
# <a name="upgrade-and-migrate-office-solutions"></a>升级和迁移Office解决方案
  如果你拥有在 Visual Studio 早期版本中创建的 Microsoft Office 项目，则必须升级该项目以在 Visual Studio 当前版本中使用。 若要升级 Microsoft Office 项目，请在包含 Microsoft Office 开发人员工具的 Visual Studio 版本中打开该项目。 有关包含开发人员工具的 Visual Studio 版本Microsoft Office，请参阅配置计算机以开发 Office[解决方案](../vsto/configuring-a-computer-to-develop-office-solutions.md)。

[!include[Add-ins note](includes/addinsnote.md)]

> [!NOTE]
> Visual Studio 无法升级使用 Visual Studio 早期版本创建的 InfoPath 窗体模板项目。 当前版本的 Visual Studio 不支持这些类型的项目。

## <a name="changes-to-upgraded-projects"></a>对已升级项目的更改
 升级 Microsoft Office 项目时，Visual Studio 会将项目修改为面向以下各项：

- 适用于 Visual Studio 运行时的 Office 2010 工具。 有关详细信息，请参阅 Visual Studio Tools for Office[运行时概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)。

- 当前程序集引用。

- 该项目类型所支持的 .NET framework 版本（仅在升级到 Visual Studio 2013 时支持）。

- 该项目类型所支持的 Microsoft Office 版本（仅在升级到 Visual Studio 2013 时支持）。

## <a name="assembly-references"></a>程序集引用
 Visual Studio 将升级项目中的以下程序集引用：

- Microsoft Office 主互操作程序集 (PIA)。

- [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]中的程序集。 有关这些程序集的信息，请参阅Visual Studio Tools for Office[概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)。

- 新的或更新版本的依赖程序集。

## <a name="targeted-net-framework"></a>已面向 .NET Framework
 将项目升级到 Visual Studio 2013 时，Visual Studio 会将该项目修改为面向 [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] 或 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]。 项目所面向的 .NET Framework 版本取决于你计算机上安装的 Office 的版本。 如果安装的是 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] ，Visual Studio 会将项目修改为面向 [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]。 否则，Visual Studio 会将项目修改为面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]。

> [!NOTE]
> 你可能需要执行一些附加步骤以在开发和最终用户计算机上运行重定目标的解决方案，并且如果你的项目使用了某些功能，它将无法再编译。 有关详细信息，请参阅将[Office 解决方案迁移到 .NET Framework 4 或更高版本](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)。

 如果面向 Office 项目中的 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本，可以使用在面向 .NET Framework 3.5 时不可用的一些功能。 有关详细信息，请参阅[设计和创建Office解决方案](../vsto/designing-and-creating-office-solutions.md)。

## <a name="targeted-office-application"></a>目标Office应用程序
 将 Office 项目升级到 Visual Studio 2013 时，Visual Studio 会将该项目修改为面向该项目类型所支持的 Microsoft Office 版本，如文档级自定义项目或 VSTO 外接程序项目。

 Visual Studio 2013 中的 Office 项目可面向 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)][!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] 和应用程序。 Visual Studio 将项目修改为面向已安装的 Office 的最新版本。 如果未安装任何上述版本的 Office，Visual Studio 将不会升级项目。

> [!NOTE]
> 如果将 VSTO 项目升级到目标或更高版本，请确保 VSTO 外接程序的事件处理程序不包含访问应用程序中文档 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] `ThisAddIn_Startup` 的代码。 有关详细信息，请参阅[在应用程序启动时访问Office文档](../vsto/programming-vsto-add-ins.md#AccessingDocuments)。

 对于文档级自定义，将项目中具有二进制格式的文档（例如具有.xls或.doc扩展名的文档）转换为 Office [!INCLUDE[vs_current_short](../sharepoint/includes/vs-current-short-md.md)] Open XML 格式。 有关 Open XML 的信息，请参阅 [新文件扩展名简介和 Open XML 格式](https://support.office.com/en-nz/article/Introduction-to-new-file-name-extensions-eca81dcb-5626-4e5b-8362-524d13ae4ec1)。

> [!NOTE]
> Word 2010 和 Excel 2010 中已弃用智能标记。 因此，如果你的解决方案使用了智能标记，则必须先删除它们，然后才能在 Visual Studio 2013 或 Visual Studio 2015 中测试和调试你的解决方案。

## <a name="upgrade-microsoft-office-2003-projects"></a>升级Microsoft Office 2003 项目
 升级面向 Microsoft Office 2003 的文档级自定义项和 VSTO 外接程序时还有一些其他的注意事项。

### <a name="document-level-projects"></a>文档级项目
 如果项目中的文档包含 Windows 窗体控件，则在升级该项目前你还必须安装 Visual Studio 2005 Tools for Office Second Edition Runtime。 如果在升级项目之前未在开发计算机上未安装此版本的运行时，升级后的项目可能包含编译或运行时错误。 完成项目升级后，如果它未被任何其他 Office 解决方案使用，你可以将 Visual Studio 2005 Tools for Office Second Edition Runtime 从开发计算机上卸载。 可以从 Microsoft 下载中心（网址为： [Microsoft Visual Studio 2005 Tools for Office Second Edition Runtime (VSTO 2005 SE) (x86)](https://www.microsoft.com/download/details.aspx?id=2392)）下载此版本的运行时作为可再发行组件包。

### <a name="vsto-add-in-projects"></a>VSTO 外接程序项目
 如果原始项目的解决方案文件包含一个已配置为安装 VSTO 外接程序的安装项目或 InstallShield Limited Edition 项目，Visual Studio 将升级该项目，但不会对项目进行任何进一步的更改。 如果你想要继续使用 Windows Installer 文件来部署 VSTO 外接程序，则必须将安装项目或 InstallShield Limited Edition 项目修改为安装新的必备组件，如 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]、Visual Studio 2010 Tools for Office Runtime 和 VSTO 外接程序引用的主互操作程序集（可选）。 有关详细信息，请参阅使用 Office[安装程序部署Windows解决方案](../vsto/deploying-a-vsto-solution-by-using-windows-installer.md)。

 如果你想要使用 ClickOnce 来部署 VSTO 外接程序，则可以完全删除安装项目或 InstallShield Limited Edition 项目。 有关使用 VSTO 部署外接程序ClickOnce，请参阅部署 Office[解决方案](../vsto/deploying-an-office-solution.md)。

## <a name="see-also"></a>另请参阅
- [如何：升级Office解决方案](/previous-versions/4bez6837(v=vs.140))
- [将Office解决方案迁移到 .NET Framework 4 或更高版本](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)
- [Project"升级"--"选项"对话框](../vsto/project-upgrade-options-dialog-box.md)