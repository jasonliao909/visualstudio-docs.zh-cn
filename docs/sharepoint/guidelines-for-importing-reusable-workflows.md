---
title: 导入可重用工作流指南|Microsoft Docs
description: 查看将设计器中创建的可重用工作流导入SharePoint导入Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, importing items
- SharePoint development in Visual Studio, reusable workflows
- importing items [SharePoint development in Visual Studio]
- reusable workflows [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 76bdfd937fb054e2fa1b9bc533371ce347761d915074bb435705f9395a2270f5
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121425426"
---
# <a name="guidelines-for-importing-reusable-workflows"></a>有关导入可重用工作流的准则
  若要导入在 SharePoint Designer 中创建的可重用工作流，请使用 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的“导入可重用 SharePoint 2010 工作流”项目模板。 此模板导入声明 *性**工作流 (* -only) 并将其转换为代码工作流 ，这是可以使用 或 代码增强的 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]  [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] [!INCLUDE[csprcs](../sharepoint/includes/csprcs-md.md)] 工作流。 [!INCLUDE[crdefault](../sharepoint/includes/crdefault-md.md)][演练：将 SharePoint 设计器可重用工作流导入 Visual Studio。](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)

 但“导入可重用 SharePoint 2010 工作流”模板只能导入场解决方案。 若要将工作流部署为沙盒解决方案，请使用“导入 SharePoint 2010 解决方案包”模板将其导入。 但是，如果这样做，则无法将工作流转换为代码工作流，同样也不能对其进行修改。

## <a name="import-reusable-workflows-by-using-the-import-reusable-workflow-template"></a>使用"导入可重用工作流"模板导入可重用工作流
 如果使用“导入可重用 SharePoint 2010 工作流”模板导入可重用工作流，则可以像运行或更改任何其他 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint 解决方案一样来运行或更改此解决方案，只不过您可能必须手动修复某些项。

### <a name="import-task-forms"></a>导入任务窗体
 “导入可重用 SharePoint 2010 工作流”项目模板将导入所有启动窗体和关联窗体，但仅导入一个任务窗体，因为代码工作流架构只允许一个任务窗体。 原始工作流解决方案中任何其他任务窗体将放入 解决方案资源管理器 中的"其他导入的文件 **"文件夹**。

## <a name="import-reusable-workflows-by-using-the-import-sharepoint-2010-solution-package-template"></a>使用"导入 2010 SharePoint包"模板导入可重用工作流
 如果使用“导入 SharePoint 2010 解决方案包”模板导入可重用工作流，您需要考虑下列问题：

- 导入工作流后，可以通过选择 F5 键立即在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中部署 **并运行** 它。 但是，如果在导入的解决方案中更改工作流中的内容，可能需要手动修复项目中的元素，然后才能部署和运行工作流。

- 由于工作流是声明性的，因此无法向它添加代码。 若要将工作流转换为代码工作流，必须使用 Import [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Reusable SharePoint 2010 Workflow 模板将其导入。

- 虽然可以在 设计视图 中编辑工作流设计器 (.xoml) 文件，但建议在"源"视图中编辑它，因为工作流设计器显示错误。

- 工作流中的调试对声明性内容不起作用。 不会命中 中设置的 [!INCLUDE[wfd2](../sharepoint/includes/wfd2-md.md)] 断点。

## <a name="import-globally-reusable-workflow-solutions"></a>导入全局可重用工作流解决方案
 无法使用“导入可重用 SharePoint 2010 工作流”模板导入全局可重用工作流。 若要导入全局可重用工作流，您必须将其转换为非全局可重用工作流或必须使用“导入 SharePoint 2010 解决方案包”模板。

 若要转换工作流，请打开工作流的快捷菜单，然后选择"另存为复制"，在 SharePoint Designer (创建全局可重用工作流的副本) 。  然后使用 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的“导入可重用 SharePoint 2010 工作流”模板导入新的可重用工作流。

 若要导入全局可重用工作流而不进行修改，请使用“导入 SharePoint 2010 解决方案包”模板。 如果你使用此方法，此工作流不会转换为代码工作流，而仍为声明性工作流。

## <a name="see-also"></a>请参阅
- [从现有的 SharePoint 网站导入项](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [演练：将 SharePoint Designer 可重用工作流导入 Visual Studio](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)
