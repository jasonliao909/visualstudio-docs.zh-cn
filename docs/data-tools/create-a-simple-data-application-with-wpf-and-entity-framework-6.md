---
title: 通过 WPF 和实体框架 6 实现的简单数据应用
description: 在此演练中，你将了解如何通过 Windows Presentation Foundation (WPF) 和实体框架 6 在 Visual Studio 中创建简单的基于数据的窗体应用。
ms.custom: SEO-VS-2020
ms.date: 08/22/2017
ms.topic: conceptual
dev_langs:
- CSharp
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 57ad43fbe06a93108afc254efeca1dc2615df5c3
ms.sourcegitcommit: 7a300823cf1bd3355be03bde561cf2777bc09eae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2021
ms.locfileid: "133978207"
---
# <a name="create-a-simple-data-application-with-wpf-and-entity-framework-6"></a>使用 WPF 和 Entity Framework 6 创建简单的数据应用程序

本演练演示如何在 Visual Studio 中创建基本的“基于数据的窗体”应用程序。 该应用使用 SQL Server LocalDB、Northwind 数据库、实体框架 6 (Entity Framework Core) 和适用于 .NET Framework（而非 .NET Core）的 Windows Presentation Foundation。 它演示如何使用大纲-细节视图执行基本数据绑定，它还具有一个自定义绑定导航器，其中包括“移动到下一个”、“移动到上一个”、“移动到开头”、“移动到末尾”、“更新”和“删除”按钮。     

本文重点介绍如何使用 Visual Studio 中的数据工具，不会尝试以任何深度阐释基础技术。 它假定你基本熟悉 XAML、实体框架和 SQL。 此示例也不演示模型-视图-视图模型 (MVVM) 体系结构，这是 WPF 应用程序的标准体系结构。 但是，你可以将此代码复制到自己的 MVVM 应用程序中，几乎不用进行修改。

## <a name="install-and-connect-to-northwind"></a>安装并连接到 Northwind

本示例使用 SQL Server Express LocalDB 和 Northwind 示例数据库。 如果该产品的 ADO.NET 数据提供程序支持实体框架，则它应该一样能与其他 SQL 数据库产品配合使用。

1. 如果尚未安装 SQL Server Express LocalDB，可以从 [SQL Server Express 下载页](https://www.microsoft.com/sql-server/sql-server-editions-express)或通过 Visual Studio 安装程序安装。 在 Visual Studio 安装程序中，可将 SQL Server Express LocalDB 作为 .NET 桌面开发工作负载的一部分安装，也可作为单独组件安装。

2. 按照以下步骤安装 Northwind 示例数据库：

    1. 在 Visual Studio 中，打开“SQL Server 对象资源管理器”窗口。 （SQL Server 对象资源管理器作为数据存储和处理工作负载的一部分安装在 Visual Studio 安装程序中。）展开“SQL Server”节点。    右键单击 LocalDB 实例并选择“新建查询”。

       此时将打开查询编辑器窗口。

    2. 将 [Northwind Transact-SQL 脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/main/docs/data-tools/samples/northwind.sql?raw=true)复制到剪贴板。 此 T-SQL 脚本从头开始创建 Northwind 数据库并用数据填充它。

    3. 将 T-SQL 脚本粘贴到查询编辑器中，然后选择“执行”按钮。

       不久后，查询完成运行并且 Northwind 数据库创建完成。

3. 为 Northwind [添加新连接](../data-tools/add-new-connections.md)。

## <a name="configure-the-project"></a>配置项目

1. 在 Visual Studio 中，创建一个新的 C# WPF 应用项目。

2. 为实体框架 6 添加 NuGet 包。 在解决方案资源管理器中，选择项目节点。 在主菜单中，选择“项目” > “管理 NuGet 包”。

     ![“管理 NuGet 包”菜单项](../data-tools/media/raddata_vs2015_manage_nuget_packages.png)

3. 在 NuGet 包管理器中，单击“浏览”链接。  实体框架可能是列表中最上面的包。 在右窗格中单击“安装”，并按照提示操作。 安装完成时，“输出”窗口将会显示此结果。

     ![实体框架 NuGet 包](../data-tools/media/raddata_vs2015_nuget_ef.png)

4. 现在，可以使用 Visual Studio 创建基于 Northwind 数据库的模型。

## <a name="create-the-model"></a>创建模型

1. 在解决方案资源管理器中右键单击项目节点，然后选择“添加” > “新增项”  。 在左窗格中的“C#”节点下，选择“数据”，然后在中间窗格中选择“ADO.NET 实体数据模型”。 

   ![实体框架模型新项](../data-tools/media/raddata-ef-new-project-item.png)

2. 调用模型 `Northwind_model` 并选择“确定”。 “实体数据模型”向导随即打开。 选择“从数据库打开 EF Designer”，然后单击“下一步”。 

   ![从数据库构建 EF 模型](../data-tools/media/raddata-ef-model-from-database.png)

3. 在下一个屏幕中，输入或选择 LocalDB Northwind 连接（例如 (localdb)\MSSQLLocalDB），指定 Northwind 数据库，然后单击“下一步”。

4. 在向导的下一页中，选择要包括在实体框架模型中的表、存储过程和其他数据库对象。 在树视图中展开 dbo 节点，然后选择“客户”、“订单”和“订单详细信息”。   保留选中默认值，并单击“完成”。

    ![为模型选择数据库对象](../data-tools/media/raddata-choose-ef-objects.png)

5. 向导会生成表示实体框架模型的 C# 类。 这些类是普通旧 C# 类，我们将其数据绑定到 WPF 用户界面。 .edmx 文件描述将类与数据库中的对象关联的关系和其他元数据。 .tt 文件是 T4 模板，它们会生成代码，该代码会对模型进行操作，并将更改保存到数据库。 可以在解决方案资源管理器中的 Northwind_model 节点下看到所有这些文件：

      ![解决方案资源管理器 EF 模型文件](../data-tools/media/raddata-solution-explorer-ef-model-files.png)

    通过 .edmx 文件的设计器图面，可以修改模型中的某些属性和关系。 本演练中不会使用设计器。

6. .tt 文件是常规用途的，需要调整其中一个文件以处理 WPF 数据绑定，这需要 ObservableCollections。 在解决方案资源管理器中，展开 Northwind_model 节点，直到找到 Northwind_model.tt。 （请确保不在 Context.tt 文件中，该文件位于 .edmx 文件正下方。） 

   - 将 <xref:System.Collections.ICollection> 的两个匹配项替换为 <xref:System.Collections.ObjectModel.ObservableCollection%601>。

   - 在第 51 行左右，将 <xref:System.Collections.Generic.HashSet%601> 的第一个匹配项替换为 <xref:System.Collections.ObjectModel.ObservableCollection%601>。 请勿替换 HashSet 的第二个匹配项。

   - 将 <xref:System.Collections.Generic> 的唯一匹配项（在第 431 行左右）替换为 <xref:System.Collections.ObjectModel>。

7. 按 Ctrl+Shift+B 生成项目。 生成完成后，模型类对数据源向导可见。

现在，你已准备好将此模型挂接到 XAML 页面，以便查看、导航和修改数据。

## <a name="databind-the-model-to-the-xaml-page"></a>将模型数据绑定到 XAML 页面

可以编写自己的数据绑定代码，但让 Visual Studio 帮你编写会更容易。

1. 在主菜单中，选择“项目” >  “添加新数据源”以打开“数据源配置向导”。 选择“对象”，因为你要绑定到模型类，而不是数据库：

     ![具有对象源的数据源配置向导](../data-tools/media/raddata-data-source-configuration-wizard-with-object-source.png)

2. 展开项目的节点，然后选择“客户”。 （从“客户”中的“顶到”导航属性自动生成订单的源。）

     ![将实体类添加为数据源](../data-tools/media/raddata-add-entity-classes-as-data-sources.png)

3. 单击“完成”  。

4. 在代码视图中导航到 MainWindow.xaml。 出于本示例的目的，我们将使 XAML 保持简单。 将 MainWindow 的标题更改为更具描述性的名称，并暂时将其高度和宽度增大到 600 x 800。 稍后随时可以更改它。 现在，将这三个行定义添加到主网格，一行用于导航按钮，一行用于客户详细信息，另一行用于显示客户订单的网格：

    ```xaml
        <Grid.RowDefinitions>
            <RowDefinition Height="auto"/>
            <RowDefinition Height="auto"/>
            <RowDefinition Height="*"/>
        </Grid.RowDefinitions>
    ```

5. 现在打开 MainWindow.xaml，以便在设计器中查看它。 这将导致“数据源”窗口显示为“工具箱”旁边的 Visual Studio 窗口边缘中的选项。  单击选项卡以打开该窗口，或按 Shift+Alt+D 或选择“查看” > “其他窗口” > “数据源”。 我们将在单独的文本框中显示 Customers 类中的每个属性。 首先，单击“客户”组合框中的箭头，然后选择“详细信息”。  然后，将节点拖动到设计图面的中间部分，让设计器知道你想要它进入中间行。 如果错放位置，稍后可以在 XAML 中手动指定行。 默认情况下，控件垂直放置在网格元素中，但现在，你可以按自己喜欢的形式排列它们。 例如，将“名称”文本框置于地址上方可能是有道理的。 本文的示例应用程序对字段重新排序，然后将它们重新排列为两列。

     ![到各个控件的客户数据源绑定](../data-tools/media/raddata-customers-data-source-binding-to-individual-controls.png)

     在代码视图中，现在可以在父网格的第 1 行（中间行）看到新的 `Grid` 元素。 父网格具有 `DataContext` 属性，该属性引用已添加到 `Windows.Resources` 元素的 CollectionViewSource。 给定该数据上下文，当第一个文本框绑定到“地址”时，该名称将映射到 CollectionViewSource 中当前 `Customer` 对象中的 `Address` 属性。

    ```xaml
    <Grid DataContext="{StaticResource customerViewSource}">
    ```

6. 当客户显示在窗口的上半部分时，最好可以在下半部分查看其订单。 在单个网格视图控件中显示订单。 要使大纲-细节数据绑定按预期工作，一定要绑定到 Customers 类中的 Orders 属性，而不是绑定到单独的 Orders 节点。 将 Customers 类的 Orders 属性拖到窗体的下半部分，以便设计器将其置于第 2 行：

     ![将 Orders 类作为网格拖动](../data-tools/media/raddata-drag-orders-classes-as-grid.png)

7. Visual Studio 生成了将 UI 控件连接到模型中的事件的所有绑定代码。 若要查看某些数据，你只需编写一些代码来填充模型即可。 首先，导航到 MainWindow.xaml，并将数据成员添加到该数据上下文的 MainWindow.xaml 类。 已生成的这一对象的行为有些类似于跟踪模型中的更改和事件的控件。 你还将为客户和订单以及关联的构造函数初始化逻辑添加 CollectionViewSource 数据成员。 类的顶部应如下所示：

     :::code language="csharp" source="../data-tools/codesnippet/CSharp/CreateWPFDataApp/MainWindow.xaml.cs" id="Snippet1":::

     为 System.Data.Entity 添加 `using` 指令，以将 Load 扩展方法添加到作用域：

     ```csharp
     using System.Data.Entity;
     ```

     现在，向下滚动并找到 `Window_Loaded` 事件处理程序。 请注意，Visual Studio 已添加 CollectionViewSource 对象。 这表示你在创建模型时选择的 NorthwindEntities 对象。 你已经添加了它，因此在这里不需要重复操作。 让我们替换 `Window_Loaded` 中的代码，使得方法现在如下所示：

     :::code language="csharp" source="../data-tools/codesnippet/CSharp/CreateWPFDataApp/MainWindow.xaml.cs" id="Snippet2":::


8. 按 **F5**。 应会看到检索到 CollectionViewSource 中的第一个客户的详细信息。 还应在数据网格中看到其订单。 格式设置不是很好，让我们来解决这个问题。 你还可以创造一种方法来查看其他记录并执行基本的 CRUD 操作。

## <a name="adjust-the-page-design-and-add-grids-for-new-customers-and-orders"></a>调整页面设计并为新客户和订单添加网格

Visual Studio 生成的默认布局对于你的应用程序而言不够理想，因此我们将在这里提供要复制到你的代码中的最终 XAML。 还需要一些“表单”（实际上是网格），让用户能够添加新客户或订单。 为了能够添加新的客户和订单，你需要另外一组没有数据绑定到 `CollectionViewSource` 的文本框。 通过在处理程序方法中设置 Visible 属性，可以控制用户在任意给定时间看到哪些网格。 最后，你要在“订单”网格中的每一行添加一个“删除”按钮，以使用户能够删除单个订单。

首先，将这些样式添加到 MainWindow.xaml 中的 `Windows.Resources` 元素：

```xaml
<Style x:Key="Label" TargetType="{x:Type Label}" BasedOn="{x:Null}">
    <Setter Property="HorizontalAlignment" Value="Left"/>
    <Setter Property="VerticalAlignment" Value="Center"/>
    <Setter Property="Margin" Value="3"/>
    <Setter Property="Height" Value="23"/>
</Style>
<Style x:Key="CustTextBox" TargetType="{x:Type TextBox}" BasedOn="{x:Null}">
    <Setter Property="HorizontalAlignment" Value="Right"/>
    <Setter Property="VerticalAlignment" Value="Center"/>
    <Setter Property="Margin" Value="3"/>
    <Setter Property="Height" Value="26"/>
    <Setter Property="Width" Value="120"/>
</Style>
```

接下来，将整个外部网格替换为以下标记：

```xaml
<Grid>
     <Grid.RowDefinitions>
         <RowDefinition Height="auto"/>
         <RowDefinition Height="auto"/>
         <RowDefinition Height="*"/>
     </Grid.RowDefinitions>
     <Grid x:Name="existingCustomerGrid" Grid.Row="1" HorizontalAlignment="Left" Margin="5" Visibility="Visible" VerticalAlignment="Top" Background="AntiqueWhite" DataContext="{StaticResource customerViewSource}">
         <Grid.ColumnDefinitions>
             <ColumnDefinition Width="Auto" MinWidth="233"/>
             <ColumnDefinition Width="Auto" MinWidth="397"/>
         </Grid.ColumnDefinitions>
         <Grid.RowDefinitions>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
         </Grid.RowDefinitions>
         <Label Content="Customer ID:" Grid.Row="0" Style="{StaticResource Label}"/>
         <TextBox x:Name="customerIDTextBox" Grid.Row="0" Style="{StaticResource CustTextBox}"
                  Text="{Binding CustomerID, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Company Name:" Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="companyNameTextBox" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding CompanyName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Contact Name:" Grid.Row="2" Style="{StaticResource Label}"/>
         <TextBox x:Name="contactNameTextBox" Grid.Row="2" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Contact title:" Grid.Row="3" Style="{StaticResource Label}"/>
         <TextBox x:Name="contactTitleTextBox" Grid.Row="3" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactTitle, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Address:" Grid.Row="4" Style="{StaticResource Label}"/>
         <TextBox x:Name="addressTextBox" Grid.Row="4" Style="{StaticResource CustTextBox}"
                  Text="{Binding Address, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="City:" Grid.Column="1" Grid.Row="0" Style="{StaticResource Label}"/>
         <TextBox x:Name="cityTextBox" Grid.Column="1" Grid.Row="0" Style="{StaticResource CustTextBox}"
                  Text="{Binding City, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Country:" Grid.Column="1" Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="countryTextBox" Grid.Column="1" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding Country, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Fax:" Grid.Column="1" Grid.Row="2" Style="{StaticResource Label}"/>
         <TextBox x:Name="faxTextBox" Grid.Column="1" Grid.Row="2" Style="{StaticResource CustTextBox}"
                  Text="{Binding Fax, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Phone:" Grid.Column="1" Grid.Row="3" Style="{StaticResource Label}"/>
         <TextBox x:Name="phoneTextBox" Grid.Column="1" Grid.Row="3" Style="{StaticResource CustTextBox}"
                  Text="{Binding Phone, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Postal Code:" Grid.Column="1" Grid.Row="4" VerticalAlignment="Center" Style="{StaticResource Label}"/>
         <TextBox x:Name="postalCodeTextBox" Grid.Column="1" Grid.Row="4" Style="{StaticResource CustTextBox}"
                  Text="{Binding PostalCode, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Region:" Grid.Column="1" Grid.Row="5" Style="{StaticResource Label}"/>
         <TextBox x:Name="regionTextBox" Grid.Column="1" Grid.Row="5" Style="{StaticResource CustTextBox}"
                  Text="{Binding Region, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
     </Grid>
     <Grid x:Name="newCustomerGrid" Grid.Row="1" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="5" DataContext="{Binding RelativeSource={RelativeSource FindAncestor, AncestorType={x:Type Window}}, Path=newCustomer, UpdateSourceTrigger=Explicit}" Visibility="Collapsed" Background="CornflowerBlue">
         <Grid.ColumnDefinitions>
             <ColumnDefinition Width="Auto" MinWidth="233"/>
             <ColumnDefinition Width="Auto" MinWidth="397"/>
         </Grid.ColumnDefinitions>
         <Grid.RowDefinitions>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
         </Grid.RowDefinitions>
         <Label Content="Customer ID:" Grid.Row="0" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_customerIDTextBox" Grid.Row="0" Style="{StaticResource CustTextBox}"
                  Text="{Binding CustomerID, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Company Name:" Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_companyNameTextBox" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding CompanyName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true }"/>
         <Label Content="Contact Name:" Grid.Row="2" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_contactNameTextBox" Grid.Row="2" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Contact title:" Grid.Row="3" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_contactTitleTextBox" Grid.Row="3" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactTitle, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Address:" Grid.Row="4" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_addressTextBox" Grid.Row="4" Style="{StaticResource CustTextBox}"
                  Text="{Binding Address, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="City:" Grid.Column="1" Grid.Row="0" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_cityTextBox" Grid.Column="1" Grid.Row="0" Style="{StaticResource CustTextBox}"
                  Text="{Binding City, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Country:" Grid.Column="1" Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_countryTextBox" Grid.Column="1" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding Country, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Fax:" Grid.Column="1" Grid.Row="2" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_faxTextBox" Grid.Column="1" Grid.Row="2" Style="{StaticResource CustTextBox}"
                  Text="{Binding Fax, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Phone:" Grid.Column="1" Grid.Row="3" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_phoneTextBox" Grid.Column="1" Grid.Row="3" Style="{StaticResource CustTextBox}"
                  Text="{Binding Phone, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Postal Code:" Grid.Column="1" Grid.Row="4" VerticalAlignment="Center" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_postalCodeTextBox" Grid.Column="1" Grid.Row="4" Style="{StaticResource CustTextBox}"
                  Text="{Binding PostalCode, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Region:" Grid.Column="1" Grid.Row="5" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_regionTextBox" Grid.Column="1" Grid.Row="5" Style="{StaticResource CustTextBox}"
                  Text="{Binding Region, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
     </Grid>
     <Grid x:Name="newOrderGrid" Grid.Row="1" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="5" DataContext="{Binding Path=newOrder, Mode=TwoWay}" Visibility="Collapsed" Background="LightGreen">
         <Grid.ColumnDefinitions>
             <ColumnDefinition Width="Auto" MinWidth="233"/>
             <ColumnDefinition Width="Auto" MinWidth="397"/>
         </Grid.ColumnDefinitions>
         <Grid.RowDefinitions>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
         </Grid.RowDefinitions>
         <Label Content="New Order Form" FontWeight="Bold"/>
         <Label Content="Employee ID:"  Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_employeeIDTextBox" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding EmployeeID, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Order Date:"  Grid.Row="2" Style="{StaticResource Label}"/>
         <DatePicker x:Name="add_orderDatePicker" Grid.Row="2"  HorizontalAlignment="Right" Width="120"
                 SelectedDate="{Binding OrderDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
         <Label Content="Required Date:" Grid.Row="3" Style="{StaticResource Label}"/>
         <DatePicker x:Name="add_requiredDatePicker" Grid.Row="3" HorizontalAlignment="Right" Width="120"
                  SelectedDate="{Binding RequiredDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
         <Label Content="Shipped Date:"  Grid.Row="4"  Style="{StaticResource Label}"/>
         <DatePicker x:Name="add_shippedDatePicker"  Grid.Row="4"  HorizontalAlignment="Right" Width="120"
                 SelectedDate="{Binding ShippedDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
         <Label Content="Ship Via:"  Grid.Row="5" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_ShipViaTextBox"  Grid.Row="5" Style="{StaticResource CustTextBox}"
                  Text="{Binding ShipVia, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Freight"  Grid.Row="6" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_freightTextBox" Grid.Row="6" Style="{StaticResource CustTextBox}"
                  Text="{Binding Freight, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
     </Grid>
     <DataGrid x:Name="ordersDataGrid" SelectionUnit="Cell" SelectionMode="Single" AutoGenerateColumns="False" CanUserAddRows="false" IsEnabled="True" EnableRowVirtualization="True" Width="auto" ItemsSource="{Binding Source={StaticResource customerOrdersViewSource}}" Margin="10,10,10,10" Grid.Row="2" RowDetailsVisibilityMode="VisibleWhenSelected">
         <DataGrid.Columns>
             <DataGridTemplateColumn>
                 <DataGridTemplateColumn.CellTemplate>
                     <DataTemplate>
                         <Button Content="Delete" Command="{StaticResource DeleteOrderCommand}" CommandParameter="{Binding}"/>
                     </DataTemplate>
                 </DataGridTemplateColumn.CellTemplate>
             </DataGridTemplateColumn>
             <DataGridTextColumn x:Name="customerIDColumn" Binding="{Binding CustomerID}" Header="Customer ID" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="employeeIDColumn" Binding="{Binding EmployeeID}" Header="Employee ID" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="freightColumn" Binding="{Binding Freight}" Header="Freight" Width="SizeToHeader"/>
             <DataGridTemplateColumn x:Name="orderDateColumn" Header="Order Date" Width="SizeToHeader">
                 <DataGridTemplateColumn.CellTemplate>
                     <DataTemplate>
                         <DatePicker SelectedDate="{Binding OrderDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
                     </DataTemplate>
                 </DataGridTemplateColumn.CellTemplate>
             </DataGridTemplateColumn>
             <DataGridTextColumn x:Name="orderIDColumn" Binding="{Binding OrderID}" Header="Order ID" Width="SizeToHeader"/>
             <DataGridTemplateColumn x:Name="requiredDateColumn" Header="Required Date" Width="SizeToHeader">
                 <DataGridTemplateColumn.CellTemplate>
                     <DataTemplate>
                         <DatePicker SelectedDate="{Binding RequiredDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
                     </DataTemplate>
                 </DataGridTemplateColumn.CellTemplate>
             </DataGridTemplateColumn>
             <DataGridTextColumn x:Name="shipAddressColumn" Binding="{Binding ShipAddress}" Header="Ship Address" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="shipCityColumn" Binding="{Binding ShipCity}" Header="Ship City" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="shipCountryColumn" Binding="{Binding ShipCountry}" Header="Ship Country" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="shipNameColumn" Binding="{Binding ShipName}" Header="Ship Name" Width="SizeToHeader"/>
             <DataGridTemplateColumn x:Name="shippedDateColumn" Header="Shipped Date" Width="SizeToHeader">
                 <DataGridTemplateColumn.CellTemplate>
                     <DataTemplate>
                         <DatePicker SelectedDate="{Binding ShippedDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
                     </DataTemplate>
                 </DataGridTemplateColumn.CellTemplate>
             </DataGridTemplateColumn>
             <DataGridTextColumn x:Name="shipPostalCodeColumn" Binding="{Binding ShipPostalCode}" Header="Ship Postal Code" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="shipRegionColumn" Binding="{Binding ShipRegion}" Header="Ship Region" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="shipViaColumn" Binding="{Binding ShipVia}" Header="Ship Via" Width="SizeToHeader"/>
         </DataGrid.Columns>
     </DataGrid>
 </Grid>
```

## <a name="add-buttons-to-navigate-add-update-and-delete"></a>添加用于导航、添加、更新和删除的按钮

在 Windows 窗体应用程序中，你将获得一个 BindingNavigator 对象，其中包含用于在数据库中的行间导航并执行基本 CRUD 操作的按钮。 WPF 并不提供 BindingNavigator，但要创建它是很容易的。 实现此操作的方法是，将按钮置于水平 StackPanel 中，并将这些按钮与绑定到代代码隐藏中的方法的命令相关联。

命令逻辑分为以下四部分：(1) 命令，(2) 绑定，(3) 按钮，(4) 代码隐藏中的命令处理程序。

### <a name="add-commands-bindings-and-buttons-in-xaml"></a>用 XAML 添加命令、绑定和按钮

1. 首先，将 MainWindow.xaml 文件中的命令添加到 `Windows.Resources` 元素中：

    ```xaml
    <RoutedUICommand x:Key="FirstCommand" Text="First"/>
    <RoutedUICommand x:Key="LastCommand" Text="Last"/>
    <RoutedUICommand x:Key="NextCommand" Text="Next"/>
    <RoutedUICommand x:Key="PreviousCommand" Text="Previous"/>
    <RoutedUICommand x:Key="DeleteCustomerCommand" Text="Delete Customer"/>
    <RoutedUICommand x:Key="DeleteOrderCommand" Text="Delete Order"/>
    <RoutedUICommand x:Key="UpdateCommand" Text="Update"/>
    <RoutedUICommand x:Key="AddCommand" Text="Add"/>
    <RoutedUICommand x:Key="CancelCommand" Text="Cancel"/>
    ```

2. CommandBinding 将 `RoutedUICommand` 事件映射到代码隐藏中的方法。 将此 `CommandBindings` 元素添加到 `Windows.Resources` 结束标记后：

    ```xaml
    <Window.CommandBindings>
        <CommandBinding Command="{StaticResource FirstCommand}" Executed="FirstCommandHandler"/>
        <CommandBinding Command="{StaticResource LastCommand}" Executed="LastCommandHandler"/>
        <CommandBinding Command="{StaticResource NextCommand}" Executed="NextCommandHandler"/>
        <CommandBinding Command="{StaticResource PreviousCommand}" Executed="PreviousCommandHandler"/>
        <CommandBinding Command="{StaticResource DeleteCustomerCommand}" Executed="DeleteCustomerCommandHandler"/>
        <CommandBinding Command="{StaticResource DeleteOrderCommand}" Executed="DeleteOrderCommandHandler"/>
        <CommandBinding Command="{StaticResource UpdateCommand}" Executed="UpdateCommandHandler"/>
        <CommandBinding Command="{StaticResource AddCommand}" Executed="AddCommandHandler"/>
        <CommandBinding Command="{StaticResource CancelCommand}" Executed="CancelCommandHandler"/>
    </Window.CommandBindings>
    ```

3. 现在，添加包含导航、添加、删除和更新按钮的 `StackPanel`。 首先，将此样式添加到 `Windows.Resources`：

    ```xaml
    <Style x:Key="NavButton" TargetType="{x:Type Button}" BasedOn="{x:Null}">
        <Setter Property="FontSize" Value="24"/>
        <Setter Property="FontFamily" Value="Segoe UI Symbol"/>
        <Setter Property="Margin" Value="2,2,2,0"/>
        <Setter Property="Width" Value="40"/>
        <Setter Property="Height" Value="auto"/>
    </Style>
    ```

     然后，将此代码粘贴到外部 `Grid` 元素的 `RowDefinitions` 之后，它靠近 XAML 页面顶部：

    ```xaml
    <StackPanel Orientation="Horizontal" Margin="2,2,2,0" Height="36" VerticalAlignment="Top" Background="Gainsboro" DataContext="{StaticResource customerViewSource}" d:LayoutOverrides="LeftMargin, RightMargin, TopMargin, BottomMargin">
        <Button Name="btnFirst" Content="|◄" Command="{StaticResource FirstCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnPrev" Content="◄" Command="{StaticResource PreviousCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnNext" Content="►" Command="{StaticResource NextCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnLast" Content="►|" Command="{StaticResource LastCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnDelete" Content="Delete Customer" Command="{StaticResource DeleteCustomerCommand}" FontSize="11" Width="120" Style="{StaticResource NavButton}"/>
        <Button Name="btnAdd" Content="New Customer" Command="{StaticResource AddCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>
        <Button Content="New Order" Name="btnNewOrder" FontSize="11" Width="80" Style="{StaticResource NavButton}" Click="NewOrder_click"/>
        <Button Name="btnUpdate" Content="Commit" Command="{StaticResource UpdateCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>
        <Button Content="Cancel" Name="btnCancel" Command="{StaticResource CancelCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>
    </StackPanel>
    ```

### <a name="add-command-handlers-to-the-mainwindow-class"></a>向 MainWindow.xaml 类添加命令处理程序

除 add 和 delete 方法外，代码隐藏是极少的。 通过对 CollectionViewSource 的 View 属性调用方法来执行导航。 `DeleteOrderCommandHandler` 演示如何对订单执行级联删除。 必须先删除与之关联的 Order_Details。 `UpdateCommandHandler` 向集合中添加新的客户或订单，或者只是使用用户在文本框中进行的更改来更新现有客户或订单。

将这些处理程序方法添加到 MainWindow.xaml.cs 中的 MainWindow 类。 如果 Customers 表的 CollectionViewSource 具有不同的名称，则需要调整以下每个方法中的名称：

:::code language="csharp" source="../data-tools/codesnippet/CSharp/CreateWPFDataApp/MainWindow.xaml.cs" id="Snippet3":::


## <a name="run-the-application"></a>运行应用程序

若要启用调试，请按 F5。 客户和订单数据应会填充到网格中，导航按钮应按预期方式工作。 输入数据后，单击“提交”将新客户或订单添加到模型。 单击“取消”，以从新客户或新订单窗体中返回而不保存数据。 可以直接在文本框中编辑现有客户和订单，这些更改会自动写入到模型中。

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
- [实体框架文档](/ef/)
