---
title: 端口 |Microsoft Docs
description: 本文介绍 Visual Studio 中调试器体系结构的端口定义和角色。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- ports
- debugging [Debugging SDK], ports
ms.assetid: 1d7f3aa7-7eff-4cab-bc53-0a566b1a9363
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: a504db1716eaad4fbf66c34985067310fada1fa1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664851"
---
# <a name="ports"></a>端口
在调试程序体系结构中， *端口*：

- 是一组在服务器上运行的进程的容器。 例如，端口可能表示通过串行电缆或联网的非 DCOM 计算机连接到基于 Windows CE 的设备。 一个专用端口称为 "本地端口"，其中包含在本地计算机上运行的所有进程。

- 可以按名称或标识符来标识自身。

- 可枚举端口上运行的所有进程，并启动和终止这些进程。

- 由 [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md) 接口表示，该接口通过将 [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md) 参数传递给 [AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)来创建。

  [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]提供一个默认端口，用于处理所有基于 Windows 的进程，包括本机和托管。 对于与不基于 Windows 的外部设备的连接，必须设置自定义端口。 若要提供此类自定义端口，还必须设置自定义端口供应商。

## <a name="see-also"></a>另请参阅
- [服务器](../../extensibility/debugger/servers-visual-studio-sdk.md)
- [进程](../../extensibility/debugger/processes.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)
- [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md)
- [AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
