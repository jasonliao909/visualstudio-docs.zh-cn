---
title: 创建SharePoint解决方案包|Microsoft Docs
description: 使用包设计器为 SharePoint解决方案创建和自定义部署包。 浏览打包工具、设计器选项和文件夹结构。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
- packages [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: f89bb6344ce7be130f0dc4e7d430327cc139175fa4298539855d5b37ec65f01c
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121425539"
---
# <a name="create-sharepoint-solution-packages"></a>创建SharePoint解决方案包
  通过使用包设计器，可以创建和自定义部署包。 例如，可以添加SharePoint项和功能、重置 IIS 服务器、设置功能激活范围和标识功能依赖项。 设计器还会生成清单，这是一个描述每个包的 XML 文件。

## <a name="packaging-tools"></a>打包工具
 可以使用包 **设计器自定义** 包并生成清单。 可以包括SharePoint项、配置是否应该重置 Web 服务器以及设置部署服务器类型。 有关详细信息，请参阅如何：使用包设计器 向包 [添加和删除功能和项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)。

 或者，可以使用打包资源管理器修改包文件中 *.wsp* (的功能) 。 有关详细信息，请参阅如何：使用打包资源管理器 向包 [添加和删除功能和项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer.md)。

 可以使用 Visual Studio 和 MSBuild 创建包 (*.wsp*) 文件以部署 SharePoint 解决方案。 此过程生成部署所需的清单SharePoint文件。 有关详细信息，请参阅[如何：使用SharePoint创建解决方案MSBuild包](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)。

## <a name="package-designer-options"></a>包设计器选项
 下表显示了可以使用包设计器 在包SharePoint **自定义的属性**。

|包设计器属性|默认设置的说明|
|-------------------------------|------------------------------------|
|名称|必需。 包的默认名称设置为 *ProjectName*。|
|重置 WebServer|可选。 选择是否要在 web 服务器上安装 *.wsp* 文件后SharePoint服务器。|
|部署服务器类型|可选。 表示承载包的服务器的类型。 如果未设置，则默认为 WebFrontEnd。<br /><br /> ApplicationServer：描述承载服务的服务器。<br /><br /> WebFrontEnd：描述托管网站的服务器。|
|解决方案中的项|所有SharePoint项目项和可添加到包的功能。|
|包中的项|可选。 所有SharePoint项和要部署在包中的功能。|

## <a name="configure-the-packaging-process"></a>配置打包过程
 在 Visual Studio 中开发 SharePoint 解决方案后，您可以自定义项目的打包方式。

 下表显示了两个MSBuild自定义 *.wsp* 文件的创建方式的两个目标。

|目标|描述|
|------------|-----------------|
|BeforeLayout|在将文件复制到中间目录之前立即执行任务的目标。 可以在创建 *.wsp* (包文件之前修改) 。|
|AfterLayout|在将文件复制到中间目录后立即执行任务的目标。|

 有关详细信息，请参阅[如何：使用 SharePoint 目标自定义MSBuild包](../sharepoint/how-to-customize-a-sharepoint-solution-package-by-using-msbuild-targets.md)。

## <a name="packaging-architecture"></a>打包体系结构
 在 Visual Studio 中为 *.wsp SharePoint .wsp (创建*) 步骤。

1. 验证功能和包，以确保包的物理和语义结构正确。

2. 枚举包中的功能、项目项和包文件。 包和功能清单文件会进行转换，以包含部署和激活所需的全部信息。 标记将替换为完全限定的值。

3. 执行可自定义的 BeforeLayout MSBuild目标。 可以在创建 *.wsp* 文件之前创建此步骤，以对包进行任何自定义修改。

4. 枚举文件将复制到中间目录。

5. 执行可自定义的 AfterLayout MSBuild目标。 可以在创建 *.wsp* 文件之前创建此步骤，以对包进行任何自定义修改。

6. 中间目录中的文件将添加到 *.wsp* 文件中。

## <a name="package-folder-structure"></a>包文件夹结构
 打包项目 *SharePoint，SolutionFolder\bin \\ \<BuildConfiguration>* 文件夹中会创建一个 *.wsp* 文件。 例如，如果解决方案位于 *C：\Visual Studio 2013\Projects\ListDefinition1，* 并且生成配置设置为 Release，*则 .wsp* 文件位于 *C：\Visual Studio 2013\Projects\ListDefinition1\bin\Release* 中。

## <a name="see-also"></a>请参阅
- [如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [如何：使用包设计器向包添加和删除功能和项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)
- [如何：使用 SharePoint 任务创建 MSBuild 解决方案包](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)
- [如何：使用 SharePoint 任务创建 MSBuild 解决方案包](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)
- [如何：使用SharePoint自定义自定义解决方案MSBuild包](../sharepoint/how-to-customize-a-sharepoint-solution-package-by-using-msbuild-targets.md)
