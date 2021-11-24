---
title: 连接到 Access 数据库中的数据
description: 了解如何在 Visual Studio 中连接到 Access 数据库（.mdb 文件或 .accdb 文件）。
ms.custom: SEO-VS-2020
ms.date: 11/02/2021
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
ms.openlocfilehash: 335801a800bd0df15dabda447338d452bff53268
ms.sourcegitcommit: aff49629012f4d5fa07c75ea0ca5bf53d28aa173
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2021
ms.locfileid: "131662424"
---
# <a name="connect-to-data-in-an-access-database"></a>连接到 Access 数据库中的数据

可以通过使用 Visual Studio 连接到 Access 数据库（.mdb 文件或 .accdb 文件）。  在定义此连接后，数据会显示在“数据源”窗口中。 可从该位置将表或视图拖动到设计图面上。
::: moniker range="vs-2017"
> [!NOTE]
> 如果正在使用 Visual Studio 链接到 Access 数据库，将需要注意低于 Visual Studio 2022 的 Visual Studio 版本都是 32 位进程。
>
> 这意味着，Visual Studio 中的某些数据工具将只能使用 32 位数据提供程序连接到 Access 数据库。

::: moniker-end

::: moniker range=">=vs-2019"
> [!NOTE]
>如果正在使用 Visual Studio 链接到 Access 数据库，将需要注意低于 Visual Studio 2022 的 Visual Studio 版本都是 32 位进程。 这意味着，Visual Studio 2019 及更低版本中的某些数据工具将只能使用 32 位数据提供程序连接到 Access 数据库。
>
>如果使用 Visual Studio 2022 连接到 Access 数据库，则需要注意 Visual Studio 2022 现在是 64 位进程。 这意味着，Visual Studio 中的某些数据工具将无法使用 32 位数据提供程序连接到 Access 数据库。
>
>如果需要维护连接到 Access 数据库的 32 位应用程序，仍可以使用 Visual Studio 2022 生成并运行该应用程序。 但是，如果需要使用任何 Visual Studio 数据工具（如服务器资源管理器、数据源向导或数据集设计器），则需要使用仍为 32 位进程的 Visual Studio 的早期版本。 32 位进程的 Visual Studio 的上一版本为 Visual Studio 2019。
>
>如果计划将项目转换为 64 位进程，则建议使用 64 位 Microsoft Access 数据库引擎，也称为访问连接引擎 (ACE)。 有关详细信息，请参阅[仅适用于 Jet 和 ODBC 驱动程序的 OLE DB 提供程序为 32 位版本](/office/troubleshoot/access/jet-odbc-driver-available-32-bit-version)。

::: moniker-end

## <a name="prerequisites"></a>先决条件

若要使用这些过程，需要 Windows 窗体或 WPF 项目，亦或 Access 数据库（.accdb 文件）或 Access 2000 - 2003 数据库（.mdb 文件） 。 按照与你的文件类型对应的过程操作。

:::moniker range=">=vs-2022"
## <a name="create-a-dataset-for-an-accdb-file"></a>为 .accdb 文件创建数据集

通过使用以下过程，可以连接到使用 Microsoft 365、Access 2016、Access 2013、Access 2010 或 Access 2007 创建的数据库。

1. 在 Visual Studio 中打开 Windows 窗体或 WPF 应用程序项目。

2. 若要打开“数据源”窗口，请按 Ctrl+Q，在搜索框中输入“数据”，然后选择“数据源”窗口   。 或在“查看”菜单中，选择“其他窗口” > “数据源”。 或在键盘上按 Shift+Alt+D  。

   ![搜索框中“数据源”的屏幕截图](../data-tools/media/vs-2022/view-data-sources.png)

3. 在 **“数据源”** 窗口中，单击 **“添加新数据源”**。

   “数据源配置”向导随即打开。

   ![显示“数据源配置向导”的屏幕截图](media/vs-2022/data-source-configuration-wizard.png)

4. 在“选择数据源类型”页上，选择“数据库”，然后选择“下一步”。  

5. 在“选择数据库模型”页上，选择“数据集”，然后选择“下一步”。  

   ![“选择数据库模型”页面的屏幕截图](media/vs-2022/data-source-configuration-wizard-2.png)

6. 在“选择数据连接”页面上选择“新建连接”，配置一个新的数据连接。

   ![“选择数据连接”页面的屏幕截图](media/vs-2022/data-source-configuration-wizard-3.png)

   随即会打开“添加连接”对话框。

   ![“添加连接”对话框的屏幕截图](media/vs-2022/add-connection.png)

7. 如果“数据源”未设置为“Microsoft Access 数据库文件”，则选择“更改”按钮。  

   “选择数据源”对话框随即打开。 在数据源列表中，选择“Microsoft Access 数据库文件”。 已预先选择了“适用于 OLE DB 的 .NET Framework 数据提供程序”选项。 选择 **“确定”** 。

   ![“选择数据源”对话框的屏幕截图](media/vs-2022/change-data-source.png)

8. 选择“数据库文件名称”旁边的“浏览”，然后导航到 .accdb 文件并选择“打开”。 

   >[!NOTE]
   > 如果 Microsoft Office 和 Visual Studio 的位数（32 位或 64 位）不匹配，你将在连接到 Access 数据库时看到错误。 在 Visual Studio 2019 中，你将收到指出数据库提供程序未注册的错误。 在 Visual Studio 2022 中，你将看到指出无法连接到 32 位数据提供程序的错误。 若要解决此错误，请确保在使用 32 位版本的 Office 时使用 Visual Studio 2019 或更低版本；对于 64 位版本的 Office，则需要 Visual Studio 2022 或更高版本。

9. 输入用户名和密码（如有必要），然后选择“确定”。

10. 在“选择你的数据连接”页上，选择“下一步”。 

    你可能会看到一个对话框，告知你当前项目中没有数据文件。 选择“是”或“否” 。

11. 在“将连接字符串保存到应用程序配置文件中”页上，选择“下一步” 。

    ![页面的屏幕截图](media/vs-2022/data-source-configuration-wizard-4.png)

12. 在“选择数据库对象”页面上展开“表”节点。

    ![“选择数据库对象”页面的屏幕截图](media/vs-2022/choose-your-database-objects.png)

13. 选择要包含在数据集中的表或视图，然后选择“完成”。

    数据集将添加到项目中，并且“数据源”窗口中将显示表和视图。

    ![“数据源”窗口的屏幕截图，其中填充了数据库对象](media/vs-2022/data-sources-window-populated.png)
:::moniker-end

:::moniker range="vs-2019"

## <a name="create-a-dataset-for-an-accdb-file"></a>为 .accdb 文件创建数据集

通过使用以下过程，可以连接到使用 Microsoft 365、Access 2016、Access 2013、Access 2010 或 Access 2007 创建的数据库。

1. 在 Visual Studio 中打开 Windows 窗体或 WPF 应用程序项目。

2. 若要打开“数据源”窗口，请按 Ctrl+Q，在搜索框中输入“数据”，然后选择“数据源”窗口   。 或在“查看”菜单中，选择“其他窗口” > “数据源”。 或在键盘上按 Shift+Alt+D  。

   ![查看其他 Windows 数据源](../data-tools/media/viewdatasources.png)

3. 在 **“数据源”** 窗口中，单击 **“添加新数据源”**。

   “数据源配置”向导随即打开。

4. 在“选择数据源类型”页上，选择“数据库”，然后选择“下一步”。  

5. 在“选择数据库模型”页上，选择“数据集”，然后选择“下一步”。  

   ![“选择数据库模型”页面的屏幕截图](media/vs-2022/data-source-configuration-wizard-2.png)

6. 在“选择数据连接”页面上选择“新建连接”，配置一个新的数据连接。

   ![“选择数据连接”页面的屏幕截图](media/vs-2022/data-source-configuration-wizard-3.png)

   随即会打开“添加连接”对话框。

   ![“添加连接”对话框的屏幕截图](media/vs-2022/add-connection.png)

7. 如果“数据源”未设置为“Microsoft Access 数据库文件”，则选择“更改”按钮。  

   “选择数据源”对话框随即打开。 在数据源列表中，选择“Microsoft Access 数据库文件”。 已预先选择了“适用于 OLE DB 的 .NET Framework 数据提供程序”选项。 选择 **“确定”** 。

   ![“选择数据源”对话框的屏幕截图](media/vs-2022/choose-data-source.png)

8. 选择“数据库文件名称”旁边的“浏览”，然后导航到 .accdb 文件并选择“打开”。 

   >[!NOTE]
   > 如果 Microsoft Office 和 Visual Studio 的位数（32 位或 64 位）不匹配，你将在连接到 Access 数据库时看到错误。 在 Visual Studio 2019 中，你将收到指出数据库提供程序未注册的错误。 在 Visual Studio 2022 中，你将看到指出无法连接到 32 位数据提供程序的错误。 若要解决此错误，请确保在使用 32 位版本的 Office 时使用 Visual Studio 2019 或更低版本；对于 64 位版本的 Office，则需要 Visual Studio 2022 或更高版本。

9. 输入用户名和密码（如有必要），然后选择“确定”。

10. 在“选择你的数据连接”页上，选择“下一步”。 

    你可能会看到一个对话框，告知你当前项目中没有数据文件。 选择“是”或“否” 。

11. 在“将连接字符串保存到应用程序配置文件中”页上，选择“下一步” 。

    ![页面的屏幕截图](media/vs-2022/data-source-configuration-wizard-4.png)

12. 在“选择数据库对象”页面上展开“表”节点。

13. 选择要包含在数据集中的表或视图，然后选择“完成”。

    数据集将添加到项目中，并且“数据源”窗口中将显示表和视图。

:::moniker-end

:::moniker range="vs-2017"

## <a name="create-a-dataset-for-an-accdb-file"></a>为 .accdb 文件创建数据集

通过使用以下过程，可以连接到使用 Microsoft 365、Access 2013、Access 2010 或 Access 2007 创建的数据库。

1. 在 Visual Studio 中打开 Windows 窗体或 WPF 应用程序项目。

2. 若要打开“数据源”窗口，请按 Ctrl+Q，在搜索框中输入“数据”，然后选择“数据源”窗口   。 或在“查看”菜单中，选择“其他窗口” > “数据源”。 或在键盘上按 Shift+Alt+D  。

3. 在 **“数据源”** 窗口中，单击 **“添加新数据源”**。

   “数据源配置”向导随即打开。

4. 在“选择数据源类型”页上，选择“数据库”，然后选择“下一步”。  

5. 在“选择数据库模型”页上，选择“数据集”，然后选择“下一步”。  

6. 在“选择数据连接”页面上选择“新建连接”，配置一个新的数据连接。

   随即会打开“添加连接”对话框。

7. 如果“数据源”未设置为“Microsoft Access 数据库文件”，则选择“更改”按钮。  

   “选择数据源”对话框随即打开。 在数据源列表中，选择“Microsoft Access 数据库文件”。 在“数据提供程序”下拉列表中，选择“适用于 OLE DB 的 .NET Framework 数据提供程序”，然后选择“确定”。  

8. 选择“数据库文件名称”旁边的“浏览”，然后导航到 .accdb 文件并选择“打开”。 

9. 输入用户名和密码（如有必要），然后选择“确定”。

10. 在“选择你的数据连接”页上，选择“下一步”。 

    你可能会看到一个对话框，告知你当前项目中没有数据文件。 选择“是”或“否” 。

11. 在“将连接字符串保存到应用程序配置文件中”页上，选择“下一步” 。

12. 在“选择数据库对象”页面上展开“表”节点。

13. 选择要包含在数据集中的表或视图，然后选择“完成”。

    数据集将添加到项目中，并且“数据源”窗口中将显示表和视图。

::: moniker-end

## <a name="create-a-dataset-for-an-mdb-file"></a>为 .mdb 文件创建数据集

通过使用以下过程，连接到使用 Access 2000 - 2003 创建的数据集。

1. 在 Visual Studio 中打开 Windows 窗体或 WPF 应用程序项目。

2. 在“查看”菜单中，选择“其他窗口” > “数据源”。

3. 在 **“数据源”** 窗口中，单击 **“添加新数据源”**。

    “数据源配置”向导随即打开。

4. 在“选择数据源类型”页上，选择“数据库”，然后选择“下一步”。  

5. 在“选择数据库模型”页上，选择“数据集”，然后选择“下一步”。  

6. 在“选择数据连接”页面上选择“新建连接”，配置一个新的数据连接。

7. 如果数据源不是“Microsoft Access 数据库文件(OLE DB)”，请选择“更改”以打开“更改数据源”对话框，并选择“Microsoft Access 数据库文件”，然后选择“确定”。    

8. 在“数据库文件名”中，指定要连接到的 .mdb 文件的路径和名称，然后选择“确定”。

   ![添加连接访问数据库文件](../data-tools/media/add-connection-access-db.png)

9. 在“选择你的数据连接”页上，选择“下一步”。 

10. 在“将连接字符串保存到应用程序配置文件中”页上，选择“下一步” 。

11. 在“选择数据库对象”页面上展开“表”节点。

12. 选择要包含在数据集中的任何表或视图，然后选择“完成”。

    数据集将添加到项目中，并且“数据源”窗口中将显示表和视图。

## <a name="next-steps"></a>后续步骤

刚刚创建的数据集出现在“数据源”窗口中。 现在可以执行以下任何任务：

- 在“数据源”窗口中选择项并将其拖到窗体或设计图面上（请参阅[在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)或 [WPF 数据绑定概述](/dotnet/desktop-wpf/data/data-binding-overview)）。

- 在数据集设计器中打开数据源，以便添加或编辑组成数据集的对象。

- 向该数据集中数据表的 <xref:System.Data.DataTable.ColumnChanging> 或 <xref:System.Data.DataTable.RowChanging> 事件添加验证逻辑（请参阅[验证数据集中的数据](../data-tools/validate-data-in-datasets.md)）。

## <a name="see-also"></a>另请参阅

- [添加连接](../data-tools/add-new-connections.md)
- [WPF 数据绑定概述](/dotnet/framework/wpf/data/data-binding-overview)
- [Windows 窗体数据绑定](/dotnet/framework/winforms/data-binding-and-windows-forms)
