---
title: BDC 模型设计工具概述 | Microsoft Docs
description: 阅读有关与业务数据连接 (BDC) 模型结合使用的设计工具的概述。 了解 BDC 设计器、“BDC 方法详细信息”窗口和 BDC 资源管理器。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.BDC.Method_Details
- VS.SharePointTools.BDC.Explorer
- VS.SharePointTools.BDC.Diagram
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], visual tools
- Business Data Connectivity service [SharePoint development in Visual Studio], visual tools
- Business Data Connectivity service [SharePoint development in Visual Studio], BDC Explorer
- BDC [SharePoint development in Visual Studio], method details
- Business Data Connectivity service [SharePoint development in Visual Studio], designer
- Business Data Connectivity service [SharePoint development in Visual Studio], method details
- BDC [SharePoint development in Visual Studio], BDC Explorer
- BDC [SharePoint development in Visual Studio], designer
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: e2045699cf0ce48edef3c9186cea3135c0a54dab
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664243"
---
# <a name="bdc-model-design-tools-overview"></a>BDC 模型设计工具概述
  可以通过使用 BDC 设计器、“BDC 方法详细信息”窗口和 BDC 资源管理器来设计业务数据连接 (BDC) 模型。 

 通过 BDC 资源管理器可以浏览模型、搜索模型和定义类型描述符。

## <a name="bdc-designer"></a>BDC 设计器
 通过 BDC 设计器可以在模型中定义实体，并直观地排列它们之间的关系。 使用 BDC 设计器来完成以下任务：

- 将实体添加到模型。

- 从模型删除实体。

- 定义实体之间的关系。

  若要打开 BDC 设计器，请双击项目中的模型文件或打开模型文件的快捷菜单并选择“打开”。 通过将“实体”从“工具箱”拖动或复制到设计器，可将实体添加到模型。  若要创建两个实体之间的关联，请选择“工具箱”中的“关联”控件，选择第一个实体，然后选择第二个实体。 

## <a name="bdc-method-details-window"></a>“BDC 方法详细信息”窗口
 使用“BDC 方法详细信息”窗口定义方法的参数、实例和筛选器描述符。

 可以在“BDC 方法详细信息”窗口中快速生成 Finder、Specific Finder、Creator、Updater 和 Deleter 方法。 生成这些方法时，Visual Studio 会将元数据（例如参数、实例和类型描述符）添加到方法。 可以修改此元数据，以满足你的特定方案。

 若要打开“BDC 方法详细信息”窗口，请在菜单栏上依次选择“视图” > “其他窗口” > “BDC 方法详细信息”。

 若要在“BDC 方法详细信息”窗口中查看方法，请在 BDC 设计器中选择实体。 所选实体的方法显示在“BDC 方法详细信息”窗口中。 如果没有在 BDC 设计器中选择实体，则“BDC 方法详细信息”窗口不会显示任何信息。

 在“BDC 方法详细信息”窗口中展开或折叠节点，以定义参数、实例和筛选器描述符。 使用 BDC 资源管理器定义类型描述符。

## <a name="bdc-explorer"></a>BDC 资源管理器
 BDC 资源管理器会显示组成模型的元素。 若要打开“BDC 资源管理器”，请在菜单栏上依次选择“视图” > “其他窗口” > “BDC 资源管理器”。 若要浏览模型，请在 BDC 资源管理器中展开节点。 每个节点都表示模型文件的 XML 中的一个元素。

 在“BDC 资源管理器”中选择节点时，“属性”窗口中将显示所选每个节点的属性。  其中许多属性对应于模型文件中的特性。 可以通过使用“BDC 资源管理器”窗口顶部的搜索框搜索模型。

> [!NOTE]
> BDC 资源管理器不显示标识符、自定义属性、本地化的字符串、关联组、操作、筛选器描述符、操作控件列表和默认参数值。

### <a name="define-type-descriptors"></a>定义类型描述符
 使用 BDC 资源管理器定义类型描述符。 通过 BDC 资源管理器，可以一次定义类型描述符，然后在模型中的其他位置重用该类型描述符。 若要实现此目的，请复制类型描述符，并将其粘贴到其他任何参数或类型描述符上。

> [!NOTE]
> 对原始类型描述符所做的更改不会影响该类型描述符的副本。

 有关详细信息，请参阅[如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)。

## <a name="see-also"></a>另请参阅
- [如何：创建 BDC 模型](../sharepoint/how-to-create-a-bdc-model.md)
- [操作说明：将实体添加到模型](../sharepoint/how-to-add-an-entity-to-a-model.md)
- [如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)
- [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)
- [如何：添加 Deleter 方法](../sharepoint/how-to-add-a-deleter-method.md)
- [如何：添加 Updater 方法](../sharepoint/how-to-add-an-updater-method.md)
- [创建实体之间的关联](../sharepoint/creating-an-association-between-entities.md)
- [演练：使用业务数据在 SharePoint 中创建外部列表](../sharepoint/walkthrough-creating-an-external-list-in-sharepoint-by-using-business-data.md)
- [将业务数据集成到 SharePoint 中](../sharepoint/integrating-business-data-into-sharepoint.md)
- [创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
