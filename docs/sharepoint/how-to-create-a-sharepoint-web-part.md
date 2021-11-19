---
title: 如何：创建 SharePoint Web 部件 |Microsoft Docs
description: 使用设计器创建和自定义 web 部件，或通过将 web 部件项添加到任何 SharePoint 项目，然后编辑 web 部件的代码文件。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Web Parts [SharePoint development in Visual Studio], adding
- Web Parts [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: ad3761012732f6191d40bfdf47da84221b78209e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126667476"
---
# <a name="how-to-create-a-sharepoint-web-part"></a>如何：创建 SharePoint web 部件
  您可以通过将 **web 部件** 项添加到任何 SharePoint 项目，然后编辑 web 部件的代码文件或使用设计器来创建和自定义 web 部件。 有关详细信息，请参阅[如何：使用设计器创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)。

### <a name="to-create-a-sharepoint-web-part"></a>创建 SharePoint web 部件

1. 创建或打开一个 SharePoint 项目。

     有关详细信息，请参阅[SharePoint 项目和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)。

2. 选择 **解决方案资源管理器** 中的 SharePoint 项目节点，然后选择 " **Project**"  >  **添加新项**"。

3. 在 "**添加新项**" 对话框中，展开 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

4. 在 SharePoint 模板列表中，选择 " **Web 部件**"。

5. 在 " **名称** " 框中，指定 web 部件的名称，然后选择 " **添加** " 按钮。

     Web 部件显示在 **解决方案资源管理器** 中。 有关 web 部件包含的文件的详细信息，请参阅[为 SharePoint 创建 web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)。

6. 在 **解决方案资源管理器** 中，打开刚刚创建的 web 部件的代码文件。

     例如，如果 web 部件的名称为 *WebPart1*，请在 c # ) 中 Visual Basic) 或 *WebPart1* (中打开 *WebPart1* (。

7. 在代码文件中，向 <xref:System.Web.UI.Control.CreateChildControls%2A> 方法添加控件。

     有关示例，请参阅[演练：为 SharePoint 创建 web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)。

## <a name="see-also"></a>另请参阅
- [为 SharePoint 创建 Web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)
- [如何：使用设计器创建 SharePoint Web 部件](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)
- [演练：为 SharePoint 创建 Web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)
- [演练：使用设计器为 SharePoint 创建 Web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)
