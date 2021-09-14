---
title: 配置计算机以开发Office解决方案
description: 了解如何安装受支持的 Visual Studio 版本、.NET Framework 和 Microsoft Office，以便创建 VSTO 外接程序和自定义Microsoft Office。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, installing tools
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 7c74dca2c88538ddb0ddb17938ca50f3ab831276
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602310"
---
# <a name="configure-a-computer-to-develop-office-solutions"></a>配置计算机以开发Office解决方案

若要为 Microsoft Office 创建 VSTO 外接程序和自定义项，请安装 Visual Studio、.NET Framework 和 Microsoft Office 的受支持版本。

|软件|支持的版本|
|--------------|------------------------|
|Visual Studio 2017| 任何具有开发 **Office/SharePoint版本**。|
|.NET Framework|- .NET Framework 4 或更高版本。|
|Microsoft Office|<ul><li>任何套件版本的 Office，Microsoft 365企业应用。</li><li>以下任一独立应用程序：<br /><br /> <ul><li>Excel</li><li>InfoPath（仅 Office 2013 和 Office 2010）</li><li>Outlook</li><li>PowerPoint</li><li>Project</li><li>Visio</li><li>Word</li></ul></li></ul><br /> Visual Basic for Applications (VBA) 必须作为 Office 的一部分安装。 **重要提示：** 不支持 2010 Office的即点即用版本。|

有关详细的安装步骤，[请参阅如何：配置计算机以开发Office解决方案](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)。

## <a name="if-project-templates-dont-appear-or-they-dont-work-in-visual-studio"></a>如果未显示项目模板，或者它们无法用于Visual Studio

如果安装了受支持的 Visual Studio、.NET Framework 和 Microsoft Office 版本，但 Office 项目模板未显示在 **Visual Studio"新建 Project"** 对话框中，或者尝试使用时收到错误，请检查以下各项：

- 确保你已经在计算机上安装了 Microsoft Office 开发人员工具。

     Office开发人员工具是 Visual Studio 的可选组件，但它们随 Visual Studio 一起自动安装。 如果通过指定要安装的功能来自定义 Visual Studio 安装，请在安装过程中选择 **“Microsoft Office 开发人员工具”** 来安装这些工具。

     若要确保已安装这些工具，请启动Visual Studio安装程序，然后选择"修改 **"** 按钮。 选中 **“Microsoft Office 开发人员工具”** 复选框，然后选择 **“更新”** 按钮。

- 请确保未运行由即点即Office提供的版本。 请参阅[如何：验证Outlook是否是计算机上"即点即用"应用程序](/previous-versions/office/developer/office-2010/ff864733(v=office.14))。

- 确保仅运行一个版本的 Microsoft Office。

如果仍然遇到问题，请参阅对解决方案 中的错误[Office支持](../vsto/additional-support-for-errors-in-office-solutions.md)。

## <a name="see-also"></a>另请参阅
- [开始&#40;Office开发Visual Studio&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [如何：配置计算机以开发Office解决方案](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)
- [如何：安装Visual Studio Tools for Office可再发行组件](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)
- [如何：安装Office互操作程序集](../vsto/how-to-install-office-primary-interop-assemblies.md)
- [应用程序类型和Office可用的功能](../vsto/features-available-by-office-application-and-project-type.md)