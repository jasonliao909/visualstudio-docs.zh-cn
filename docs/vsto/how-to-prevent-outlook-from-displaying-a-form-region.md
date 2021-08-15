---
title: 如何：阻止 Outlook 显示窗体区域
description: 了解如何防止 Microsoft Office Outlook 显示特定项的窗体区域。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], canceling display
- canceling form region display
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 331667013d5591f57d96b9f1bfa5f7542042ecc072c2eb650bf2ae5bbd0292a0
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121408794"
---
# <a name="how-to-prevent-outlook-from-displaying-a-form-region"></a>如何：阻止 Outlook 显示窗体区域
  在某些情况下，您可能不希望 Microsoft Office Outlook 显示特定项的窗体区域。 例如，如果某一联系人项不包含业务地址，则可以阻止显示该业务在地图中的位置的窗体区域。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="to-prevent-outlook-from-displaying-a-form-region"></a>阻止 Outlook 显示窗体区域

1. 打开要修改的窗体区域的代码文件。

2. 展开 **窗体区域工厂** 代码区域。

3. 向 `FormRegionInitializing` 事件处理程序添加代码，用于将 <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> 类的属性设置 <xref:Microsoft.Office.Tools.Outlook.FormRegionInitializingEventArgs> 为 **true**。

   在此示例中，如果联系人项不包含地址，则将 <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> 属性设置为 **true**，并且不会显示窗体区域。

## <a name="example"></a>示例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Separate_O12/MapIt.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Separate_O12/MapIt.vb" id="Snippet1":::


## <a name="see-also"></a>另请参阅
- [创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)
- [演练：设计 Outlook 窗体区域](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [如何：将窗体区域添加到 Outlook 外接程序项目](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)
- [演练：设计 Outlook 窗体区域](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [演练：导入在 Outlook 中设计的窗体区域](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
