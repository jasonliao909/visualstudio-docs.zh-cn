---
title: 扩展 SharePoint Project System |Microsoft Docs
description: 扩展 SharePoint 项目系统。 了解如何扩展SharePoint系统。 了解常见的开发任务。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, extending projects
- SharePoint development in Visual Studio, extending project items
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 0fea459c7a442d25363c66efc7be69d21a5e3fb2fd5b31b94e8f09665415d872
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121425383"
---
# <a name="extend-the-sharepoint-project-system"></a>扩展 SharePoint 项目系统
  可以使用SharePoint中的一组项目模板和项模板来创建Visual Studio。 这些模板满足许多开发方案的要求，但你可能会发现它们不提供所需功能的情况。 在这些情况下，可以扩展SharePoint系统。

## <a name="overview-of-the-sharepoint-project-system"></a>项目SharePoint概述
 项目SharePoint系统基于项目项 *的基本SharePoint组件*。 项目SharePoint项表示单个SharePoint自定义项，例如列表定义、Web 部件或内容类型。

 项目SharePoint是一Visual Studio项目，其中包含一个或多个SharePoint项目项。 SharePoint还包含其他组件，这些组件定义如何将项目项分组到要部署的功能和包中。

 有关项目项和SharePoint项目SharePoint的详细信息，请参阅为项目项 创建SharePoint[模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

## <a name="how-to-extend-the-sharepoint-project-system"></a>如何扩展SharePoint系统
 可以通过以下SharePoint扩展项目系统：

- 定义自己的SharePoint项类型，并将其与项目中的新项模板或项目模板Visual Studio。 例如，可以定义一SharePoint项类型，以创建自定义操作或字段。 有关详细信息，请参阅[定义自定义SharePoint项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)。

- 扩展SharePoint中已安装的项目项Visual Studio。 例如，可以将快捷菜单项添加到 解决方案资源管理器开发人员选择菜单项时自定义项目项。 有关详细信息，请参阅[扩展SharePoint项目项](../sharepoint/extending-sharepoint-project-items.md)。

- 扩展SharePoint项目。 例如，可以添加事件处理程序，以在项目中添加或删除项时执行SharePoint任务。 有关详细信息，请参阅[扩展SharePoint项目](../sharepoint/extending-sharepoint-projects.md)。

- 扩展项目项和SharePoint项的打包SharePoint行为。 例如，你可以创建自己的部署步骤，以在部署或收回项目时执行，也可以执行其他自定义任务Visual Studio执行某些部署步骤。 有关详细信息，请参阅扩展[SharePoint和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)。

## <a name="common-development-tasks"></a>常见开发任务
 可以在项目系统的扩展中执行SharePoint任务：

- 使用项目项和几种不同类型的项目文件保存自定义字符串数据。 有关详细信息，请参阅[将数据保存在项目系统的](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)扩展SharePoint中。

- 将项目系统中SharePoint转换为自动化对象模型Visual Studio或集成对象模型中的相应对象，反之亦然。 有关详细信息，请参阅在项目[SharePoint类型和其他项目类型Visual Studio之间。](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)

## <a name="see-also"></a>另请参阅
- [定义自定义SharePoint项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [扩展SharePoint项](../sharepoint/extending-sharepoint-project-items.md)
- [扩展SharePoint项目](../sharepoint/extending-sharepoint-projects.md)
- [扩展SharePoint打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [将数据保存在项目系统的SharePoint扩展中](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)
- [在项目SharePoint类型与其他项目类型Visual Studio转换](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)
- [扩展 Visual Studio 中的 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)
- [SharePoint 工具扩展的编程概念和功能](../sharepoint/programming-concepts-and-features-for-sharepoint-tools-extensions.md)
