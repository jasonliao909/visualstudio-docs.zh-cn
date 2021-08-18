---
title: 如何：将窗体区域添加到Outlook外接程序项目
description: 了解如何使用"新建窗体区域"向导创建Microsoft Office Outlook区域以扩展标准Outlook自定义窗体。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VSTO.NewFormRegionWizard.Page1
- VSTO.NewFormRegionWizard.Page3
- VSTO.NewFormRegionWizard.Page2
- VSTO.NewFormRegionWizard.Page0
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], adding
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 4afff086588d70ea8b09b6aaf74a3899c663d9ce
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122139863"
---
# <a name="how-to-add-a-form-region-to-an-outlook-add-in-project"></a>如何：将窗体区域添加到Outlook外接程序项目
  使用  “新建 Outlook 窗体区域”向导创建窗体区域，从而扩展标准或自定义 Microsoft Office Outlook 窗体。 你可以在 Visual Studio 中创建一个新的窗体区域并设计用户界面，也可以导入在 Outlook 中设计的窗体区域并添加 Visual Basic 或 C# 代码。

 如果具有在其他 Outlook 项目中使用的 Outlook 窗体区域，可通过使用 **“添加现有项”** 对话框在当前 Outlook VSTO 外接程序项目中重新使用它。 有关详细信息，请参阅[创建Outlook区域。](../vsto/creating-outlook-form-regions.md)

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

### <a name="to-add-a-new-form-region-to-an-outlook-project"></a>向 Outlook 项目中添加新的窗体区域

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中打开或创建 Outlook VSTO 外接程序项目。 有关详细信息，请参阅[如何：在 Office 创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

2. 在 “解决方案资源管理器”中，选择 Outlook VSTO 外接程序项目节点。

3. 在 **“项目”** 菜单上，单击 **“添加新项”**。

4. 在  “添加新项”对话框中，选择 “Outlook 窗体区域”。

5. 在  “名称”框中键入窗体区域的名称，然后单击 “添加”。

     **NewOutlook 窗体区域向导** 将启动。

6. 在  “选择窗体区域的创建方式”页上，选择是要通过将托管控件拖到可视化设计器来设计窗体区域，还是导入在 Outlook 中设计的窗体区域。

    > [!NOTE]
    > 如果选择导入在 Outlook 中设计的窗体区域，则必须指定 Outlook Form 存储 (*.ofs)* 文件的位置。 不能将托管控件添加到在 Outlook 中设计的窗体区域；只能在现有 UI 背后添加代码。 有关详细信息，请参阅[创建Outlook区域。](../vsto/creating-outlook-form-regions.md)

7. 在  “选择要创建的窗体区域的类型”页上，查看窗体区域类型并选择一个，然后单击“下一步” 。 有关窗体区域类型的信息，请参阅[创建Outlook区域](../vsto/creating-outlook-form-regions.md)。

8. 在“提供说明性文本并选择显示首选项”  页上，在“名称”  框中键入窗体区域的名称。 对于替换和全部替换窗体区域类型，还需要填写“标题”  和“说明”  框。

     有关在部署窗体区域时名称、标题和Outlook在窗体区域中的显示位置的信息，请参阅创建Outlook[区域](../vsto/creating-outlook-form-regions.md)。

9. 根据需要为窗体区域选择一个或多个显示模式。

     所有窗体区域类型都能够以撰写模式（用于创建项目）和阅读模式（用于查看项目）显示在检查器中。 相邻、替换和全部替换窗体区域类型也可以在阅读窗格中显示。

10. 单击“下一步”。

11. 在“标识将显示此窗体区域的 message 类”  页上，选择标准 Outlook message 类或者键入一个或多个自定义 message 类的名称，然后单击“完成” 。 有关详细信息，请参阅[将窗体区域与消息Outlook关联](../vsto/associating-a-form-region-with-an-outlook-message-class.md)。

## <a name="see-also"></a>请参阅
- [运行时访问窗体区域](../vsto/accessing-a-form-region-at-run-time.md)
- [Outlook解决方案](../vsto/outlook-solutions.md)
- [创建Outlook窗体区域](../vsto/creating-outlook-form-regions.md)
- [有关创建窗体Outlook指南](../vsto/guidelines-for-creating-outlook-form-regions.md)
- [演练：设计Outlook区域](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [演练：导入在窗体中设计的Outlook](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
- [窗体Outlook中的自定义操作](../vsto/custom-actions-in-outlook-form-regions.md)
