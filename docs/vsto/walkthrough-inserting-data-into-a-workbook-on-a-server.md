---
title: 演练：将数据插入到服务器上的工作簿
description: 了解如何将数据插入到 Microsoft Excel 工作簿中缓存的数据集，而无需使用 ServerDocument 类启动 Excel。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- datasets [Office development in Visual Studio], accessing on server
- server-side data access [Office development in Visual Studio]
- data [Office development in Visual Studio], accessing on server
- documents [Office development in Visual Studio], server-side data access
- workbooks [Office development in Visual Studio], inserting data
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 376c0c4a51fa6d4514af403322956f60bfe9fad3
ms.sourcegitcommit: 7a820b7698a8dcf076eb36e3d766fb0751f56bb1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2021
ms.locfileid: "131127879"
---
# <a name="walkthrough-insert-data-into-a-workbook-on-a-server"></a>演练：将数据插入到服务器上的工作簿
  本演练演示如何将数据插入到在 Microsoft Office Excel 工作簿中缓存的数据集，而无需使用类启动 Excel <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 本演练演示以下任务：

- 定义包含 AdventureWorksLT 数据库中的数据的数据集。

- 在 Excel 工作簿项目和控制台应用程序项目中创建数据集的实例。

- 创建一个 <xref:Microsoft.Office.Tools.Excel.ListObject> 绑定到工作簿中的数据集的。

- 将工作簿中的数据集添加到数据缓存。

- 通过在控制台应用程序中运行代码，将数据插入缓存的数据集，而无需启动 Excel。

  虽然本演练假定你在开发计算机上运行代码，但本演练演示的代码可以在未安装 Excel 的服务器上使用。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] 或 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- 访问 Microsoft SQL Server 或附加了 AdventureWorksLT 示例数据库的 Microsoft SQL Server Express 的正在运行的实例。 可以从 [CodePlex 网站](/sql/samples/adventureworks-install-configure)下载 AdventureWorksLT 数据库。 有关附加数据库的详细信息，请参阅下列主题：

  - 若要使用 SQL Server Management Studio 或 SQL Server Management Studio Express 附加数据库，请参阅[如何：附加数据库 (SQL Server Management Studio) ](/sql/relational-databases/databases/attach-a-database)。

  - 若要使用命令行来附加数据库，请参阅[如何：将数据库文件附加到 SQL Server Express](/previous-versions/sql/)。

## <a name="create-a-class-library-project-that-defines-a-dataset"></a>创建用于定义数据集的类库项目
 若要在 Excel 工作簿项目和控制台应用程序中使用相同的数据集，则必须在这两个项目都引用的单独程序集中定义数据集。 对于本演练，请在类库项目中定义数据集。

### <a name="to-create-the-class-library-project"></a>创建类库项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在 **“文件”** 菜单上，指向 **“新建”** ，再单击 **“项目”** 。

3. 在 "模板" 窗格中，展开 " **Visual c #** " 或 " **Visual Basic**"，然后单击 " **Windows**"。

4. 在项目模板列表中 **，选择 "类库"**。

5. 在 " **名称** " 框中，键入 **AdventureWorksDataSet**。

6. 单击 "**浏览**"，导航到 *%UserProfile%\My 文档* (Windows XP 和更早版本) 或 *%UserProfile%\Documents* (对于 Windows Vista) 文件夹，然后单击 "**选择文件夹**"。

7. 在 "**新建 Project** " 对话框中，确保未选中 "**创建解决方案的目录**" 复选框。

8. 单击“确定”。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 **AdventureWorksDataSet** 项目添加到 **解决方案资源管理器** ，并打开 **class1** 或 **class1** 代码文件。

9. 在 **解决方案资源管理器** 中，右键单击 **class1** 或 **Class1**，然后单击 " **删除**"。 对于本演练，不需要此文件。

## <a name="define-a-dataset-in-the-class-library-project"></a>在类库项目中定义数据集
 定义一个类型化数据集，其中包含 AdventureWorksLT 数据库中 SQL Server 2005 的数据。 稍后在本演练中，你将从 Excel 工作簿项目和控制台应用程序项目中引用此数据集。

 数据集是一个 *类型化数据集* ，它表示 AdventureWorksLT 数据库的 Product 表中的数据。 有关类型化数据集的详细信息，请参阅[Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)。

### <a name="to-define-a-typed-dataset-in-the-class-library-project"></a>定义类库项目中的类型化数据集

1. 在 **解决方案资源管理器** 中，单击 **AdventureWorksDataSet** 项目。

2. 如果 "**数据源**" 窗口不可见，请在菜单栏上选择 "**查看**  >  **其他 Windows**  >  **数据源**"，将其显示出来。

3. 选择 **“添加新数据源”** 以启动 **“数据源配置向导”**。

4. 单击“数据库” ，然后单击“下一步” 。

5. 如果有与 AdventureWorksLT 数据库的连接，请选择此连接，然后单击 " **下一步**"。

    否则，单击“新建连接” ，然后使用“添加连接”  对话框创建新连接。 有关详细信息，请参阅[如何：连接数据库中的数据](../vsto/walkthrough-inserting-data-into-a-workbook-on-a-server.md)。

6. 在“将连接字符串保存到应用程序配置文件中”  页中，单击“下一步” 。

7. 在 " **选择数据库对象** " 页上，展开 " **表** "，然后选择 " **Product (SalesLT)**"。

8. 单击“完成”  。

    *Adventureworksltdataset.xsd* 文件将添加到 **AdventureWorksDataSet** 项目中。 此文件定义以下各项：

   - 一个名为 `AdventureWorksLTDataSet`的类型化数据集。 此数据集表示 AdventureWorksLT 数据库中的 Product 表的内容。

   - 名为的 TableAdapter `ProductTableAdapter` 。 此 TableAdapter 可用于在中读取和写入数据 `AdventureWorksLTDataSet` 。 有关详细信息，请参阅 [TableAdapter 概述](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview)。

     在本演练后面的部分中，你将使用这两个对象。

9. 在 **解决方案资源管理器** 中，右键单击 **AdventureWorksDataSet** ，然后单击 " **生成**"。

     验证此项目是否已生成且未发生错误。

## <a name="create-an-excel-workbook-project"></a>创建 Excel 工作簿项目
 为数据的接口创建 Excel 工作簿项目。 稍后在本演练中，您将创建一个 <xref:Microsoft.Office.Tools.Excel.ListObject> 显示数据的，并将数据集的一个实例添加到工作簿中的数据缓存。

### <a name="to-create-the-excel-workbook-project"></a>创建 Excel 工作簿项目

1. 在 **解决方案资源管理器** 中，右键单击 **AdventureWorksDataSet** 解决方案，指向 "**添加**"，然后单击 "**新建 Project**"。

2. 在模板窗格中，展开 **“Visual C#”** 或 **“Visual Basic”**，然后展开 **“Office/SharePoint”**。

3. 在展开的 **“Office/SharePoint”** 节点下方，选择 **“Office 外接程序”** 节点。

4. 在项目模板列表中，选择 **“Excel 2010 工作簿”** 或 **“Excel 2013 工作簿”** 项目。

5. 在 " **名称** " 框中，键入 **AdventureWorksReport**。 请勿修改位置。

6. 单击“确定”。

     将打开“Visual Studio Tools for Office 项目向导”  。

7. 确保已选中 " **创建新文档** "，然后单击 **"确定"**。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 在设计器中打开 **AdventureWorksReport** 工作簿，并将 **AdventureWorksReport** 项目添加到 **解决方案资源管理器**。

## <a name="add-the-dataset-to-data-sources-in-the-excel-workbook-project"></a>将数据集添加到 Excel 工作簿项目中的数据源
 必须首先将数据集添加到 Excel 工作簿项目中的数据源，然后才能在 Excel 工作簿中显示数据集。

### <a name="to-add-the-dataset-to-the-data-sources-in-the-excel-workbook-project"></a>将数据集添加到 Excel 工作簿项目中的数据源

1. 在 **解决方案资源管理器** 中，双击 " **AdventureWorksReport** " 项目下的 " **sheet1** " 或 " **sheet1** "。

     工作簿将在设计器中打开。

2. 在 **“数据”** 菜单上，单击 **“添加新数据源”**。

     " **数据源配置向导** " 将打开。

3. 单击 " **对象**"，然后单击 " **下一步**"。

4. 在 " **选择要绑定到的对象** " 页上，单击 " **添加引用**"。

5. 在 " **项目** " 选项卡上，单击 " **AdventureWorksDataSet** "，然后单击 **"确定"**。

6. 在 **AdventureWorksDataSet** 程序集的 **AdventureWorksDataSet** 命名空间下，单击 " **adventureworksltdataset.xsd** "，然后单击 "**完成**"。

     此时将打开 " **数据源** " 窗口，并将 **adventureworksltdataset.xsd** 添加到数据源列表。

## <a name="create-a-listobject-that-is-bound-to-an-instance-of-the-dataset"></a>创建绑定到数据集实例的 ListObject
 若要在工作簿中显示数据集，请创建一个 <xref:Microsoft.Office.Tools.Excel.ListObject> 绑定到数据集实例的。 有关将控件绑定到数据的详细信息，请参阅[在 Office 解决方案中将数据绑定到控件](../vsto/binding-data-to-controls-in-office-solutions.md)。

### <a name="to-create-a-listobject-that-is-bound-to-an-instance-of-the-dataset"></a>创建绑定到数据集实例的 ListObject

1. 在 "**数据源**" 窗口中，展开 " **AdventureWorksDataSet**" 下的 **adventureworksltdataset.xsd** 节点。

2. 选择 " **产品** " 节点，单击显示的下拉箭头，然后在下拉列表中选择 " **ListObject** "。

     如果下拉箭头未出现，请确认已在设计器中打开该工作簿。

3. 将 **Product** 表拖到单元格 A1。

     在 <xref:Microsoft.Office.Tools.Excel.ListObject> 工作表上创建一个名为的控件 `productListObject` ，从 A1 单元格开始。 同时，向项目添加了一个名为 `adventureWorksLTDataSet` 的数据集对象和一个名为 <xref:System.Windows.Forms.BindingSource> 的 `productBindingSource` 。 已将 <xref:Microsoft.Office.Tools.Excel.ListObject> 绑定到 <xref:System.Windows.Forms.BindingSource>，而后者又绑定到该数据集对象。

## <a name="add-the-dataset-to-the-data-cache"></a>将数据集添加到数据缓存
 若要使工作簿Excel外部的代码访问工作簿中的数据集，必须将数据集添加到数据缓存。 有关数据缓存详细信息，请参阅文档级自定义 [项](../vsto/cached-data-in-document-level-customizations.md) 中的缓存数据和 [缓存数据](../vsto/caching-data.md)。

### <a name="to-add-the-dataset-to-the-data-cache"></a>将数据集添加到数据缓存

1. 在设计器中，单击 **"adventureWorksLTDataSet"。**

2. 在"**属性"** 窗口中，将 **"修饰符"** 属性设置为 **"公共"。**

3. 将 **CacheInDocument** 属性设置为 **True。**

## <a name="checkpoint"></a>检查点
 生成并运行Excel工作簿项目，以确保它在编译和运行时不会出错。

### <a name="to-build-and-run-the-project"></a>生成并运行此项目

1. 在 **解决方案资源管理器** 中，右键单击 **AdventureWorksReport** 项目，选择"调试 **"，然后单击**"**启动新实例"。**

     项目已生成，工作簿将在 Excel。 <xref:Microsoft.Office.Tools.Excel.ListObject> **Sheet1 中的** 为空，因为数据缓存中的 `adventureWorksLTDataSet` 对象还没有数据。 下一部分将使用控制台应用程序来填充 `adventureWorksLTDataSet` 对象的数据。

2. 关闭 Excel。 不要保存更改。

## <a name="create-a-console-application-project"></a>创建控制台应用程序项目
 创建一个控制台应用程序项目，用于将数据插入到工作簿的缓存数据集中。

### <a name="to-create-the-console-application-project"></a>创建控制台应用程序项目

1. 在 **解决方案资源管理器** 中，右键单击 **AdventureWorksDataSet** 解决方案，指向"添加"，然后单击"新建 **Project"。**

2. 在 **"Project"** 窗格中，展开 **"Visual C#"****或** Visual Basic，然后单击 **"Windows"。**

3. 在 **“模板”** 窗格中，选择 **“控制台应用程序”**。

4. 在" **名称"** 框中，键入 **DataWriter**。 不要修改位置。

5. 单击“确定”。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 **DataWriter** 项目添加到 **解决方案资源管理器** 并打开 **Program.cs** 或 **Module1.vb** 代码文件。

## <a name="add-data-to-the-cached-dataset-by-using-the-console-application"></a>使用控制台应用程序将数据添加到缓存的数据集
 使用 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 控制台应用程序中的 类，使用数据填充工作簿中的缓存数据集。

### <a name="to-add-data-to-the-cached-dataset"></a>将数据添加到缓存的数据集

1. 在 **解决方案资源管理器** 中，右键单击 **DataWriter 项目**，然后单击"**添加引用"。**

2. 在 **".NET"选项卡** 上，选择 **"Microsoft.VisualStudio.Tools.Applications.ServerDocument"。**

3. 单击“确定”。

4. 在 **解决方案资源管理器** 中，右键单击 **DataWriter 项目**，然后单击"**添加引用"。**

5. 在"**项目"选项卡上**，选择 **"AdventureWorksDataSet"，** 然后单击"确定 **"。**

6. 在代码 *编辑器中打开 Program.cs* 或 *Module1.vb* 文件。

7. 使用 **C# (** 的 ) 或 (for Visual Basic) 语句的 **Imports** 代码添加到代码文件的顶部。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs" id="Snippet1":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb" id="Snippet1":::

8. 将以下代码添加到 `Main` 方法中。 此代码声明以下对象：

   - `AdventureWorksLTDataSet` `ProductTableAdapter` **AdventureWorksDataSet** 项目中定义的 和 类型的实例。

   - AdventureWorksReport 项目生成文件夹中 **AdventureWorksReport 工作簿** 的路径。

   - <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument>用于访问工作簿中数据缓存的 对象。

     > [!NOTE]
     > 以下代码假定你使用的工作簿具有 *.xlsx扩展名* 。 如果项目中的工作簿具有不同的文件扩展名，请根据需要修改路径。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb" id="Snippet3":::

9. 在上一步骤 `Main` 中添加的代码之后，将以下代码添加到 方法。 此代码执行以下任务：

   - 它使用表适配器填充类型数据集对象。

   - 它使用 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> 类的 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 属性访问工作簿中的缓存数据集。

   - 它使用 <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.SerializeDataInstance%2A> 方法使用本地类型数据集中的数据填充缓存的数据集。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb" id="Snippet4":::

10. 在 **解决方案资源管理器** 中，右键单击 **DataWriter** 项目，指向"调试 **"，然后单击**"**启动新实例"。**

     项目已生成，控制台应用程序在填充本地数据集以及应用程序将数据保存到工作簿中的缓存数据集时显示多个状态消息。 按 **Enter** 关闭应用程序。

## <a name="test-the-workbook"></a>测试工作簿
 打开工作簿时， 现在显示使用控制台应用程序添加到缓存 <xref:Microsoft.Office.Tools.Excel.ListObject> 数据集的数据。

### <a name="to-test-the-workbook"></a>测试工作簿

1. 如果 AdventureWorksReport 工作簿仍处于打开Visual Studio设计器中，请关闭该工作簿。

2. 在文件资源管理器，打开 AdventureWorksReport 项目的生成文件夹中的 **AdventureWorksReport** 工作簿。 默认情况下，生成文件夹位于以下位置之一：

    - *%UserProfile%\我的文档\AdventureWorksReport\bin\Debug* (Windows XP 及更早版本) 

    - *%UserProfile%\Documents\AdventureWorksReport\bin\Debug* (Windows Vista) 

3. 打开 <xref:Microsoft.Office.Tools.Excel.ListObject> 工作簿后，验证 是否填充了数据。

## <a name="next-steps"></a>后续步骤

可以从以下主题详细了解如何处理缓存数据：

- 在不启动缓存数据集的情况下更改Excel。 有关详细信息，请参阅演练： [更改服务器上工作簿中的缓存数据](../vsto/walkthrough-changing-cached-data-in-a-workbook-on-a-server.md)。

## <a name="see-also"></a>请参阅

- [演练：更改服务器上工作簿中的缓存数据](../vsto/walkthrough-changing-cached-data-in-a-workbook-on-a-server.md)
