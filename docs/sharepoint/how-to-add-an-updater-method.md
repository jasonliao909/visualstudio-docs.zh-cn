---
title: 如何：添加 Updater 方法|Microsoft Docs
description: 了解如何通过添加 Updater 方法使用户能够更新SharePoint外部列表中的业务数据。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], updating data
- BDC [SharePoint development in Visual Studio], Updater
- Business Data Connectivity service [SharePoint development in Visual Studio], updating data
- Business Data Connectivity service [SharePoint development in Visual Studio], Updater
- Business Data Connectivity service [SharePoint development in Visual Studio], updating entity instances
- BDC [SharePoint development in Visual Studio], updating entity instances
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: dbdd742184ebea14912bbcca2938192b8de459f3
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122093094"
---
# <a name="how-to-add-an-updater-method"></a>如何：添加 Updater 方法
  通过创建 *Updater* 方法，SharePoint更新外部列表中的业务数据。 有关详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

### <a name="to-create-an-updater-method"></a>创建 Updater 方法

1. 在 BDC 设计器上，选择一个实体。

2. 在菜单栏上，选择"**查看** 其他Windows  >    >  **BDC 方法详细信息"。**

    “BDC 方法详细信息”窗口将打开。 有关此窗口详细信息，请参阅 [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)。

3. 在"**添加方法"列表中**，选择 **"创建更新程序方法"。**

    Visual Studio向模型添加以下元素。 这些元素显示在"BDC 方法详细信息"窗口中。

   - 名为 Update **的方法**。

   - 方法的输入参数。

   - 参数的类型描述符。 默认情况下，Visual Studio使用为 Finder 方法定义的实体类型描述符，例如 (联系人) 。

   - 方法的方法实例。

     有关详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

   > [!NOTE]
   > 如果实体类型的标识符表示未自动生成的数据库表中的字段，则将"更新前字段"**属性设置为****True。**

4. 在 **解决方案资源管理器** 中，打开为实体生成的服务代码文件的快捷菜单，然后选择"查看 **代码"。**

    实体服务代码文件将在代码编辑器 **中打开**。 有关该文件的信息，请参阅 [创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

5. 将代码添加到 Update 方法以更新数据。 以下示例更新 AdventureWorks 示例数据库中联系人的信息，SQL Server。

   > [!NOTE]
   > 将 字段 `ServerName` 的值替换为服务器的名称。

    :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet5":::
    :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet5":::

## <a name="see-also"></a>请参阅
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [如何：添加查找器方法](../sharepoint/how-to-add-a-finder-method.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)
- [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)
- [如何：添加 Updater 方法](../sharepoint/how-to-add-an-updater-method.md)
- [如何：添加 Deleter 方法](../sharepoint/how-to-add-a-deleter-method.md)
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [如何：向方法添加参数](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)
