---
title: 文本模板的安全性
description: 了解安全性和文本模板，其中包括任意代码和恶意指令处理器之类的主题。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, security
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 376abb9674519cc87afdfd9af81bea4a6d495903
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663901"
---
# <a name="security-of-text-templates"></a>文本模板的安全性
文本模板具有以下安全问题：

- 文本模板容易出现任意代码插入。

- 如果主机用于查找指令处理器的机制不安全，恶意指令处理器可能会运行。

## <a name="arbitrary-code"></a>任意代码
 在你编写模板时，可以将任何代码放入 \<# #> 标记中。 这样就可以从文本模板中执行任意代码。

 确保从受信任的源获取模板。 确保提醒应用程序的最终用户，不要执行来自不受信任的源的模板。

## <a name="malicious-directive-processor"></a>恶意指令处理器
 文本模板引擎与转换主机和一个或多个指令处理器进行交互，将模板文本转换为输出文件。 有关详细信息，请参阅[文本模板转换过程](../modeling/the-text-template-transformation-process.md)。

 如果主机用于查找指令处理器的机制不安全，则存在可能运行恶意指令处理器的风险。 在模板运行时，恶意指令处理器可以提供在 `FullTrust` 模式下运行的代码。 如果创建自定义文本模板转换主机，必须使用安全机制（如注册表），让引擎找到指令处理器。
