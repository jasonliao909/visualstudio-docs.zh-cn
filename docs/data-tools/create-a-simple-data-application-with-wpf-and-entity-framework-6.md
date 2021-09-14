---
title: 具有 WPF 和 实体框架 6 的简单数据应用
description: 在此演练中，请参阅如何使用 Visual Studio WPF Windows Presentation Foundation () 实体框架 6 在 Visual Studio 中创建简单的基于窗体的数据应用。
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
ms.openlocfilehash: ee9f34adcd5e654b03dcd180f85840b6c76d4456
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601201"
---
# <a name="create-a-simple-data-application-with-wpf-and-entity-framework-6"></a>使用 WPF 和 Entity Framework 6 创建简单的数据应用程序

本演练演示如何在 Visual Studio 中创建基本的"基于数据的窗体"应用程序。 该应用使用 SQL Server LocalDB、Northwind 数据库、实体框架 6 (Entity Framework Core) ，Windows Presentation Foundation .NET Framework (.NET Core) 。 它演示如何使用母版-详细信息视图执行基本数据绑定，它还具有一个自定义绑定导航器，该导航器具有"下一步移动"、"移动上一个"、"**移动到** 开始"、"移动到末尾"、"更新"和"**删除"按钮**。  

本文重点介绍在 Visual Studio 中使用数据工具，不会尝试任何深度地解释基础技术。 它假定你基本熟悉 XAML、实体框架和 SQL。 此示例也不演示 Model-View-ViewModel (MVVM) 体系结构，这是 WPF 应用程序的标准体系结构。 但是，可以将此代码复制到自己的 MVVM 应用程序中，只做一些修改。

## <a name="install-and-connect-to-northwind"></a>安装并连接到 Northwind

此示例使用 SQL Server Express LocalDB 和 Northwind 示例数据库。 如果 ADO.NET 产品的数据提供程序支持实体框架，则它还应SQL其他数据库产品。

1. 如果尚未安装SQL Server Express LocalDB，请从下载页SQL Server Express安装 [它，或者](https://www.microsoft.com/sql-server/sql-server-editions-express)通过 **Visual Studio 安装程序。** 在 Visual Studio 安装程序中，可将 SQL Server Express LocalDB 作为 .NET 桌面开发工作负载的一部分安装，也可作为单独组件安装。

2. 按照以下步骤安装 Northwind 示例数据库：

    1. 在Visual Studio中，**打开SQL Server 对象资源管理器窗口**。 **(SQL Server 对象资源管理器** 作为数据存储和处理工作负荷的一部分安装在 Visual Studio 安装程序 **.)** 展开 SQL Server **节点。** 右键单击实例LocalDB并选择"新建 **查询"。**

       查询编辑器窗口随即打开。

    2. 将[Northwind Transact-SQL脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)复制到剪贴板。 此 T-SQL脚本从头开始创建 Northwind 数据库，并使用数据填充该数据库。

    3. 将 T-SQL脚本粘贴到查询编辑器中，然后选择"执行 **"** 按钮。

       短时间后，查询完成运行，并创建 Northwind 数据库。

3. [为](../data-tools/add-new-connections.md) Northwind 添加新连接。

## <a name="configure-the-project"></a>配置项目

1. 在Visual Studio中，创建新的 C# **WPF 应用** 项目。

2. 为 NuGet 6 添加实体框架包。 在 **解决方案资源管理器** 中，选择项目节点。 在主菜单中，**选择"Project**  >  **管理NuGet包"。**

     ![管理NuGet包"菜单项](../data-tools/media/raddata_vs2015_manage_nuget_packages.png)

3. 在 **"NuGet 程序包管理器"** 中，单击"**浏览"** 链接。 实体框架可能是列表中排名第一的包。 单击 **右** 窗格中的"安装"，并按照提示操作。 "输出"窗口指示安装何时完成。

     ![实体框架 NuGet包](../data-tools/media/raddata_vs2015_nuget_ef.png)

4. 现在，可以使用Visual Studio Northwind 数据库创建模型。

## <a name="create-the-model"></a>创建模型

1. 在解决方案资源管理器中右键单击项目节点，然后选择“添加” > “新增项”  。 在左窗格中的"C#"节点下，选择 **"数据**"，在中间窗格中选择 **"ADO.NET 实体数据模型"。**

   ![实体框架模型新项](../data-tools/media/raddata-ef-new-project-item.png)

2. 调用模型， `Northwind_model` 然后选择"确定 **"。** 随即 **实体数据模型向导** 。 从 **数据库中选择"EF 设计器"，** 然后单击"下一 **步"。**

   ![数据库中的 EF 模型](../data-tools/media/raddata-ef-model-from-database.png)

3. 在下一个屏幕中，输入或选择 LocalDB Northwind 连接 (例如 (localdb) \MSSQLLocalDB) ，指定 Northwind 数据库，然后单击"下一步 **"。**

4. 在向导的下一页中，选择要包括在数据库模型中的表、存储过程实体框架对象。 展开树视图中的 dbo 节点，然后选择"客户 **"、"订单**"和"**订单详细信息"。** 选中默认值，然后单击"完成 **"。**

    ![为模型选择数据库对象](../data-tools/media/raddata-choose-ef-objects.png)

5. 向导生成表示模型模型的 C# 实体框架类。 这些类是普通旧 C# 类，它们是我们数据绑定到 WPF 用户界面的类。 *.edmx* 文件描述将类与数据库中的对象关联的关系和其他元数据。 *.tt* 文件是 T4 模板，用于生成对模型进行操作的代码，并保存对数据库的更改。 可以在节点下 **看到解决方案资源管理器文件** Northwind_model文件：

      ![解决方案资源管理器 EF 模型文件](../data-tools/media/raddata-solution-explorer-ef-model-files.png)

    *.edmx* 文件的设计器图面使你能够修改模型中的一些属性和关系。 本演练中不会使用设计器。

6. *.tt* 文件是常规用途文件，需要调整其中一个文件以使用 WPF 数据绑定，这需要 ObservableCollections。 在 **解决方案资源管理器** 中，展开Northwind_model节点，直到找到 *Northwind_model.tt*。  (确保不在 中 *。Context.tt* 文件，位于 *.edmx* file.) 

   - 将 出现的两个 <xref:System.Collections.ICollection> 替换为 <xref:System.Collections.ObjectModel.ObservableCollection%601> 。

   - 将 的第一个匹配项 <xref:System.Collections.Generic.HashSet%601> 替换为 <xref:System.Collections.ObjectModel.ObservableCollection%601> 大约第 51 行。 不要替换 HashSet 的第二个匹配项。

   - 将第 <xref:System.Collections.Generic> 431 行 (出现的唯一) 替换为 <xref:System.Collections.ObjectModel> 。

7. 按 **Ctrl** + **Shift** + **B** 生成项目。 生成完成后，模型类对数据源向导可见。

现在，你已准备好将此模型挂接到 XAML 页，以便可以查看、导航和修改数据。

## <a name="databind-the-model-to-the-xaml-page"></a>将模型数据绑定到 XAML 页

可以编写自己的数据绑定代码，但让Visual Studio更容易。

1. 在主菜单中，选择  >  **Project"添加新** 数据源"以打开 **"数据源配置向导"。** 选择 **"** 对象"，因为你绑定到模型类，而不是数据库：

     ![使用对象源的数据源配置向导](../data-tools/media/raddata-data-source-configuration-wizard-with-object-source.png)

2. 展开项目的节点，然后选择"客户 **"。**  (Customer.) 中的"订单"导航属性自动生成订单) 

     ![将实体类添加为数据源](../data-tools/media/raddata-add-entity-classes-as-data-sources.png)

3. 单击“完成”  。

4. 在代码 *视图中导航到 MainWindow.xaml。* 为方便本示例，我们将使 XAML 保持简单。 将 MainWindow 的标题更改为更具描述性的名称，现在将"高度"和"宽度"增大到 600 x 800。 以后始终可以更改它。 现在，将这三个行定义添加到主网格，一行用于导航按钮，一行用于客户详细信息，另一行用于显示其订单的网格：

    ```xaml
        <Grid.RowDefinitions>
            <RowDefinition Height="auto"/>
            <RowDefinition Height="auto"/>
            <RowDefinition Height="*"/>
        </Grid.RowDefinitions>
    ```

5. 现在打开 *MainWindow.xaml，* 以便你在设计器中查看它。 这将导致"**数据源"** 窗口显示为"工具箱"旁边的Visual Studio窗口 **边距中的一个选项**。 单击选项卡以打开窗口，或者按 **Shift** Alt D 或选择"查看其他Windows +  +   >    >  **数据源"。** 我们将在 Customers 类中，在其自己的单个文本框中显示每个属性。 首先，单击"客户"**组合框中的** 箭头，然后选择"详细信息 **"。** 然后，将节点拖动到设计图面的中间部分，以便设计器知道你想要它进入中间行。 如果错放该行，可以在 XAML 中稍后手动指定该行。 默认情况下，控件垂直放置在网格元素中，但此时，可以按喜欢的形式排列它们。 例如，将"名称"文本框置于地址上方可能有意义。 本文的示例应用程序对字段重新排序，然后将它们重新排列为两列。

     ![客户数据源绑定到各个控件](../data-tools/media/raddata-customers-data-source-binding-to-individual-controls.png)

     在代码视图中，现在可以在父 Grid 的中间 (第 `Grid` 1 行) 元素。 父 Grid 具有 `DataContext` 一个 属性，该属性引用已添加到 元素的 `Windows.Resources` CollectionViewSource。 给定该数据上下文，当第一个文本框绑定到 **Address** 时，该名称将映射到 CollectionViewSource 中当前对象 `Address` `Customer` 中的 属性。

    ```xaml
    <Grid DataContext="{StaticResource customerViewSource}">
    ```

6. 当客户在窗口的上半部分可见时，你想要在下半部分查看其订单。 在单个网格视图控件中显示订单。 若要使 master-detail 数据绑定正常工作，必须绑定到 Customers 类中的 Orders 属性，而不是绑定到单独的 Orders 节点。 将 Customers 类的 Orders 属性拖到窗体的下半部分，以便设计器将其置于第 2 行：

     ![将 Orders 类作为网格拖动](../data-tools/media/raddata-drag-orders-classes-as-grid.png)

7. Visual Studio 生成了将 UI 控件连接到模型中的事件的所有绑定代码。 若要查看某些数据，你只需编写一些代码来填充模型。 首先，导航到 *mainwindow.xaml* ，并将数据成员添加到数据上下文的 mainwindow.xaml 类。 已为您生成的此对象的行为类似于跟踪模型中的更改和事件的控件。 你还将为客户和订单添加 CollectionViewSource 数据成员和关联的构造函数初始化逻辑。 类的顶部应如下所示：

     :::code language="csharp" source="../data-tools/codesnippet/CSharp/CreateWPFDataApp/MainWindow.xaml.cs" id="Snippet1":::

     为 system.string 添加 `using` 指令以将负载扩展方法添加到作用域中：

     ```csharp
     using System.Data.Entity;
     ```

     现在，向下滚动并找到 `Window_Loaded` 事件处理程序。 请注意，Visual Studio 已添加 CollectionViewSource 对象。 这表示创建模型时选择的 NorthwindEntities 对象。 您已经添加了该程序，因此您不需要这样做。 让我们替换中的代码， `Window_Loaded` 使方法现在如下所示：

     :::code language="csharp" source="../data-tools/codesnippet/CSharp/CreateWPFDataApp/MainWindow.xaml.cs" id="Snippet2":::


8. 按 **F5**。 应会看到检索到 CollectionViewSource 中的第一个客户的详细信息。 还应在数据网格中看到它们的顺序。 格式设置不是很好，因此让我们来解决这个问题。 您还可以创建一种方法来查看其他记录并执行基本的 CRUD 操作。

## <a name="adjust-the-page-design-and-add-grids-for-new-customers-and-orders"></a>调整页面设计并为新客户和订单添加网格

Visual Studio 生成的默认布局并非适用于你的应用程序，因此我们将在此处提供最终 XAML 以复制到你的代码中。 还需要一些 "表单" (，它们实际上是网格) ，以使用户能够添加新客户或订单。 为了能够添加新的客户和订单，您需要一组不是数据绑定到的单独的文本框 `CollectionViewSource` 。 通过在处理程序方法中设置 Visible 属性，可以控制用户在任意给定时间看到的网格。 最后，将 "删除" 按钮添加到 "订单" 网格中的每一行，以使用户能够删除单个订单。

首先，将这些样式添加到 `Windows.Resources` *mainwindow.xaml* 中的元素：

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

在 Windows 窗体应用程序中，您将获得一个 BindingNavigator 对象，其中包含用于在数据库中的行间导航并执行基本 CRUD 操作的按钮。 WPF 并不提供 BindingNavigator，但可以很容易创建一个。 使用水平 System.windows.controls.stackpanel> 中的按钮执行该操作，并将这些按钮与代码隐藏中的方法绑定的命令相关联。

命令逻辑分为以下四部分： (1) 命令， (2) 绑定， (3) 按钮， (4) 代码隐藏中的命令处理程序。

### <a name="add-commands-bindings-and-buttons-in-xaml"></a>在 XAML 中添加命令、绑定和按钮

1. 首先，将 *mainwindow.xaml* 文件中的命令添加到 `Windows.Resources` 元素中：

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

2. System.windows.input.commandbinding> 将事件映射 `RoutedUICommand` 到代码隐藏中的方法。 将此 `CommandBindings` 元素添加到 `Windows.Resources` 结束标记后：

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

3. 现在，请将添加到 " `StackPanel` 导航"、"添加"、"删除" 和 "更新" 按钮。 首先，将以下样式添加到 `Windows.Resources` ：

    ```xaml
    <Style x:Key="NavButton" TargetType="{x:Type Button}" BasedOn="{x:Null}">
        <Setter Property="FontSize" Value="24"/>
        <Setter Property="FontFamily" Value="Segoe UI Symbol"/>
        <Setter Property="Margin" Value="2,2,2,0"/>
        <Setter Property="Width" Value="40"/>
        <Setter Property="Height" Value="auto"/>
    </Style>
    ```

     然后，将此代码粘贴到紧邻 `RowDefinitions` `Grid` XAML 页顶部的外部元素之后：

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

### <a name="add-command-handlers-to-the-mainwindow-class"></a>向 Mainwindow.xaml 类添加命令处理程序

除 add 和 delete 方法外，代码隐藏是最少的。 通过对 CollectionViewSource 的 View 属性调用方法来执行导航。 `DeleteOrderCommandHandler`演示如何对订单执行级联删除。 我们必须先删除与之关联的 Order_Details。 向 `UpdateCommandHandler` 集合中添加新的客户或订单，或者只是使用用户在文本框中做出的更改来更新现有客户或订单。

将这些处理程序方法添加到 *mainwindow.xaml* 中的 mainwindow.xaml 类。 如果 "客户" 表的 CollectionViewSource 具有不同的名称，则需要调整其中每个方法中的名称：

:::code language="csharp" source="../data-tools/codesnippet/CSharp/CreateWPFDataApp/MainWindow.xaml.cs" id="Snippet3":::


## <a name="run-the-application"></a>运行应用程序

若要启用调试，请按 F5。 应会看到 "客户" 和 "订单" 数据已填充到网格中，导航按钮应按预期方式工作。 在输入数据后，单击 " **提交** " 将新客户或订单添加到模型。 单击 " **取消** " 以从新客户或新订单窗体中返回，而不保存数据。 您可以直接在文本框中编辑现有客户和订单，这些更改会自动写入到模型中。

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
- [实体框架文档](/ef/)
