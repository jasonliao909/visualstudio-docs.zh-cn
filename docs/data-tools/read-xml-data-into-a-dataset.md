---
title: 将 XML 数据读入到数据集中
description: 将 XML 数据读入数据集。 本演练将创建一个Windows将 XML 数据加载到数据集的应用程序。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- reading XML
- data access [Visual Studio], XML data
- reading files, XML
- data [Visual Studio], reading from XML files
- reading data, XML files
- XML [Visual Studio], reading
- XML documents, reading
- datasets [Visual Basic], reading XML data
ms.assetid: fae72958-0893-47d6-b3dd-9d42418418e4
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: b188bb7bc7727c84f517e21d45650078817757067604ee2020933c6ac2c7e524
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121346981"
---
# <a name="read-xml-data-into-a-dataset"></a>将 XML 数据读入到数据集中

ADO.NET 提供了用于处理 XML 数据的简单方法。 本演练将创建一个Windows将 XML 数据加载到数据集的应用程序。 然后，数据集将显示在 控件 <xref:System.Windows.Forms.DataGridView> 中。 最后，基于 XML 文件内容的 XML 架构显示在文本框中。

## <a name="create-a-new-project"></a>创建新项目

为 **C# Windows窗体应用** 项目创建新的 Visual Basic。 将项目命名 **ReadingXML**。

## <a name="generate-the-xml-file-to-be-read-into-the-dataset"></a>生成要读入数据集的 XML 文件

由于本演练侧重于将 XML 数据读取到数据集中，因此提供了 XML 文件的内容。

1. 在“项目”菜单上，选择“添加新项”。

2. 选择 **"XML 文件**"，将文件 **authors.xml，** 然后选择"添加 **"。**

   XML 文件将加载至设计器中，并已准备好进行编辑。

3. 将以下 XML 数据粘贴到 XML 声明下方的编辑器中：

   ```xml
   <Authors_Table>
     <authors>
       <au_id>172-32-1176</au_id>
       <au_lname>White</au_lname>
       <au_fname>Johnson</au_fname>
       <phone>408 496-7223</phone>
       <address>10932 Bigge Rd.</address>
       <city>Menlo Park</city>
       <state>CA</state>
       <zip>94025</zip>
       <contract>true</contract>
     </authors>
     <authors>
       <au_id>213-46-8915</au_id>
       <au_lname>Green</au_lname>
       <au_fname>Margie</au_fname>
       <phone>415 986-7020</phone>
       <address>309 63rd St. #411</address>
       <city>Oakland</city>
       <state>CA</state>
       <zip>94618</zip>
       <contract>true</contract>
     </authors>
     <authors>
       <au_id>238-95-7766</au_id>
       <au_lname>Carson</au_lname>
       <au_fname>Cheryl</au_fname>
       <phone>415 548-7723</phone>
       <address>589 Darwin Ln.</address>
       <city>Berkeley</city>
       <state>CA</state>
       <zip>94705</zip>
       <contract>true</contract>
     </authors>
     <authors>
       <au_id>267-41-2394</au_id>
       <au_lname>Hunter</au_lname>
       <au_fname>Anne</au_fname>
       <phone>408 286-2428</phone>
       <address>22 Cleveland Av. #14</address>
       <city>San Jose</city>
       <state>CA</state>
       <zip>95128</zip>
       <contract>true</contract>
     </authors>
     <authors>
       <au_id>274-80-9391</au_id>
       <au_lname>Straight</au_lname>
       <au_fname>Dean</au_fname>
       <phone>415 834-2919</phone>
       <address>5420 College Av.</address>
       <city>Oakland</city>
       <state>CA</state>
       <zip>94609</zip>
       <contract>true</contract>
     </authors>
   </Authors_Table>
   ```

4. 在"文件 **"菜单** 上，选择"**保存authors.xml"。**

## <a name="create-the-user-interface"></a>创建用户界面

此应用程序的用户界面包括以下各项：

- 一 <xref:System.Windows.Forms.DataGridView> 个控件，该控件将 XML 文件的内容显示为数据。

- 显示 <xref:System.Windows.Forms.TextBox> XML 文件的 XML 架构的控件。

- 两 <xref:System.Windows.Forms.Button> 个控件。

  - 一个按钮将 XML 文件读入数据集，并显示在 <xref:System.Windows.Forms.DataGridView> 控件中。

  - 第二个按钮从数据集中提取架构，并通过 在 <xref:System.IO.StringWriter> 控件中显示 <xref:System.Windows.Forms.TextBox> 架构。

### <a name="to-add-controls-to-the-form"></a>向窗体添加控件

1. 在设计 `Form1` 视图中打开 。

2. 从" **工具箱"** 中，将以下控件拖到窗体上：

    - 一 <xref:System.Windows.Forms.DataGridView> 个控件

    - 一 <xref:System.Windows.Forms.TextBox> 个控件

    - 两 <xref:System.Windows.Forms.Button> 个控件

3. 设置以下属性：

    |控制|属性|设置|
    |-------------|--------------|-------------|
    |`TextBox1`|**多行**|`true`|
    ||**ScrollBars**|**垂直**|
    |`Button1`|**名称**|`ReadXmlButton`|
    ||**Text**|`Read XML`|
    |`Button2`|**名称**|`ShowSchemaButton`|
    ||**Text**|`Show Schema`|

## <a name="create-the-dataset-that-receives-the-xml-data"></a>创建接收 XML 数据的数据集

在此步骤中，将创建名为 的新数据集 `authors` 。 有关数据集详细信息，请参阅 数据集[中的数据集Visual Studio。](../data-tools/dataset-tools-in-visual-studio.md)

1. 在 **解决方案资源管理器** 中，选择 **Form1** 的源文件，然后选择 **视图设计器工具栏上的****解决方案资源管理器按钮**。

2. 从" [工具箱"的"数据"选项卡](../ide/reference/toolbox-data-tab.md)中，将 **数据集拖到** **Form1 上**。

3. 在"**添加数据集"** 对话框中，选择 **"未类型化数据集"，** 然后选择"确定 **"。**

     **DataSet1** 将添加到组件栏中。

4. 在" **属性** "窗口中， **设置** 的名称 <xref:System.Data.DataSet.DataSetName%2A> 和属性 `AuthorsDataSet` 。

## <a name="create-the-event-handler-to-read-the-xml-file-into-the-dataset"></a>创建事件处理程序以将 XML 文件读入数据集

" **读取 XML"** 按钮将 XML 文件读入数据集。 然后，它在控件上 <xref:System.Windows.Forms.DataGridView> 设置属性，以将其绑定到数据集。

1. 在 **解决方案资源管理器** 中，选择 **"Form1"，** 然后选择 **视图设计器工具栏上的****"解决方案资源管理器** 按钮。

2. 选择" **读取 XML"** 按钮。

     代码 **编辑器将在** 事件处理程序 `ReadXmlButton_Click` 中打开。

3. 在事件处理程序中键入 `ReadXmlButton_Click` 以下代码：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/CS/Form1.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/VB/Form1.vb" id="Snippet2":::

4. 在 `ReadXMLButton_Click` 事件处理程序代码中，将 `filepath =` 条目更改为正确的路径。

## <a name="create-the-event-handler-to-display-the-schema-in-the-textbox"></a>创建事件处理程序以在文本框中显示架构

" **显示** 架构"按钮创建一个用架构 <xref:System.IO.StringWriter> 填充并显示在 控件 <xref:System.Windows.Forms.TextBox> 中的 对象。

1. 在 **解决方案资源管理器** 中，选择 **"Form1"，****然后选择"视图设计器** 按钮。

2. 选择" **显示架构"** 按钮。

     代码 **编辑器将在** 事件处理程序 `ShowSchemaButton_Click` 中打开。

3. 将下面的代码粘贴到 `ShowSchemaButton_Click` 事件处理程序中。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/CS/Form1.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/VB/Form1.vb" id="Snippet3":::

## <a name="test-the-form"></a>测试窗体

现在可以测试窗体，以确保其行为与预期一样。

1. 选择 **F5** 以运行应用程序。

2. 选择" **读取 XML"** 按钮。

     DataGridView 显示 XML 文件的内容。

3. 选择" **显示架构"** 按钮。

     文本框显示 XML 文件的 XML 架构。

## <a name="next-steps"></a>后续步骤

本演练将指导你了解将 XML 文件读取到数据集以及基于 XML 文件内容创建架构的基础知识。 下面是一些下一步可能执行的任务：

- 编辑数据集中的数据，并写回 XML 格式。 有关详细信息，请参阅 <xref:System.Data.DataSet.WriteXml%2A>。

- 编辑数据集中的数据，并写出到数据库。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
- [Visual Studio 中的 XML 工具](../xml-tools/xml-tools-in-visual-studio.md)
