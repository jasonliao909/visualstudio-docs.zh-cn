---
title: 创建业务数据连接模型|Microsoft Docs
description: 使用 BDC (模型) 业务数据连接，或者使用 Visual Studio 自定义现有 BDC 模型。 每个项目SharePoint只能包含一个模型。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], model
- BDC [SharePoint development in Visual Studio], creating a model
- Business Data Connectivity service [SharePoint development in Visual Studio], creating a model
- SharePoint development in Visual Studio, Business Data Connectivity service
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 639b86f0c4b17faf72fb8a74caf9ef6398d770a4
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600673"
---
# <a name="create-a-business-data-connectivity-model"></a>创建业务数据连接模型
  可以使用 BDC (模型) 业务数据连接，或者使用 Visual Studio。 每个项目SharePoint只能包含一个模型。 有关详细信息，请参阅[将业务数据集成到 SharePoint。](../sharepoint/integrating-business-data-into-sharepoint.md)

## <a name="create-a-new-model"></a>创建新模型
 若要创建新模型，请创建业务 **数据连接模型** 项目，或将业务 **数据连接模型** 项添加到空 **SharePoint Project。**

> [!NOTE]
> 必须 [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] 已安装在计算机上。

 Visual Studio向项目添加文件夹。 此文件夹具有你在"添加新项"对话框中为" **业务数据** 连接模型"项 **指定的名称** 。 如果创建新的业务数据 **连接模型** 项目，Visual Studio文件夹 **BdcModel1**。

 Visual Studio将以下文件添加到新文件夹：

|文件|说明|
|----------|-----------------|
|模型定义文件|包含 XML，用于定义实体、方法、业务线 (LOB) 系统对象以及描述模型的其他元数据。<br /><br /> 使用 BDC 设计器 **、BDC** 资源管理器 **、BDC 方法详细信息** 窗口和"属性"窗口修改 **此文件中的** 元数据。|
|实体服务代码文件|包含检索、更新和删除默认实体实例的方法。|

 若要定义实体的属性，请编辑实体代码文件。 有关详细信息，请参阅 [如何：向模型添加实体](../sharepoint/how-to-add-an-entity-to-a-model.md)。

 若要检索、更新和删除实体的实例，请向实体服务代码文件添加代码。 有关详细信息，请参阅 [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

 编译项目时，Visual Studio创建程序集。 确保不要将其他项添加到项目，而将代码添加到项目程序集 (例如：顺序工作流项或 Web 部件) 。  部署解决方案时，该项的代码不会运行，因为解决方案包不会将程序集复制到全局程序集缓存。  解决方案包仅将程序集部署到 SharePoint 数据库。

> [!NOTE]
> Visual Studio调试项目时，将程序集复制到本地计算机的两个位置。

## <a name="add-an-existing-model"></a>添加现有模型
 可以使用其他工具（如设计器）导入SharePoint模型。 在下列情况下，可以选择将现有模型导入项目：

- 自定义已部署到数据库服务器场SharePoint模型。

- 将现有模型打包并部署到多个SharePoint服务器场。

  在任一情况下，在导入的模型中定义的 LOB 系统不受影响，将继续按预期工作。 若要将现有模型添加到SharePoint，请使用"Visual Studio **现有项"** 对话框。 有关详细信息，请参阅[如何：将现有 BDC 模型文件添加到SharePoint项目](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)。

  可以通过选择"添加 .NET 程序集 LobSystem"中的选项，将类型为 .NET Framework 的 **LOB 系统添加到导入的模型**。 这样，你可编写自定义代码，并使用设计器定义导入模型的元数据。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[如何：创建 BDC 模型](../sharepoint/how-to-create-a-bdc-model.md)|演示如何创建新的 BDC 模型。|
|[如何：将现有 BDC 模型文件添加到 SharePoint 项目](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)|演示如何将现有模型导入到 SharePoint 项目中。|
|[如何：使用资源文件指定本地化名称、属性和权限](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)|介绍如何在 Web 部件或网页使用模型时提供与模型元数据合并的字符串。|
|[如何：在 BDC 功能中包括自定义程序集](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)|演示如何在功能中包括自定义程序集。|
