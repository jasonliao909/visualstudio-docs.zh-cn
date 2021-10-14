---
description: 此错误表示远程调试器服务正在运行，但是运行它的用户帐户在连接到正在从中进行调试的计算机时无法进行身份验证。
title: 目标计算机上的 Visual Studio 远程调试器服务无法重新连接到此计算机 | Microsoft Docs
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.service_access_denied_oncallback
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: db58549f437c87b2fe5a4c6dc278b141a5a63e0c
ms.sourcegitcommit: 8fae163333e22a673fd119e1d2da8a1ebfe0e51a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2021
ms.locfileid: "129969640"
---
# <a name="error-the-visual-studio-remote-debugger-service-on-the-target-computer-cannot-connect-back-to-this-computer"></a>错误：目标计算机上的 Visual Studio 远程调试器服务无法重新连接到此计算机 | Microsoft Docs
此错误表示远程调试器服务正在运行，但是运行它的用户帐户在连接到正在从中进行调试的计算机时无法进行身份验证。 使用旧版调试引擎进行远程调试，且远程调试器作为服务运行时，可能会发生此错误。

 下表显示可访问该计算机的帐户：

|方案|LocalSystem 帐户|域帐户|在双方计算机上具有相同用户名和密码的本地帐户|
|-|-|-|-|
|双方计算机处于同一个域中|是|是|是|
|双方计算机处于具有双向信任的域中|否|否|是|
|双方计算机中有一台或两台都处于工作组中|否|否|是|
|不同域中的计算机|否|否|是|

 此外：

- 运行“Visual Studio 远程调试器”服务的帐户应为远程计算机上的管理员，这样它就能调试任何进程。

- 还必须授予该帐户在使用“本地安全策略”管理工具的远程计算机上 `Log on as a service` 的特权。

- 如果正使用本地帐户访问计算机，则必须在本地帐户下运行“Visual Studio 远程调试器”服务。

### <a name="to-correct-this-error"></a>更正此错误

1. 确保在远程计算机上正确设置“Visual Studio 远程调试器”服务。 有关详细信息，请参阅[远程调试](../debugger/remote-debugging.md)。

2. 以可以访问调试器主机的帐户运行远程调试器服务，如上表所示。

### <a name="to-add-log-on-as-a-service-privilege"></a>添加“作为服务登录”特权

1. 在“开始”菜单上，选择“控制面板” 。

2. 在控制面板中，选择“经典视图”（如有必要）。

3. 双击 **“管理工具”** 。

4. 在“管理工具”窗口中双击“本地安全策略”。

5. 在“本地安全设置”窗口中展开“本地策略”文件夹 。

6. 单击“用户权限分配”。

7. 在“策略”列中，双击“作为服务登录”，在“作为服务登录”对话框中查看当前的本地组策略分配  。

8. 若要添加新用户，请单击“添加用户或组”按钮。

9. 完成添加用户后，单击“确定”。

### <a name="to-work-around-this-error"></a>解决此错误

- 将“远程调试监视器”作为应用程序（而不是作为服务）运行。

## <a name="see-also"></a>请参阅
- [远程调试错误和疑难解答](../debugger/remote-debugging-errors-and-troubleshooting.md)
- [远程调试](../debugger/remote-debugging.md)
