---
title: 模块|Microsoft Docs
description: 本文介绍模块在 Visual Studio 调试器体系结构中的定义和Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- modules
- debugging [Debugging SDK], modules
ms.assetid: c4cf2809-dbdb-4e75-9273-b3d3d77b67d0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 224e6da359f38e2c936a46f56fdfbe2ef1be9fdc00bb9e5d89cf9a3b867199c8
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121434589"
---
# <a name="modules"></a>模块
就调试器体系结构而言，模块 *为*：

- 是代码的物理容器，例如可执行文件或 DLL。

- 可以重新加载其符号并描述自身。 模块说明显示在 IDE 的"模块"窗口中。

- 由 [IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md) 接口表示，该接口由调试引擎创建，用于描述模块。

## <a name="see-also"></a>另请参阅
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md)
