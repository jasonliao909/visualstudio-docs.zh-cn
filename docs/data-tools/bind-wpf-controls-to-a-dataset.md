---
title: 将 WPF 控件绑定到数据集
description: 在 Visual Studio 中创建一个 WPF 应用程序，该应用程序包含绑定到数据集中封装的产品记录的数据绑定控件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio], walkthroughs
- WPF Designer, data binding
ms.assetid: 177420b9-568b-4dad-9d16-1b0e98a24d71
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 7f1188df1a13d83964f455738250544149d7044e
ms.sourcegitcommit: 7a820b7698a8dcf076eb36e3d766fb0751f56bb1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2021
ms.locfileid: "131127424"
---
# <a name="bind-wpf-controls-to-a-dataset"></a>将 WPF 控件绑定到数据集

在本演练中，你将创建一个包含数据绑定控件的 WPF 应用程序。 这些控件将绑定到在数据集中封装的产品记录。 还可添加按钮以浏览产品并保存对产品记录所做的更改。

本演练演示以下任务：

- 创建一个 WPF 应用程序和一个利用 AdventureWorksLT 示例数据库中的数据生成的数据集。

- 通过将数据表从“数据源”窗口拖到 WPF 设计器的窗口中，创建一组数据绑定控件。

- 创建用于向前/向后导航产品记录的按钮。

- 创建一个用于将用户对产品记录所做的更改保存到数据表和基础数据源的按钮。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="prerequisites"></a>先决条件

您需要满足以下条件才能完成本演练：

- Visual Studio

- 访问 SQL Server 或 SQL Server Express 的运行实例，其中包含 AdventureWorks 灯 (AdventureWorksLT) 示例数据库附加到它。 若要下载数据库，请参阅 [AdventureWorks 示例数据库](/sql/samples/adventureworks-install-configure?tabs=ssms)。

事先了解以下概念也很有用，但对于完成本演练并不是必需的：

- 数据集和 TableAdapter。 有关详细信息，请参阅 Visual Studio 和[tableadapter](../data-tools/create-and-configure-tableadapters.md)[中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)。

- WPF 数据绑定。 有关详细信息，请参阅 [数据绑定概述](/dotnet/desktop-wpf/data/data-binding-overview)。

## <a name="create-the-project"></a>创建项目

创建新的 WPF 项目以显示产品记录。

::: moniker range="vs-2017"

1. 打开 Visual Studio。

2. 在“文件”  菜单上，选择“新建”  >“项目”  。

3. 展开“Visual Basic”或“Visual C#”，然后选择“Windows”。

4. 选择 " **WPF 应用程序** " 项目模板。

5. 在 " **名称** " 框中，输入 **AdventureWorksProductsEditor** ，然后选择 **"确定"**。

::: moniker-end

::: moniker range=">=vs-2019"

1. 打开 Visual Studio。

2. 在“开始”窗口上，选择“创建新项目”  。

3. 搜索 c # **WPF 应用程序** 项目模板，然后按照步骤创建项目，将项目命名为 **AdventureWorksProductsEditor**。

::: moniker-end

   Visual Studio 创建 AdventureWorksProductsEditor 项目。

## <a name="create-a-dataset-for-the-application"></a>为应用程序创建数据集

必须先为应用程序定义数据模型并将此模型添加到“数据源”窗口中，然后才能创建数据绑定控件。 在本演练中，你将创建要用作数据模型的数据集。

1. 在 **“数据”** 菜单上，单击 **“显示数据源”**。

   “数据源”窗口随即打开。

2. 在 **“数据源”** 窗口中，单击 **“添加新数据源”**。

   " **数据源配置** 向导" 将打开。

3. 在“选择数据源类型”页上，选择“数据库”，然后单击“下一步”。

4. 在“选择数据库模型”页上，选择“数据集”，然后单击“下一步”。

5. 在“选择你的数据连接”页面上，选择以下选项之一：

   - 如果下拉列表中包含到 AdventureWorksLT 示例数据库的数据连接，请选择该连接，然后单击“下一步”。

   - 单击“新建连接”，然后创建到 AdventureWorksLT 数据库的连接。

6. 在“将连接字符串保存到应用程序配置文件中”页面上，选中“是，将连接另存为”复选框，然后单击“下一步”。

7. 在“选择数据库对象”页面上，展开“表”，然后选择“Product (SalesLT)”表。

8. 单击“完成”  。

   Visual Studio 将新 `AdventureWorksLTDataSet.xsd` 文件添加到项目中，并将相应的 **adventureworksltdataset.xsd** 项添加到 "**数据源**" 窗口。 `AdventureWorksLTDataSet.xsd`文件定义名为的类型化数据集 `AdventureWorksLTDataSet` 和名为的 TableAdapter `ProductTableAdapter` 。 在本演练后面的部分中，你将使用 `ProductTableAdapter` 向数据集填充数据，并将更改保存回数据库中。

9. 生成项目。

## <a name="edit-the-default-fill-method-of-the-tableadapter"></a>编辑 TableAdapter 的默认填充方法

若要向数据集填充数据，请使用 `Fill` 的 `ProductTableAdapter` 方法。 默认情况下，`Fill` 方法将向 `ProductDataTable` 中的 `AdventureWorksLTDataSet` 填充 Product 表包含的所有数据行。 你可以修改此方法以仅返回行的子集。 对于本演练而言，将修改 `Fill` 方法以仅返回具有照片的产品行。

1. 在“解决方案资源管理器”中，双击“AdventureWorksLTDataSet.xsd”文件。

     这将打开数据集设计器。

2. 在此设计器中，右键单击“填充”、GetData() 查询，然后选择“配置”。

     “TableAdapter 配置”向导随即打开。

3. 在“输入 SQL 语句”页面上，在文本框中的 `SELECT` 语句后添加以下 WHERE 子句。

    ```sql
    WHERE ThumbnailPhotoFileName <> 'no_image_available_small.gif'
    ```

4. 单击“完成”  。

## <a name="define-the-user-interface"></a>定义用户界面

通过在 WPF 设计器中修改 XAML，将多个按钮添加到该窗口中。 在本演练后面的部分中，你将添加可让用户通过使用这些按钮来滚动和保存对产品记录所做的更改的代码。

1. 在 **解决方案资源管理器** 中，双击 " *mainwindow.xaml*"。

    窗口将在 **WPF 设计器** 中打开。

2. 在设计器的 [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] 视图中，在 `<Grid>` 标记之间添加以下代码：

   ```xaml
   <Grid.RowDefinitions>
       <RowDefinition Height="75" />
       <RowDefinition Height="625" />
   </Grid.RowDefinitions>
   <Button HorizontalAlignment="Left" Margin="22,20,0,24" Name="backButton" Width="75">&lt;</Button>
   <Button HorizontalAlignment="Left" Margin="116,20,0,24" Name="nextButton" Width="75">&gt;</Button>
   <Button HorizontalAlignment="Right" Margin="0,21,46,24" Name="saveButton" Width="110">Save changes</Button>
   ```

3. 生成项目。

## <a name="create-data-bound-controls"></a>创建数据绑定控件

通过 `Product` 将表从 " **数据源** " 窗口拖到 WPF 设计器，创建显示客户记录的控件。

1. 在“数据源”窗口中，单击“Product”节点的下拉菜单，然后选择“详细信息”。

2. 展开“Product”节点。

3. 在本示例中，某些字段不会显示，因此只需单击下列节点旁边的下拉菜单，然后选择“无”：

    - ProductCategoryID

    - ProductModelID

    - ThumbnailPhotoFileName

    - rowguid

    - ModifiedDate

4. 单击“ThumbNailPhoto”节点旁边的下拉菜单，然后选择“图像”。

    > [!NOTE]
    > 默认情况下，已将“数据源”窗口中表示图片的项的默认控件设置为“无”。 这是因为，图片是作为字节数组存储在数据库中的，并且从简单的字节数组到大型应用程序的可执行文件都可以包含在字节数组中。

5. 从“数据源”窗口，将“Product”节点拖到包含按钮的行下方的网格行。

     Visual Studio 生成 XAML，它定义了一组绑定到“Products”表中的数据的控件。 它还会生成用于加载数据的代码。 有关生成的 XAML 和代码的详细信息，请参阅[在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)。

6. 在设计器中，单击“Product ID”标签旁边的文本框。

7. 在“属性”窗口，选中“IsReadOnly”属性旁边的复选框。

## <a name="navigate-product-records"></a>导航产品记录

添加使用户能够通过使用按钮滚动产品记录的代码 **\<** and **>** 。

1. 在设计器中，双击 **<** 窗口图面上的按钮。

     Visual Studio 打开代码隐藏文件，并为 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件创建新的 `backButton_Click` 事件处理程序。

2. 修改 `Window_Loaded` 事件处理程序，使 `ProductViewSource`、`AdventureWorksLTDataSet` 和 `AdventureWorksLTDataSetProductTableAdapter` 位于该方法的外部，并使它们在整个窗体中可访问。 仅将这些项声明为全局窗体，然后在事件处理程序中将其分配如下 `Window_Loaded` ：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_ProTools/data_wpfdataset/cs/mainwindow.xaml.cs" id="Snippet1":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_ProTools/data_wpfdataset/vb/mainwindow.xaml.vb" id="Snippet1":::

3. 将以下代码添加到 `backButton_Click` 事件处理程序中：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_ProTools/data_wpfdataset/cs/mainwindow.xaml.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_ProTools/data_wpfdataset/vb/mainwindow.xaml.vb" id="Snippet2":::

4. 返回到设计器，然后双击 **>** 按钮。

5. 将以下代码添加到 `nextButton_Click` 事件处理程序中：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_ProTools/data_wpfdataset/cs/mainwindow.xaml.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_ProTools/data_wpfdataset/vb/mainwindow.xaml.vb" id="Snippet3":::

## <a name="save-changes-to-product-records"></a>保存对产品记录所做的更改

添加代码，该代码可让用户通过使用“保存更改”按钮来保存对产品记录所做的更改。

1. 在设计器中，双击“保存更改”按钮。

     Visual Studio 打开代码隐藏文件，并为 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件创建新的 `saveButton_Click` 事件处理程序。

2. 将以下代码添加到 `saveButton_Click` 事件处理程序中：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_ProTools/data_wpfdataset/cs/mainwindow.xaml.cs" id="Snippet4":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_ProTools/data_wpfdataset/vb/mainwindow.xaml.vb" id="Snippet4":::

    > [!NOTE]
    > 此示例使用 `Save` 的 `TableAdapter` 方法来保存更改。 这对于本演练很合适，因为本演练中只会更改一个数据表。 如果你需要保存对多个数据表所做的更改，则还可以使用 Visual Studio 利用你的数据集生成的 `UpdateAll` 的 `TableAdapterManager` 方法。 有关详细信息，请参阅 [TableAdapters](../data-tools/create-and-configure-tableadapters.md)。

## <a name="test-the-application"></a>测试应用程序

生成并运行应用程序。 验证你是否可以查看和更新产品记录。

1. 按 **F5**。

     这将生成并运行应用程序。 检查下列各项：

    - 文本框显示具有图片的第一条产品记录的数据。 此产品的产品 ID 为 713，名称为“Long-Sleeve Logo Jersey, S”。

    - 可以单击 **>** 或 **<** 按钮来浏览其他产品记录。

2. 在某一产品记录中，更改“大小”值，然后依次“保存更改”。

3. 关闭该应用程序，然后在 Visual Studio 中按 F5 重启该应用程序。

4. 导航到已更改的产品记录，然后验证是否已保存更改。

5. 关闭该应用程序。

## <a name="next-steps"></a>后续步骤

完成本演练后，可以尝试以下相关任务：

- 了解如何使用 Visual Studio 中的“数据源”窗口将 WPF 控件绑定到其他类型的数据源上。 有关详细信息，请参阅将 [WPF 控件绑定到 WCF 数据服务](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)。

- 了解如何使用 Visual Studio 中的“数据源”窗口在 WPF 控件中显示相关数据（即父-子关系中的数据）。 有关详细信息，请参阅 [演练：在 WPF 应用中显示相关的数据](../data-tools/display-related-data-in-wpf-applications.md)。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)
- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
- [数据绑定概述](/dotnet/desktop-wpf/data/data-binding-overview)
