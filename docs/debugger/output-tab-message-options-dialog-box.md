---
title: “消息选项”对话框 ->“输出”选项卡 | Microsoft Docs
description: 使用“消息选项”的“输出”选项卡指定要在“消息视图”中显示的消息数据。 本文介绍可用的设置。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- message options, Output
ms.assetid: 22dd48c2-6d17-41b1-b84c-9ddeaef68411
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 41a6e5aef6654b06b21481328a6fdd50f672095b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126644469"
---
# <a name="output-tab-message-options-dialog-box"></a>“消息选项”对话框 ->“输出”选项卡
使用“输出”选项卡指定每个消息中的哪些数据要在[消息视图](../debugger/messages-view.md)中列出。 若要显示[“消息选项”对话框](../debugger/message-options-dialog-box.md)，请从 Spy 菜单中选择“日志消息” 。

 “输出”选项卡中有以下可用设置：

 **行号** 显示行号。

 **消息嵌套级别** 为每个级别的嵌套消息添加一个句点前缀。

 **原始消息参数** 显示十六进制 wParam 和 lParam 值 。

 **已解码的消息参数** 显示 wParam 和 lParam 值的特定于消息的解码结果 。

 **原始返回值** 显示十六进制 lResult 返回值。

 **已解码的返回值** 显示 lResult 返回值的特定于消息的解码结果。

 **消息原始时间** 自 Windows 系统启动后的运行时间（仅适用于已发布的消息）。

 **消息鼠标位置** 发布消息时鼠标的屏幕坐标（仅适用于已发布的消息）。

 **最大行数** 限制在当前所选消息视图中保留的行数。

 **同时将消息记录到文件** 指定消息日志的输出文件。 此输出文件与消息日志窗口同时写入。

 **保存为默认设置** 为新消息流窗口保存之前的设置。 退出 Spy++ 时保存这些设置。