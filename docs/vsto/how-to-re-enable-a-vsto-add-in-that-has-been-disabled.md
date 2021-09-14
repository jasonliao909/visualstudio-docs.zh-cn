---
title: 如何：重新启用VSTO禁用的外接程序
description: 了解如何使用 Visual Studio 来重新启用已在 Microsoft Office 应用程序中禁用的 VSTO 外接程序。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VST.Warning.DisabledAddIn
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- disabled add-ins
- add-ins [Office development in Visual Studio], disabled
- add-ins [Office development in Visual Studio], enabling
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: ecaca6e262113ae4926ff21af5c468703fe78ae9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664954"
---
# <a name="how-to-re-enable-a-vsto-add-in-that-has-been-disabled"></a>如何：重新启用VSTO禁用的外接程序
  Microsoft Office 应用程序可禁用行为异常的 VSTO 外接程序。 当你尝试对 VSTO 外接程序进行调试时，如果应用程序不加载它，则此应用程序可能已硬禁用或软禁用此 VSTO 外接程序。

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

## <a name="hard-disabled-vsto-add-ins"></a>硬禁用VSTO外接程序
 当外接程序导致VSTO意外关闭时，可能会发生硬禁用。 如果 VSTO 外接程序中的 <xref:Microsoft.Office.Tools.AddIn.Startup> 事件处理程序正在执行时停止了调试器，则硬禁用也可能发生在开发计算机上。

### <a name="to-re-enable-a-vsto-add-in"></a>若要重新启用 VSTO 外接程序

1. 在应用程序中，单击 **“文件”** 选项卡。

2. 单击 *"ApplicationName* **选项"** 按钮。

3. 在类别窗格中，单击 **“外接程序”**。

4. 在详细信息窗格中，确保 VSTO 外接程序显示在 **“禁用的应用程序外接程序”** 列表中。

     **“名称”** 列指定程序集的名称， **“位置”** 列指定应用程序清单的完整路径。

5. 在 **“管理”** 框中，单击 **“禁用项”**，然后单击 **“跳转”**。

6. 选择 VSTO 外接程序并单击 **“启用”**。

7. 单击“关闭”  。

## <a name="soft-disabled-vsto-add-ins"></a>已软禁用VSTO外接程序
 当 VSTO 外接程序产生不会导致应用程序意外关闭的错误时，可能会发生软禁用。 例如，如果 <xref:Microsoft.Office.Tools.AddIn.Startup> 事件处理程序正在执行时，某个应用程序引发了未处理异常，则此应用程序可能软禁用 VSTO 外接程序。

> [!NOTE]
> 当重新启用软禁用的 VSTO 外接程序时，应用程序将立即尝试加载该 VSTO 外接程序。 如果最初导致应用程序软禁用 VSTO 外接程序的问题未得到解决，则该应用程序将再次软禁用 VSTO 外接程序。

### <a name="to-re-enable-a-vsto-add-in"></a>若要重新启用 VSTO 外接程序

1. 在应用程序中，单击 **“文件”** 选项卡。

2. 单击 *"ApplicationName* **选项"** 按钮。

3. 在类别窗格中，单击 **“外接程序”**。

4. 在详细信息窗格中，确保 VSTO 外接程序显示在 **“非活动应用程序外接程序”** 列表中。

     **“名称”** 列指定程序集的名称， **“位置”** 列指定应用程序清单的完整路径。

5. 在 **“管理”** 框中，单击 **“COM 外接程序”**，然后单击 **“跳转”**。

6. 在 **“COM 外接程序”** 对话框中，选中已禁用 VSTO 外接程序旁的复选框。

7. 单击 **“确定”** 。

## <a name="see-also"></a>请参阅
- [生成Office解决方案](../vsto/building-office-solutions.md)
- [调试Office项目](../vsto/debugging-office-projects.md)
- [程序VSTO外接程序](../vsto/programming-vsto-add-ins.md)
