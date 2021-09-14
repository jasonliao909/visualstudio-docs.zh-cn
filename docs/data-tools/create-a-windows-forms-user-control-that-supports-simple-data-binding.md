---
title: 创建支持简单数据绑定的用户控件
description: 了解如何使用 Windows 中的 DefaultBindingPropertyAttribute 类创建支持简单数据绑定的 Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom controls [Visual Studio], Data Sources Window
- Data Sources Window, controls
ms.assetid: b1488366-6dfb-454e-9751-f42fd3f3ddfb
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 213bededbd5d6eea8a0eb6b01f742c6cf82d8e4a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601188"
---
# <a name="create-a-windows-forms-user-control-that-supports-simple-data-binding"></a>创建支持简单数据绑定的 Windows 窗体用户控件

在 Windows 应用程序的窗体上显示数据时，可以从“工具箱”中选择现有的控件，而当标准控件无法提供应用程序所要求的功能时，还可以创作自定义控件。 本演练显示了如何创建实现 <xref:System.ComponentModel.DefaultBindingPropertyAttribute> 的控件。 用于实现 <xref:System.ComponentModel.DefaultBindingPropertyAttribute> 的控件可以包含一个可以绑定到数据的属性。 此类控件类似于 <xref:System.Windows.Forms.TextBox> 或 <xref:System.Windows.Forms.CheckBox>。

有关控件创作的信息，请参阅在设计[时Windows窗体控件。](/dotnet/framework/winforms/controls/developing-windows-forms-controls-at-design-time)

创作控件以用于数据绑定方案时，应实现以下数据绑定属性之一：

|数据绑定属性用法|
| - |
|在简单控件上实现 <xref:System.ComponentModel.DefaultBindingPropertyAttribute>（如 <xref:System.Windows.Forms.TextBox>），此类控件用于显示数据的单个列（或属性）。 （本演练页面描述了此过程）。|
|在控件上实现 <xref:System.ComponentModel.ComplexBindingPropertiesAttribute>（如 <xref:System.Windows.Forms.DataGridView>），此类控件用于显示数据列表（或表）。 有关详细信息，请参阅[创建支持Windows绑定的窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)。|
|在控件上实现 <xref:System.ComponentModel.LookupBindingPropertiesAttribute>（如 <xref:System.Windows.Forms.ComboBox>），此类控件用于显示数据列表（或表），也需要显示数据的单个列或属性。 有关详细信息，请参阅[创建支持Windows绑定的窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md)。|

本演练创建了一个简单控件，用于显示表中单个列的数据。 此示例使用 Northwind 示例数据库的 `Phone` 表中的 `Customers` 列。 简单的用户控件使用 ，将掩码设置为电话号码，以标准电话号码格式 <xref:System.Windows.Forms.MaskedTextBox> 显示客户的电话号码。

在本演练中，你将学会如何执行以下任务：

- 创建新的 Windows **窗体应用程序**。

- 将新的“用户控件”添加到项目中。

- 以可视方式设计用户控件。

- 实现 `DefaultBindingProperty` 特性。

- 使用"数据源配置 **"向导创建** 数据集。

- 在“数据源”窗口中，设置“电话”列，以使用新的控件。

- 创建一个用于在新控件中显示数据的窗体。

## <a name="prerequisites"></a>先决条件

本演练使用 SQL Server Express LocalDB 和 Northwind 示例数据库。

1. 如果尚未安装SQL Server Express LocalDB，请从下载页SQL Server Express安装 [它，或者](https://www.microsoft.com/sql-server/sql-server-editions-express)通过 **Visual Studio 安装程序。** 在 **Visual Studio 安装程序** 中，可以将 SQL Server Express LocalDB作为数据存储和处理工作负荷的一部分安装，也可以作为单个组件安装。

2. 按照以下步骤安装 Northwind 示例数据库：

    1. 在Visual Studio中，**打开SQL Server 对象资源管理器窗口**。  (SQL Server 对象资源管理器作为数据存储和处理工作负荷的一部分安装在Visual Studio 安装程序 **.)** 展开 **SQL Server节点。** 右键单击实例LocalDB并选择"新建 **查询"。**

       查询编辑器窗口随即打开。

    2. 将[Northwind Transact-SQL脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)复制到剪贴板。 此 T-SQL脚本从头开始创建 Northwind 数据库，并使用数据填充该数据库。

    3. 将 T-SQL脚本粘贴到查询编辑器中，然后选择"执行 **"** 按钮。

       短时间后，查询完成运行，并创建 Northwind 数据库。

## <a name="create-a-windows-forms-application"></a>创建 Windows 窗体应用程序

第一步是创建一个 **Windows窗体应用程序**：

1. 在 Visual Studio 的“文件”菜单中，依次选择“新建” > “项目”    。

2. 在左侧 **窗格中展开"Visual C#"****或**"Visual Basic"，然后选择"Windows **桌面"。**

3. 在中间窗格中，选择"Windows **窗体应用"** 项目类型。

4. 将项目 **命名为 SimpleControlWalkthrough**，然后选择"确定 **"。**

     创建“SimpleControlWalkthrough”项目并将其添加到“解决方案资源管理器”中。

## <a name="add-a-user-control-to-the-project"></a>将用户控件添加到项目中

本演练从用户控件 创建一个简单的数据可 **绑定控件**。 将 **用户控件项** 添加到 **SimpleControlWalkthrough** 项目：

1. 从“项目”菜单，选择“添加用户控件”。

2. 在名称区域键入“PhoneNumberBox”，然后单击“添加”。

     将“PhoneNumberBox”控件添加到“解决方案资源管理器”中，并在设计器中打开它。

## <a name="design-the-phonenumberbox-control"></a>设计 PhoneNumberBox 控件

本演练将扩展现有 以 <xref:System.Windows.Forms.MaskedTextBox> 创建 **PhoneNumberBox** 控件：

1. 将 <xref:System.Windows.Forms.MaskedTextBox> 从“工具箱”拖到该用户控件的设计图面上。

2. 选择刚刚拖动的 <xref:System.Windows.Forms.MaskedTextBox> 上的智能标记，然后选择“设置掩码”。

3. 在“输入掩码”对话框中选择“电话号码”，然后单击“确定”以设置掩码。

## <a name="add-the-required-data-binding-attribute"></a>添加所需的数据绑定属性

对于支持数据绑定的简单控件，实现 <xref:System.ComponentModel.DefaultBindingPropertyAttribute>：

1. 将 **PhoneNumberBox** 控件切换到代码视图。 （在“视图”菜单上，选择“代码”。）

2. 将 **PhoneNumberBox 中的代码** 替换为以下内容：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/PhoneNumberBox.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/PhoneNumberBox.vb" id="Snippet3":::

3. 从 **“生成”** 菜单中选择 **“生成解决方案”** 。

## <a name="create-a-data-source-from-your-database"></a>从数据库创建数据源

此步骤使用 **数据源配置** 向导基于 Northwind 示例数据库中的 表创建 `Customers` 数据源。 你必须具有对 Northwind 示例数据库的访问权限，才能创建连接。 有关设置 Northwind 示例数据库的信息，请参阅 [如何：安装示例数据库](../data-tools/installing-database-systems-tools-and-samples.md)。

1. 若要打开"**数据源"** 窗口，请在"数据 **"** 菜单上单击"**显示数据源"。**

2. 在" **数据源"** 窗口中， **选择"添加新数据源** "以启动 **"数据源配置"** 向导。

3. 在“选择数据源类型”页上，选择“数据库”，然后单击“下一步”。

4. 在 **"选择数据连接"** 页上，执行以下操作之一：

    - 如果下拉列表中包含到 Northwind 示例数据库的数据连接，请选择该连接。

    - 选择“新建连接”以启动“添加/修改连接”对话框。

5. 如果数据库需要密码，请选择该选项以包括敏感数据，再单击“下一步”。

6. 在"**将连接字符串保存到应用程序配置文件"页上**，单击"下一 **步"。**

7. 在“选择数据库对象”页上，展开“表”节点。

8. 选择 `Customers` 表，然后单击“完成”。

     **NorthwindDataSet** 将添加到项目中，表 `Customers` 将显示在"数据源 **"** 窗口中。

## <a name="set-the-phone-column-to-use-the-phonenumberbox-control"></a>将电话列设置为使用 PhoneNumberBox 控件

在 **"数据源"** 窗口中，可以在将项拖动到窗体之前设置要创建的控件：

1. 在设计器中打开“Form1”。

2. 在“数据源”窗口中展开“Customers”节点。

3. 在“Customers”节点上单击下拉箭头，然后从控件列表中选择“详细信息”。

4. 单击“电话”列上的下拉箭头，然后选择“自定义”。

5. 从“数据 UI 自定义选项”对话框中的“关联的控件”列表中，选择“PhoneNumberBox”。

6. 单击“电话”列上的下拉箭头，然后选择“PhoneNumberBox”。

## <a name="add-controls-to-the-form"></a>向窗体添加控件

通过将“数据源”窗口中的项拖到窗体上，可创建数据绑定控件。

若要在窗体上创建数据绑定控件，请将"数据源"窗口中的主"客户"节点拖到窗体上，并验证 **PhoneNumberBox** 控件是否用于显示 电话 **列中的数据**。

带有描述性标签的数据绑定控件将显示在窗体上，同时还显示一个工具条 (<xref:System.Windows.Forms.BindingNavigator>)，用于在记录间进行导航。 组件栏中显示[“NorthwindDataSet”](../data-tools/dataset-tools-in-visual-studio.md)、CustomersTableAdapter、<xref:System.Windows.Forms.BindingSource> 和 <xref:System.Windows.Forms.BindingNavigator>。

## <a name="run-the-application"></a>运行应用程序

按 **F5** 运行该应用程序。

## <a name="next-steps"></a>后续步骤

根据应用程序的需求，在创建了支持数据绑定的控件后，可能还需要执行一些步骤。 接下来的一些常见步骤包括：

- 将你的自定义控件置于控件库中，以便在其他应用程序中重用它们。

- 创建支持更复杂的数据绑定方案的控件。 有关详细信息，请参阅[创建](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)Windows复杂数据绑定的窗体用户控件和创建Windows查找数据绑定 的[窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md)。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [设置从“数据源”窗口中拖动时要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)
