---
title: SharePoint 项目项的项模板/项目模板
description: 为 SharePoint 项目项创建项模板和项目模板。 为项模板和项目模板创建向导。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665294"
---
# <a name="create-item-templates-and-project-templates-for-sharepoint-project-items"></a>为 SharePoint 项目项创建项模板和项目模板

定义自定义 SharePoint 项目项类型时，可将其与项模板或项目模板进行关联。 有了这种关联，其他开发人员就能使用 Visual Studio 中的项目项。 还可为模板创建向导。

例如，Visual Studio 没有用于向 SharePoint 站点添加字段的项目模板或项模板。 你可定义表示某字段的 SharePoint 项目项类型，然后构造一个项模板，供其他开发人员使用来将字段项添加到 SharePoint 项目。 或者，你可构造一个项目模板，使开发人员能够新建具有字段项的 SharePoint 项目。 在这两种情况下，你还可提供一个向导，在开发人员使用你的模板时显示。 此向导可从开发人员那里收集信息来配置新项或新项目。

项模板和项目模板是 .zip 文件，其中包含 Visual Studio 创建项目项或项目时使用的文件。 若要详细了解项模板和项目模板的基础知识，请参阅[创建项目和项模板](../ide/creating-project-and-item-templates.md)。

## <a name="create-item-templates"></a>创建项模板
 为 SharePoint 项目项创建项模板时，有一些文件始终是必需的，也有一些可选文件，某些类型的项目项可能会使用它们。 有关演示如何定义 SharePoint 项目项类型并为其创建项模板的演练，请参阅[演练：使用项模板创建自定义操作项目项（第 1 部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)。

 下表列出了为 SharePoint 项目项创建项模板所需的文件。

|所需文件|说明|
|-------------------|-----------------|
|.spdata 文件|此 XML 文件指定项目项的内容和默认行为。 此文件必须包含在项模板中。 若要详细了解 .spdata 文件的内容，请查看 [SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)。|
|.vstemplate 文件。|此文件向 Visual Studio 提供在“添加新项”对话框中显示模板和根据模板创建项目项所需的信息。 此文件必须包含在项模板中。 有关详细信息，请参阅 [Visual Studio 模板元数据文件](/previous-versions/visualstudio/visual-studio-2010/xsxc3ete\(v\=vs.100\))。|
|实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 接口的 Visual Studio 扩展程序集。|此程序集定义了项目项的运行时行为。 此程序集必须包含在具有项模板的 VSIX 包中。 有关详细信息，请参阅[定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)和[在 Visual Studio 中为 SharePoint 工具部署扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。|

 下表列出了可包含在项模板中的一些最常见的可选文件。 某些类型的项目项可能需要此处未列出的其他文件。

| 可选文件 | 说明 |
|----------------------| - |
| Elements.xml | 功能元素文件。 此文件定义由项目项创建的自定义的 UI 和行为。 每种类型的自定义（例如列表实例、内容类型或自定义操作）都有不同的架构，用于定义此文件的内容。 有关详细信息，请参阅[构建基块：功能](/previous-versions/office/developer/sharepoint-2010/ee537350(v=office.14))和[功能架构](/previous-versions/office/developer/sharepoint-2010/ms414322(v=office.14))。 |
| Schema.xml | 列表定义的架构文件。 有关详细信息，请参阅[构建基块：列表和文档库](/previous-versions/office/developer/sharepoint-2010/ee534985(v=office.14))和 [Schema.xml](/previous-versions/office/developer/sharepoint-2010/ms459356(v=office.14))。 |
| .webpart | Web 部件定义文件。 此文件包含 Web 部件的属性设置。 有关详细信息，请参阅[构建基块：Web 部件](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))。 |
| *.ascx* | ASP.NET UserControl 文件。 此文件定义可视 Web 部件的 UI。 |
| *.aspx* | ASP.NET 页面文件。 此文件包含用于定义应用程序页面的 XML 标记。 |
| .cs 或 .vb 文件  | 这些代码文件定义 SharePoint 自定义的行为，这些自定义具有可通过 Visual C# 或 Visual Basic 代码（例如应用程序页、Web 部件和工作流）访问的编程模型。 |

## <a name="create-project-templates"></a>创建项目模板
 创建 SharePoint 项目模板时，有一些文件始终是必需的，也有一些可选文件，某些类型的项目可能会使它们。 通常，SharePoint 项目至少包含一个 SharePoint 项目项。 不过，这不是必需的。 例如，你可定义一个 SharePoint 项目模板，该模板仅用于部署在其他项目中创建的 SharePoint 解决方案。

 有关演示如何定义 SharePoint 项目项类型并为其创建项目模板的演练，请参阅[演练：使用项目模板创建站点列项目项（第 1 部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)。

 下表列出了 SharePoint 项目模板中必须包含的文件。

|所需文件|说明|
|-------------------|-----------------|
|.vstemplate 文件|此文件向 Visual Studio 提供在“新建项目”对话框中显示模板和通过模板创建项目所需的信息。 有关详细信息，请参阅 [Visual Studio 模板元数据文件](/previous-versions/visualstudio/visual-studio-2010/xsxc3ete\(v\=vs.100\))。|
|.csproj 或 .vbproj 文件 |这是项目文件。 它定义项目的内容和配置设置。|
|Package.package|此文件定义项目的部署包。 使用包设计器自定义项目的解决方案包时，Visual Studio 会在此文件中存储该解决方案包的相关数据。<br /><br /> 创建自定义 SharePoint 项目模板时，建议仅在 Package.package 文件中包含最少必需内容，并且通过在与项目模板关联的扩展中使用 <xref:Microsoft.VisualStudio.SharePoint.Packages> 命名空间中的 API 来配置该解决方案包。 如果执行此操作，你的项目模板将受到保护，以免将来 Package.package 文件的结构发生变化。 有关演示如何创建仅包含最少必需内容的 Package.package 文件的示例，请参阅[演练：使用项目模板创建站点列项目项（第 1 部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)。<br /><br /> 如果要直接修改 Package.package 文件，可使用 %Program Files (x86)%\Microsoft Visual Studio 11.0\Xml\Schemas\PackageModelSchema.xsd 中的架构来验证内容 。|
|Package.Template.xml|此文件为从项目生成的 SharePoint 解决方案包 (.wsp) 的解决方案清单文件 (manifest.xml) 提供了基础 。 如果想要指定一些你的项目类型的用户不可更改的行为，可向此文件中添加内容。 有关详细信息，请参阅[构建基块：解决方案](/previous-versions/office/developer/sharepoint-2010/ee537008(v=office.14))和[解决方案架构](/sharepoint/dev/schema/solution-schema)。<br /><br /> 从项目生成解决方案包时，Visual Studio 会将 Package.package 和 Package.Template.xml 文件的内容合并到解决方案清单文件中 。 若要详细了解如何生成解决方案包，请参阅[如何：使用 MSBuild 任务创建 SharePoint 解决方案包](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)。|

 下表列出了可包含在项目模板中的可选文件。

|可选文件|说明|
|-------------------|-----------------|
|SharePoint 项目项|可包含一个或多个定义 SharePoint 项目项类型的 .spdata 文件。 每个 .spdata 文件都必须在扩展程序集中具有匹配的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 实现，该程序集与项目模板一起包含在 VSIX 包中。 有关详细信息，请参阅[创建项模板](#create-item-templates)。<br /><br /> 通常，SharePoint 项目至少包含一个 SharePoint 项目项。 不过，这不是必需的。|
|\<featureName>.feature|此文件定义了一项 SharePoint 功能，它用于对多个项目项分组来进行部署。 使用功能设计器自定义项目中的功能时，Visual Studio 会在此文件中存储有关功能的数据。 如果想要将项目项分组到不同的功能，可包含多个 .feature 文件。<br /><br /> 创建自定义 SharePoint 项目模板时，建议仅在每个 .feature 文件中包含最少必需内容，并且通过在与项目模板关联的扩展中使用 <xref:Microsoft.VisualStudio.SharePoint.Features> 命名空间中的 API 来配置功能。 如果执行此操作，你的项目模板将受到保护，以免将来 .feature 文件的结构发生变化。 有关演示如何创建仅包含最少必需内容的 .feature 文件的示例，请参阅[演练：使用项目模板创建站点列项目项（第 1 部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)。<br /><br /> 如果要直接修改 .feature 文件，可使用 %Program Files (x86)%\Microsoft Visual Studio 11.0\Xml\Schemas\FeatureModelSchema.xsd 中的架构来验证内容 。|
|\<featureName>.Template.xml|此文件为从项目生成的每个功能的功能清单文件 (Feature.xml) 提供基础。 如果想要指定一些你的项目类型的用户不可更改的行为，可向此文件中添加内容。 有关详细信息，请参阅[构建基块：功能](/previous-versions/office/developer/sharepoint-2010/ee537350(v=office.14))和 [Feature.xml](/sharepoint/dev/schema/feature-xml-files) 文件。<br /><br /> 从项目生成解决方案包时，Visual Studio 会将每对 \<featureName>.feature 文件和 \<featureName>.Template.xml 文件的内容合并到一个功能清单文件中 。 若要详细了解如何生成解决方案包，请参阅[如何：使用 MSBuild 任务创建 SharePoint 解决方案包](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)。|

## <a name="create-wizards-for-item-templates-and-project-templates"></a>为项模板和项目模板创建向导
 定义 SharePoint 项目项类型并将其与项或项目模板关联后，还可创建一个向导。 当开发人员使用项模板将 SharePoint 项目项添加到项目中时，或者当开发人员使用项目模板创建包含 SharePoint 项目项的新项目时，会显示该向导。 可使用该向导从开发人员那里收集信息，并初始化新的 SharePoint 项目项。

 有关演示如何为项模板和项目模板创建向导的演练，请参阅[演练：使用项模板创建自定义操作项目项（第 2 部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)和[演练：使用项目模板创建站点列项目项（第 2 部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)。

## <a name="see-also"></a>另请参阅

- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [演练：使用项模板创建自定义操作项目项（第 1 部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [演练：使用项模板创建自定义操作项目项（第 2 部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)
- [演练：使用项目模板创建站点列项目项（第 1 部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [演练：使用项目模板创建站点列项目项（第 2 部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
