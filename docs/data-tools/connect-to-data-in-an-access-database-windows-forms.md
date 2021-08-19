---
title: 连接到 Access 数据库中的数据
description: 了解如何连接到 Access 数据库中的数据， (.mdb 文件或 .accdb.file) 文件Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 07/18/2019
ms.topic: how-to
helpviewer_keywords:
- data [Visual Studio], connecting
- connecting to data, Access databases
- Access databases, connecting
ms.assetid: 4159e815-d430-4ad0-a234-e4125fcbef18
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: b8280c29649a792839e2bc18a409e76f276b71e4
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122154935"
---
# <a name="connect-to-data-in-an-access-database"></a>连接到 Access 数据库中的数据

可以使用 *.mdb (.accdb* 文件或 *.accdb* 文件) Access 数据库Visual Studio。 在定义此连接后，数据会显示在“数据源”窗口中。 可以在那里将表或视图拖动到设计图面上。

## <a name="prerequisites"></a>必备条件

若要使用这些过程，需要 Windows Forms 或 WPF 项目以及 Access 数据库 (*.accdb* 文件) 或 Access 2000-2003 数据库 (*.mdb*) 。 按照与你的文件类型对应的过程操作。

## <a name="create-a-dataset-for-an-accdb-file"></a>为 .accdb 文件创建数据集

连接以下过程Microsoft 365使用 Microsoft 365、Access 2013、Access 2010 或 Access 2007 创建的数据库。

1. 在 Windows 中打开一个窗体或 WPF Visual Studio。

2. 若要打开"**数据源"窗口**，请在"视图 **"** 菜单上，选择"其他Windows  >  **数据源"。**

   ![查看其他 Windows 数据源](../data-tools/media/viewdatasources.png)

3. 在 **“数据源”** 窗口中，单击 **“添加新数据源”**。

   " **数据源配置向导"随即** 打开。

4. 在 **"选择** 数据源 **类型"页上选择**"数据库"，然后选择"下一 **步"。**

5. 在 **"选择** 数据库 **模型"页上** 选择"数据集"，然后选择"下一 **步"。**

6. 在“选择数据连接”页面上选择“新建连接”，配置一个新的数据连接。

   随即会打开“添加连接”对话框。

7. 如果 **"数据源** "未设置为 **"Microsoft Access 数据库文件"，** 请选择" **更改"** 按钮。

   " **更改数据源"** 对话框随即打开。 在数据源列表中，选择 **"Microsoft Access 数据库文件"。** 在"**数据提供程序"** 下拉列表中，选择.NET Framework **数据提供程序OLE DB，然后选择**"确定 **"。**

8. 选择 **"** 数据库文件名 **"旁边的"浏览"，** 然后导航到 *.accdb* 文件，然后选择"打开 **"。**

9. 如有必要，输入用户名和密码 (输入) ，然后选择"确定 **"。**

10. 在 **"选择** 数据 **连接"页上选择"下一步** "。

    可能会看到一个对话框，告知数据文件不在当前项目中。 选择 **"是"** 或"**否"。**

11. 在 **"将** 连接字符串 **保存到应用程序配置文件"页上选择"下一步** "。

12. 在“选择数据库对象”页面上展开“表”节点。

13. 选择要包括在数据集中的表或视图，然后选择"完成 **"。**

    数据集将添加到项目中，并且“数据源”窗口中将显示表和视图。

## <a name="create-a-dataset-for-an-mdb-file"></a>为 .mdb 文件创建数据集

连接以下过程，将 数据库还原到使用 Access 2000-2003 创建的数据库。

1. 在 Windows 中打开一个窗体或 WPF Visual Studio。

2. 在"视图 **"** 菜单上，选择 **"其他Windows**  >  **数据源"。**

   ![查看其他 Windows 数据源](../data-tools/media/viewdatasources.png)

3. 在 **“数据源”** 窗口中，单击 **“添加新数据源”**。

    " **数据源配置向导"随即** 打开。

4. 在 **"选择** 数据源 **类型"页上选择**"数据库"，然后选择"下一 **步"。**

5. 在 **"选择** 数据库 **模型"页上** 选择"数据集"，然后选择"下一 **步"。**

6. 在“选择数据连接”页面上选择“新建连接”，配置一个新的数据连接。

7. 如果数据源不是 Microsoft **Access** 数据库文件 (OLE DB) ，请选择"更改"以打开"更改数据源"对话框，然后选择 **"Microsoft Access 数据库** 文件"，然后选择"确定 **"。**

8. 在 **"数据库文件名"** 中，指定要连接到 *的 .mdb* 文件的路径和名称，然后选择"确定 **"。**

   ![添加连接访问数据库文件](../data-tools/media/add-connection-access-db.png)

9. 在 **"选择** 数据 **连接"页上选择"下一步** "。

10. 在 **"将** 连接字符串 **保存到应用程序配置文件"页上选择"下一步** "。

11. 在“选择数据库对象”页面上展开“表”节点。

12. 在数据集中选择所需的任何表或视图，然后选择"完成 **"。**

    数据集将添加到项目中，并且“数据源”窗口中将显示表和视图。

## <a name="next-steps"></a>后续步骤

刚刚创建的数据集在"数据源" **窗口中** 可用。 现在可以执行以下任何任务：

- 在"数据源"窗口中选择项，并将其拖动到窗体或设计图面上 (请参阅将 Windows 窗体控件绑定到[Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)或[WPF](/dotnet/desktop-wpf/data/data-binding-overview)数据绑定概述) 。

- 在数据集设计器中打开数据源，以便添加或编辑组成数据集的对象。

- 将验证逻辑添加到数据集 <xref:System.Data.DataTable.ColumnChanging> 中数据表的 <xref:System.Data.DataTable.RowChanging> 或 事件， (验证数据集[中的数据) 。](../data-tools/validate-data-in-datasets.md)

## <a name="see-also"></a>请参阅

- [添加连接](../data-tools/add-new-connections.md)
- [WPF 数据绑定概述](/dotnet/framework/wpf/data/data-binding-overview)
- [Windows窗体数据绑定](/dotnet/framework/winforms/data-binding-and-windows-forms)
