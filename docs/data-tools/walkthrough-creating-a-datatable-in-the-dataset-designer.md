---
title: 在数据集设计器中创建 DataTable
description: 在本演练中，将使用数据集设计器创建 DataTable（不包含 TableAdapter）。 创建一个新的 Windows 窗体应用程序，并将新的数据集添加到该应用程序。
ms.custom: SEO-VS-2020
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- DataTable objects, creating
- Dataset Designer, creating data tables
- tables [Visual Studio], creating
- data [Visual Studio], Dataset Designer
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 6f93279bd67a8e293d3883e573ad6dbb8aee8ccc
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601061"
---
# <a name="walkthrough-create-a-datatable-in-the-dataset-designer"></a>演练：在数据集设计器中创建数据表

本演练说明如何使用数据集设计器创建 <xref:System.Data.DataTable>（不包含 TableAdapter）。 有关创建包含 TableAdapter 的数据表的信息，请参阅[创建和配置 TableAdapter](../data-tools/create-and-configure-tableadapters.md)。

## <a name="create-a-new-windows-forms-application"></a>创建新的 Windows 窗体应用程序

1. 在 Visual Studio 的“文件”菜单中，依次选择“新建” > “项目”    。

2. 在左侧窗格中展开“Visual C#”或“Visual Basic”，然后选择“Windows 桌面”  。

3. 在中间窗格中，选择“Windows 窗体应用”项目类型。

4. 将项目命名为“DataTableWalkthrough”，然后选择“确定” 。

     “DataTableWalkthrough”项目即被创建并添加到“解决方案资源管理器”中 。

## <a name="add-a-new-dataset-to-the-application"></a>向应用程序添加新的数据集

1. 在“项目”菜单上，选择“添加新项”。

     此时会显示“添加新项”对话框。

2. 在左侧窗格中，选择“数据”，然后在中间窗格中选择“数据集” 。

3. 选择“添加”。

     Visual Studio 会将名为 DataSet1.xsd 的文件添加到项目中，并在“数据集设计器”中打开它 。

## <a name="add-a-new-datatable-to-the-dataset"></a>向数据集添加新 DataTable

1. 将 DataTable 从“工具箱”的“数据集”选项卡拖到“数据集设计器”上   。

     将名为 DataTable1 的表添加到数据集。

2. 单击 DataTable1 的标题栏，并将其重命名为 `Music`。

## <a name="add-columns-to-the-datatable"></a>将列添加到 DataTable

1. 右键单击“Music”表。 指向“添加”，然后单击“列” 。

2. 将列命名为 `SongID`。

3. 在“属性”  窗口中，将 <xref:System.Data.DataColumn.DataType%2A> 属性设置为 <xref:System.Int16?displayProperty=fullName>。

4. 重复此过程并添加以下列：

     `SongTitle`: <xref:System.String?displayProperty=fullName>

     `Artist`: <xref:System.String?displayProperty=fullName>

     `Genre`: <xref:System.String?displayProperty=fullName>

## <a name="set-the-primary-key-for-the-table"></a>设置表的主键

所有数据表都应有一个主键。 主键用于唯一标识数据表中的特定记录。

若要设置主键，请右键单击“SongID”列，然后单击“设置主键” 。 此时 SongID 列旁将显示一个“键”图标。

## <a name="save-your-project"></a>保存项目

若要保存 DataTableWalkthrough 项目，请在“文件”菜单上，选择“全部保存”  。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中创建和配置数据集](../data-tools/create-and-configure-datasets-in-visual-studio.md)
- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [验证数据](../data-tools/validate-data-in-datasets.md)
