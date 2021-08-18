---
title: 如何：显示外接程序用户界面错误
description: 了解如何使用 Visual Studio 以编程方式在应用程序中显示 VTSO 外接程序Microsoft Office错误。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- add-ins [Office development in Visual Studio], user interface errors
- errors [Office development in Visual Studio], user interface errors
- user interfaces [Office development in Visual Studio], errors
- application-level add-ins [Office development in Visual Studio], user interface errors
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: ef5a8780e56da76476038605cfad957cfcd8ba0e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122099615"
---
# <a name="how-to-show-add-in-user-interface-errors"></a>如何：显示外接程序用户界面错误
  默认情况下，如果VSTO外接程序尝试在 UI Microsoft Office用户界面 (操作) 失败，则不显示错误消息。 但是，你可以配置 Microsoft Office 应用程序以显示与 UI 相关的错误的消息。 可以使用这些消息来帮助确定自定义功能区不显示的原因，或者功能区出现但不显示控件的原因。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

## <a name="to-show-vsto-add-in-user-interface-errors"></a>显示 VSTO 外接程序用户界面错误

1. 启动应用程序。

2. 单击 **“文件”** 选项卡。

3. 单击“选项”。

4. 在类别窗格中，单击“高级” 。

5. 在细节窗格中，选择“显示 VSTO 外接程序用户界面错误” ，然后单击“确定” 。

    > [!NOTE]
    > 对于 Outlook，“显示 VSTO 外接程序用户界面错误”  复选框位于细节窗格的“开发工具”  部分。 对于其他应用程序，该复选框位于细节窗格的“常规”  部分。

## <a name="see-also"></a>请参阅
- [OfficeUI 自定义](../vsto/office-ui-customization.md)
- [创建Outlook窗体区域](../vsto/creating-outlook-form-regions.md)
- [功能区概述](../vsto/ribbon-overview.md)
- [操作窗格概述](../vsto/actions-pane-overview.md)
