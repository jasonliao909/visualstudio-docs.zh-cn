---
title: 线程就绪连接器 | Microsoft Docs
description: 了解在单击阻塞段以查看调用堆栈及其取消阻塞的堆栈时，还可能会显示线程就绪连接器。
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.threadready
helpviewer_keywords:
- Concurrency Visualizer, Thread Ready
ms.assetid: 68e1ec38-4b10-4b01-b32f-6c9a00b2443c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 4c245ed7e7a77de16b1ae89d37511e4b6031b738
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122141202"
---
# <a name="thread-ready-connector"></a>线程就绪连接器
单击阻止段以查看调用堆栈及其解除阻止的堆栈时，还可能会显示线程就绪连接器。 如果解除阻止的事件在当前进程中的另一个线程上发生，则线程就绪连接器可直观地标识允许阻止的线程继续执行的线程和执行段。