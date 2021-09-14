---
title: 如何：在功能区上显示"开发人员"选项卡
description: 了解如何使用 Visual Studio 在文档的功能区上以编程方式Microsoft Word选项卡。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Ribbon [Office development in Visual Studio], tabs
- Developer tab [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 382f9f62367734785c997989fb96ccf6414e9360
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664703"
---
# <a name="how-to-show-the-developer-tab-on-the-ribbon"></a>如何：在功能区上显示"开发人员"选项卡
  若要 **访问应用程序** 功能区上的Office选项卡，必须将其配置为显示该选项卡，因为它默认不显示。 例如，如果要向 Word 的文档级自定义项添加一个 <xref:Microsoft.Office.Tools.Word.GroupContentControl>，则必须显示该选项卡。

> [!NOTE]
> 本指南仅适用于 Office 2010 或更高版本的应用程序。 如果要在 2007 Microsoft Office System 中显示此选项卡，请参阅本主题的以下版本如何：在功能区 上显示"开发人员["选项卡](https://web.archive.org/web/20140303033431/msdn.microsoft.com/library/bb608625(v=vs.90).aspx
)。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

> [!NOTE]
> 访问权限没有"开发人员 **"** 选项卡。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="to-show-the-developer-tab"></a>显示“开发工具”选项卡

1. 启动本主题支持的任何 Office 应用程序。 请参阅 **本主题前面部分** 中的"适用范围：注意"。

2. 在" **文件"** 选项卡上，选择" **选项"** 按钮。

     下图显示了 2010年 1 月中的"文件"选项卡和Office按钮。 

     ![在 Outlook 2010 中选择“文件”、“选项”](../vsto/media/vsto-office-file-tab.png "在 Outlook 2010 中选择“文件”、“选项”")

     下图显示了 2013 年 1 月Office选项卡。 

     ![Outlook 2013 中的“文件”选项卡](../vsto/media/vsto-office2013-filetab.png "Outlook 2013 中的“文件”选项卡")

     下图显示了 2013 Office中的"选项"按钮。 

     ![Outlook 2013 Preview 中的“选项”按钮](../vsto/media/vsto-office2013-optionsbutton.png "Outlook 2013 Preview 中的“选项”按钮")

3. 在 _"ApplicationName_**选项"** 对话框中，选择" **自定义功能区"** 按钮。

     下图显示了 2010 年1 月中的"选项"对话框和"自定义功能Excel按钮。  此按钮的位置在本主题顶部附近“适用于”部分中列出的所有其他应用程序中是类似的。

     ![“自定义功能区”按钮](../vsto/media/vsto-office2010-customizeribbonbutton.png "“自定义功能区”按钮")

4. 在主选项卡列表中，选中"开发人员 **"** 复选框。

     下图显示了 Word  2010 和 中的"开发人员"复选框 [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] 。 此复选框的位置在本主题顶部附近“适用于”部分中列出的所有其他应用程序中是类似的。

     ![“Word 选项”对话框中的“开发人员”复选框](../vsto/media/vsto-office2010-developercheckbox.png "“Word 选项”对话框中的“开发人员”复选框")

5. 选择" **确定"** 按钮以关闭 **"选项"** 对话框。

## <a name="see-also"></a>另请参阅
- [OfficeUI 自定义](../vsto/office-ui-customization.md)
