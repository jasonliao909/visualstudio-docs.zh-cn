---
title: 事件说明 |Microsoft Docs
description: 了解事件类型及其使用原因。 每种类型的事件都有特定的用途。
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
ms.openlocfilehash: 4a9aae8668bbe2b0a92524ccfc5d8d0d18565fd80ea1a7dec2211f47e37f179d
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121342799"
---
# <a name="event-descriptions"></a>事件说明
每种类型的事件都有特定的用途。

## <a name="events-and-the-reasons-for-their-use"></a>事件及其使用原因

|事件|说明|
|-----------|-----------------|
|激活文档事件|当调试引擎 (DE) 希望 IDE 打开或将文档置于前台时出现。|
|断点绑定或断点错误事件|当绑定断点时，或在无法绑定断点时发送，并且返回错误。|
|断点未绑定事件|绑定断点从代码解除绑定时发生。|
|可以停止事件|发送到 IDE 来确定用户是否想要在代码中的指定位置停止。|
|断点事件|命中代码或数据断点时发生。|
|记录文本事件|在文档中的文本更改时发生。 不通过方法发送这些事件 `IDebugEventCallBack2::Event` 。|
|引擎创建事件|在首次创建引擎时发送。|
|入口点事件|当正在调试的程序运行其初始化代码并到达其第一个用户入口点时发送。|
|异常事件|当正在运行的程序遇到异常时发送。|
|表达式计算完成事件数|异步表达式计算完成后发送。|
|查找符号事件|当 DE 需要请求用户查找模块的符号时发送。|
|加载完成事件|仅当初始程序加载完成并且第一个代码即将在程序中运行时发送。|
|消息事件|发送消息给用户时发送。|
|模块加载事件|加载或卸载新模块时发送。|
|输出字符串事件|当程序写入调试输出时发送。|
|创建和销毁事件|发送以公告进程、程序、属性、会话和线程的创建或销毁，以便 Visual Studio IDE 可以跟踪正在调试的程序的状态。|
|步骤完成事件|步骤完成后发送。|
|线程名称更改事件|当用户更改线程的名称时发送。|
|程序名称更改事件|当用户更改程序的名称时发送。|

## <a name="see-also"></a>另请参阅
- [发送事件](../../extensibility/debugger/sending-events.md)
