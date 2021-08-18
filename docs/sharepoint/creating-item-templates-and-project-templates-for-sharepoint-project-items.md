---
title: 用于项目项的项SharePoint模板
description: 为项目项创建项模板SharePoint模板。 为项模板和项目模板创建向导。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, creating custom templates
- .spdata files
- projects [SharePoint development in Visual Studio], creating custom templates
- SharePoint projects, creating custom templates
- SharePoint development in Visual Studio, creating custom project and item templates
- project items [SharePoint development in Visual Studio], creating custom templates
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: edcc56e0b92d5a694793f54ede8056fbe81ce2b1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122149632"
---
# <a name="create-item-templates-and-project-templates-for-sharepoint-project-items"></a>为项目项创建项模板SharePoint模板

定义自定义项目SharePoint类型时，可以将其与项模板或项目模板关联。 此关联允许其他开发人员使用项目中的项目Visual Studio。 还可以为模板创建向导。

例如，Visual Studio不包含项目模板或项模板，无法将字段添加到SharePoint站点。 可以定义一SharePoint字段的项目项类型，然后构造一个项模板，其他开发人员可以使用该模板将字段项添加到SharePoint项目。 或者，可以构造项目模板，以便开发人员可以创建SharePoint字段项的新项目。 在这两种情况下，还可以提供开发人员使用模板时出现的向导。 此向导可以从开发人员收集信息来配置新项或项目。

项模板和项目模板是.zip文件，其中包含项目Visual Studio创建项目项或项目的文件。 有关项模板和项目模板的基础的详细信息，请参阅 [创建项目和项模板](../ide/creating-project-and-item-templates.md)。

## <a name="create-item-templates"></a>创建项模板
 为项目项创建SharePoint模板时，某些文件始终是必需的，还有一些可选文件可能由某些类型的项目项使用。 有关演示如何定义 SharePoint 项目项类型并为此类型创建项模板的演练，请参阅演练：使用项模板创建自定义操作项目项，第[1 部分](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)。

 下表列出了为项目项创建项模板SharePoint文件。

|所需文件|说明|
|-------------------|-----------------|
|*.spdata* 文件|此 XML 文件指定项目项的内容和默认行为。 此文件必须包含在项模板中。 有关 *.spdata* 文件内容的详细信息，请参阅SharePoint [项目项架构引用](../sharepoint/sharepoint-project-item-schema-reference.md)。|
|*.vstemplate* 文件。|此文件提供Visual Studio在"添加新项"对话框中显示模板以及从模板创建项目项所需的信息。 此文件必须包含在项模板中。 有关详细信息，请参阅模板[Visual Studio文件 。](/previous-versions/visualstudio/visual-studio-2010/xsxc3ete\(v\=vs.100\))|
|一Visual Studio接口的扩展 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 程序集。|此程序集定义项目项的运行时行为。 此程序集必须包含在具有项模板的 VSIX 包中。 有关详细信息，请参阅[定义自定义SharePoint项目项](../sharepoint/defining-custom-sharepoint-project-item-types.md)类型和在 Visual Studio 中为 SharePoint[工具部署Visual Studio。](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)|

 下表列出了项模板中可包含的一些最常见的可选文件。 某些类型的项目项可能需要此处未列出的其他文件。

| 可选文件 | 说明 |
|----------------------| - |
| Elements.xml | Feature *元素* 文件。 此文件定义项目项创建的自定义项的 UI 和行为。 每种类型的自定义（例如列表实例、内容类型或自定义操作）都有一个不同的架构来定义此文件的内容。 有关详细信息，请参阅 [构建基块：](/previous-versions/office/developer/sharepoint-2010/ee537350(v=office.14)) 特性 [和功能架构](/previous-versions/office/developer/sharepoint-2010/ms414322(v=office.14))。 |
| *Schema.xml* | 列表定义的架构文件。 有关详细信息，请参阅构建[基块：列表和文档库](/previous-versions/office/developer/sharepoint-2010/ee534985(v=office.14))以及[Schema.xml。 ](/previous-versions/office/developer/sharepoint-2010/ms459356(v=office.14)) |
| *.webpart* | Web *部件定义* 文件。 此文件包含 Web 部件的属性设置。 有关详细信息，请参阅构建[基块：Web 部件。](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14)) |
| *.ascx* | 一 ASP.NET UserControl 文件。 此文件定义 Visual Web 部件 UI。 |
| *.aspx* | 一 ASP.NET 页文件。 此文件包含定义应用程序页的 XML 标记。 |
| *.cs* 或 *.vb* 文件 | 这些代码文件定义了SharePoint自定义项的行为，这些自定义项具有可以从 Visual C# 或 Visual Basic 代码（如应用程序页、Web 部件和工作流）访问的编程模型。 |

## <a name="create-project-templates"></a>创建项目模板
 创建项目SharePoint模板时，始终需要一些文件和某些类型的项目可能使用的可选文件。 通常，SharePoint项目至少包含一SharePoint项目项。 不过，这不是必需的。 例如，可以定义一SharePoint模板，该模板仅用于部署在其他SharePoint中创建的解决方案。

 有关演示如何定义 SharePoint 项目项类型并为此类型创建项目模板的演练，请参阅演练：使用项目模板创建站点列项目项，第[1 部分](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)。

 下表列出了必须包含在项目模板SharePoint文件。

|所需文件|说明|
|-------------------|-----------------|
|*.vstemplate* 文件|此文件提供Visual Studio"新建模板"对话框中显示模板以及从模板创建Project所需信息。 有关详细信息，请参阅模板[Visual Studio文件 。](/previous-versions/visualstudio/visual-studio-2010/xsxc3ete\(v\=vs.100\))|
|*.csproj* 或 *.vbproj* 文件|这是项目文件。 它定义项目的内容和配置设置。|
|*Package.package*|此文件定义项目的部署包。 使用包设计器自定义项目的解决方案包时，Visual Studio此文件中存储有关解决方案包的数据。<br /><br /> 创建自定义 SharePoint 项目模板时，建议仅在 *Package.package* 文件中包含所需的最低内容，并且使用与项目模板关联的扩展插件中的 命名空间中的 API 来配置解决方案 <xref:Microsoft.VisualStudio.SharePoint.Packages> 包。 如果这样做，项目模板将受到保护，防止将来对 *Package.package 文件的结构进行更改* 。 有关演示如何创建仅包含最少所需内容的 *Package.package* 文件的示例，请参阅演练：使用项目模板创建站点列项目项，第 [1 部分](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)。<br /><br /> 如果要直接修改 *Package.package* 文件，可以使用 *%Program Files (x86) %\Microsoft Visual Studio 11.0\Xml\Schemas\PackageModelSchema.xsd 中的* 架构来验证内容。|
|*Package.Template.xml*|此文件为 *从项目生成的* SharePoint 解决方案包 (manifest.xml) *(.wsp*) 解决方案清单文件提供基础。 如果要指定一些不应由项目类型的用户更改的行为，可以将内容添加到此文件。 有关详细信息，请参阅[构建基块：解决方案](/previous-versions/office/developer/sharepoint-2010/ee537008(v=office.14))[和解决方案架构](/sharepoint/dev/schema/solution-schema)。<br /><br /> 从项目生成解决方案包时，Visual Studio *Package.package* 和Package.Template.xml文件的内容合并到解决方案清单文件中。  有关生成解决方案包的信息，请参阅如何：使用SharePoint创建[解决方案包MSBuild包](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)。|

 下表列出了可包含在项目模板中的可选文件。

|可选文件|说明|
|-------------------|-----------------|
|SharePoint 项目项|可以包含一个或多个 .spdata 文件，用于定义SharePoint项类型。 每个 *.spdata* 文件在扩展程序集中必须有一个匹配的实现，该扩展程序集包含在具有项目模板的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> VSIX 包中。 有关详细信息，请参阅 [创建项模板](#create-item-templates)。<br /><br /> 通常，SharePoint项目至少包含一SharePoint项目项。 不过，这不是必需的。|
|*\<featureName>.feature*|此文件定义了一个SharePoint功能，该功能用于对多个项目项进行分组以用于部署。 使用功能设计器自定义项目中的功能时，Visual Studio将有关该功能的数据存储在此文件中。 如果要将项目项分组到不同的功能中，可以包含多个 *.feature* 文件。<br /><br /> 创建自定义 SharePoint 项目模板时，建议在每个 *.feature* 文件中仅包含所需的最低内容，并且通过使用与项目模板关联的扩展插件中的 命名空间中的 API 来配置功能。 <xref:Microsoft.VisualStudio.SharePoint.Features> 如果这样做，项目模板将受到保护，防止将来更改 *.feature* 文件的结构。 有关演示如何创建仅包含最少所需内容的 *.feature* 文件的示例，请参阅演练：使用项目模板创建站点列项目项，第 [1 部分](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)。<br /><br /> 如果要直接修改 *功能* 文件，可使用 *% Program Files (x86) % \ Microsoft Visual Studio 11.0 \ Xml\Schemas\FeatureModelSchema.xsd* 中的架构验证内容。|
|*\<featureName>.Template.xml*|此文件为从项目生成的每项功能 (*Feature.xml*) 提供功能清单文件的基础。 如果您想要指定不打算由您的项目类型的用户更改的某些行为，则可以向此文件中添加内容。 有关详细信息，请参阅 [构建基块：功能](/previous-versions/office/developer/sharepoint-2010/ee537350(v=office.14)) 和 [Feature.xml](/sharepoint/dev/schema/feature-xml-files) 文件。<br /><br /> 从项目生成解决方案包时，Visual Studio 会将每对 *\<featureName> 功能* 文件中的内容和 *\<featureName>.Template.xml* 文件合并到一个功能清单文件中。 有关生成解决方案包的详细信息，请参阅[如何：使用 MSBuild 任务创建 SharePoint 解决方案包](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)。|

## <a name="create-wizards-for-item-templates-and-project-templates"></a>为项模板和项目模板创建向导
 定义 SharePoint 项目项类型并将其与项或项目模板关联后，还可以创建一个向导。 当开发人员使用项模板将 SharePoint 项目项添加到项目中时，或者当开发人员使用项目模板创建包含 SharePoint 项目项的新项目时，该向导将显示。 此向导可用于从开发人员收集信息并初始化新的 SharePoint 项目项。

 有关演示如何为项模板和项目模板创建向导的演练，请参阅 [演练：使用项模板创建自定义操作项目项、第2部分](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md) 和 [演练：使用项目模板创建网站栏项目项（第2部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)。

## <a name="see-also"></a>请参阅

- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [演练：使用项模板创建自定义操作项目项（第1部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [演练：使用项模板创建自定义操作项目项（第2部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)
- [演练：使用项目模板创建网站栏项目项（第1部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [演练：使用项目模板创建网站栏项目项（第2部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
