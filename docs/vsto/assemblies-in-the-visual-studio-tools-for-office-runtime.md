---
title: Visual Studio Tools for Office 运行时中的程序集
description: 了解 Visual Studio 会自动将引用添加到 Visual Studio Tools for Office 运行时程序集。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual Studio Tools for Office runtime, assemblies
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: a811040f9106666a86778db4a8278d0f5f450855
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122083773"
---
# <a name="assemblies-in-the-visual-studio-tools-for-office-runtime"></a>Visual Studio Tools for Office 运行时中的程序集
  在创建新的 Office 项目时，Visual Studio 会自动添加对项目类型和项目的目标 .NET Framework 使用的 [!INCLUDE[vsto_runtime](includes/vsto-runtime-md.md)] 程序集的引用。 在 .NET Framework 3.5、 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]和 [!INCLUDE[net_v45](includes/net-v45-md.md)]的 Office 扩展中存在不同的程序集。 有关 Office 扩展的详细信息，请参阅[Visual Studio Tools for Office 运行时概述](visual-studio-tools-for-office-runtime-overview.md)。

## <a name="assemblies-in-the-office-extensions-for-the-net-framework-4-and-the-net_v45"></a>.NET Framework 4 和的 Office 扩展中的程序集[!INCLUDE[net_v45](includes/net-v45-md.md)]
 下表列出了包含在 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 和 [!INCLUDE[net_v45](includes/net-v45-md.md)]的 Office 扩展中的程序集。 有关这些程序集中的命名空间和类型的文档，请参阅[Visual Studio&#41;中 Office 开发的托管引用 &#40;](managed-reference-office-development-in-visual-studio.md)。

|程序集名称|说明|
|-------------------|-----------------|
|Microsoft.Office.Tools.Common.dll|提供以下类型：<br /><br /> -用于创建功能区自定义和智能标记的类型。 **注意：**      在和中已弃用智能标记 [!INCLUDE[Excel_14_short](includes/excel-14-short-md.md)] [!INCLUDE[Word_14_short](includes/word-14-short-md.md)] 。<br />-用于在文档级自定义项中创建操作窗格的类型和 VSTO 外接程序中的自定义任务窗格。|
|Microsoft.Office.Tools.Excel.dll|提供表示 Excel 项目的主机项和主机控件以及支持类型的接口。 有关详细信息，请参阅[使用扩展对象自动 Excel](automating-excel-by-using-extended-objects.md)。|
|Microsoft.Office.Tools.Outlook.dll|提供可用于在 Outlook VSTO 外接程序中创建自定义窗体区域的类型。|
|Microsoft.Office.Tools.Word.dll|提供表示 Word 项目的主机项和主机控件及支持类型的接口。 有关详细信息，请参阅 [使用扩展对象实现 Word 自动化](automating-word-by-using-extended-objects.md)。|
|Microsoft.Office.Tools.v4.0.Framework.dll|提供以下类型：<br /><br /> -可以由 Visual Studio Tools for Office 运行时引发的异常。<br />-在创建 Outlook 窗体区域时可使用的属性。|
|Microsoft.Office.Tools.dll|提供作为 Visual Studio Tools for Office Runtime 基础结构一部分，并且不应在代码中直接使用的类型。|
|Microsoft.VisualStudio.Tools.Applications.Runtime.dll|提供以下类型：<br /><br /> - <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 属性和 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType> 接口，可用于在文档级自定义项中缓存数据对象。 有关详细信息，请参阅 [缓存数据](caching-data.md)。<br />- <xref:Microsoft.VisualStudio.Tools.Applications.Deployment.IAddInPostDeploymentAction> 接口，可以实现该接口，以便将其他安装步骤作为 Office 解决方案的 ClickOnce 安装程序的最后一步来运行。 有关详细信息，请参阅[使用 ClickOnce 部署 Office 解决方案](deploying-an-office-solution-by-using-clickonce.md)。<br />-可以由 Visual Studio Tools for Office 运行时引发的异常。<br />-作为 Visual Studio Tools for Office 运行时基础结构一部分的其他类型，不应在代码中直接使用。|
|Microsoft.VisualStudio.Tools.Applications.ServerDocument.dll|提供以下类型：<br /><br /> - <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 类，可用于将自定义程序集附加到文档并访问文档中的缓存数据。 有关详细信息，请参阅 [使用 ServerDocument 类管理服务器上的文档](managing-documents-on-a-server-by-using-the-serverdocument-class.md)。<br />-表示文档级自定义中的缓存数据层次结构的几个类。 有关详细信息，请参阅在 [服务器上访问文档中的数据](accessing-data-in-documents-on-the-server.md)。|

 以 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或 [!INCLUDE[net_v45](includes/net-v45-md.md)] 为目标的项目还引用以下程序集。 这些程序集不属于 [!INCLUDE[vsto_runtime](includes/vsto-runtime-md.md)] 可再发行组件。 相反，它们是必须与解决方案一起部署的依赖程序集。 默认情况下，它们复制到项目的生成输出文件夹（这些程序集的 **“本地属性”** 属性设置为 **“True”**）。 如果使用 ClickOnce 部署项目，这些程序集包含在生成的包中。

|程序集名称|说明|
|-------------------|-----------------|
|Microsoft.Office.Tools.Common.v4.0.Utilities.dll|提供 VSTO 外接程序项目中生成的 `ThisAddIn` 类和所有项目中生成的功能区类的基类。|
|Microsoft.Office.Tools.Excel.v4.0.Utilities.dll|提供以下类型：<br /><br /> - `ThisWorkbook` `Sheet` Excel 的文档级项目中生成的类和类的基类。<br />-Windows 窗体可以在 Excel 项目中的工作表上使用的控件。|
|Microsoft.Office.Tools.Outlook.v4.0.Utilities.dll|提供 Outlook 项目中生成的 `ThisAddIn` 和窗体区域类的基类。|
|Microsoft.Office.Tools.Word.v4.0.Utilities.dll|提供以下类型：<br /><br /> - `ThisDocument` Word 的文档级项目中生成的类的基类。<br />-Windows 窗体可以在 Word 项目中的文档上使用的控件。|

## <a name="assemblies-in-the-office-extensions-for-the-net-framework-35"></a>.NET Framework 3.5 的 Office 扩展中的程序集
 下表列出了包含在 .NET Framework 3.5 的 Office 扩展中的程序集。 有关这些程序集中的命名空间和类的文档，请参阅 Visual Studio 2008 文档中的以下参考部分： [http://go.microsoft.com/fwlink/?LinkId=160658](managed-reference-office-development-in-visual-studio.md) 。

|程序集名称|说明|
|-------------------|-----------------|
|Microsoft.Office.Tools.Common.v9.0.dll|提供以下类型：<br /><br /> -Microsoft。Office。VSTO 外接程序的加载项基类。<br />-用于创建功能区自定义和智能标记的类。 **注意：**      在和中已弃用智能标记 [!INCLUDE[Excel_14_short](includes/excel-14-short-md.md)] [!INCLUDE[Word_14_short](includes/word-14-short-md.md)] 。<br />-用于在文档级自定义项中创建操作窗格的类，以及 VSTO 外接程序中的自定义任务窗格。|
|Microsoft.Office.Tools.Excel.v9.0.dll|提供 Excel 解决方案的主机项和主机控件。 有关详细信息，请参阅[使用扩展对象自动 Excel](automating-excel-by-using-extended-objects.md)。|
|Microsoft.Office.Tools.Outlook.v9.0.dll|提供可用于在 Outlook VSTO 外接程序中创建自定义窗体区域的类。|
|Microsoft.Office.Tools.Word.v9.0.dll|提供 Word 解决方案的主机项和主机控件。 有关详细信息，请参阅 [使用扩展对象实现 Word 自动化](automating-word-by-using-extended-objects.md)。|
|Microsoft.Office.Tools.v9.0.dll|提供以下类型：<br /><br /> - [RemoteBindableComponent](/previous-versions/visualstudio/visual-studio-2008/bb546360(v=vs.90)) 类，该类提供文档级自定义项中的主机控件的数据绑定功能。<br />-作为 Visual Studio Tools for Office 运行时基础结构一部分的其他类型，不应在代码中直接使用。|
|Microsoft.VisualStudio.Tools.Applications.Runtime.v9.0.dll|提供以下类型：<br /><br /> - <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 属性和 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType> 接口，可用于在文档级自定义项中缓存数据对象。 有关详细信息，请参阅 [缓存数据](caching-data.md)。<br />-可以由 Visual Studio Tools for Office 运行时引发的异常。<br />-作为 Visual Studio Tools for Office 运行时基础结构一部分的其他类型，不应在代码中直接使用。|
|Microsoft.VisualStudio.Tools.Applications.Runtime.v10.0.dll|提供 <xref:Microsoft.VisualStudio.Tools.Applications.Deployment.IAddInPostDeploymentAction> 接口，可实现该接口以将其他安装步骤作为 Office 解决方案的 ClickOnce 安装程序的最后一步进行运行。 有关详细信息，请参阅[高级 Office 解决方案部署](/previous-versions/visualstudio/visual-studio-2010/dd234217(v=vs.100))。|
|Microsoft.VisualStudio.Tools.Applications.ServerDocument.v10.0.dll|提供以下类型：<br /><br /> - <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 类，可用于以编程方式将自定义程序集附加到文档并访问文档中的缓存数据。 有关详细信息，请参阅 [使用 ServerDocument 类管理服务器上的文档](managing-documents-on-a-server-by-using-the-serverdocument-class.md)。<br />-表示文档级自定义中的缓存数据层次结构的几个类。 有关详细信息，请参阅 [访问服务器上文档中的数据](accessing-data-in-documents-on-the-server.md)。|
|Microsoft.VisualStudio.Tools.Office.Runtime.v10.0.dll|提供以下类型：<br /><br /> - Microsoft.VisualStudio.Tools。Office。Runtime.Security.AddInSecurityEntry 和 Microsoft.VisualStudio.Tools。Office。Runtime.Security.UserInclusionList 类，可用于创建用户包含列表条目，以向面向 Office 3.5 的 .NET Framework Office 解决方案授予信任。<br />- 属于运行时基础结构Visual Studio Tools for Office，不应直接在代码中使用的其他类型。|

## <a name="see-also"></a>请参阅
- [Visual Studio Tools for Office运行时概述](visual-studio-tools-for-office-runtime-overview.md)
- [Visual Studio Tools for Office运行时安装方案](visual-studio-tools-for-office-runtime-installation-scenarios.md)
