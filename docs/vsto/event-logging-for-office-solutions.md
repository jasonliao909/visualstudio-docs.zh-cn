---
title: 解决方案的事件Office日志记录
description: 了解如何使用 Windows 中的事件查看器来查看由 Visual Studio Tools for Office 捕获的异常消息。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], event viewer
- ClickOnce deployment [Office development in Visual Studio], event viewer
- deploying applications [Office development in Visual Studio], event viewer
- Office development in Visual Studio, event viewer
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 9dedf882fcd149c2eecc04d712df19af980b5c48
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602290"
---
# <a name="event-logging-for-office-solutions"></a>解决方案的事件Office日志记录
  你可以使用 Windows 事件查看器来查看当你安装或卸载 Office 解决方案时，由 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 捕捉到的异常消息。 你可使用事件记录器中的这些消息来解决安装和部署问题。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="read-the-event-log"></a>读取事件日志
 打开“事件查看器”  和筛选器以筛选出你想要查看的事件。

### <a name="to-read-the-event-log-in-windows-server-2003-and-windows-xp"></a>读取 Windows Server 2003 和 Windows XP 中的事件日志

1. 在控制面板中，打开 **"管理工具"。**

2. 启动 **事件查看器。**

3. 在事件日志的列表中，选择“应用程序” 。

4. 在“视图”  菜单中，单击“筛选器” 。

5. 在“事件源”  列表中，选择“VSTO 4.0” 。

6. 对于安装事件，在“事件 ID”  框中，键入 **4096**。

7. 单击“确定”  ，以查看已筛选的视图。

### <a name="to-read-the-event-log-in-windows-7-windows-vista-and-windows-server-2008"></a>若要在 Windows 7、Windows Vista 和 Windows Server 2008 中读取事件日志

1. 在控制面板中，打开 **"管理工具"。**

2. 启动 **事件查看器。**

3. 展开“Windows 日志” 。

4. 在事件日志的列表中，选择“应用程序” 。

5. 在 **“操作”** 菜单上，单击 **“筛选当前日志”**。

6. 在“事件源”  列表中，选择“VSTO 4.0” 。

7. 对于安装事件，在“事件 ID”  框中，键入 **4096**。

8. 单击“确定”  ，以查看已筛选的视图。

   事件查看器包括以下信息：

- 解决方案部署清单的位置。

- 描述此错误或异常原因的消息。

  这些异常消息可以帮助你确定安装问题的原因，例如不受信任的证书、不受信任的文档位置或无效的部署清单。

  卸载 Office 解决方案后，异常消息保留在事件日志中。

  若要在运行解决方案时显示Office记录异常消息，请参阅调试Office[和](../vsto/debugging-office-projects.md)调试Office[项目](../vsto/debugging-office-projects.md)。

### <a name="localization"></a>本地化
 异常消息的语言由 Visual Studio Tools for Office 运行时语言确定。 例如，如果最终用户计算机安装了日语语言包，则异常消息会以日语写入事件日志。

## <a name="disable-the-event-logger"></a>禁用事件记录器
 默认情况下，安装或卸载 Office 解决方案时事件记录器处于禁用状态。 你可以通过将 VSTO_EVENTLOGDISABLED 环境变量设置为“1”（一）来禁用事件记录器。

### <a name="to-disable-the-event-log"></a>禁用事件日志

1. 在“控制面板”中，打开“系统” 。

2. 在 **“高级”** 选项卡上，单击 **“环境变量”**。

3. 在“系统变量”  窗格中，单击“新建” 。

4. 在“新建系统变量”  对话框中，在“变量名称”  框中键入 **VSTO_EVENTLOGDISABLED** 。

5. 在“变量值”  框中，键入 **1**。

6. 单击 **“确定”** 。

## <a name="see-also"></a>请参阅
- [部署Office解决方案](../vsto/deploying-an-office-solution.md)
- [解决方案Office疑难解答](../vsto/troubleshooting-office-solution-deployment.md)
