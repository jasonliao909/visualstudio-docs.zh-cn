---
title: 如何：在工作表中滚动浏览数据库记录
description: 了解如何使用设计器在工作表中的数据库表中显示Microsoft Excel字段
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- databases [Office development in Visual Studio], scrolling records
- records [Office development in Visual Studio], scrolling
- data [Office development in Visual Studio], scrolling database records
- worksheets [Office development in Visual Studio], scrolling records
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: abe1ff62b651c8f8456eea0e3a5ca83e37b70d9d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122032675"
---
# <a name="how-to-scroll-through-database-records-in-a-worksheet"></a>如何：在工作表中滚动浏览数据库记录
  以下过程演示如何使用设计器在 Microsoft Office Excel 工作表中显示数据库表中的单个字段，以及使最终用户能够滚动浏览所有记录的控件。

 只能在文档级项目中使用设计器。 但是，还可以添加控件，并运行时以编程方式将其绑定到数据。 有关详细信息，请参阅演练：在外接程序项目中VSTO[数据绑定](../vsto/walkthrough-simple-data-binding-in-vsto-add-in-project.md)。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

## <a name="to-scroll-through-database-records-in-a-worksheet"></a>滚动浏览工作表中的数据库记录

1. 在 Visual Studio 中打开 Excel 应用程序项目。

2. 打开 **"数据源"** 窗口，从数据库创建数据源。 有关详细信息，请参阅 [添加新连接](../data-tools/add-new-connections.md)。

3. 展开包含要显示的数据的表，然后选择特定列。

4. 打开控件列表，然后选择 **"NamedRange"。**

5. 将 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件拖到要显示数据的单元格上。

6. 从Windows **的**"窗体"选项卡中，将控件添加到工作表，并设置 <xref:System.Windows.Forms.BindingNavigator> 想要使用的控件。 有关详细信息，请参阅[BindingNavigator 控件概述&#40;Windows窗体&#41;。 ](/dotnet/framework/winforms/controls/bindingnavigator-control-overview-windows-forms)

## <a name="see-also"></a>请参阅
- [将数据绑定到解决方案中的Office控件](../vsto/binding-data-to-controls-in-office-solutions.md)
