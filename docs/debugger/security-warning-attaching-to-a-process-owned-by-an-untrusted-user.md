---
title: 安全警告：附加到不受信任的用户所拥有的进程可能很危险。 如果以下信息看起来可疑或你对此无法确定，请勿附加到此进程 | Microsoft Docs
ms.date: 1/15/2021
ms.topic: conceptual
f1_keywords:
- vs.debug.attachsecuritywarning
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 52246c1e-a371-40a0-b756-a435cc51876f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2ec174a03e62cb8cb033be0b92db679fb19f0180
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99881251"
---
# <a name="security-warning-attaching-to-a-process-owned-by-an-untrusted-user-can-be-dangerous-if-the-following-information-looks-suspicious-or-you-are-unsure-do-not-attach-to-this-process"></a>安全警告：附加到不受信任的用户所拥有的进程可能很危险。 如果以下信息看上去可疑或者你无法确定，请勿附加到此进程

如果附加到包含部分可信代码或由不可信用户拥有的进程，则在该附加操作发生之前，会出现此警告对话框。 包含恶意代码的不可信进程可能会损害执行调试的计算机。 如果有理由不信任该进程，则应单击“取消”阻止调试。

在 IIS 方案中，如果使用不受信任的自定义应用程序池，则可能会看到此警告。

若要在调试合法方案时禁止显示此警告：

1. 关闭 Visual Studio。

1. 将 `DisableAttachSecurityWarning` 注册表项的值设置为 1。

   在 `HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\<version>\Debugger` 下查找或创建键，并将其设置为 1。

   从 Visual Studio 2017 开始，如果想要查看完整的注册表设置，需要加载专用注册表配置单元。 有关详细信息，请参阅[如何检查 Visual Studio 2017 注册表](https://github.com/microsoft/VSProjectSystem/blob/master/doc/overview/examine_registry.md)。 启动 Visual Studio 之前，请确保先卸载专用注册表配置单元。

1. 重新启动 Visual Studio。

1. 在调试完方案后，请将值重置为 0，并重新启动 Visual Studio。

“可信用户”包括您自己以及一组标准用户，通常在安装有 .NET Framework 的计算机上定义了这些用户（如 `aspnet`、`localsystem`、`networkservice` 和 `localservice`）。

## <a name="uielement-list"></a>UIElement 列表

 名称 为调试而请求的程序集的名称

 用户 当前用户

 附加 按下它即可通过附加来继续进行调试

 不附加 不附加到进程

## <a name="see-also"></a>请参阅
- [附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [调试器安全](../debugger/debugger-security.md)
