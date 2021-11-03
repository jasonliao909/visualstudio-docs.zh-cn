---
title: 演练：从服务器上工作簿中检索缓存的数据
description: 了解如何从缓存在数据工作簿中的数据集Microsoft Excel数据，而无需Excel ServerDocument 类启动数据。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks [Office development in Visual Studio], retrieving data
- datasets [Office development in Visual Studio], accessing on server
- server-side data access [Office development in Visual Studio]
- data [Office development in Visual Studio], accessing on server
- documents [Office development in Visual Studio], server-side data access
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 77b6006b54da383a763ea1dbd93d078a40a88aaf
ms.sourcegitcommit: 7a820b7698a8dcf076eb36e3d766fb0751f56bb1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2021
ms.locfileid: "131126982"
---
# <a name="walkthrough-retrieve-cached-data-from-a-workbook-on-a-server"></a>演练：从服务器上工作簿中检索缓存的数据
  本演练演示如何从数据工作簿中缓存的数据集Microsoft Office Excel数据，而无需Excel 类启动 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 数据。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 本演练演示以下任务：

- 定义包含 *AdventureWorksLT* 数据库中的数据的数据集。

- 在工作簿项目和控制台应用程序Excel创建数据集的实例。

- 创建绑定到工作簿中数据集的 ，在打开工作簿时 <xref:Microsoft.Office.Tools.Excel.ListObject> <xref:Microsoft.Office.Tools.Excel.ListObject> 使用数据填充 。

- 将工作簿中的数据集添加到数据缓存。

- 将数据从缓存的数据集读取到控制台应用程序中的数据集中，而无需Excel。

  尽管本演练假定你在开发计算机上运行代码，但本演练演示的代码可以在未安装 Excel服务器上使用。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] 或 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- 对包含 AdventureWorksLT Microsoft SQL Server或Microsoft SQL Server Express的运行实例的访问权限。 可以从 [CodePlex](/sql/samples/adventureworks-install-configure)网站 下载 AdventureWorksLT 数据库。 有关附加数据库的详细信息，请参阅下列主题：

  - 若要使用 SQL Server Management Studio 或 SQL Server Management Studio Express 附加数据库，请参阅[如何：将数据库附加到 (SQL Server Management Studio) 。 ](/sql/relational-databases/databases/attach-a-database)

  - 若要使用命令行附加数据库，请参阅[如何：将数据库文件附加到 SQL Server Express。](/previous-versions/sql/)

## <a name="create-a-class-library-project-that-defines-a-dataset"></a>创建定义数据集的类库项目
 若要在工作簿项目和Excel应用程序中使用相同的数据集，必须在这两个项目引用的单独程序集中定义数据集。 对于本演练，请定义类库项目中的数据集。

### <a name="create-the-class-library-project"></a>创建类库项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在 **“文件”** 菜单上，指向 **“新建”** ，再单击 **“项目”** 。

3. 在模板窗格中，展开 **"Visual C#"****或** Visual Basic，然后单击 **"Windows"。**

4. 在项目模板列表中，选择"类 **库"。**

5. 在" **名称"** 框中，键入 **AdventureWorksDataSet**。

6. 单击 **"** 浏览"，导航到 Windows XP 及更早) 的 *%UserProfile%\我的文档* (或 Windows Vista) 文件夹的 *%UserProfile%\Documents* (，然后单击"选择文件夹 **"。**

7. 在 **"Project"** 对话框中，确保未选中"为解决方案 **创建** 目录"复选框。

8. 单击“确定”。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 **AdventureWorksDataSet** 项目添加到 **解决方案资源管理器** 并打开 *Class1.cs* 或 *Class1.vb* 代码文件。

9. 在 **解决方案资源管理器** 中，右键单击 *Class1.cs* 或 *Class1.vb，* 然后单击"删除 **"。** 本演练不需要此文件。

## <a name="define-a-dataset-in-the-class-library-project"></a>在类库项目中定义数据集
 定义一个类型数据集，其中包含 2005 年 1 月 AdventureWorksLT SQL Server的数据。 本演练的稍后部分将引用此数据集，Excel工作簿项目和控制台应用程序项目中。

 数据集是一 *个类型数据集* ，表示 AdventureWorksLT 数据库的 Product 表中的数据。 有关类型数据集详细信息，请参阅 Visual Studio 中的[数据集](../data-tools/dataset-tools-in-visual-studio.md)工具。

### <a name="define-a-typed-dataset-in-the-class-library-project"></a>在类库项目中定义类型数据集

1. 在 **解决方案资源管理器** 中，单击 **AdventureWorksDataSet** 项目。

2. 如果"**数据源"** 窗口不可见，请通过选择菜单栏上的"查看其他数据源"Windows  >    >  **显示它**。

3. 选择 **“添加新数据源”** 以启动 **“数据源配置向导”**。

4. 单击“数据库” ，然后单击“下一步” 。

5. 如果已连接到 AdventureWorksLT 数据库，请选择此连接，然后单击"下一步 **"。**

    否则，单击“新建连接” ，然后使用“添加连接”  对话框创建新连接。 有关详细信息，请参阅 [添加新连接](../data-tools/add-new-connections.md)。

6. 在“将连接字符串保存到应用程序配置文件中”  页中，单击“下一步” 。

7. 在"**选择数据库对象"** 页中，展开 **"表****"，然后选择"SalesLT (") "**。

8. 单击“完成”  。

    *AdventureWorksLTDataSet.xsd* 文件将添加到 **AdventureWorksDataSet** 项目。 此文件定义以下各项：

   - 一个名为 `AdventureWorksLTDataSet`的类型化数据集。 此数据集表示 AdventureWorksLT 数据库中 Product 表的内容。

   - 名为 的 TableAdapter。 `ProductTableAdapter` 此 TableAdapter 可用于读取和写入 中的数据 `AdventureWorksLTDataSet` 。 有关详细信息，请参阅 [TableAdapter 概述](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview)。

     在本演练后面的部分中，你将使用这两个对象。

9. 在 **解决方案资源管理器** 中，右键单击 **"AdventureWorksDataSet"，然后单击**"生成 **"。**

     验证此项目是否已生成且未发生错误。

## <a name="create-an-excel-workbook-project"></a>创建Excel工作簿项目
 为Excel接口创建一个工作簿项目。 本演练稍后将创建一个显示数据的 ，并且将数据集的实例添加到工作簿 <xref:Microsoft.Office.Tools.Excel.ListObject> 中的数据缓存中。

### <a name="create-the-excel-workbook-project"></a>创建Excel工作簿项目

1. 在 **解决方案资源管理器** 中，右键单击 **AdventureWorksDataSet** 解决方案，指向"添加"，然后单击"新建 **Project"。**

2. 在模板窗格中，展开 **“Visual C#”** 或 **“Visual Basic”**，然后展开 **“Office/SharePoint”**。

3. 在展开的 **“Office/SharePoint”** 节点下方，选择 **“Office 外接程序”** 节点。

4. 在项目模板列表中，选择 **“Excel 2010 工作簿”** 或 **“Excel 2013 工作簿”** 项目。

5. 在" **名称"** 框中，键入 **AdventureWorksReport**。 不要修改位置。

6. 单击“确定”。

     将打开“Visual Studio Tools for Office 项目向导”  。

7. 确保选中 **"创建新文档"，** 然后单击"确定 **"。**

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]在设计器 **中打开 AdventureWorksReport** 工作簿，并将 **AdventureWorksReport** 项目添加到 **解决方案资源管理器。**

## <a name="add-the-dataset-to-data-sources-in-the-excel-workbook-project"></a>将数据集添加到工作簿项目中Excel数据源
 必须先将数据集添加到 Excel 工作簿项目中的数据源，然后才能在 Excel工作簿中显示数据集。

1. 在 **解决方案资源管理器** 中，双击 **AdventureWorksReport** 项目下的 *Sheet1.cs* 或 *Sheet1.vb。*

     工作簿将在设计器中打开。

2. 在 **“数据”** 菜单上，单击 **“添加新数据源”**。

     " **数据源配置向导"随即** 打开。

3. 单击 **"对象**"，然后单击"下一 **步"。**

4. 在"**选择要绑定到的对象"页中**，单击"**添加引用"。**

5. 在"**项目"选项卡上**，单击 **"AdventureWorksDataSet"，** 然后单击"确定 **"。**

6. 在 **AdventureWorksDataSet 程序集的 AdventureWorksDataSet** 命名空间下，单击 **"AdventureWorksLTDataSet"，** 然后单击"完成 **"。** 

     " **数据源"** 窗口随即打开 **，AdventureWorksLTDataSet** 将添加到数据源列表。

## <a name="create-a-listobject-that-is-bound-to-an-instance-of-the-dataset"></a>创建绑定到数据集实例的 ListObject
 若要在工作簿中显示数据集，请创建 <xref:Microsoft.Office.Tools.Excel.ListObject> 绑定到数据集实例的 。 有关将控件绑定到数据的更多信息，请参阅[将数据绑定到解决方案 中的Office控件](../vsto/binding-data-to-controls-in-office-solutions.md)。

1. 在" **数据源"窗口中** ，展开 **"AdventureWorksLTDataSet"** 下的 **"AdventureWorksLTDataSet"节点**。

2. 选择 **"产品**"节点，单击出现的下拉箭头，然后选择下拉列表中的 **"ListObject"。**

     如果未显示下拉箭头，请确认工作簿在设计器中已打开。

3. 将 Product **表** 拖到单元格 A1。

     从 <xref:Microsoft.Office.Tools.Excel.ListObject> 单元格 `productListObject` A1 开始，在工作表上创建名为 的控件。 同时，向项目添加了一个名为 `adventureWorksLTDataSet` 的数据集对象和一个名为 <xref:System.Windows.Forms.BindingSource> 的 `productBindingSource` 。 已将 <xref:Microsoft.Office.Tools.Excel.ListObject> 绑定到 <xref:System.Windows.Forms.BindingSource>，而后者又绑定到该数据集对象。

## <a name="add-the-dataset-to-the-data-cache"></a>将数据集添加到数据缓存
 若要使工作簿Excel外部的代码访问工作簿中的数据集，必须将数据集添加到数据缓存。 有关数据缓存详细信息，请参阅文档级自定义 [项](../vsto/cached-data-in-document-level-customizations.md) 中的缓存数据和 [缓存数据](../vsto/caching-data.md)。

1. 在设计器中，单击 **"adventureWorksLTDataSet"。**

2. 在"**属性"** 窗口中，将 **"修饰符"** 属性设置为 **"公共"。**

3. 将 **CacheInDocument** 属性设置为 **True。**

## <a name="initialize-the-dataset-in-the-workbook"></a>初始化工作簿中的数据集
 必须先使用数据填充缓存数据集，然后才能使用控制台应用程序从缓存数据集检索数据。

1. 在 **解决方案资源管理器** 中，右键单击 *Sheet1.cs* 或 *Sheet1.vb* 文件，然后单击"**查看代码"。**

2. 将 `Sheet1_Startup` 事件处理程序替换为以下代码。 此代码使用 AdventureWorksDataSet 项目中定义的 类的实例来填充缓存的数据集（如果 `ProductTableAdapter` 当前为空）。 

     :::code language="csharp" source="../vsto/codesnippet/CSharp/AdventureWorksDataSet/AdventureWorksReport/Sheet1.cs" id="Snippet8":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/AdventureWorksReport/Sheet1.vb" id="Snippet8":::

## <a name="checkpoint"></a>检查点
 生成并运行Excel工作簿项目，以确保它在编译和运行时不会出错。 此操作还会填充缓存的数据集，并保存工作簿中的数据。

### <a name="build-and-run-the-project"></a>生成并运行项目

1. 在 **解决方案资源管理器** 中，右键单击 **AdventureWorksReport** 项目，选择"调试 **"，然后单击**"**启动新实例"。**

     项目已生成，工作簿将在 Excel。 检查下列各项：

    - 填充 <xref:Microsoft.Office.Tools.Excel.ListObject> 数据。

    - 第一行 **的 ListPrice** 列中的值为 <xref:Microsoft.Office.Tools.Excel.ListObject> 1431.5。 本演练稍后将使用控制台应用程序修改 **ListPrice** 列中的值。

2. 保存该工作簿。 请勿修改文件名或工作簿的位置。

3. 关闭 Excel。

## <a name="create-a-console-application-project"></a>创建控制台应用程序项目
 创建一个控制台应用程序项目，用于修改工作簿中缓存数据集中的数据。

1. 在 **解决方案资源管理器** 中，右键单击 **AdventureWorksDataSet** 解决方案，指向"添加"，然后单击"新建 **Project"。**

2. 在 **"Project"** 窗格中，展开 **"Visual C#"****或** Visual Basic，然后单击 **"Windows"。**

3. 在 **“模板”** 窗格中，选择 **“控制台应用程序”**。

4. 在" **名称"** 框中，键入 **DataReader**。 不要修改位置。

5. 单击“确定”。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 **DataReader** 项目 **添加到** 解决方案资源管理器并打开 *Program.cs* 或 *Module1.vb* 代码文件。

## <a name="retrieve-data-from-the-cached-dataset-by-using-the-console-application"></a>使用控制台应用程序从缓存数据集中检索数据
 使用 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 控制台应用程序中的 类将数据读入本地 `AdventureWorksLTDataSet` 对象。 为了确认本地数据集已使用缓存数据集中的数据初始化，应用程序显示本地数据集中的行数。

### <a name="retrieve-data-from-the-cached-dataset"></a>从缓存的数据集检索数据

1. 在 **解决方案资源管理器** 中，右键单击 **DataReader** 项目，然后单击"**添加引用"。**

2. 在 **".NET"选项卡** 上，选择 **"Microsoft.VisualStudio.Tools.Applications.ServerDocument"。**

3. 单击“确定”。

4. 在 **解决方案资源管理器** 中，右键单击 **DataReader** 项目，然后单击"**添加引用"。**

5. 在"**项目"选项卡上**，选择 **"AdventureWorksDataSet"，** 然后单击"确定 **"。**

6. 在代码 *编辑器中打开 Program.cs* 或 *Module1.vb* 文件。

7. 使用 **C# (** 的 ) 或 (for Visual Basic) 语句的 **Imports** 代码添加到代码文件的顶部。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs" id="Snippet1":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb" id="Snippet1":::

8. 将以下代码添加到 `Main` 方法中。 此代码声明以下对象：

   - `AdventureWorksLTDataSet` **AdventureWorksDataSet** 项目中定义的类型的实例。

   - AdventureWorksReport 项目生成文件夹中 **AdventureWorksReport 工作簿** 的路径。

   - <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument>用于访问工作簿中数据缓存的 对象。

     > [!NOTE]
     > 以下代码假定工作簿是使用.xlsx *保存的* 。 如果项目中的工作簿具有不同的扩展名，请根据需要修改路径。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs" id="Snippet10":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb" id="Snippet10":::

9. 在上一步骤 `Main` 中添加的代码之后，将以下代码添加到 方法。 此代码执行以下任务：

   - 它使用 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> 类的 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 属性访问工作簿中的缓存数据集。

   - 它将缓存数据集中的数据读入本地数据集。

   - 它显示本地数据集中的行数，以确认其包含数据。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb" id="Snippet11":::

10. 在"生成 **"菜单** 上，单击"**生成数据""读取程序"。**

## <a name="test-the-project"></a>测试项目
 运行控制台应用程序时，它显示本地数据集中的行数。

### <a name="test-the-workbook"></a>测试工作簿

1. 在 **解决方案资源管理器** 中，右键单击 **DataReader** 项目，指向"调试 **"，然后单击**"**启动新实例"。**

     验证应用程序是否报告本地数据集有 295 行。

2. 按 **Enter** 关闭应用程序。

## <a name="next-steps"></a>后续步骤
 可以从以下主题详细了解如何处理缓存数据：

- 在不启动缓存数据集的情况下更改Excel。 有关详细信息，请参阅演练： [更改服务器上工作簿中的缓存数据](../vsto/walkthrough-changing-cached-data-in-a-workbook-on-a-server.md)。

## <a name="see-also"></a>请参阅

- [演练：将数据插入到服务器的工作簿中](../vsto/walkthrough-inserting-data-into-a-workbook-on-a-server.md)
- [演练：更改服务器上工作簿中的缓存数据](../vsto/walkthrough-changing-cached-data-in-a-workbook-on-a-server.md)
