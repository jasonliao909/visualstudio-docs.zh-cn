---
title: 启用要调试的程序 |Microsoft Docs
description: 了解如何启动调试引擎或将调试引擎附加到现有程序以调试程序。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], enabling for programs
ms.assetid: 61d24820-0cd9-48b6-8674-6813f7493237
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 231934a246a5ce57f87bf08b134c0e288c6f5534
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122138882"
---
# <a name="enable-a-program-to-be-debugged"></a>启用要调试的程序
在调试引擎 (DE) 可以调试程序之前，必须先启动 DE，或将其附加到现有的程序。

## <a name="in-this-section"></a>本节内容
 [获取端口](../../extensibility/debugger/getting-a-port.md) 讨论如何获取端口，作为实现程序调试的第一步。

 [注册程序](../../extensibility/debugger/registering-the-program.md) 说明启用要调试的程序的下一步：使用端口注册程序。 注册后，程序可通过附加或实时 (JIT) 调试的过程进行调试。

 [附加到程序](../../extensibility/debugger/attaching-to-the-program.md) 说明接下来的步骤：将调试器附加到程序。

 [基于启动的附加](../../extensibility/debugger/launch-based-attachment.md) 描述从启动到程序的附件，该程序是由 SDM 启动时自动完成的。

 [发送所需的事件](../../extensibility/debugger/sending-the-required-events.md) (DE) 并将其附加到程序时，逐步执行所需的事件。

## <a name="related-sections"></a>相关章节
 [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md) 定义调试引擎 (DE) ，并介绍通过取消接口实现的服务，以及如何使调试器在不同的运行模式之间过渡。
