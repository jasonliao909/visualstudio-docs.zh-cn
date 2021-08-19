---
title: 符号提供程序 |Microsoft Docs
description: 了解 Visual Studio 提供的符号提供程序，以便使表达式计算器能够计算变量和表达式。
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
ms.openlocfilehash: 49f26713bcda948220fabdefaa62032e10fde8a2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122152583"
---
# <a name="symbol-provider"></a>符号提供程序
表达式计算器实现必须访问语言编译器生成的符号调试信息，才能计算变量和表达式。 它通过使用符号提供程序 (SP) （也称为符号处理程序）的接口来实现此目的。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 使用程序数据库为托管代码和本机代码提供 Sp (PDB) 符号文件格式。 除非你的程序很难使用以自定义格式存储的符号，否则建议你使用提供的 Sp [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

## <a name="implementation-notes"></a>实现说明
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试引擎需要使用公共语言运行时 (CLR) 接口与 SPs 进行通信。 因此，将使用 Visual Studio 调试引擎的 SP 必须支持 CLR。 可以在 debugref.doc 中找到所有 CLR 调试接口的完整列表，该列表是的一部分 [!INCLUDE[winsdklong](../../deployment/includes/winsdklong_md.md)] 。

 如果您的 SP 只使用您的自定义调试引擎，则可以根据调试引擎的需求，根据您的需要实现 SP。

## <a name="see-also"></a>请参阅
- [调试器组件](../../extensibility/debugger/debugger-components.md)
