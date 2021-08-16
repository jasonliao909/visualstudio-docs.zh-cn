---
title: SharePoint 解决方案|Microsoft Docs
description: 了解Visual Studio哪些功能可帮助增强应用程序SharePoint的安全性。
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
ms.openlocfilehash: c46356124b7ed957d3ff61d4118ade2638538d242686875f4a69972b254a3a16
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121367422"
---
# <a name="security-for-sharepoint-solutions"></a>解决方案SharePoint的安全性
  [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]包含以下功能，以帮助增强应用程序SharePoint的安全性。

## <a name="safe-control-entries"></a>保险箱控件条目
 在 中创建SharePoint项目项 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 都有一个保险箱 **控件项**"属性，该属性表示安全控件集合。 通过 **保险箱** 子属性，可以指定你认为安全的控件。 有关详细信息，请参阅在[项目项](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)中提供包和部署信息和[指定保险箱 Web 部件。](/previous-versions/office/developer/sharepoint2003/dd583154(v=office.11)#specifying-safe-web-parts)

## <a name="allowpartiallytrustedcallers-attribute"></a>AllowPartiallyTrustedCallers 属性
 默认情况下，只有运行时代码访问安全性完全受信任的应用程序 (CAS) 系统可以访问共享托管代码程序集。 使用 AllowPartiallyTrustedCallers 属性标记完全受信任的程序集允许部分受信任的程序集访问它。

 AllowPartiallyTrustedCallers SharePoint添加到任何未部署到系统全局程序集缓存的 [!INCLUDE[TLA2#tla_gac](../sharepoint/includes/tla2sharptla-gac-md.md)] () 。 这包括部署到应用程序 Bin 目录的沙SharePoint解决方案。 有关详细信息，请参阅 Microsoft .NET Framework 的版本[1](/previous-versions/msp-n-p/ff921345(v=pandp.10))安全更改和[SharePoint Foundation](/previous-versions/office/developer/sharepoint-2010/cc768621(v=office.14))中的 Web 部件 部署。

## <a name="safe-against-script-property"></a>保险箱脚本属性
 *脚本注入* 是向控件或网页插入潜在恶意代码。 为了帮助保护 2010 SharePoint 2010 站点，参与者默认无法查看或编辑 Web 部件及其属性。 此行为由名为 SafeAgainstScript 的 SafeControl 属性控制。 在 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中，在项目项的"控件项"子保险箱 **针对** 脚本 设置 **保险箱此属性**。 有关详细信息，请参阅在项目项中提供包和 [部署](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md) 信息和 [如何：将控件标记为安全控件](../sharepoint/how-to-mark-controls-as-safe-controls.md)。

## <a name="vista-and-windows-7-user-account-control"></a>Vista 和 Windows 7 用户帐户控制
 [!INCLUDE[windowsver](../sharepoint/includes/windowsver-md.md)] 和 [!INCLUDE[win7](../sharepoint/includes/win7-md.md)] 合并了名为用户帐户控制和 UAC (的) 。 若要在 SharePoint 和 系统上开发解决方案 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] [!INCLUDE[windowsver](../sharepoint/includes/windowsver-md.md)] [!INCLUDE[win7](../sharepoint/includes/win7-md.md)] ，UAC 要求以 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 系统管理员角色运行 。 在"**开始**"菜单中，打开 的快捷菜单 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，然后选择"**以管理员模式运行"。**

 若要将快捷方式配置为始终以管理员方式运行，请打开其快捷菜单，选择"属性"，在"属性"对话框中选择"高级"按钮，然后选择"以管理员方式 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 运行"复选框。    

 有关详细信息，请参阅了解和配置 Windows [Vista 中的用户帐户控制](/previous-versions/windows/it-pro/windows-vista/cc709628(v=ws.10))。 和[Windows 7 用户帐户控制](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731416(v=ws.10))。

## <a name="sharepoint-permissions-considerations"></a>SharePoint权限注意事项
 若要开发SharePoint解决方案，必须具有足够的权限才能运行和调试SharePoint解决方案。 在测试SharePoint之前，请执行以下步骤以确保你拥有必要的权限：

1. 将用户帐户添加为系统管理员。

2. 将用户帐户添加为 SharePoint 服务器的场管理员。

    1. 在 SharePoint 2010 管理中心中，选择"**管理场管理员"组** 链接。

    2. 在" **场管理员"** 页上，选择" **新建"** 菜单选项

3. 将用户帐户添加到组WSS_ADMIN_WPG组。

## <a name="additional-security-resources"></a>其他安全资源
 有关安全问题的信息，请参阅以下内容。

### <a name="visual-studio-security"></a>Visual Studio 安全

- [安全性和用户权限](/previous-versions/visualstudio/visual-studio-2010/ms165099(v=vs.100))

- [本机代码和 .NET Framework 代码的安全性](/previous-versions/visualstudio/visual-studio-2010/1787tk12(v=vs.100))

- [.NET Framework 中的安全性](/previous-versions/dotnet/netframework-4.0/fkytk30f(v=vs.100))

### <a name="sharepoint-security"></a>SharePoint安全性

- [SharePoint基础管理和安全性](/previous-versions/office/developer/sharepoint-2010/ee537811(v=office.14))

- [SharePoint安全资源汇](/sharepoint/dev/)

- [保护 Web 部件 Foundation SharePoint](/previous-versions/office/developer/sharepoint-2010/cc768613(v=office.14))

- [提高 Web 应用程序安全性：威胁和措施](/previous-versions/msp-n-p/ff649874(v=pandp.10))

### <a name="general-security"></a>常规安全性

- [MSDN 安全开发生命周期](https://www.microsoft.com/msrc?rtc=1)

- [生成安全的 ASP.NET 应用程序：身份验证、授权和安全通信](/previous-versions/msp-n-p/ff649100(v=pandp.10))

## <a name="see-also"></a>另请参阅

- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)