---
title: “进程属性”对话框 ->“页文件”选项卡 | Microsoft Docs
description: 使用“进程属性”的“页面文件”选项卡检查进程的页面文件。 本文介绍可用的设置。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Process properties for Windows NT
ms.assetid: daf41a06-8a55-48f6-95f5-49a8416bd308
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 2c1c2e703a0c07e36594bc5fa67c5da6f2e060d9
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122153857"
---
# <a name="page-file-tab-process-properties-dialog-box"></a>“进程属性”对话框 ->“页文件”选项卡
使用“页文件”选项卡检查进程的页文件。 若要显示[“进程属性”对话框](../debugger/process-properties-dialog-box.md)，请将焦点移动到[进程视图](../debugger/processes-view.md)窗口。 在树中选择任意进程节点，然后从“视图”菜单选择“属性” 。

 “页文件”选项卡中有以下可用设置：

|条目|描述|
|-----------|-----------------|
|**页文件字节数**|此进程在页文件中使用的当前页数。 页文件存储进程使用，但不包含在其他文件中的数据页。 所有进程都使用页文件，所以页文件中的空间不足会导致其他进程运行时出现错误。|
|**峰值页文件字节数**|此进程在页文件中使用的最大页数。|
|**页面错误**|此进程中执行的线程导致的页面错误数。 如果线程引用的虚拟内存页面不在其主内存内的工作集中，则会发生页面故障。 因此，如果页面在待机列表中并且因此也已经在主内存中，或者页面被共享页面的另一个进程使用，则可能不会从磁盘中检索页面。|