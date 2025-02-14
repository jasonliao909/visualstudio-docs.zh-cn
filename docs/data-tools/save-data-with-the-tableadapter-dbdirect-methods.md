---
title: 用 TableAdapter DBDirect 方法保存数据
description: 在本教程中，SQL TableAdapter 的 DBDirect 方法直接对数据库运行语句。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TableAdapters, tutorials
- data [Visual Studio], saving
- saving data, tutorials
- data [Visual Studio], TableAdapter
ms.assetid: 74a6773b-37e1-4d96-a39c-63ee0abf49b1
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: e2f3e1f5761b4cbe85f190e09a542a0c406b8480
ms.sourcegitcommit: 11a02f6a01fe73349084663a0b39909969ce6931
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/24/2022
ms.locfileid: "140812365"
---
# <a name="save-data-with-the-tableadapter-dbdirect-methods"></a>用 TableAdapter DBDirect 方法保存数据

本教程提供有关使用 TableAdapter 的 DBDirect SQL数据库直接运行语句的详细说明。 TableAdapter 的 DBDirect 方法可对数据库更新进行精确的控制。 可以使用这些方法通过调用应用程序所需的单个 `Insert`、`Update` 和 `Delete` 方法来运行特定的 SQL 语句和存储的步骤（而不是在一次调用中执行全部 UPDATE、INSERT 和 DELETE 语句的重载的 `Update` 方法）。

在本教程中，你将了解如何：

- 使用[数据源配置向导](../data-tools/media/data-source-configuration-wizard.png)创建和配置数据集。

- 选择从“数据源”窗口拖动某些项时要在窗体上创建的控件。 有关详细信息，请参阅[设置从“数据源”窗口中拖动时要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

- 通过将某些项从“数据源”窗口拖到窗体上来创建数据绑定窗体。

- 添加直接访问数据库的方法以及执行插入、更新和删除的方法。

## <a name="prerequisites"></a>先决条件

本教程中的步骤用于.NET Framework Windows应用程序。

本教程使用 SQL Server Express LocalDB 和 Northwind 示例数据库。

1. 如果尚未安装 SQL Server Express LocalDB，可以从 [SQL Server Express 下载页](https://www.microsoft.com/sql-server/sql-server-editions-express)或通过 Visual Studio 安装程序安装。 在 Visual Studio 安装程序中，可以将 SQL Server Express LocalDB 作为数据存储和处理工作负载的一部分或作为单个组件进行安装 。

2. 按照以下步骤安装 Northwind 示例数据库：

    1. 在 Visual Studio 中，打开“SQL Server 对象资源管理器”窗口。 （在 Visual Studio 安装程序中 SQL Server 对象资源管理器作为数据存储和处理工作负载的一部分安装。）展开 SQL Server 节点 。 右键单击 LocalDB 实例并选择“新建查询”。

       此时将打开查询编辑器窗口。

    2. 将 [Northwind Transact-SQL 脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/main/docs/data-tools/samples/northwind.sql?raw=true)复制到剪贴板。 此 T-SQL 脚本从头开始创建 Northwind 数据库并用数据填充它。

    3. 将 T-SQL 脚本粘贴到查询编辑器中，然后选择“执行”按钮。

       不久后，查询完成运行并且 Northwind 数据库创建完成。

## <a name="create-a-windows-forms-application"></a>创建 Windows 窗体应用程序

第一步是创建“Windows 窗体应用程序”。 使用 C# **或 Windows窗体应用项目** 类型创建Visual Basic。

> [!NOTE]
> 本教程的代码在 C# 和 Visual Basic 中提供。 若要在 C# 和 Visual Basic 之间切换此页上的代码语言，请使用右侧页面顶部的代码语言切换器。

## <a name="create-a-data-source-from-your-database"></a>从数据库创建数据源

此步骤根据 Northwind 示例数据库中的 `Region` 表，使用“数据源配置”向导创建数据源。 你必须具有对 Northwind 示例数据库的访问权限，才能创建连接。 有关设置 Northwind 示例数据库的信息，请参阅[如何：安装示例数据库](../data-tools/installing-database-systems-tools-and-samples.md)。

### <a name="to-create-the-data-source"></a>创建数据源

1. 在“数据”菜单上，选择“显示数据源” 。

   “数据源”窗口随即打开。

2. 在“数据源”窗口，选择“添加新数据源”以启动“数据源配置”向导。

3. 在“选择数据源类型”屏幕中，选择“数据库”，然后选择“下一步”  。

4. 在“选择数据连接”屏幕中，执行以下操作之一：

    - 如果下拉列表中包含到 Northwind 示例数据库的数据连接，请选择该连接。

         -或-

    - 选择“新建连接”以启动“添加/修改连接”对话框。

5. 如果数据库需要密码，请选择该选项以包括敏感数据，再选择“下一步”。

6. 在“将连接字符串保存到应用程序配置文件”屏幕中，选择“下一步” 。

7. 在“选择数据库对象”屏幕中，展开“表”节点 。

8. 选择 `Region` 表，然后选择“完成”。

     将“NorthwindDataSet”添加到项目后，“数据源”窗口中即会显示 `Region` 表。

## <a name="add-controls-to-the-form-to-display-the-data"></a>将控件添加到要显示数据的窗体

通过将某些项从“数据源”窗口拖到窗体上来创建数据绑定控件。

若要在 Windows 窗体上创建数据绑定控件，请将主“区域”节点从“数据源”窗口拖动到窗体 。

用于导航记录的 <xref:System.Windows.Forms.DataGridView> 控件和工具栏（<xref:System.Windows.Forms.BindingNavigator>）将显示在窗体上。 此时组件栏中显示 [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)、`RegionTableAdapter`、<xref:System.Windows.Forms.BindingSource> 和 <xref:System.Windows.Forms.BindingNavigator>。

### <a name="to-add-buttons-that-will-call-the-individual-tableadapter-dbdirect-methods"></a>添加将调用单个 TableAdapter DbDirect 方法的按钮

1. 将三个 <xref:System.Windows.Forms.Button> 控件从“工具箱”拖到“Form1”上（在“RegionDataGridView”的下面）。

2. 在每个按钮上设置下列“名称”和“文本”属性。

    |名称|文本|
    |----------|----------|
    |`InsertButton`|插入|
    |`UpdateButton`|**更新**|
    |`DeleteButton`|**删除**|

### <a name="to-add-code-to-insert-new-records-into-the-database"></a>添加将新记录插入数据库所使用的代码

1. 选择“InsertButton”以创建 Click 事件的事件处理程序，并在代码编辑器中打开窗体。

2. 用下面的代码替换 `InsertButton_Click` 事件处理程序：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form1.vb" id="Snippet1":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form1.cs" id="Snippet1":::

     > [!NOTE]
     > 根据你Visual Studio `regionTableAdapter` `regionTableAdapter1`版本和所使用的项目模板，此代码中使用的变量名称可能在生成的代码中有尾随 1，也可能没有尾随 1。 在代码中进行任何更正，以确保在任何位置使用正确的名称。 Visual Studio显示一个红色长线，其中名称不正确。

### <a name="to-add-code-to-update-records-in-the-database"></a>添加更新数据库中的记录所使用的代码

1. 双击“UpdateButton”以创建 Click 事件的事件处理程序，并在代码编辑器中打开窗体。

2. 用下面的代码替换 `UpdateButton_Click` 事件处理程序：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form1.vb" id="Snippet2":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form1.cs" id="Snippet2":::

### <a name="to-add-code-to-delete-records-from-the-database"></a>添加删除数据库中的记录所使用的代码

1. 选择“DeleteButton”以创建 Click 事件的事件处理程序，并在代码编辑器中打开窗体。

2. 用下面的代码替换 `DeleteButton_Click` 事件处理程序：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form1.vb" id="Snippet3":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form1.cs" id="Snippet3":::

## <a name="run-the-application"></a>运行应用程序

- 选择 F5 运行该应用程序。

- 选择“插入”按钮，并验证新记录是否出现在网格中。

- 选择“更新”按钮，并验证是否在网格中更新该记录。

- 选择“删除”按钮，并验证是否从网格中移除该记录。

## <a name="next-steps"></a>后续步骤

根据应用程序的需求，创建数据绑定窗体后，还需要执行一些步骤。 你可以对本教程进行一些增强，包括：

- 将搜索功能添加到该窗体。

- 通过从“数据源”窗口中选择“使用向导配置数据集”，将其他表添加到数据集中。 可以通过将相关节点拖到窗体上来添加显示相关数据的控件。 有关详细信息，请参阅[数据集中的关系](relationships-in-datasets.md)。

## <a name="see-also"></a>另请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
