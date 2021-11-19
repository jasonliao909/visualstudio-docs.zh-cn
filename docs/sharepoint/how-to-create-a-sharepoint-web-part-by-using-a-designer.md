---
title: 如何：使用设计器SharePoint创建 Web 部件|Microsoft Docs
titleSuffix: ''
description: 通过将可视化 Web 部件项添加到 SharePoint 项目来创建 Web 部件，这将在 Visual Studio 中打开 Visual Web 开发人员设计器。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Web Parts [SharePoint development in Visual Studio], designer
- Web Parts [SharePoint development in Visual Studio], adding
- Web Parts [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 5f1c22bd8f7ea1c48d9b5f84f2c63cc82c3f27b5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671931"
---
# <a name="how-to-create-a-sharepoint-web-part-by-using-a-designer"></a>如何：使用设计器SharePoint Web 部件

  可以通过向任何项目添加 **Visual Web 部件** 项来创建SharePoint部件。 这将打开 Visual Web 开发人员设计器Visual Studio，可在其中向 Web 部件添加控件和代码。 视觉 Web 部件的功能与 Web 部件的功能相同。 唯一的区别是在 Visual Web 开发人员设计器中设计可视化 Web 部件。

## <a name="to-create-a-project-for-visual-web-parts"></a>为可视 Web 部件创建项目

1. 在菜单栏上，依次选择“文件” >“新建” > “项目”。
::: moniker range="=vs-2017"

2. 在 **"新建Project"** 对话框中的 **"Visual C#"** 或"Visual Basic"下，展开 **"Office/SharePoint"** 节点，然后选择"SharePoint **解决方案"** 类别。 

3. 在项目模板列表中，选择"SharePoint **2013 - Visual Web 部件**"，然后选择"确定 **"** 按钮。

     将显示 **SharePoint自定义向导**。
::: moniker-end
::: moniker range=">=vs-2019"
2. 在"**创建新Project** 对话框中，选择SharePoint安装的特定版本的 SharePoint Visual *Web* 部件 *。 例如，如果安装了 2019 SharePoint，请选择"SharePoint **2019 - Visual Web 部件"** 模板。
    [!INCLUDE[new-project-dialog-search](../sharepoint/includes/new-project-dialog-search-md.md)]

3. 如果需要，请更改项目的名称，然后选择"创建 **"** 按钮。

::: moniker-end
4. 在 **"指定** 用于调试的站点和安全级别"页上，SharePoint本地计算机上站点 URL，然后选择"完成 **"** 按钮。

     在 **解决方案资源管理器** 中，将显示一个 Web 部件。 在 Visual Web 开发人员设计器中设计 Web 部件后，你将在指定的站点上测试它。

### <a name="to-add-a-visual-web-part-to-an-existing-sharepoint-project"></a>将可视化 Web 部件添加到现有 SharePoint 项目

1. 在菜单栏上，依次选择“项目” > “添加新项”。

2. 在"**添加新项"** 对话框中，选择 **Office/SharePoint** 节点。

3. 在项目模板列表中，选择 **"Visual Web 部件**"，将其命名，然后选择"添加 **"** 按钮。

     在 **解决方案资源管理器** 中，将显示 Web 部件。 在 Visual Web 开发人员设计器中设计 Web 部件后，你将在指定的站点上测试它。

## <a name="see-also"></a>另请参阅

- [为 SharePoint 创建 Web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)
- [如何：创建 SharePoint Web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md)
- [演练：为 SharePoint 创建 Web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)
- [演练：使用设计器为 SharePoint 创建 Web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)
