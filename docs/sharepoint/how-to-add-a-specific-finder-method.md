---
title: 如何：添加特定的 Finder 方法 |Microsoft Docs
description: 通过添加 Finder 方法获取实体实例。 当用户选择业务数据 web 部件或外部列表中的实体时，BDC 服务将调用方法。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], Specific Finder
- BDC [SharePoint development in Visual Studio], return an entity
- BDC [SharePoint development in Visual Studio], get an entity
- Business Data Connectivity service [SharePoint development in Visual Studio], return an entity
- BDC [SharePoint development in Visual Studio], Specific Finder
- Business Data Connectivity service [SharePoint development in Visual Studio], get an entity
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 8dd983f9a7929298dc6f5e3ef549027d9ab15ba4cbe180483a617712f3e30af6
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121315182"
---
# <a name="how-to-add-a-specific-finder-method"></a>如何：添加特定的 Finder 方法
  您可以通过创建 *特定的 Finder* 方法返回单个实体实例。 当用户选择业务数据 web 部件或外部列表中的实体时， (BDC) 服务的业务数据连接将执行特定的 Finder 方法。 有关详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

### <a name="to-create-a-specific-finder-method"></a>创建特定的 Finder 方法

1. 在 **BDC 设计器** 中选择一个实体。

    有关如何将实体添加到 Visual Studio 中的 **BDC 设计器** 的信息，请参阅 [如何：将实体添加到模型](../sharepoint/how-to-add-an-entity-to-a-model.md)。

2. 在菜单栏上，选择 "**查看**  >  **其他 Windows**"、" **BDC 方法详细信息**"。

    此时将打开 " **BDC 方法详细信息** " 窗口。 有关该窗口的详细信息，请参阅 [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)。

3. 在 " **添加方法** " 列表中，选择 " **创建特定的 Finder 方法**"。

    Visual Studio 将以下元素添加到模型中。 这些元素出现在 " **BDC 方法详细信息** " 窗口中。

   - 方法。

   - 方法的输入参数。

   - 方法的返回参数。

   - 每个参数的类型描述符。

   - 方法的方法实例。

     有关详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

4. 打开 Visual Studio **属性**"窗口。

5. 将返回参数的类型描述符配置为实体类型描述符。 有关如何创建实体类型描述符的信息，请参阅 [如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)。

   > [!NOTE]
   > 如果已向实体中添加了 Finder 方法，则无需执行此步骤。 Visual Studio 使用您在 Finder 方法中定义的类型描述符。

   > [!NOTE]
   > 如果实体类型的标识符字段表示数据库表中自动生成的字段，请将标识符字段的 **只读** 属性设置为 **True**。

6. 在 " **方法详细信息** " 窗口中，选择方法的方法实例。

7. 在 " **属性" 窗口** 中，将 " **返回参数名称** " 属性设置为方法的返回参数的名称。 有关方法实例属性的详细信息，请参阅 [MethodInstance](/previous-versions/office/developer/sharepoint-2010/ee556838(v=office.14))。

8. 在 **解决方案资源管理器** 中，打开为实体生成的服务代码文件的快捷菜单，然后选择 " **查看代码**"。

    实体服务代码文件将在代码编辑器中打开。 有关实体服务代码文件的详细信息，请参阅 [创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

9. 向特定的 Finder 方法添加代码。 此代码执行以下任务：

   - 从数据源中检索记录。

   - 返回 BDC 服务的实体。

     下面的示例从 AdventureWorks 示例数据库中返回一个用于 SQL Server 的联系人。

     > [!NOTE]
     > 将字段的值替换 `ServerName` 为服务器的名称。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet3":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet3":::

## <a name="see-also"></a>另请参阅
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)
- [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)
- [如何：添加删除器方法](../sharepoint/how-to-add-a-deleter-method.md)
- [如何：添加更新程序方法](../sharepoint/how-to-add-an-updater-method.md)
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [如何：向方法添加参数](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)
