---
title: 如何：添加 Finder 方法|Microsoft Docs
description: 在 Visual Studio 中添加 Finder 方法，该方法使 BDC () 服务的业务数据连接能够在 SharePoint Web 部件或列表中显示实体列表。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], get entities
- Business Data Connectivity service [SharePoint development in Visual Studio], return entities
- BDC [SharePoint development in Visual Studio], return entities
- Business Data Connectivity service [SharePoint development in Visual Studio], Finder method
- Business Data Connectivity service [SharePoint development in Visual Studio], get entities
- BDC [SharePoint development in Visual Studio], Finder method
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 5c7bb3cf932c1e90c0540cd4c8ec378487563b0b5122818a2d2744fd5e2ebb66
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121425357"
---
# <a name="how-to-add-a-finder-method"></a>如何：添加查找器方法
  若要使 BDC (BDC) 服务能够显示 Web 部件或列表中的实体列表，必须创建 *Finder* 方法。 Finder 方法是返回实体实例集合的特殊方法。 有关详细信息，请参阅 [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

### <a name="to-create-a-finder-method"></a>创建 Finder 方法

1. 在 **BDC 设计器上**，选择一个实体。

    有关详细信息，请参阅 [如何：向模型添加实体](../sharepoint/how-to-add-an-entity-to-a-model.md)。

2. 在菜单栏上，选择"**查看其他** Windows  >    >  **BDC 方法详细信息"。**

    **"BDC 方法详细信息"窗口** 随即打开。 有关 **"BDC 方法详细信息"窗口** 的详细信息，请参阅 [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)。

3. 在"**添加方法"列表中**，选择 **"创建查找器方法"。**

    Visual Studio添加方法、返回参数和类型描述符。

4. 将类型描述符配置为实体集合类型描述符。 若要详细了解如何创建实体集合类型描述符，请参阅如何：定义参数 的类型 [描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)。

   > [!NOTE]
   > 如果向实体添加了特定 Finder 方法，则不需要执行此步骤。 Visual Studio使用特定 Finder 方法中定义的类型描述符。

5. 在 **解决方案资源管理器** 中，打开为实体生成的服务代码文件的快捷菜单，然后选择"查看 **代码"。** 有关服务代码文件的信息，请参阅 [创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

6. 将代码添加到 Finder 方法。 此代码执行以下任务：

   - 从数据源检索数据。

   - 将实体列表返回到 BDC 服务。

     以下示例通过使用 AdventureWorks 示例数据库中的数据返回实体的集合 `Contact` ，SQL Server。

   > [!NOTE]
   > 将 字段 `ServerName` 的值替换为服务器的名称。

    :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet2":::
    :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet2":::

## <a name="see-also"></a>请参阅
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)
- [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)
- [如何：添加 Deleter 方法](../sharepoint/how-to-add-a-deleter-method.md)
- [如何：添加 Updater 方法](../sharepoint/how-to-add-an-updater-method.md)
- [如何：向方法添加参数](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)
