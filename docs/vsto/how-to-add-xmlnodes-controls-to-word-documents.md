---
title: 如何：将 XMLNodes 控件添加到 Word 文档
description: 请注意，当您将重复的 XML 架构元素映射到 Microsoft Office Word 文档时，Visual Studio 会自动将 XMLNodes 控件添加到文档中。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLNodes control, adding to documents
- controls [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 69320f9734951bae3af6a4bf5447302435db1541
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122122847"
---
# <a name="how-to-add-xmlnodes-controls-to-word-documents"></a>如何：将 XMLNodes 控件添加到 Word 文档
  **重要提示** 本主题中的关于 Microsoft Word 的信息是专门针对美国及其区域以外的个人和组织的权益和使用的，或者开发在上运行的程序 Microsoft Word （在2010年1月之前，microsoft 从 Microsoft Word 中的自定义 XML 删除了特定功能的实现。 对于在2010年1月10日之后使用、或开发 Microsoft Word 的程序 Microsoft Word 产品的美国或其所在区域中的个人或组织，可能无法读取或使用与有关的信息。对于该日期之前许可的产品，这些产品的行为并不相同，也不会在美国之外购买和许可。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 将重复的 XML 架构元素映射到 Microsoft Office Word 文档时，Visual Studio 会自动将 <xref:Microsoft.Office.Tools.Word.XMLNodes> 控件添加到文档中。

 有关映射非重复 XML 架构元素的信息，请参阅 [如何：向 Word 文档添加 XMLNode 控件](../vsto/how-to-add-xmlnode-controls-to-word-documents.md)。

> [!NOTE]
> 控件在 " <xref:Microsoft.Office.Tools.Word.XMLNodes> **工具箱** " 或 " **数据源** " 窗口中不可用，也不能以编程方式创建。

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-add-an-xmlnodes-control-to-a-document"></a>向文档中添加 XMLNodes 控件

1. 在 Visual Studio 设计器的文档中，单击功能区上的 "**开发人员**" 选项卡。

    > [!NOTE]
    > 如果看不到 **“开发人员”** 选项卡，则必须首先显示它。 有关详细信息，请参阅 [如何：在功能区上显示 "开发人员" 选项卡](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)。

2. 在 " **XML** " 组中，单击 " **架构**"。

     此时将打开 " **模板和外接程序** " 对话框。

3. 单击 " **XML 架构** " 选项卡。

4. 单击 " **添加架构**"。

     " **添加架构** " 对话框随即打开。

5. 选择包含重复架构元素的 XML 架构，并单击 " **打开**"。

     此时将显示 "**架构设置**" 对话框。

6. 分配一个别名，或者单击 **"确定"** 以添加没有别名的架构。

     架构将添加到 " **添加架构** " 对话框中。

7. 在 " **添加架构** " 对话框中，单击 **"确定"**。

     此时将打开 " **XML 结构** " 任务窗格。

8. 单击 " **XML 结构** " 任务窗格中的 "重复架构" 元素，将其添加到文档中。

     <xref:Microsoft.Office.Tools.Word.XMLNodes>创建一个控件，并将其添加到该项目中。

## <a name="see-also"></a>请参阅
- [XMLNodes 控件](../vsto/xmlnodes-control.md)
- [使用扩展对象实现 Word 自动化](../vsto/automating-word-by-using-extended-objects.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
