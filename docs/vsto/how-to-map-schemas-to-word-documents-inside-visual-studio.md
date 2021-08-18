---
title: 如何：将架构映射到 Visual Studio 中的 Word 文档
description: 了解如何在 Visual Studio 中打开文档时，如何将 XML 架构映射到 Microsoft Office Word 文档中。
titleSuffix: ''
ms.custom: seodec18, SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XML schemas [Office development in Visual Studio], mapping
- mappings [Office development in Visual Studio], XML schemas to Word documents
- Word [Office development in Visual Studio], mapping XML schemas
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: e14283c61480796e58cd2f5df0b055fb66ce2ac5
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122083435"
---
# <a name="how-to-map-schemas-to-word-documents-inside-visual-studio"></a>如何：将架构映射到 Visual Studio 中的 Word 文档
  **重要提示** 本主题中的关于 Microsoft Word 的信息是专门针对美国及其区域以外的个人和组织的权益和使用的，或者开发在上运行的程序 Microsoft Word （在2010年1月之前，microsoft 从 Microsoft Word 中的自定义 XML 删除了特定功能的实现。 对于在2010年1月10日之后使用、或开发 Microsoft Word 的程序 Microsoft Word 产品的美国或其所在区域中的个人或组织，可能无法读取或使用与有关的信息。对于该日期之前许可的产品，这些产品的行为并不相同，也不会在美国之外购买和许可。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 在 Visual Studio 中打开文档时，可以将 XML 架构映射到文档。 使用与在 Visual Studio 外打开文档时使用的相同 Microsoft Office Word 工具。 无论在创建 Word 解决方案之前还是之后将架构映射到文档，Office 项目都将创建相同的对象。

## <a name="to-map-an-xml-schema-to-a-word-document-in-visual-studio"></a>若要将 XML 架构映射到 Visual Studio 中的 Word 文档

1. 在 Visual Studio 中打开 Word 文档或模板项目。

2. 在文档中单击以将焦点移到设计器。

3. 在功能区上，单击 " **开发人员** " 选项卡。

    > [!NOTE]
    > 如果看不到 **“开发人员”** 选项卡，则必须首先显示它。 有关详细信息，请参阅 [如何：在功能区上显示 "开发人员" 选项卡](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)。

4. 在 " **XML** " 组中，单击 " **架构**"。

     此时将打开 " **模板和外接程序** " 对话框。

5. 单击 " **XML 架构** " 选项卡。

6. 单击 " **添加架构**"。

     " **添加架构** " 对话框随即打开。

7. 浏览到您的架构文件，选择它，然后单击 " **打开**"。

     此时将打开 "**架构设置**" 对话框。

8. 分配一个别名，或者单击 **"确定"** 以添加没有别名的架构。

9. 单击“确定”。

     此时将打开 " **XML 结构** " 窗口。

10. 将元素从 " **XML 结构** " 窗口拖到您要在其中创建相应控件的文档中的位置。

## <a name="see-also"></a>请参阅
- [如何：将架构映射到 Visual Studio 中的工作表](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)
- [文档级自定义项中的 XML 架构和数据](../vsto/xml-schemas-and-data-in-document-level-customizations.md)
