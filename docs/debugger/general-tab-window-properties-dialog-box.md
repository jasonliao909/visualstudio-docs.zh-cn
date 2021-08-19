---
title: 常规选项卡，窗口属性对话框 |Microsoft 文档
description: 查看“常规”选项卡，了解有关窗口的信息，包括标题栏、句柄、矩形、应用程序实例句柄、菜单句柄和用户数据。
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Window Properties dialog box, General Tab
ms.assetid: 19142c60-9b32-46ba-a556-b62fd77568c1
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: ce5dda5f3fb1581e5239d9d3ffcdee8de864498a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122154299"
---
# <a name="general-tab-window-properties-dialog-box"></a>“窗口属性”对话框 ->“常规”选项卡
使用“常规”选项卡来显示所选窗口的信息。 若要显示[窗口属性对话框](../debugger/window-properties-dialog-box.md)，将焦点移动到 [Windows 视图](../debugger/windows-view.md)窗口。 在树中选择任意窗口节点，然后从“视图”菜单选择“属性” 。

 “常规”选项卡中有以下可用设置：

|条目|描述|
|-----------|-----------------|
|**窗口标题**|窗口标题中的文本，如果窗口是控件，则为窗口中包含的文本。|
|**窗口句柄**|此窗口的唯一 ID。 窗口句柄号是重复使用的；它们仅在该窗口的生存期内标识窗口。|
|**窗口进程**|此窗口的窗口过程函数的虚拟地址。 此字段还指示此窗口是否为 Unicode 窗口，以及是否为子类。|
|**矩形**|窗口的边框。 矩形的大小也会显示。 单位是屏幕坐标中的像素。|
|**还原矩形**|还原的窗口的边框。 矩形的大小也会显示。 仅当窗口最大化或最小化时，还原矩形才会与矩形不同。 单位是屏幕坐标中的像素。|
|**客户端矩形**|窗口工作区的边框。 矩形的大小也会显示。 单位是相对于窗口工作区左上角的像素。|
|**实例句柄**|应用程序的实例句柄。 实例句柄不是唯一的。|
|控件 ID 或菜单句柄|如果显示的窗口是子窗口，则会显示“控件 ID”标签。 控件 ID 是一个整数，用于标识此子窗口的控件 ID。 如果显示的窗口不是子窗口，则会显示“菜单句柄”标签。 菜单句柄是一个整数，用于标识与此窗口关联的菜单的句柄。|
|**用户数据**|附加到此窗口结构的特定于应用程序的数据。|
|**窗口字节**|与此窗口关联的额外字节数。 这些字节的含义由应用程序确定。 展开列表框可查看 DWORD 格式的字节值。|