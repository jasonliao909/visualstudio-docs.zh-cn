---
title: 如何：将架构映射到文档中的 Word Visual Studio
description: 了解如何在文档打开时将 XML 架构Microsoft Office Word 文档Visual Studio。
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
ms.openlocfilehash: 46948fe54142dcffb1b90290c01feefd770b4ae89648e98157694ccf18c3760a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121408807"
---
# <a name="how-to-map-schemas-to-word-documents-inside-visual-studio"></a>如何：将架构映射到文档中的 Word Visual Studio
  **重要** 本主题中介绍的关于 Microsoft Word 的信息专门供位于 美国 及其区域之外、正在使用或开发运行于 2010 年 1 月之前由 Microsoft 许可的 Microsoft Word 产品（当 Microsoft 从 Microsoft Word 中删除与自定义 XML 相关的特定功能的实现时）的个人或组织受益和使用。 有关 Microsoft Word 的信息不能由 美国 或其区域使用或开发在 2010 年 1 月 10 日之后由 Microsoft 许可的 Microsoft Word 产品运行的程序的个人或组织读取或使用;这些产品的行为与该日期之前许可的产品或购买和许可在产品外部使用的产品美国。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 可以在打开文档时将 XML 架构映射到文档Visual Studio。 使用在Microsoft Office外部打开文档时使用的 Word 工具Visual Studio。 无论Office Word 解决方案之前或之后将架构映射到文档，项目都创建相同的对象。

## <a name="to-map-an-xml-schema-to-a-word-document-in-visual-studio"></a>将 XML 架构映射到文档中的 Word Visual Studio

1. 打开 Word 文档或模板项目Visual Studio。

2. 单击文档以将焦点移动到设计器。

3. 在功能区上，单击" **开发人员"** 选项卡。

    > [!NOTE]
    > 如果看不到 **“开发人员”** 选项卡，则必须首先显示它。 有关详细信息，请参阅 [功能区 上的"如何：显示开发人员"选项卡](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)。

4. 在 **XML 组中**，单击"架构 **"。**

     " **模板和外接程序"** 对话框随即打开。

5. 单击 **"XML 架构"** 选项卡。

6. 单击"**添加架构"。**

     " **添加架构"** 对话框随即打开。

7. 浏览到架构文件，将其选中，然后单击"打开 **"。**

     "**架构设置** 对话框随即打开。

8. 分配别名或单击 **"确定** "以添加不带别名的架构。

9. 单击“确定”。

     "XML **结构"** 窗口随即打开。

10. 将元素从 **"XML 结构** "窗口拖到文档中要创建相应控件的位置。

## <a name="see-also"></a>请参阅
- [如何：将架构映射到工作表中的Visual Studio](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)
- [文档级自定义项中的 XML 架构和数据](../vsto/xml-schemas-and-data-in-document-level-customizations.md)
