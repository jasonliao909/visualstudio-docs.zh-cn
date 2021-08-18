---
title: 运行时中的Visual Studio Tools for Office程序集
description: 了解Visual Studio运行时程序集Visual Studio Tools for Office添加引用。
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
ms.openlocfilehash: e14f2437380b8391c4261b95fd7da022b75a77dc9302ed2348c432e8a4b3ecb3
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121352287"
---
# <a name="assemblies-in-the-visual-studio-tools-for-office-runtime"></a>运行时中的Visual Studio Tools for Office程序集
  在创建新的 Office 项目时，Visual Studio 会自动添加对项目类型和项目的目标 .NET Framework 使用的 [!INCLUDE[vsto_runtime](includes/vsto-runtime-md.md)] 程序集的引用。 在 .NET Framework 3.5、 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]和 [!INCLUDE[net_v45](includes/net-v45-md.md)]的 Office 扩展中存在不同的程序集。 有关扩展扩展Office，请参阅 Visual Studio Tools for Office[运行时概述](visual-studio-tools-for-office-runtime-overview.md)。

## <a name="assemblies-in-the-office-extensions-for-the-net-framework-4-and-the-net_v45"></a>Office 4 和 的 .NET Framework 扩展中的程序集[!INCLUDE[net_v45](includes/net-v45-md.md)]
 下表列出了包含在 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 和 [!INCLUDE[net_v45](includes/net-v45-md.md)]的 Office 扩展中的程序集。 有关这些程序集中的命名空间和类型的文档，请参阅 &#40;Office[中的托管Visual Studio&#41;。 ](managed-reference-office-development-in-visual-studio.md)

|程序集名称|说明|
|-------------------|-----------------|
|Microsoft.Office.Tools.Common.dll|提供以下类型：<br /><br /> - 用于创建功能区自定义项和智能标记的类型。 **注意：**      智能标记在 和 中 [!INCLUDE[Excel_14_short](includes/excel-14-short-md.md)] 已弃用 [!INCLUDE[Word_14_short](includes/word-14-short-md.md)] 。<br />- 在文档级自定义项和外接程序中的自定义任务窗格中创建VSTO的类型。|
|Microsoft.Office.Tools.Excel.dll|提供表示 Excel 项目的主机项和主机控件以及支持类型的接口。 有关详细信息，请参阅使用[扩展Excel自动执行扩展](automating-excel-by-using-extended-objects.md)。|
|Microsoft.Office.Tools.Outlook.dll|提供可用于在 Outlook VSTO 外接程序中创建自定义窗体区域的类型。|
|Microsoft.Office.Tools.Word.dll|提供表示 Word 项目的主机项和主机控件及支持类型的接口。 有关详细信息，请参阅使用[扩展对象 自动执行 Word。](automating-word-by-using-extended-objects.md)|
|Microsoft.Office.Tools.v4.0.Framework.dll|提供以下类型：<br /><br /> - 运行时可能引发的Visual Studio Tools for Office异常。<br />- 创建窗体区域时Outlook属性。|
|Microsoft.Office.Tools.dll|提供作为 Visual Studio Tools for Office Runtime 基础结构一部分，并且不应在代码中直接使用的类型。|
|Microsoft.VisualStudio.Tools.Applications.Runtime.dll|提供以下类型：<br /><br /> - <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 属性 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType> 和接口，可用于在文档级自定义项中缓存数据对象。 有关详细信息，请参阅缓存 [数据](caching-data.md)。<br />- 接口，你可以实现该接口来运行其他安装步骤，作为 ClickOnce <xref:Microsoft.VisualStudio.Tools.Applications.Deployment.IAddInPostDeploymentAction> 解决方案的应用程序安装程序Office步骤。 有关详细信息，请参阅使用[Office 部署 ClickOnce。](deploying-an-office-solution-by-using-clickonce.md)<br />- 运行时可能引发的Visual Studio Tools for Office异常。<br />- 属于运行时基础结构Visual Studio Tools for Office，不应直接在代码中使用的其他类型。|
|Microsoft.VisualStudio.Tools.Applications.ServerDocument.dll|提供以下类型：<br /><br /> - <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 类，可用于将自定义程序集附加到文档和访问文档中的缓存数据。 有关详细信息，请参阅使用 [ServerDocument 类管理服务器上的文档](managing-documents-on-a-server-by-using-the-serverdocument-class.md)。<br />- 多个类，这些类表示文档级自定义项中缓存数据的层次结构。 有关详细信息，请参阅 [访问服务器上文档中的数据](accessing-data-in-documents-on-the-server.md)。|

 以 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或 [!INCLUDE[net_v45](includes/net-v45-md.md)] 为目标的项目还引用以下程序集。 这些程序集不属于 [!INCLUDE[vsto_runtime](includes/vsto-runtime-md.md)] 可再发行组件。 相反，它们是必须与解决方案一起部署的依赖程序集。 默认情况下，它们复制到项目的生成输出文件夹（这些程序集的 **“本地属性”** 属性设置为 **“True”**）。 如果使用 ClickOnce 部署项目，这些程序集包含在生成的包中。

|程序集名称|说明|
|-------------------|-----------------|
|Microsoft.Office.Tools.Common.v4.0.Utilities.dll|提供 VSTO 外接程序项目中生成的 `ThisAddIn` 类和所有项目中生成的功能区类的基类。|
|Microsoft.Office.Tools.Excel.v4.0.Utilities.dll|提供以下类型：<br /><br /> - 生成的 和 `ThisWorkbook` 文档 `Sheet` 级项目中的类的基类，Excel。<br />- Windows窗体控件，可用于项目Excel工作表。|
|Microsoft.Office.Tools.Outlook.v4.0.Utilities.dll|提供 Outlook 项目中生成的 `ThisAddIn` 和窗体区域类的基类。|
|Microsoft.Office.Tools.Word.v4.0.Utilities.dll|提供以下类型：<br /><br /> - Word 的文档级 `ThisDocument` 项目中生成的类的基类。<br />- Windows Word 项目中的文档使用的窗体控件。|

## <a name="assemblies-in-the-office-extensions-for-the-net-framework-35"></a>.NET Framework 3.5 Office扩展中的程序集
 下表列出了包含在 .NET Framework 3.5 的 Office 扩展中的程序集。 有关这些程序集中的命名空间和类的文档，请参阅 Visual Studio 2008 文档中的以下参考部分 [http://go.microsoft.com/fwlink/?LinkId=160658](managed-reference-office-development-in-visual-studio.md) ：。

|程序集名称|说明|
|-------------------|-----------------|
|Microsoft.Office.Tools.Common.v9.0.dll|提供以下类型：<br /><br /> - Microsoft。Office。用于外接程序的 Tools.AddIn VSTO类。<br />- 用于创建功能区自定义项和智能标记的类。 **注意：**      智能标记在 和 中 [!INCLUDE[Excel_14_short](includes/excel-14-short-md.md)] 已弃用 [!INCLUDE[Word_14_short](includes/word-14-short-md.md)] 。<br />- 在文档级自定义项和外接程序中的自定义任务VSTO创建操作窗格的类。|
|Microsoft.Office.Tools.Excel.v9.0.dll|提供 Excel 解决方案的主机项和主机控件。 有关详细信息，请参阅使用[扩展Excel自动执行扩展](automating-excel-by-using-extended-objects.md)。|
|Microsoft.Office.Tools.Outlook.v9.0.dll|提供可用于在 Outlook VSTO 外接程序中创建自定义窗体区域的类。|
|Microsoft.Office.Tools.Word.v9.0.dll|提供 Word 解决方案的主机项和主机控件。 有关详细信息，请参阅使用[扩展对象 自动执行 Word。](automating-word-by-using-extended-objects.md)|
|Microsoft.Office.Tools.v9.0.dll|提供以下类型：<br /><br /> - [RemoteBindableComponent](/previous-versions/visualstudio/visual-studio-2008/bb546360(v=vs.90)) 类，该类为文档级自定义项中的宿主控件提供数据绑定功能。<br />- 属于运行时基础结构Visual Studio Tools for Office，不应直接在代码中使用的其他类型。|
|Microsoft.VisualStudio.Tools.Applications.Runtime.v9.0.dll|提供以下类型：<br /><br /> - <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 属性 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType> 和接口，可用于在文档级自定义项中缓存数据对象。 有关详细信息，请参阅缓存 [数据](caching-data.md)。<br />- 运行时可能引发的Visual Studio Tools for Office异常。<br />- 属于运行时基础结构Visual Studio Tools for Office，不应直接在代码中使用的其他类型。|
|Microsoft.VisualStudio.Tools.Applications.Runtime.v10.0.dll|提供 <xref:Microsoft.VisualStudio.Tools.Applications.Deployment.IAddInPostDeploymentAction> 接口，可实现该接口以将其他安装步骤作为 Office 解决方案的 ClickOnce 安装程序的最后一步进行运行。 有关详细信息，请参阅高级[Office解决方案部署](/previous-versions/visualstudio/visual-studio-2010/dd234217(v=vs.100))。|
|Microsoft.VisualStudio.Tools.Applications.ServerDocument.v10.0.dll|提供以下类型：<br /><br /> - 类，可用于以编程方式将自定义程序集附加到 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 文档，以及访问文档中缓存的数据。 有关详细信息，请参阅使用 [ServerDocument 类管理服务器上的文档](managing-documents-on-a-server-by-using-the-serverdocument-class.md)。<br />- 多个类，这些类表示文档级自定义项中缓存数据的层次结构。 有关详细信息，请参阅在 [服务器上访问文档中的数据](accessing-data-in-documents-on-the-server.md)。|
|Microsoft.VisualStudio.Tools.Office.Runtime.v10.0.dll|提供以下类型：<br /><br /> -VisualStudio。Office。AddInSecurityEntry 和 VisualStudio 中的。Office。UserInclusionList 类，可用于创建用户包含列表项，以便向面向 .NET Framework 3.5 的 Office 解决方案授予信任。<br />-作为 Visual Studio Tools for Office 运行时基础结构一部分的其他类型，不应在代码中直接使用。|

## <a name="see-also"></a>请参阅
- [Visual Studio Tools for Office 运行时概述](visual-studio-tools-for-office-runtime-overview.md)
- [Visual Studio Tools for Office 运行时安装方案](visual-studio-tools-for-office-runtime-installation-scenarios.md)
