---
title: 符号提供程序|Microsoft Docs
description: 了解为启用表达式Visual Studio计算变量和表达式而提供的符号提供程序。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- symbol handler
- debugging [Debugging SDK], symbol handler
ms.assetid: 5fce651b-fead-4418-81b0-a011df7644ab
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: d7c4d9a0e760d19ace9310ed532f52d08735a36f79dc06d33ee850bc03d0a0c8
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121306291"
---
# <a name="symbol-provider"></a>符号提供程序
表达式计算程序实现必须访问语言编译器生成的符号调试信息，才能计算变量和表达式。 为此，它使用 SP (SP) （也称为符号处理程序）的接口。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 使用 Program DataBase (PDB 为托管代码和本机代码提供 SPS) 符号文件格式。 除非程序非常需要使用以自定义格式存储的符号，否则建议使用 提供的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IP。

## <a name="implementation-notes"></a>实现说明
 调试 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 引擎预期使用公共语言运行时和 CLR 接口 (IP) 。 因此，将与调试引擎一Visual Studio SP 必须支持 CLR。 所有 CLR 调试接口的完整列表可在 debugref.doc，它是 的一部分 [!INCLUDE[winsdklong](../../deployment/includes/winsdklong_md.md)] 。

 如果 SP 将仅与自定义调试引擎一起工作，则根据调试引擎的需求，你可以根据需要实现 SP。

## <a name="see-also"></a>另请参阅
- [调试器组件](../../extensibility/debugger/debugger-components.md)
