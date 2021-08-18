---
title: 用 TableAdapter DBDirect 方法保存数据
description: 在此演练中，SQL TableAdapter 的 DBDirect 方法直接对数据库运行语句。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TableAdapters, walkthroughs
- data [Visual Studio], saving
- saving data, walkthroughs
- data [Visual Studio], TableAdapter
ms.assetid: 74a6773b-37e1-4d96-a39c-63ee0abf49b1
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: cf7ed024e98382ea134c27cd697cdae932d735d5
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122113778"
---
# <a name="save-data-with-the-tableadapter-dbdirect-methods"></a>用 TableAdapter DBDirect 方法保存数据

本演练提供有关使用 TableAdapter 的 DBDirect SQL数据库直接运行语句的详细说明。 TableAdapter 的 DBDirect 方法可对数据库更新进行精确的控制。 可以使用它们来运行特定的 SQL 语句和存储过程，方法是调用应用程序 (所需的单个 、 和 方法，而不是在一个调用) 中执行 `Insert` `Update` `Delete` `Update` UPDATE、INSERT 和 DELETE 语句的重载方法。

在本演练中，你将学会如何执行以下任务：

- 创建新的 Windows **窗体应用程序**。

- 使用数据源配置向导 [创建和配置数据集](../data-tools/media/data-source-configuration-wizard.png)。

- 选择从“数据源”窗口拖动某些项时要在窗体上创建的控件。 有关详细信息，请参阅设置从"数据源"窗口拖动时 [要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

- 通过将某些项从“数据源”窗口拖到窗体上来创建数据绑定窗体。

- 添加直接访问数据库并执行插入、更新和删除的方法。

## <a name="prerequisites"></a>必备条件

本演练使用 SQL Server Express LocalDB和 Northwind 示例数据库。

1. 如果尚未安装SQL Server Express LocalDB，请从下载页SQL Server Express安装它，或者通过 [](https://www.microsoft.com/sql-server/sql-server-editions-express)**Visual Studio 安装程序。** 在 **Visual Studio 安装程序** 中，可以将 SQL Server Express LocalDB作为数据存储和处理工作负荷的一部分安装，也可以作为单个组件安装。

2. 按照以下步骤安装 Northwind 示例数据库：

    1. 在Visual Studio中，**打开SQL Server 对象资源管理器窗口**。  (SQL Server 对象资源管理器作为数据存储和处理工作负荷的一部分安装在Visual Studio 安装程序.) 展开 **SQL Server节点。** 右键单击实例LocalDB并选择"新建 **查询"。**

       查询编辑器窗口随即打开。

    2. 将[Northwind Transact-SQL脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)复制到剪贴板。 此 T-SQL脚本从头开始创建 Northwind 数据库，并使用数据填充该数据库。

    3. 将 T-SQL脚本粘贴到查询编辑器中，然后选择"执行 **"** 按钮。

       短时间后，查询完成运行，并创建 Northwind 数据库。

## <a name="create-a-windows-forms-application"></a>创建 Windows 窗体应用程序

第一步是创建一Windows **窗体应用程序**。

1. 在 Visual Studio 的“文件”菜单中，依次选择“新建” > “项目”    。

2. 在左侧 **窗格中展开"Visual C#"****或**"Visual Basic"，然后选择"Windows **桌面"。**

3. 在中间窗格中，选择"Windows **窗体应用"** 项目类型。

4. 将项目 **"TableAdapterDbDirectMethodsWalkthrough"** 命名，然后选择"确定 **"。**

     创建“TableAdapterDbDirectMethodsWalkthrough”项目并将其添加到“解决方案资源管理器”中。

## <a name="create-a-data-source-from-your-database"></a>从数据库创建数据源

此步骤根据 Northwind 示例数据库中的 `Region` 表，使用“数据源配置”向导创建数据源。 你必须具有对 Northwind 示例数据库的访问权限，才能创建连接。 有关设置 Northwind 示例数据库的信息，请参阅 [如何：安装示例数据库](../data-tools/installing-database-systems-tools-and-samples.md)。

### <a name="to-create-the-data-source"></a>创建数据源

1. 在“数据”菜单上，选择“显示数据源” 。

   “数据源”窗口随即打开。

2. 在“数据源”窗口，选择“添加新数据源”以启动“数据源配置”向导。

3. 在"**选择数据源类型"屏幕上**，选择"**数据库"，** 然后选择"下一 **步"。**

4. 在 **"选择数据连接"屏幕上** ，执行以下操作之一：

    - 如果下拉列表中包含到 Northwind 示例数据库的数据连接，请选择该连接。

         -或-

    - 选择“新建连接”以启动“添加/修改连接”对话框。

5. 如果数据库需要密码，请选择包含敏感数据的选项，然后选择"下一步 **"。**

6. 在"**将连接字符串保存到应用程序配置文件"屏幕上**，选择"下一 **步"。**

7. 在" **选择数据库对象"屏幕上** ，展开" **表"** 节点。

8. 选择表 `Region` ，然后选择"完成 **"。**

     将“NorthwindDataSet”添加到项目后，“数据源”窗口中即会显示 `Region` 表。

## <a name="add-controls-to-the-form-to-display-the-data"></a>向窗体添加控件以显示数据

通过将某些项从“数据源”窗口拖到窗体上来创建数据绑定控件。

若要在窗体上创建数据绑定Windows，请将"数据源"窗口中的主"区域"节点拖到窗体上。

用于导航记录的 <xref:System.Windows.Forms.DataGridView> 控件和工具栏（<xref:System.Windows.Forms.BindingNavigator>）将显示在窗体上。 [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md) `RegionTableAdapter` 、、 <xref:System.Windows.Forms.BindingSource> 和 <xref:System.Windows.Forms.BindingNavigator> 显示在组件栏中。

### <a name="to-add-buttons-that-will-call-the-individual-tableadapter-dbdirect-methods"></a>添加将调用单个 TableAdapter DbDirect 方法的按钮

1. 将三个 <xref:System.Windows.Forms.Button> 控件从“工具箱”拖到“Form1”上（在“RegionDataGridView”的下面）。

2. 在每个按钮上设置下列“名称”和“文本”属性。

    |名称|文本|
    |----------|----------|
    |`InsertButton`|插入|
    |`UpdateButton`|**更新**|
    |`DeleteButton`|**删除**|

### <a name="to-add-code-to-insert-new-records-into-the-database"></a>添加将新记录插入数据库所使用的代码

1. 选择 **"插入""** 按钮"，为单击事件创建事件处理程序，在代码编辑器中打开窗体。

2. 用下面的代码替换 `InsertButton_Click` 事件处理程序：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form1.vb" id="Snippet1":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form1.cs" id="Snippet1":::

### <a name="to-add-code-to-update-records-in-the-database"></a>添加更新数据库中的记录所使用的代码

1. 双击“UpdateButton”以创建 Click 事件的事件处理程序，并在代码编辑器中打开窗体。

2. 用下面的代码替换 `UpdateButton_Click` 事件处理程序：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form1.vb" id="Snippet2":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form1.cs" id="Snippet2":::

### <a name="to-add-code-to-delete-records-from-the-database"></a>添加代码以从数据库中删除记录

1. 选择 **"DeleteButton"** 为单击事件创建事件处理程序，然后打开代码编辑器中的窗体。

2. 用下面的代码替换 `DeleteButton_Click` 事件处理程序：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form1.vb" id="Snippet3":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form1.cs" id="Snippet3":::

## <a name="run-the-application"></a>运行应用程序

- 选择 **F5** 以运行应用程序。

- 选择" **插入** "按钮，并验证新记录是否显示在网格中。

- 选择 **"更新** "按钮，并验证记录在网格中是否更新。

- 选择" **删除** "按钮，并验证记录是否从网格中删除。

## <a name="next-steps"></a>后续步骤

根据应用程序要求，可能需要在创建数据绑定窗体后执行几个步骤。 你可以通过以下操作来增强此演练的效果：

- 将搜索功能添加到该窗体。

- 通过从“数据源”窗口中选择“使用向导配置数据集”，将其他表添加到数据集中。 可以通过将相关节点拖到窗体上来添加显示相关数据的控件。 有关详细信息，请参阅 [数据集中的关系](relationships-in-datasets.md)。

## <a name="see-also"></a>请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
