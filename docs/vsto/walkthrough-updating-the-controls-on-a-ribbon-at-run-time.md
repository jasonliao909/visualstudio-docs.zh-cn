---
title: 演练：运行时更新功能区上的控件
description: 了解如何在功能区加载到功能区应用程序后，使用功能区对象模型Office控件。
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
ms.openlocfilehash: ee3fd72ef1ad75512b87d3fae61efa271c2773ba155663502bb5d489b243b0ee
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121408157"
---
# <a name="walkthrough-update-the-controls-on-a-ribbon-at-run-time"></a>演练：运行时更新功能区上的控件

本演练演示如何在功能区加载到功能区应用程序后，使用功能区对象模型Office控件。

[!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

此示例提取来自 Northwind 示例数据库的数据，以填充 Microsoft Office Outlook 中的组合框和菜单。 在这些控件中选择的项会自动填充 **电子邮件中的"** 收件人"和"主题"等字段。

本演练演示以下任务：

- 创建一Outlook VSTO外接程序项目。

- 设计自定义功能区组。

- 将自定义组添加到内置选项卡。

- 运行时更新功能区上的控件。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件

您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Outlook

## <a name="create-a-new-outlook-vsto-add-in-project"></a>创建新的Outlook VSTO外接程序项目

首先，创建 Outlook VSTO 外接程序项目。

### <a name="to-create-a-new-outlook-vsto-add-in-project"></a>创建新的 Outlook VSTO 外接程序项目

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中，Outlook VSTO名称为 的外接程序 **Ribbon_Update_At_Runtime。**

2. 在 **“新建项目”** 对话框中，选择 **“创建解决方案的目录”**。

3. 将项目保存到默认项目目录中。

     有关详细信息，请参阅[如何：在 Office 创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

## <a name="design-a-custom-ribbon-group"></a>设计自定义功能区组

当用户撰写新邮件时，将显示此示例的功能区。 若要为功能区创建自定义组，请首先将功能区项添加到项目，然后在功能区设计器中设计该组。 此自定义组将帮助你从数据库拉取名称和订单历史记录，从而生成发送给客户的跟进电子邮件。

### <a name="to-design-a-custom-group"></a>设计自定义组

1. 在 **“项目”** 菜单上，单击 **“添加新项”**。

2. 在 **“添加新项”** 对话框中，选择 **“功能区(可视化设计器)”**。

3. 将新功能区的名称更改为 **CustomerRibbon，** 然后单击"添加 **"。**

     *CustomerRibbon.cs* 或 *CustomerRibbon.vb* 文件在功能区设计器中打开并显示默认选项卡和组。

4. 单击功能区设计器以将其选定。

5. 在"**属性"** 窗口中，单击 **RibbonType** 属性旁边的下拉箭头，然后单击 **"Microsoft.Outlook.Mail.Compose"。**

     这样，当用户在邮件中撰写新邮件时，功能区Outlook。

6. 在功能区设计器中，单击 **"Group1"** 将其选中。

7. 在"**属性"** 窗口中，将 **"标签"** 设置为 **"客户购买"。**

8. 从 **"Office"的**"功能区控件"**选项卡中，** 将 **ComboBox** **拖到"客户购买"** 组中。

9. 单击 **"ComboBox1"** 将其选中。

10. 在"**属性"** 窗口中，将 **"标签"** 设置为 **"客户"。**

11. 从 **"Office"** 的"功能区控件"选项卡 **中，** 将 **"菜单**"**拖到"客户购买"** 组中。

12. 在"**属性"窗口中**，将 **"标签"设置为****"已购买产品"。**

13. 将 **"动态"** 设置为 **"true"。**

     这样，在功能区加载到应用程序后，可以运行时在菜单上添加Office控件。

## <a name="add-the-custom-group-to-a-built-in-tab"></a>将自定义组添加到内置选项卡

内置选项卡是已在资源管理器或检查器的功能区Outlook选项卡。 在此过程中，将自定义组添加到内置选项卡，然后指定自定义组在选项卡上的位置。

### <a name="to-add-the-custom-group-to-a-built-in-tab"></a>将自定义组添加到内置选项卡

1. 单击" **内置 (选项卡")** 选项卡以将其选中。

2. 在" **属性"** 窗口中，展开 **ControlId 属性** ，然后将 **OfficeId** 设置为 **TabNewMailMessage**。

     这会将 **"客户购买"** 组添加到新邮件中显示的功能区的"消息"选项卡。

3. 单击" **客户购买"** 组以将其选中。

4. 在"**属性"** 窗口中，展开 **"位置**"属性，单击 **"PositionType"** 属性旁边的下拉箭头，然后单击 **"BeforeOfficeId"。**

5. 将 **OfficeId 属性** 设置为 **GroupClipboard**。

     这会将 **"客户购买"组** 定位 **到"消息"选项卡的** 剪 **贴板组** 之前。

## <a name="create-the-data-source"></a>创建数据源

使用 **“数据源”** 窗口将类型化数据集添加到项目中。

### <a name="to-create-the-data-source"></a>创建数据源

1. 在 **“数据”** 菜单上，单击 **“添加新数据源”**。

     这会启动 **数据源配置向导**。

2. 选择 **"数据库"，** 然后单击"下一 **步"。**

3. 选择 **"数据集**"，然后单击"下一 **步"。**

4. 选择 4.0 数据库的 Northwind Microsoft SQL Server Compact连接，或者使用"新建连接"按钮 **添加新** 连接。

5. 选择或创建连接后，单击"下一 **步"。**

6. 单击 **"下** 一步"保存连接字符串。

7. 在"**选择数据库对象"页上**，展开"表 **"。**

8. 选中以下每个表格旁的复选框：

    1. **客户**

    2. **订单详细信息**

    3. **Orders**

    4. **产品**

9. 单击“完成”。

## <a name="update-controls-in-the-custom-group-at-run-time"></a>运行时更新自定义组中控件

使用功能区对象模型执行以下任务：

- 将客户名称添加到" **客户"** 组合框。

- 将菜单和按钮控件添加到 **表示** 销售订单和已售产品的"已购买产品"菜单中。

- 使用"客户"组合框和"购买的产品"菜单中的数据填充新邮件的"收件人"、主题和 **正文字段。**

### <a name="to-update-controls-in-the-custom-group-by-using-the-ribbon-object-model"></a>使用功能区对象模型更新自定义组中的控件

1. 在“项目”菜单上，单击“添加引用” 。

2. 在"**添加引用"** 对话框中，单击 **".NET"** 选项卡，选择 **System.Data.Linq** 程序集，然后单击"确定 **"。**

    此程序集包含有关使用语言集成查询 (LINQ) 的类。 你将通过 LINQ 使用 Northwind 数据库中的数据填充自定义组中的控件。

3. 在 **解决方案资源管理器，** 单击 **"CustomerRibbon.cs"** 或 **"CustomerRibbon.vb"** 将其选中。

4. 在 **“视图”** 菜单上，单击 **“代码”**。

    功能区代码文件将在代码编辑器中打开。

5. 将下面的语句添加到功能区代码文件的顶部。 通过执行这些语句，可轻松访问 LINQ 命名空间和 Outlook 主互操作程序集 (PIA) 的命名空间。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs" id="Snippet1":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb" id="Snippet1":::

6. 在 类中添加以下 `CustomerRibbon` 代码。 此代码声明了将用于存储 Northwind 数据库的“客户”、“订单”、“订单明细”和“产品”表中信息的数据表和表适配器。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs" id="Snippet2":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb" id="Snippet2":::

7. 将以下代码块添加到 `CustomerRibbon` 类中。 此代码添加三个帮助程序方法，这些方法可运行时为功能区创建控件。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs" id="Snippet3":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb" id="Snippet3":::

8. 将 `CustomerRibbon_Load` 事件处理程序方法替换为以下代码。 此代码使用 LINQ 查询执行以下任务：

   - 使用 **Northwind** 数据库中 20 个客户的 ID 和名称填充"客户"组合框。

   - 调用 `PopulateSalesOrderInfo` 帮助程序方法。 此方法使用与 **当前所选客户相关的销售订单号更新 ProductsPurchased** 菜单。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb" id="Snippet4":::

9. 将以下代码添加到 `CustomerRibbon` 类。 此代码使用 LINQ 查询执行以下任务：

   - 将子菜单添加到与所选客户相关的每个销售订单的 **ProductsPurchased** 菜单。

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

2. 在Outlook"菜单 **上**，指向"**新建**"，然后单击"邮件 **"。**

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

## <a name="see-also"></a>另请参阅

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