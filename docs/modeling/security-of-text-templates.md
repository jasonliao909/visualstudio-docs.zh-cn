---
title: 文本模板的安全性
description: 了解安全和文本模板，包括任意代码和恶意指令处理器等主题。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, security
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0a740a6f7a4c532a61a5e412c94fa4321c5da707
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385755"
---
# <a name="security-of-text-templates"></a>文本模板的安全性
文本模板具有以下安全问题：

- 文本模板容易受到任意代码插入的影响。

- 如果主机用于查找指令处理器的机制不安全，则可能会运行恶意指令处理器。

## <a name="arbitrary-code"></a>任意代码
 编写模板时，可以将任何代码放入 \<# #> 标记中。 这允许从文本模板内执行任意代码。

 请确保从受信任的源获取模板。 请务必警告应用程序的最终用户不要执行不来自受信任源的模板。

## <a name="malicious-directive-processor"></a>恶意指令处理器
 文本模板引擎与转换主机和一个或多个指令处理器交互，以将模板文本转换为输出文件。 有关详细信息，请参阅文本 [模板转换过程](../modeling/the-text-template-transformation-process.md)。

 如果主机用于查找指令处理器的机制不安全，则存在运行恶意指令处理器的风险。 恶意指令处理器可以提供在运行模板时 `FullTrust` 在 模式下运行的代码。 如果创建自定义文本模板转换主机，则必须使用安全机制（如注册表）让引擎查找指令处理器。
