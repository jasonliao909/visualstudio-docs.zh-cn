---
title: 在数据绑定中使用查找表 - Windows窗体
description: 了解如何使用 Windows 中的 LookupBindingPropertiesAttribute 类创建支持查找数据绑定的 Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data binding, user controls
- LookupBindingPropertiesAttribute class, examples
- user controls [Visual Basic], creating
ms.assetid: c48b4d75-ccfc-4950-8b14-ff8adbfe4208
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 279d45c46d42f1df2011e7164e66f5aa7fa8eecb543eed8eea3970edcf625765
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121347514"
---
# <a name="create-a-windows-forms-user-control-that-supports-lookup-data-binding"></a>创建支持查找数据绑定的 Windows 窗体用户控件

在 Windows 窗体上显示数据时，你可以从“工具箱”中选择现有的控件，或者，如果应用程序需要标准控件中无法实现的功能时，你还可以创作自定义控件。 本演练显示了如何创建实现 <xref:System.ComponentModel.LookupBindingPropertiesAttribute> 的控件。 实现 <xref:System.ComponentModel.LookupBindingPropertiesAttribute> 的控件可以包含三个属性，这些属性可以绑定到数据。 此类控件类似于 <xref:System.Windows.Forms.ComboBox>。

有关控件创作的信息，请参阅在设计[时Windows窗体控件](/dotnet/framework/winforms/controls/developing-windows-forms-controls-at-design-time)。

创作用于数据绑定方案中的控件时，你需要实现以下数据绑定特性之一：

|数据绑定属性用法|
| - |
|在简单控件上实现 <xref:System.ComponentModel.DefaultBindingPropertyAttribute>（如 <xref:System.Windows.Forms.TextBox>），此类控件用于显示数据的单个列（或属性）。 有关详细信息，请参阅[创建支持Windows绑定的窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md)。|
|在控件上实现 <xref:System.ComponentModel.ComplexBindingPropertiesAttribute>（如 <xref:System.Windows.Forms.DataGridView>），此类控件用于显示数据列表（或表）。 有关详细信息，请参阅[创建支持Windows绑定的窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)。|
|在控件上实现 <xref:System.ComponentModel.LookupBindingPropertiesAttribute>（如 <xref:System.Windows.Forms.ComboBox>），该控件用于显示数据列表（或表），也需要显示数据的单个列或属性。 （本演练页面描述了此过程）。|

本演练创建绑定到源自两个表的数据的查找控件。 此示例使用源自 Northwind 示例数据库的 `Customers` 和 `Orders` 表。 查找控件绑定到表中的 `CustomerID` `Orders` 字段。 它使用此值从表中 `CompanyName` `Customers` 查找 。

本演练将学习如何：

- 创建新的 Windows **窗体应用程序**。

- 将新的“用户控件”添加到项目中。

- 以可视方式设计用户控件。

- 实现 `LookupBindingProperty` 特性。

- 使用"数据源配置 **"向导创建** 数据集。

- 在“数据源”窗口中，设置“Orders”表上的“CustomerID”列，以使用新的控件。

- 创建一个用于在新控件中显示数据的窗体。

## <a name="prerequisites"></a>必备条件

本演练使用 SQL Server Express LocalDB和 Northwind 示例数据库。

1. 如果尚未安装SQL Server Express LocalDB，请从下载页SQL Server Express安装它，或者通过 [](https://www.microsoft.com/sql-server/sql-server-editions-express) **Visual Studio 安装程序。** 在 **Visual Studio 安装程序** 中，可以将 SQL Server Express LocalDB作为数据存储和处理工作负荷的一部分安装，也可以作为单个组件安装。

2. 按照以下步骤安装 Northwind 示例数据库：

    1. 在Visual Studio中，**打开SQL Server 对象资源管理器窗口**。  (SQL Server 对象资源管理器作为数据存储和处理工作负荷的一部分安装在Visual Studio 安装程序.) **展开SQL Server节点**。 右键单击实例LocalDB并选择"新建 **查询"。**

       查询编辑器窗口随即打开。

    2. 将[Northwind Transact-SQL脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)复制到剪贴板。 此 T-SQL脚本从头开始创建 Northwind 数据库，并使用数据填充该数据库。

    3. 将 T-SQL脚本粘贴到查询编辑器中，然后选择"执行 **"** 按钮。

       短时间后，查询完成运行，并创建 Northwind 数据库。

## <a name="create-a-windows-forms-app-project"></a>创建Windows窗体应用项目

第一步是创建一个Windows **窗体应用程序** 项目。

1. 在 Visual Studio 的“文件”菜单中，依次选择“新建” > “项目”    。

2. 展开左侧 **窗格中Visual Basic"Visual C#"** 或"Windows"。 

3. 在中间窗格中，选择"Windows **窗体应用"** 项目类型。

4. 将项目 **"LookupControlWalkthrough"命名**，然后选择"确定 **"。**

     创建“LookupControlWalkthrough”项目并添加到“解决方案资源管理器”中。

## <a name="add-a-user-control-to-the-project"></a>将用户控件添加到项目中

由于本演练从“用户控件”创建查找控件，所以必须将“用户控件”项添加到“LookupControlWalkthrough”项目中。

1. 从“项目”菜单中，选择“添加用户控件”。

2. 在 `LookupBox` "名称 **"区域中键入**，然后单击"添加 **"。**

     将“LookupBox”控件添加到“解决方案资源管理器”中，并在设计器中打开该控件。

## <a name="design-the-lookupbox-control"></a>设计 LookupBox 控件

若要设计 LookupBox 控件，请将 从"工具箱"拖动到 <xref:System.Windows.Forms.ComboBox> 用户控件的设计图面上。 

## <a name="add-the-required-data-binding-attribute"></a>添加所需的数据绑定属性

对于支持数据绑定的查找控件，你可以实现 <xref:System.ComponentModel.LookupBindingPropertiesAttribute>。

1. 将“LookupBox”控件切换到代码视图。 （在“视图”菜单上，选择“代码”。）

2. 将 `LookupBox` 中的代码替换为以下内容：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/LookupBox.vb" id="Snippet5":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/LookupBox.cs" id="Snippet5":::

3. 从 **“生成”** 菜单中选择 **“生成解决方案”** 。

## <a name="create-a-data-source-from-your-database"></a>从数据库创建数据源

此步骤根据 Northwind 示例数据库中的 `Customers` 和 `Orders` 表，使用“数据源配置”向导创建数据源。

1. 若要打开"**数据源"** 窗口，请在"数据 **"** 菜单上单击"**显示数据源"。**

2. 在" **数据源"** 窗口中， **选择"添加新数据源** "以启动 **"数据源配置"** 向导。

3. 在 **“选择数据源类型”** 页上选择 **“数据库”** ，然后单击 **“下一步”**。

4. 在“选择数据连接”页面上，执行以下操作之一：

    - 如果下拉列表中包含到 Northwind 示例数据库的数据连接，请选择该连接。

    - 选择“新建连接”以启动“添加/修改连接”对话框。

5. 如果数据库需要密码，请选择该选项以包括敏感数据，再单击“下一步”。

6. 在"**将连接字符串保存到应用程序配置文件"页上**，单击"下一 **步"。**

7. 在“选择数据库对象”页上，展开“表”节点。

8. 选择 `Customers` 和 `Orders` 表，然后单击“完成”。

     **NorthwindDataSet** 将添加到项目中，并且 和 `Customers` `Orders` 表显示在"**数据源"** 窗口中。

## <a name="set-the-customerid-column-of-the-orders-table-to-use-the-lookupbox-control"></a>将 Orders 表的 CustomerID 列设置为使用 LookupBox 控件

在“数据源”窗口中，可以先设置要创建的控件，然后再将项拖动到窗体上。

1. 在设计器中打开“Form1”。

2. 在“数据源”窗口中展开“Customers”节点。

3. 展开“Orders”节点（“Customers”节点中“Fax”列下面的节点）。

4. 单击“Orders”节点上的下拉箭头，然后从控件列表中选择“详细信息”。

5. 单击“CustomerID”列（在“Orders”节点中）上的下拉箭头，然后选择“自定义”。

6. 在“数据 UI 自定义选项”对话框中，从“关联的控件”列表中选择“LookupBox”。

7. 单击“确定”。

8. 单击“CustomerID”列上的下拉箭头，然后选择“LookupBox”。

## <a name="add-controls-to-the-form"></a>向窗体添加控件

通过将某些项从“数据源”窗口中拖到“Form1”上，可创建数据绑定控件。

若要在 Windows 窗体上创建数据绑定控件，请将"数据源"窗口中的"订单"节点拖到 Windows 窗体上，并验证 **LookupBox** 控件是否用于显示列中 `CustomerID` 的数据。

## <a name="bind-the-control-to-look-up-companyname-from-the-customers-table"></a>绑定 控件以从 Customers 表中查找 CompanyName

若要设置查找绑定，请在"数据源"窗口中选择"客户"主节点，并将其拖动到 **Form1** 上的 **CustomerIDLookupBox** 中的组合框上。

此操作对数据绑定进行设置，使其显示 `Customers` 表中的 `CompanyName`同时保留 `Orders` 表中的 `CustomerID` 值。

## <a name="run-the-application"></a>运行应用程序

- 按 **F5** 运行该应用程序。

- 通过某些记录进行定位，并验证 `LookupBox` 控件中是否显示 `CompanyName`。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
