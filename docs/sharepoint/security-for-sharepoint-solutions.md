---
title: SharePoint 解决方案的安全性 |Microsoft Docs
description: 了解 Visual Studio 包含哪些功能以帮助提高 SharePoint 应用程序的安全性。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- security [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, security
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: d287552b07f67c7415688fefd87f876242b230f4
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602534"
---
# <a name="security-for-sharepoint-solutions"></a>SharePoint 解决方案的安全性
  [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]包含以下功能，以帮助增强 SharePoint 应用程序的安全性。

## <a name="safe-control-entries"></a>保险箱控件项
 中创建的每个 SharePoint 项目项 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 都具有一个表示安全控件集合的 **保险箱控件项** 属性。 通过其 **保险箱** 子属性，您可以指定您认为安全的控件。 有关详细信息，请参阅[在项目项中提供包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)和[指定保险箱 Web 部件](/previous-versions/office/developer/sharepoint2003/dd583154(v=office.11)#specifying-safe-web-parts)。

## <a name="allowpartiallytrustedcallers-attribute"></a>AllowPartiallyTrustedCallers 属性
 默认情况下，只有运行时代码访问安全 (CA) 系统完全信任的应用程序才能访问共享的托管代码程序集。 使用 AllowPartiallyTrustedCallers 特性标记完全受信任的程序集允许部分受信任的程序集访问它。

 AllowPartiallyTrustedCallers 属性将添加到任何未部署到系统全局程序集缓存 () 的 SharePoint 解决方案中 [!INCLUDE[TLA2#tla_gac](../sharepoint/includes/tla2sharptla-gac-md.md)] 。 这包括已部署到 SharePoint 应用程序 Bin 目录的沙盒解决方案或解决方案。 有关详细信息，请参阅[Microsoft .NET Framework 的版本1安全更改](/previous-versions/msp-n-p/ff921345(v=pandp.10))和[在 SharePoint Foundation 中部署 Web 部件](/previous-versions/office/developer/sharepoint-2010/cc768621(v=office.14))。

## <a name="safe-against-script-property"></a>保险箱脚本属性
 *脚本注入* 是指在控件或网页中插入潜在的恶意代码。 为了帮助保护 SharePoint 2010 站点免受脚本注入，参与者默认情况下不能查看或编辑 Web 部件或其属性。 此行为由名为 SafeAgainstScript 的 SafeControl 属性控制。 在中 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，在项目项的 **保险箱控件项**"子属性"**保险箱对照脚本** 中设置此特性。 有关详细信息，请参阅 [在项目项中提供包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md) 和 [如何：将控件标记为安全控件](../sharepoint/how-to-mark-controls-as-safe-controls.md)。

## <a name="vista-and-windows-7-user-account-control"></a>Vista 和 Windows 7 用户帐户控制
 [!INCLUDE[windowsver](../sharepoint/includes/windowsver-md.md)] 并 [!INCLUDE[win7](../sharepoint/includes/win7-md.md)] 将一个称为用户帐户控制的安全功能合并 (UAC) 。 若要在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 和系统上开发 SharePoint 解决方案 [!INCLUDE[windowsver](../sharepoint/includes/windowsver-md.md)] [!INCLUDE[win7](../sharepoint/includes/win7-md.md)] ，UAC 要求以 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 系统管理员身份运行。 从 " **开始** " 菜单中，打开的快捷菜单 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，然后选择 "以 **管理员身份运行**"。

 若要将 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 快捷方式配置为始终以管理员身份运行，请打开其快捷菜单，选择 "**属性**"，选择 "**属性**" 对话框中的 "**高级**" 按钮，然后选择 "**以管理员身份运行**" 复选框。

 有关详细信息，请参阅[了解和配置 Windows Vista 中的用户帐户控制](/previous-versions/windows/it-pro/windows-vista/cc709628(v=ws.10))。 和[Windows 7 用户帐户控制](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731416(v=ws.10))。

## <a name="sharepoint-permissions-considerations"></a>SharePoint 权限注意事项
 若要开发 SharePoint 解决方案，必须具有足够的权限来运行和调试 SharePoint 解决方案。 在测试 SharePoint 解决方案之前，请执行以下步骤以确保具有必要的权限：

1. 将用户帐户添加为系统上的管理员。

2. 添加用户帐户作为 SharePoint 服务器的场管理员。

    1. 在 SharePoint 2010 中心管理 "中，选择"**管理场管理员组**"链接。

    2. 在 " **场管理员** " 页上，选择 " **新建** " 菜单选项

3. 将用户帐户添加到 WSS_ADMIN_WPG 组。

## <a name="additional-security-resources"></a>其他安全资源
 有关安全问题的详细信息，请参阅以下内容。

### <a name="visual-studio-security"></a>Visual Studio 安全

- [安全性和用户权限](/previous-versions/visualstudio/visual-studio-2010/ms165099(v=vs.100))

- [本机代码和 .NET Framework 代码的安全性](/previous-versions/visualstudio/visual-studio-2010/1787tk12(v=vs.100))

- [.NET Framework 中的安全性](/previous-versions/dotnet/netframework-4.0/fkytk30f(v=vs.100))

### <a name="sharepoint-security"></a>SharePoint 安全性

- [SharePoint基础管理和安全](/previous-versions/office/developer/sharepoint-2010/ee537811(v=office.14))

- [SharePoint安全资源汇](/sharepoint/dev/)

- [在 SharePoint Foundation 中保护 Web 部件](/previous-versions/office/developer/sharepoint-2010/cc768613(v=office.14))

- [提高 Web 应用程序安全性：威胁和对策](/previous-versions/msp-n-p/ff649874(v=pandp.10))

### <a name="general-security"></a>一般安全性

- [MSDN 安全开发生命周期](https://www.microsoft.com/msrc?rtc=1)

- [生成安全的 ASP.NET 应用程序：身份验证、授权和安全通信](/previous-versions/msp-n-p/ff649100(v=pandp.10))

## <a name="see-also"></a>另请参阅

- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)