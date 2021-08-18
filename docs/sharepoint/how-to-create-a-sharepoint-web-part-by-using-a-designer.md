---
title: 如何：使用设计器创建 SharePoint Web 部件 |Microsoft Docs
titleSuffix: ''
description: 通过向 SharePoint 项目添加 "可视 web 部件" 项来创建一个 web 部件，该项目将打开 Visual Studio 中的 visual web Developer 设计器。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122131022"
---
# <a name="how-to-create-a-sharepoint-web-part-by-using-a-designer"></a>如何：使用设计器创建 SharePoint Web 部件

  可以通过将 **可视 web 部件** 项添加到任何 SharePoint 项目来创建 web 部件。 这会在 Visual Studio 中打开 Visual Web Developer 设计器，你可以在其中向 Web 部件添加控件和代码。 可视化 web 部件的工作方式与 web 部件的工作方式相同。 唯一的区别是，在 Visual Web Developer 设计器中设计可视 web 部件。

## <a name="to-create-a-project-for-visual-web-parts"></a>为可视 web 部件创建项目

1. 在菜单栏上，依次选择“文件” >“新建” > “项目”。
::: moniker range="=vs-2017"

2. 在 "**新建 Project** " 对话框中的 " **Visual c #** " 或 " **Visual Basic**" 下，展开 **Office/SharePoint** 节点，然后选择 " **SharePoint 解决方案**" 类别。

3. 在项目模板列表中，选择 " **SharePoint 2013-可视 Web 部件**"，然后选择 **"确定"** 按钮。

     此时将显示 " **SharePoint 自定义向导**"。
::: moniker-end
::: moniker range=">=vs-2019"
2. 在 "**创建新 Project** " 对话框中，选择 *SharePoint 的 Visual Web Part**，以获取已安装 SharePoint 的特定版本。 例如，如果您有 SharePoint 2019 安装，请选择 " **SharePoint 2019-可视 Web 部件** 模板"。
    [!INCLUDE[new-project-dialog-search](../sharepoint/includes/new-project-dialog-search-md.md)]

3. 如果需要，请更改项目的名称，然后选择 " **创建** " 按钮。

::: moniker-end
4. 在 "**指定用于调试的站点和安全级别**" 页上，指定本地计算机上的 SharePoint 站点的 URL，然后选择 "**完成**" 按钮。

     在 **解决方案资源管理器** 中，将显示一个 web 部件。 在 Visual Web Developer 设计器中设计 web 部件之后，您将在您指定的站点上对其进行测试。

### <a name="to-add-a-visual-web-part-to-an-existing-sharepoint-project"></a>向现有 SharePoint 项目添加可视 web 部件

1. 在菜单栏上，依次选择“项目” > “添加新项”。

2. 在 "**添加新项**" 对话框中，选择 " **Office/SharePoint** " 节点。

3. 在项目模板列表中，选择 " **可视 Web 部件**"，将其命名为，然后选择 " **添加** " 按钮。

     在 **解决方案资源管理器** 中，将显示你的 web 部件。 在 Visual Web Developer 设计器中设计 web 部件之后，您将在您指定的站点上对其进行测试。

## <a name="see-also"></a>请参阅

- [为 SharePoint 创建 Web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)
- [如何：创建 SharePoint Web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md)
- [演练：为 SharePoint 创建 Web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)
- [演练：使用设计器为 SharePoint 创建 Web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)
