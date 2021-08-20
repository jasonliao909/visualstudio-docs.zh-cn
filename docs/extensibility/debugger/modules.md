---
title: 模块 |Microsoft Docs
description: 本文介绍 Visual Studio 中调试器体系结构中的模块的定义和角色。
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
ms.openlocfilehash: 91011c021c429c5f09556f749e305572097a8de6
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122160356"
---
# <a name="modules"></a>模块
就调试器体系结构而言， *模块* 如下：

- 是一个物理代码容器，如可执行文件或 DLL。

- 可以重新加载其符号并对其进行描述。 模块说明显示在 IDE 的 "模块" 窗口中。

- 由调试引擎创建的 [IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md) 接口表示，用于说明模块。

## <a name="see-also"></a>请参阅
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md)
