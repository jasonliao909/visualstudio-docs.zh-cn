---
title: “窗口属性”对话框 ->“窗口”选项卡 | Microsoft Docs
description: 使用“窗口属性”的“窗口”选项卡显示与所选窗口相关的窗口的信息。 查看本文了解设置。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Window Properties dialog box, Windows Tab
ms.assetid: 9001342a-09a8-4f5e-b6ed-881a3b9d7246
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: ff9e7acf648e57dbb3d50a7841e06594fad35733
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122112238"
---
# <a name="windows-tab-window-properties-dialog-box"></a>“窗口属性”对话框 ->“窗口”选项卡
使用“窗口”选项卡显示所选窗口相关的窗口的信息。 若要显示[窗口属性对话框](../debugger/window-properties-dialog-box.md)，将焦点移动到 [Windows 视图](../debugger/windows-view.md)窗口。 在树中选择任意窗口节点，然后从“视图”菜单选择“属性” 。

 “窗口”选项卡中有以下可用设置：

|条目|描述|
|-----------|-----------------|
|**下一个窗口**|下一个同级窗口的句柄，采用窗口树状视图中显示的相同顺序（Z 顺序）（如果没有下一个窗口，则为“无”）。 选择此条目可查看下一个窗口的属性。|
|**上一个窗口**|上一个同级窗口的句柄，采用窗口树状视图中显示的相同顺序（Z 顺序）（如果没有上一个窗口，则为“无”）。 选择此条目可查看上一个窗口的属性。|
|**父窗口**|此窗口的父窗口的句柄（如果没有父窗口，则为“无”）。 选择此条目可查看父窗口的属性。|
|**第一个子窗口**|此窗口的第一个子窗口的句柄，采用窗口树状视图中显示的顺序（Z 顺序）（如果没有子窗口，则为“无”）。 选择此值可查看第一个子窗口的属性。|
|**所有者窗口**|此窗口的所有者窗口的句柄。 例如，应用程序的主窗口通常拥有系统模式对话框窗口（如果没有所有者，则为“无”）。 选择此条目可查看所有者窗口的属性。|