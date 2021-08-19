---
title: 演练：在运行时更新功能区上的控件
description: 了解如何使用功能区对象模型在功能区加载到 Office 应用程序中后，在功能区上更新控件。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], controls
- updating Ribbon controls
- Ribbon [Office development in Visual Studio], dynamic menu
- dynamic menus [Office development in Visual Studio]
- Ribbon [Office development in Visual Studio], updating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 2d53e3ca57781052cf4691dd010496246a6010f7
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122046069"
---
# <a name="walkthrough-update-the-controls-on-a-ribbon-at-run-time"></a>演练：在运行时更新功能区上的控件

本演练演示如何使用功能区对象模型在功能区加载到 Office 的应用程序中后，在功能区上更新控件。

[!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

此示例提取来自 Northwind 示例数据库的数据，以填充 Microsoft Office Outlook 中的组合框和菜单。 在这些控件中选择的项会自动填充电子邮件中的字段，例如 **To** 和 **Subject** 。

本演练演示以下任务：

- 创建新的 Outlook VSTO 外接程序项目。

- 设计自定义功能区组。

- 将自定义组添加到内置选项卡。

- 在运行时更新功能区上的控件。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件

您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Outlook

## <a name="create-a-new-outlook-vsto-add-in-project"></a>新建 Outlook VSTO 外接程序项目

首先，创建 Outlook VSTO 外接程序项目。

### <a name="to-create-a-new-outlook-vsto-add-in-project"></a>创建新的 Outlook VSTO 外接程序项目

1. 在中 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，创建一个 Outlook VSTO **Ribbon_Update_At_Runtime** 名称的外接程序项目。

2. 在 **“新建项目”** 对话框中，选择 **“创建解决方案的目录”**。

3. 将项目保存到默认项目目录中。

     有关详细信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

## <a name="design-a-custom-ribbon-group"></a>设计自定义功能区组

当用户撰写一封新邮件时，将显示此示例的功能区。 若要为功能区创建自定义组，请首先向项目中添加一个功能区项，然后在功能区设计器中设计该组。 此自定义组将帮助你通过从数据库中提取名称和订单历史记录来向客户生成跟进电子邮件。

### <a name="to-design-a-custom-group"></a>设计自定义组

1. 在 **“项目”** 菜单上，单击 **“添加新项”**。

2. 在 **“添加新项”** 对话框中，选择 **“功能区(可视化设计器)”**。

3. 将新功能区的名称更改为 **CustomerRibbon**，然后单击 " **添加**"。

     *CustomerRibbon* 或 *CustomerRibbon* 文件将在功能区设计器中打开，并显示一个默认选项卡和组。

4. 单击功能区设计器以将其选定。

5. 在 "**属性**" 窗口中，单击 "RibbonType" 属性旁边的下拉箭头，然后 **Outlook** 单击 "  "。

     这样，当用户在 Outlook 中撰写一封新邮件时，功能区就会出现。

6. 在功能区设计器中，单击 " **Group1** " 以将其选中。

7. 在 " **属性** " 窗口中，将 " **标签** " 设置为 " **客户购买**"。

8. 从 "**工具箱**" 的 " **Office 功能区控件**" 选项卡中，将 **ComboBox** 拖到 "**客户采购**" 组。

9. 单击 **combobox1.location** 以将其选中。

10. 在 " **属性** " 窗口中，将 " **标签** " 设置为 " **客户**"。

11. 从 "**工具箱**" 的 " **Office 功能区控件**" 选项卡中，将 **菜单** 拖到 "**客户采购**" 组。

12. 在 " **属性** " 窗口中，将 " **标签** " 设置为 " **购买产品**"。

13. 将 **动态** 设置为 **true**。

     这使你可以在功能区加载到 Office 应用程序中之后，在运行时添加和删除菜单上的控件。

## <a name="add-the-custom-group-to-a-built-in-tab"></a>将自定义组添加到内置选项卡

内置选项卡是 Outlook 资源管理器或检查器的功能区上已存在的选项卡。 在此过程中，将自定义组添加到内置选项卡，然后指定自定义组在选项卡上的位置。

### <a name="to-add-the-custom-group-to-a-built-in-tab"></a>将自定义组添加到内置选项卡

1. 单击 " **成 tabaddins (内置)** " 选项卡以将其选中。

2. 在 " **属性** " 窗口中，展开 " **ControlId** " 属性，然后将 " **OfficeId** " 设置为 " **TabNewMailMessage**"。

     这会将 " **客户采购** " 组添加到新邮件消息的功能区的 " **消息** " 选项卡中。

3. 单击 " **客户采购** " 组以将其选中。

4. 在 " **属性** " 窗口中，展开 " **位置** " 属性，单击 " **PositionType** " 属性旁边的下拉箭头，然后单击 " **BeforeOfficeId**"。

5. 将 **OfficeId** 属性设置为 **GroupClipboard**。

     这会将 "**客户采购**" 组置于 "**消息**" 选项卡的 "**剪贴板**" 组之前。

## <a name="create-the-data-source"></a>创建数据源

使用 **“数据源”** 窗口将类型化数据集添加到项目中。

### <a name="to-create-the-data-source"></a>创建数据源

1. 在 **“数据”** 菜单上，单击 **“添加新数据源”**。

     这将启动 " **数据源配置向导**"。

2. 选择 **数据库**，然后单击 " **下一步**"。

3. 选择 " **数据集**"，然后单击 " **下一步**"。

4. 选择与 Northwind 示例 Microsoft SQL Server Compact 4.0 数据库的数据连接，或使用 "**新建连接**" 按钮添加新连接。

5. 选择或创建连接后，单击 " **下一步**"。

6. 单击 " **下一步** " 保存连接字符串。

7. 在 " **选择数据库对象** " 页上，展开 " **表**"。

8. 选中以下每个表格旁的复选框：

    1. **客户**

    2. **订单详细信息**

    3. **Orders**

    4. **产品**

9. 单击“完成”。

## <a name="update-controls-in-the-custom-group-at-run-time"></a>在运行时更新自定义组中的控件

使用功能区对象模型执行以下任务：

- 将客户名称添加到 " **客户** " 组合框。

- 将菜单和按钮控件添加到表示销售订单和销售的产品的 **产品购买** 菜单。

- 使用 " **客户** " 组合框和 " **购买的产品** " 菜单中的数据填充新邮件的 "发件人"、"主题" 和 "正文" 字段。

### <a name="to-update-controls-in-the-custom-group-by-using-the-ribbon-object-model"></a>使用功能区对象模型更新自定义组中的控件

1. 在“项目”菜单上，单击“添加引用” 。

2. 在 "**添加引用**" 对话框中，单击 " **.net** " 选项卡，选择 ""，然后单击 **"确定** **"。**

    此程序集包含有关使用语言集成查询 (LINQ) 的类。 你将通过 LINQ 使用 Northwind 数据库中的数据填充自定义组中的控件。

3. 在 **解决方案资源管理器** 中，单击 " **CustomerRibbon** " 或 " **CustomerRibbon** " 以将其选中。

4. 在 **“视图”** 菜单上，单击 **“代码”**。

    功能区代码文件将在代码编辑器中打开。

5. 将下面的语句添加到功能区代码文件的顶部。 通过执行这些语句，可轻松访问 LINQ 命名空间和 Outlook 主互操作程序集 (PIA) 的命名空间。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs" id="Snippet1":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb" id="Snippet1":::

6. 在类中添加以下代码 `CustomerRibbon` 。 此代码声明了将用于存储 Northwind 数据库的“客户”、“订单”、“订单明细”和“产品”表中信息的数据表和表适配器。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs" id="Snippet2":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb" id="Snippet2":::

7. 将以下代码块添加到 `CustomerRibbon` 类中。 此代码添加了三个帮助器方法，这些方法可在运行时创建功能区控件。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs" id="Snippet3":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb" id="Snippet3":::

8. 将 `CustomerRibbon_Load` 事件处理程序方法替换为以下代码。 此代码使用 LINQ 查询执行以下任务：

   - 在 Northwind 数据库中使用20个客户的 ID 和名称填充 " **客户** " 组合框。

   - 调用 `PopulateSalesOrderInfo` 帮助程序方法。 此方法用与当前所选客户相关的销售订单号更新 **ProductsPurchased** 菜单。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb" id="Snippet4":::

9. 将以下代码添加到 `CustomerRibbon` 类。 此代码使用 LINQ 查询执行以下任务：

   - 为与所选客户相关的每个销售订单，将子菜单添加到 " **ProductsPurchased** " 菜单。

   - 将按钮添加到与销售订单相关的产品的每个子菜单中。

   - 将事件处理程序添加到每个按钮。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb" id="Snippet6":::

10. 在 **解决方案资源管理器** 中，双击功能区代码文件。

     功能区设计器随即打开。

11. 在功能区设计器中，双击" **客户"** 组合框。

     功能区代码文件将在代码编辑器中打开，并且将显示 `ComboBox1_TextChanged` 事件处理程序。

12. 将 `ComboBox1_TextChanged` 事件处理程序替换为以下代码。 此代码执行以下任务：

    - 调用 `PopulateSalesOrderInfo` 帮助程序方法。 此方法使用与 **所选客户** 相关的销售订单更新"已购买产品"菜单。

    - 调用 `PopulateMailItem` 帮助程序方法并传入当前文本，该文本是所选客户名称。 此方法填充新邮件的"收件人"、"主题"和"正文"字段。

      :::code language="csharp" source="../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs" id="Snippet5":::
      :::code language="vb" source="../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb" id="Snippet5":::

13. 向 `Click` 类添加以下 `CustomerRibbon` 事件处理程序。 此代码将所选产品的名称添加到新邮件的"正文"字段。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs" id="Snippet8":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb" id="Snippet8":::

14. 将以下代码添加到 `CustomerRibbon` 类。 此代码执行以下任务：

    - 使用当前所选客户的电子邮件地址填充新邮件的"收件人"行。

    - 向新邮件的"主题"和"正文"字段添加文本。

      :::code language="csharp" source="../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs" id="Snippet7":::
      :::code language="vb" source="../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb" id="Snippet7":::

## <a name="test-the-controls-in-the-custom-group"></a>测试自定义组中控件

在功能区中打开新的邮件Outlook，功能区的"消息"选项卡上会显示一个名为 **"客户** 购买"的自定义组。

若要创建客户跟进电子邮件，请选择客户，然后选择客户购买的产品。 客户购买 **组中的** 控件会使用 Northwind 数据库中的数据运行时进行更新。

### <a name="to-test-the-controls-in-the-custom-group"></a>测试自定义组中的控件

1. 按 **F5** 运行项目。

     Outlook 启动。

2. 在Outlook"菜单上，指向"**新建**"，然后单击"邮件 **"。**

     执行以下操作：

    - 出现新的邮件消息检查器窗口。

    - 在功能 **区的"** 消息"选项卡上，" **客户购买"** 组显示在 **剪贴板组** 之前。

    - 组中 **"** 客户"组合框使用 Northwind 数据库中的客户名称进行更新。

3. 在 **功能区的"** 消息"选项卡上的" **客户购买"** 组中，从"客户 **"组合框中选择** 客户。

     执行以下操作：

    - " **购买的产品** "菜单已更新，以显示所选客户的每个销售订单。

    - 每笔销售订单子菜单进行更新，以显示该笔订单中购买的产品。

    - 所选客户的电子邮件地址将添加到邮件的"收件人"行，邮件的主题和正文中填充了文本。

4. 单击 **"产品购买"** 菜单，指向任何销售订单，然后单击销售订单中的产品。

     该产品名称将添加到邮件消息的正文中。

## <a name="next-steps"></a>后续步骤

可从以下主题了解有关如何自定义 Office 用户界面的更多信息：

- 将基于上下文的 UI 添加到任何文档级自定义项。 有关详细信息，请参阅操作 [窗格概述](../vsto/actions-pane-overview.md)。

- 扩展标准的或自定义的 Microsoft Office Outlook 窗体。 有关详细信息，请参阅[演练：设计Outlook区域 。](../vsto/walkthrough-designing-an-outlook-form-region.md)

- 将自定义任务窗格添加到 Outlook。 有关详细信息，请参阅自定义 [任务窗格](../vsto/custom-task-panes.md)。

## <a name="see-also"></a>请参阅

- [运行时访问功能区](../vsto/accessing-the-ribbon-at-run-time.md)
- [功能区概述](../vsto/ribbon-overview.md)
- [语言集成查询 (LINQ)](/dotnet/csharp/linq/index)
- [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [功能区设计器](../vsto/ribbon-designer.md)
- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [功能区对象模型概述](../vsto/ribbon-object-model-overview.md)
- [自定义用于自定义Outlook](../vsto/customizing-a-ribbon-for-outlook.md)
- [如何：更改功能区上选项卡的位置](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)
- [如何：自定义内置选项卡](../vsto/how-to-customize-a-built-in-tab.md)
- [如何：向 Backstage 视图添加控件](../vsto/how-to-add-controls-to-the-backstage-view.md)
- [如何：将功能区从功能区设计器导出到功能区 XML](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)
- [如何：显示外接程序用户界面错误](../vsto/how-to-show-add-in-user-interface-errors.md)