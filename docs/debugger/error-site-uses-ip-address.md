---
description: 调试器尝试自动附加到正在使用 IP 地址的 Web 应用程序时，会发生该错误。
title: 站点使用 IP 地址 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.webdbg_siteusesipaddress
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, Web application errors
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: f141cf050e41e5f2a30b66c47e68b1b3c35aeb5c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126735796"
---
# <a name="error-site-uses-ip-address"></a>错误：站点使用 IP 地址
调试器尝试自动附加到正在使用 IP 地址的 Web 应用程序时，会发生该错误。 如果在 IIS 中将“网站标识”更改为“使用特定 IP 地址”，会发生这种情况 。

 要使自动附加能够工作，需要创建具有特定 IP 地址而不只是计算机名称的项目。 否则，调试器会将计算机名称更改为 localhost，而这会导致无法将调试谓词发送到 IIS。

### <a name="to-correct-this-error"></a>更正此错误

1. 改用手动附加（从“调试”菜单中选择“附加到进程”）。

     \- 或 -

2. 更改“IIS 网站标识”设置。

## <a name="see-also"></a>请参阅
- [调试 Web 应用程序：错误和疑难解答](../debugger/debugging-web-applications-errors-and-troubleshooting.md)
