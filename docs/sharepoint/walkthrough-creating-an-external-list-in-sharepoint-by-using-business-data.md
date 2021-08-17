---
title: 使用业务数据在 SharePoint 中创建外部列表
description: 为 BDC 服务创建一个模型，该模型返回有关企业数据库中联系人的信息，然后使用此模型在 SharePoint 中创建外部列表。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], business data in a Web Part
- BDC [SharePoint development in Visual Studio], external list
- Business Data Connectivity service [SharePoint development in Visual Studio], business data in a SharePoint list
- BDC [SharePoint development in Visual Studio], business data in a SharePoint list
- BDC [SharePoint development in Visual Studio], business data in a Web Part
- BDC [SharePoint development in Visual Studio], entity backed list
- Business Data Connectivity service [SharePoint development in Visual Studio], entity backed list
- Business Data Connectivity service [SharePoint development in Visual Studio], external list
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: a265a80116da0d1d2ffac469f7193c737a65a93a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122075900"
---
# <a name="walkthrough-create-an-external-list-in-sharepoint-by-using-business-data"></a>演练：使用业务数据在 SharePoint 中创建外部列表

利用业务数据连接 (BDC) 服务，SharePoint 可以显示后端服务器应用程序、Web 服务和数据库中的业务数据。

本演练演示如何为 BDC 服务创建一个模型，该模型返回有关示例数据库中的联系人的信息。 然后，您将使用此模型在 SharePoint 中创建外部列表。

本演练演示以下任务：

- 创建项目。
- 将实体添加到模型。
- 添加 finder 方法。
- 添加特定的 Finder 方法。
- 测试项目。

## <a name="prerequisites"></a>先决条件

您需要满足以下条件才能完成本演练：

- 支持的 Windows 和 SharePoint 版本。

- 访问 AdventureWorks 示例数据库。 有关如何安装 AdventureWorks 数据库的详细信息，请参阅[SQL Server 示例数据库](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)。

## <a name="create-a-project-that-contains-a-bdc-model"></a>创建包含 BDC 模型的项目

1. 在 Visual Studio 的菜单栏上，选择 "**文件**" "  >  **新建**  >  **Project**"。

     **“新建项目”** 对话框随即打开。

2. 在 **Visual c #** 或 **Visual Basic** 下，展开 " **SharePoint** " 节点，然后选择 **2010** 项。

3. 在 "**模板**" 窗格中，选择 **SharePoint 2010 Project**，将项目命名为 **AdventureWorksTest**，然后选择 **"确定"** 按钮。

     此时将显示 " **SharePoint 自定义向导**"。 在此向导中，您可以指定用于调试项目的站点并设置解决方案的信任级别。

4. 选择 " **部署为场解决方案** " 选项按钮以设置信任级别。

5. 选择 "**完成**" 按钮以接受默认的本地 SharePoint 站点。

6. 在 **解决方案资源管理器** 中，选择 "SharePoint 项目" 节点。

7. 在菜单栏上，依次选择“项目” > “添加新项”。

     此时将打开“添加新项”对话框。

8. 在 " **模板** " 窗格中，选择 " **业务数据连接模型 (场解决方案仅)**，将项目命名为" **AdventureWorksContacts**"，然后选择" **添加** "按钮。

## <a name="add-data-access-classes-to-the-project"></a>将数据访问类添加到项目

1. 在菜单栏上，选择 "**工具**" "  >  **连接到数据库**"。

     随即会打开“添加连接”对话框。

2. 将连接添加到 SQL Server AdventureWorks 示例数据库。

     有关详细信息，请参阅[添加/修改连接 (Microsoft SQL Server) ](/previous-versions/dxb6fxah(v=vs.140))。

3. 在 **“解决方案资源管理器”** 中，选择项目节点。

4. 在菜单栏上，依次选择“项目” > “添加新项”。

5. 在 " **已安装的模板** " 窗格中，选择 " **数据** " 节点。

6. 在 "**模板**" 窗格中选择 " **LINQ to SQL 类**"。

7. 在 " **名称** " 框中，指定 **AdventureWorks**，然后选择 " **添加** " 按钮。

     .dbml 文件会添加到项目中，对象关系设计器（O/R 设计器）将打开。

8. 在菜单栏上，选择 "**查看**  >  **服务器资源管理器**"。

9. 在 **服务器资源管理器** 中，展开表示 AdventureWorks 示例数据库的节点，然后展开 " **表** " 节点。

10. 将 **Contact (Person)** 表添加到 O/R 设计器上。

     一个实体类将创建并显示在设计图面上。 实体类具有映射到 Contact (Person) 表中的列的属性。

## <a name="remove-the-default-entity-from-the-bdc-model"></a>从 BDC 模型中删除默认实体

**业务数据连接模型** 项目向模型中添加一个名为 Entity1 的默认实体。 删除此实体。 稍后，您将添加一个新实体。 从空模型开始可减少完成此演练所需的步骤数。

1. 在 **解决方案资源管理器** 中，展开 " **BdcModel1** " 节点，然后打开 " *BdcModel1* " 文件。

2. 业务数据连接模型文件将在 BDC 设计器中打开。

3. 在设计器中，打开 " **Entity1**" 的快捷菜单，然后选择 " **删除**"。

4. 在 **解决方案资源管理器** 中，打开 Visual Basic () 中的 *Entity1* (快捷菜单，并选择 "**删除** *"。*

5. 打开 Visual Basic) 中的 *Entity1Service* (的快捷菜单或 c # 中的 *Entity1Service* () ，然后选择 "**删除**"。

## <a name="add-an-entity-to-the-model"></a>向模型添加实体

将实体添加到模型。 可以将 Visual Studio **工具箱** 中的实体添加到 BDC 设计器中。

1. 在菜单栏上，选择 "**视图**  >  **" "工具箱**"。

2. 在 "**工具箱**" 的 " **BusinessDataConnectivity** " 选项卡上，将 **实体** 添加到 BDC 设计器上。

     新实体将显示在设计器上。 Visual Studio 会将名为 *EntityService* (的文件以 c # (中的 Visual Basic) 或 *EntityService* ) 添加到项目。

3. 在菜单栏上，选择 "**查看**  >  **属性**  >  **窗口**"。

4. 在 " **属性** " 窗口中，将 " **名称** " 属性值设置为 " **联系人**"。

5. 在设计器中，打开实体的快捷菜单，选择 " **添加**"，然后选择 " **标识符**"。

     实体上将显示一个新的标识符。

6. 在 " **属性** " 窗口中，将标识符的名称更改为 **ContactID**。

7. 在 "**类型名称**" 列表中 **，选择 "system.string"。**

## <a name="add-a-specific-finder-method"></a>添加特定的 Finder 方法

若要使 BDC 服务能够显示特定的联系人，您必须添加特定的 Finder 方法。 当用户选择列表中的项，然后在功能区上选择 " **查看项** " 按钮时，BDC 服务将调用特定的 Finder 方法。

使用 " **BDC 方法详细信息** " 窗口向 Contact 实体添加特定的 Finder 方法。 若要返回特定实体，请将代码添加到方法。

1. 在 BDC 设计器中，选择 " **联系人** " 实体。

2. 在菜单栏上，选择 "**查看**  >  **其他 Windows**  >  **BDC 方法详细信息**"。

     “BDC 方法详细信息”窗口将打开。

3. 在 " **添加方法** " 列表中，选择 " **创建特定的 Finder 方法**"。

     Visual Studio 将以下元素添加到模型中。 这些元素出现在 " **BDC 方法详细信息** " 窗口中。

    - 名为 ReadItem 的方法。

    - 方法的输入参数。

    - 方法的返回参数。

    - 每个参数的类型描述符。

    - 方法的方法实例。

4. 在 " **BDC 方法详细信息** " 窗口中，打开为 " **联系人** 类型" 描述符显示的列表，然后选择 " **编辑**"。

     " **BDC 资源管理器** " 将打开，并提供模型的层次结构视图。

5. 在 "**属性**" 窗口中，打开 " **TypeName** " 属性旁边的列表，选择 "**当前 Project** " 选项卡，然后选择 "**联系人**" 属性。

6. 在 " **BDC 资源管理器**" 中，打开 **联系人** 的快捷菜单，然后选择 " **添加类型描述符**"。

     " **BDC 资源管理器**" 中将显示名为 " **TypeDescriptor1** " 的新类型描述符。

7. 在 " **属性** " 窗口中，将 " **名称** " 属性值设置为 **ContactID**。

8. 打开 " **TypeName** " 属性旁边的列表，然后选择 " **Int32**"。

9. 打开 " **标识符** " 属性旁边的列表，然后选择 " **ContactID**"。

10. 重复步骤6，为以下每个字段创建类型描述符。

    |名称|类型名称|
    |----------|---------------|
    |FirstName|System.String|
    |LastName|System.String|
    |电话|System.String|
    |EmailAddress|System.String|
    |EmailPromotion|System.Int32|
    |NameStyle|System.Boolean|
    |PasswordHash|System.String|
    |PasswordSalt|System.String|

11. 在 BDC 设计器中的 **Contact** 实体上，打开 **ReadItem** 方法。

     "联系人"服务代码文件将在代码编辑器中打开。

12. 在 `ContactService` 类中，将 `ReadItem` 方法替换为以下代码。 此代码执行以下任务：

    - 从 AdventureWorks 数据库的 Contact 表中检索记录。

    - 将 Contact 实体返回到 BDC 服务。

    > [!NOTE]
    > 将 字段 `ServerName` 的值替换为服务器的名称。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet3":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet3":::

## <a name="add-a-finder-method"></a>添加查找器方法

若要使 BDC 服务能够显示列表中的联系人，必须添加 Finder 方法。 使用 **"BDC** 方法详细信息"窗口将 Finder 方法添加到 Contact 实体。 若要将实体集合返回到 BDC 服务，请向 方法添加代码。

1. 在 BDC 设计器中，选择 **"联系人"** 实体。

2. 在 **"BDC 方法详细信息"** 窗口中，折叠 **ReadItem** 节点。

3. 在 ReadList **方法下的"添加** 方法 **"列表中**，选择"**创建查找器方法"。**

     Visual Studio添加方法、返回参数和类型描述符。

4. 在 BDC 设计器中的 **Contact** 实体上，打开 **ReadList** 方法。

     联系人服务代码文件随即在代码编辑器中打开。

5. 在 `ContactService` 类中，将 `ReadList` 方法替换为以下代码。 此代码执行以下任务：

   - 从 AdventureWorks 数据库的 Contacts 表中检索数据。

   - 返回 BDC 服务的联系人实体列表。

     > [!NOTE]
     > 将 字段 `ServerName` 的值替换为服务器的名称。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet2":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet2":::

## <a name="test-the-project"></a>测试项目

运行项目时，将打开SharePoint站点，Visual Studio模型添加到业务数据连接服务。 在引用 Contact 实体SharePoint创建外部列表。 AdventureWorks 数据库中的联系人数据显示在列表中。

> [!NOTE]
> 在调试解决方案之前，可能需要SharePoint中的安全设置。 有关详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

1. 选择 F5。

     随即SharePoint站点。

2. 在" **站点操作"** 菜单上，选择" **更多选项"** 命令。

3. 在" **创建** "页上，选择" **外部列表"** 模板，然后选择"创建 **"** 按钮。

4. 将自定义列表命名 **为"联系人"。**

5. 选择"外部内容类型" **字段旁边的浏览** 按钮。

6. 在" **外部内容类型选取器** "对话框中，选择 **"AdventureWorksContacts.BdcModel1.Contact"** 项，然后选择"创建 **"** 按钮。

     SharePoint 随即创建包含 AdventureWorks 示例数据库中的联系人的外部列表。

7. 若要测试特定的 Finder 方法，请在列表中选择联系人。

8. 在功能区上，选择" **项"** 选项卡，然后选择"查看 **项"** 命令。

     所选联系人的详细信息随即显示在窗体中。

## <a name="next-steps"></a>后续步骤

可以在以下主题中详细了解如何为 BDC 服务SharePoint模型：

- [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)。
- [如何：添加 Updater 方法](../sharepoint/how-to-add-an-updater-method.md)。
- [如何：添加 Deleter 方法](../sharepoint/how-to-add-a-deleter-method.md)。

## <a name="see-also"></a>请参阅

[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md) 
[创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md) 
[BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md) 
[将业务数据集成到SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)