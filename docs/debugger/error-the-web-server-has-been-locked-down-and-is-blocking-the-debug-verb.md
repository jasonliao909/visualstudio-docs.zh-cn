---
description: 由于运行了 IIS 锁定工具并且安装并激活了 URLScan，单步执行 Web 应用程序或 XML Web services 失败。
title: Web 服务器已被锁定，并阻止 DEBUG 谓词 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.webdbg_debug_verb_blocked
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
ms.openlocfilehash: 3c8bcf18ea7c86036061c117beed07ecd9563525
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126735785"
---
# <a name="error-the-web-server-has-been-locked-down-and-is-blocking-the-debug-verb"></a>错误：Web 服务器已被锁定，并阻止 DEBUG 谓词
由于运行了 IIS 锁定工具并且安装并激活了 URLScan，单步执行 Web 应用程序或 XML Web services 失败。 这种情况下将禁止 IIS 接收 DEBUG 谓词。

 URLScan 是与 IIS 锁定工具一同使用的安全工具，它使 IIS 网站管理员能够关闭不必要的功能并限制服务器处理的 HTTP 请求类型。 通过阻塞特定的 HTTP 请求，URLScan 安全工具可防止有潜在危害的请求到达服务器造成损害。

 如果应用程序正在 Windows Server 2003 的 IIS 6.0 上运行，则不需要运行 IIS 锁定工具，因为 IIS 6.0 提供了相同功能。

### <a name="to-enable-debugging-on-a-web-server-with-urlscan-installed"></a>在安装有 URLScan 的 Web 服务器上启用调试

1. 找到 Urlscan.ini 文件。 通常，在类似下面这样的目录中可以找到它：

     C:\WINNT\System32\Inetsrv\urlscan

2. 创建此文件的副本并将它命名为 Urlscan.old。

3. 使用“记事本”或选定的文本编辑器打开 Urlscan.ini 文件的原始副本。

4. 在 Urlscan.ini 中，找到 [AllowVerbs] 节。 将“DEBUG”添加到 [AllowVerbs] 节中。 如果在 [AllowVerbs] 节中看到“;DEBUG”，请移除分号，以取消谓词的注释状态。

5. 找到 [DenyVerbs] 节。 如果 DEBUG 出现在 [DenyVerbs] 节中，请将其删除。

6. 保存该文件。

7. 重新启动服务器或重新启动 IIS。

## <a name="see-also"></a>请参阅
- [调试 Web 应用程序：错误和疑难解答](../debugger/debugging-web-applications-errors-and-troubleshooting.md)
- [错误：Web 服务器找不到所请求的资源](../debugger/error-the-web-server-could-not-find-the-requested-resource.md)
