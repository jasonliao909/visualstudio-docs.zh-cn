---
title: 启用要调试的程序|Microsoft Docs
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
ms.openlocfilehash: 2c09fd6f9862fb3c3426b74bb7c0f62e947bc6050ea02edcbc81990f283bee58
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121343007"
---
# <a name="enable-a-program-to-be-debugged"></a>启用要调试的程序
在调试引擎 (DE) 调试程序之前，必须先启动 DE 或将其附加到现有程序。

## <a name="in-this-section"></a>本节内容
 [获取端口](../../extensibility/debugger/getting-a-port.md) 讨论如何获取端口作为启用要调试的程序的第一步。

 [注册程序](../../extensibility/debugger/registering-the-program.md) 说明启用要调试的程序的下一步：向端口注册程序。 注册后，可以通过在 JIT 中附加或实时 (程序) 调试。

 [附加到程序](../../extensibility/debugger/attaching-to-the-program.md) 说明下一步：将调试器附加到程序。

 [基于启动的附加](../../extensibility/debugger/launch-based-attachment.md) 描述程序基于启动的附件，该附件在 SDM 启动时自动执行。

 [发送所需的事件](../../extensibility/debugger/sending-the-required-events.md) 在 DE 中创建调试引擎并将其附加到 (时) 所需事件。

## <a name="related-sections"></a>相关章节
 [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md) 在 DE (定义) 引擎，并描述通过 DE 接口实现的服务，以及这些服务如何导致调试器在不同操作模式之间转换。
