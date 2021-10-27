---
title: 展开和折叠 Spy++ 树| Microsoft Docs
description: 了解用于展开和折叠“窗口”、“进程”和“线程”视图的两种方法。 可以单击窗口中的图标或使用“树”菜单。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Expanding and Collapsing Spy++ Trees
ms.assetid: 22993182-7026-4155-8046-b84fd99f803c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 90f939e62783cb2b3189cb04783f84fd3dcffa41
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126640955"
---
# <a name="how-to-expand-and-collapse-spy-trees"></a>如何：展开和折叠 Spy++ 树
可以使用两种方法展开和折叠窗口、进程和线程视图：单击窗口中的图标或使用“树”菜单。 树中 + 和 - 图标的用途与它们在 C++ 项目窗口中的用途相同。

 “树”菜单包含四个命令：

|菜单命令|描述|
|------------------|-----------------|
|**展开一级**|将当前所选项展开到下一个级别。|
|展开分支|完全展开当前所选项。|
|**全部展开**|完全展开窗口中的所有项。|
|**折叠**|完全折叠当前所选项。|

> [!TIP]
> 如果展开某个进程，则会看到该进程拥有的所有线程。 如果展开某个线程，则会看到它拥有的所有窗口的列表。

### <a name="to-expand-or-collapse-spy-trees"></a>展开或折叠 Spy++ 树

1. 在窗口、进程或线程视图中突出显示一个项。

2. 从“树”菜单中，选择一个展开或折叠命令。

## <a name="see-also"></a>请参阅
- [使用 Spy++](../debugger/using-spy-increment.md)
- [Spy++ 视图](../debugger/spy-increment-views.md)
- [Spy++ 参考](../debugger/spy-increment-reference.md)