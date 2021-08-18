---
title: 事件说明|Microsoft Docs
description: 了解事件的类型及其使用原因。 每种类型的事件都有特定的用途。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], events
ms.assetid: 09f61652-7e16-4bb0-8055-f61a84bf384e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: d1632fde2f9f2040a3883f371291c06d190564c2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122153532"
---
# <a name="event-descriptions"></a>事件说明
每种类型的事件都有特定的用途。

## <a name="events-and-the-reasons-for-their-use"></a>事件及其使用原因

|事件|说明|
|-----------|-----------------|
|激活文档事件|当调试引擎 (DE) IDE 打开文档或将文档引入前台时发生。|
|断点绑定或断点错误事件|在断点绑定或断点无法绑定并返回错误时发送。|
|断点未绑定事件|绑定断点与代码取消绑定时发生。|
|可以停止事件|发送到 IDE 以确定用户是否要在代码中的指定点停止。|
|断点事件|在命中代码或数据断点时发生。|
|记录文本事件|更改文档中的文本时发生。 这些事件不会通过 方法 `IDebugEventCallBack2::Event` 发送。|
|引擎创建事件|首次创建引擎时发送。|
|入口点事件|当正在调试的程序已运行其初始化代码并到达其第一个用户入口点时发送。|
|异常事件|当正在运行的程序达到异常时发送。|
|表达式计算完成事件|异步表达式计算完成时发送。|
|查找符号事件|每当 DE 需要要求用户查找模块的符号时发送。|
|加载完整事件|仅在初始程序加载完成且第一个代码即将在程序中运行时发送。|
|消息事件|在将消息发送给用户时发送。|
|模块加载事件|加载或卸载新模块时发送。|
|输出字符串事件|在程序写入调试输出时发送。|
|创建和销毁事件|发送以宣布创建或销毁进程、程序、属性、会话和线程，以便 Visual Studio IDE 可以跟踪正在调试的程序的状态。|
|步骤完成事件|在步骤完成时发送。|
|线程名称更改事件|当用户更改线程的名称时发送。|
|程序名称更改事件|当用户更改程序的名称时发送。|

## <a name="see-also"></a>请参阅
- [发送事件](../../extensibility/debugger/sending-events.md)
