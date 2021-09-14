---
title: 使用 ADO.NET 创建简单的数据应用程序
description: 了解如何在 Visual Studio 中通过使用 Windows 窗体和 ADO.NET 创建简单的表单到数据Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 08/23/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
ms.assetid: 2222841f-e443-4a3d-8c70-4506aa905193
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 506983ffacf846969f6e74fd503344d90180ca91
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601202"
---
# <a name="create-a-simple-data-application-by-using-adonet"></a>使用 ADO.NET 创建简单的数据应用程序

当你创建操作数据库中的数据的应用程序时，就执行了如定义连接字符串、插入数据以及运行存储过程等基本任务。 通过遵循本主题，你可以了解如何使用 Visual C# 或 Visual Basic 和 ADO.NET 从简单的 Windows 窗体"基于数据"应用程序中与数据库进行交互。  所有 .NET 数据技术（包括数据集、LINQ to SQL和实体框架）最终执行的步骤与本文中所示的步骤非常相似。

本文演示了一种快速从数据库获取数据的简单方法。 如果应用程序需要以非普通方式修改数据并更新数据库，则应考虑使用 实体框架 和数据绑定，以自动将用户界面控件与基础数据中的更改同步。

> [!IMPORTANT]
> 要使代码保持简单，请不要包括生产就绪的异常处理。

## <a name="prerequisites"></a>先决条件

要创建应用程序，你将需要：

- Visual Studio。

- SQL Server Express LocalDB。 如果尚未安装SQL Server Express LocalDB，可以从下载页[SQL Server Express它](https://www.microsoft.com/sql-server/sql-server-editions-express)。

本主题假定你熟悉 Visual Studio IDE 的基本功能，并可以创建 Windows Forms 应用程序、向项目添加窗体、将按钮和其他控件放在窗体上、设置控件的属性以及编写简单事件代码。 如果你对这些任务不太熟悉，建议在开始本演练之前完成[Visual C# Visual Basic](../ide/quickstart-visual-basic-console.md)主题。

## <a name="set-up-the-sample-database"></a>设置示例数据库

按照以下步骤创建示例数据库：

1. 在Visual Studio中，**打开服务器资源管理器窗口**。

2. 右键单击"数据 **连接"，** 然后选择 **"新建SQL Server数据库"。**

3. 在" **服务器名称"** 文本框中 **， (localdb) \mssqllocaldb**。

4. 在"**新建数据库名称"** 文本框中，输入 **"Sales"，** 然后选择"确定 **"。**

     空 **的 Sales** 数据库将创建并添加到 服务器资源管理器 中的"数据连接"节点。

5. 右键单击"销售 **数据连接**"，然后选择"新建 **查询"。**

     查询编辑器窗口随即打开。

6. 将[Sales Transact-SQL脚本](https://github.com/MicrosoftDocs/visualstudio-docs/raw/master/docs/data-tools/samples/sales.sql)复制到剪贴板。

7. 将 T-SQL脚本粘贴到查询编辑器中，然后选择"执行 **"** 按钮。

     在短时间内，查询完成运行并创建数据库对象。 数据库包含两个表：Customer 和 Orders。 这些表最初不包含任何数据，但可以在运行要创建的应用程序时添加数据。 该数据库还包含四个简单的存储过程。

## <a name="create-the-forms-and-add-controls"></a>创建窗体并添加控件

1. 创建 Windows 窗体应用程序项目，然后将其命名为“SimpleDataApp”。

    Visual Studio 将创建项目以及若干个文件，其中包括名为“Form1”的空 Windows 窗体。

2. 添加两个 Windows 窗体到项目中，以使其具有三个窗体，然后给予它们下列名称：

   - **导航**

   - **NewCustomer**

   - **FillOrCancel**

3. 对于每个窗体，添加文本框、按钮和其他控件，如下图所示。 对于每个控件，设置表中描述的属性。

   > [!NOTE]
   > 分组框和标签控件可提高清晰度，但不在代码中使用。

   **Navigation 窗体**

   ![“导航”对话框](../data-tools/media/simpleappnav.png)

|Navigation 窗体的控件|属性|
| - |----------------|
|Button|Name = btnGoToAdd|
|Button|Name = btnGoToFillOrCancel|
|Button|Name = btnExit|

**NewCustomer 窗体**

![添加新客户或提交订单](../data-tools/media/simpleappnewcust.png)

|NewCustomer 窗体的控件|属性|
| - |----------------|
|TextBox|Name = txtCustomerName|
|TextBox|Name = txtCustomerID<br /><br /> Readonly = True|
|Button|Name = btnCreateAccount|
|NumericUpdown|DecimalPlaces = 0<br /><br /> Maximum = 5000<br /><br /> Name = numOrderAmount|
|DateTimePicker|Format = Short<br /><br /> Name = dtpOrderDate|
|Button|Name = btnPlaceOrder|
|Button|Name = btnAddAnotherAccount|
|Button|Name = btnAddFinish|

**FillOrCancel 窗体**

![填充或取消订单](../data-tools/media/simpleappcancelfill.png)

|FillOrCancel 窗体的控件|属性|
| - |----------------|
|TextBox|Name = txtOrderID|
|Button|Name = btnFindByOrderID|
|DateTimePicker|Format = Short<br /><br /> Name = dtpFillDate|
|DataGridView|Name = dgvCustomerOrders<br /><br /> Readonly = True<br /><br /> RowHeadersVisible = False|
|Button|Name = btnCancelOrder|
|Button|Name = btnFillOrder|
|Button|Name = btnFinishUpdates|

## <a name="store-the-connection-string"></a>存储连接字符串
当应用程序尝试打开数据库的连接时，应用程序必须能够访问连接字符串。 为了避免在每个窗体上手动输入字符串，请将字符串存储在项目中 *的App.config* 文件中，并创建一个方法，该方法在从应用程序的任何窗体调用 方法时返回字符串。

可以通过右键单击"销售数据连接"并选择"属性"来 **服务器资源管理器字符串。**  找到 **ConnectionString 属性**，然后使用 **Ctrl** + **A** 和 **Ctrl** C 选择字符串 + ，然后将字符串复制到剪贴板。

1. 如果使用 C#，则 **解决方案资源管理器，展开** 项目下的"属性"节点，然后打开 **设置.settings** 文件。
    如果使用的是 Visual Basic，请在 解决方案资源管理器 中单击"**显示** 所有文件"，展开"我的 Project"节点，然后打开 **设置.settings** 文件。

2. 在" **名称"** 列中，输入 `connString` 。

3. 在" **类型"** 列表中，选择 **" (字符串) "**。

4. 在"**作用域"** 列表中，选择"应用程序 **"。**

5. 在" **值** "列中，输入连接字符串 (不带任何外部引号) ，然后保存所做的更改。

> [!NOTE]
> 在真实应用程序中，应安全存储连接字符串，如连接字符串和 [配置文件 中所述](/dotnet/framework/data/adonet/connection-strings-and-configuration-files)。

## <a name="write-the-code-for-the-forms"></a>编写窗体代码

本部分包含每个窗体的简要概述。 它还提供在单击窗体上的按钮时定义基础逻辑的代码。

### <a name="navigation-form"></a>Navigation 窗体

运行应用程序时，Navigation 窗体将打开。 按“添加帐户”按钮可以打开 NewCustomer 窗体。 按“填写或取消订单”按钮可以打开 FillOrCancel 窗体。 按“退出”按钮可以关闭应用程序。

#### <a name="make-the-navigation-form-the-startup-form"></a>使 Navigation 窗体成为启动窗体

如果使用 C#，则在“解决方案资源管理器”中，打开 Program.cs，然后将 `Application.Run` 行更改为 `Application.Run(new Navigation());`

如果使用的是 Visual Basic，请在 解决方案资源管理器 中打开"**属性**"窗口，选择"应用程序"选项卡，然后在"启动窗体"列表中选择 **"SimpleDataApp.Navigation"。** 

#### <a name="create-auto-generated-event-handlers"></a>创建自动生成的事件处理程序

双击"导航"窗体上的三个按钮，以创建空事件处理程序方法。 双击按钮还会在设计器代码文件中添加自动生成的代码，使按钮单击能够引发事件。

#### <a name="add-code-for-the-navigation-form-logic"></a>为导航窗体逻辑添加代码

在"导航"窗体的代码页中，完成三个按钮单击事件处理程序的方法主体，如以下代码所示。

:::code language="csharp" source="../data-tools/codesnippet/CSharp/SimpleDataApp/Navigation.cs" id="Snippet1":::
:::code language="vb" source="../data-tools/codesnippet/VisualBasic/SimpleDataApp/Navigation.vb" id="Snippet1":::

### <a name="newcustomer-form"></a>NewCustomer 窗体

输入客户名称并选择"创建帐户"按钮时，NewCustomer 窗体将创建一个客户帐户，SQL Server IDENTITY 值作为新的客户 ID 返回。 然后，可以通过指定金额和订单日期并选择"下单"按钮来下 **新帐户** 的订单。

#### <a name="create-auto-generated-event-handlers"></a>创建自动生成的事件处理程序

双击四个按钮中的每个按钮，为 NewCustomer 窗体上的每个按钮创建空的 Click 事件处理程序。 双击按钮还会在设计器代码文件中添加自动生成的代码，使按钮单击能够引发事件。

#### <a name="add-code-for-the-newcustomer-form-logic"></a>为 NewCustomer 窗体逻辑添加代码

若要完成 NewCustomer 窗体逻辑，请执行以下步骤。

1. 将 `System.Data.SqlClient` 命名空间纳入范围，以便不必完全限定其成员的名称。

     ```csharp
     using System.Data.SqlClient;
     ```

     ```vb
     Imports System.Data.SqlClient
     ```

2. 将一些变量和帮助程序方法添加到 类，如以下代码所示。

     :::code language="csharp" source="../data-tools/codesnippet/CSharp/SimpleDataApp/NewCustomer.cs" id="Snippet1":::
     :::code language="vb" source="../data-tools/codesnippet/VisualBasic/SimpleDataApp/NewCustomer.vb" id="Snippet1":::

3. 完成四个按钮单击事件处理程序的方法主体，如以下代码所示。

     :::code language="csharp" source="../data-tools/codesnippet/CSharp/SimpleDataApp/NewCustomer.cs" id="Snippet2":::
     :::code language="vb" source="../data-tools/codesnippet/VisualBasic/SimpleDataApp/NewCustomer.vb" id="Snippet2":::

### <a name="fillorcancel-form"></a>FillOrCancel 窗体

当输入订单 ID，然后单击"查找订单"按钮时，FillOrCancel 窗体将运行查询以 **返回** 订单。 返回的行在只读数据网格中显示。 如果选择"取消订单"按钮 (X) ，可以将订单标记为已取消;如果选择"填充订单"按钮 (F) 可以将订单标记为已 **填充**。 如果再次选择" **查找顺序"** 按钮，则会显示更新的行。

#### <a name="create-auto-generated-event-handlers"></a>创建自动生成的事件处理程序

通过双击这些按钮，为 FillOrCancel 窗体上的四个按钮创建空的 Click 事件处理程序。 双击按钮还会在设计器代码文件中添加自动生成的代码，使按钮单击能够引发事件。

#### <a name="add-code-for-the-fillorcancel-form-logic"></a>为 FillOrCancel 窗体逻辑添加代码

若要完成 FillOrCancel 窗体逻辑，请执行以下步骤。

1. 将以下两个命名空间纳入范围，以便你不必完全限定其成员的名称。

     ```csharp
     using System.Data.SqlClient;
     using System.Text.RegularExpressions;
     ```

     ```vb
     Imports System.Data.SqlClient
     Imports System.Text.RegularExpressions
     ```

2. 将变量和 helper 方法添加到 类，如以下代码所示。

     :::code language="csharp" source="../data-tools/codesnippet/CSharp/SimpleDataApp/FillOrCancel.cs" id="Snippet1":::
     :::code language="vb" source="../data-tools/codesnippet/VisualBasic/SimpleDataApp/FillOrCancel.vb" id="Snippet1":::

3. 完成四个按钮单击事件处理程序的方法主体，如以下代码所示。

     :::code language="csharp" source="../data-tools/codesnippet/CSharp/SimpleDataApp/FillOrCancel.cs" id="Snippet2":::
     :::code language="vb" source="../data-tools/codesnippet/VisualBasic/SimpleDataApp/FillOrCancel.vb" id="Snippet2":::

## <a name="test-your-application"></a>测试应用程序

在对每个 Click 事件处理程序进行编码且完成编码后，请按 F5 键以生成并测试应用程序。

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
