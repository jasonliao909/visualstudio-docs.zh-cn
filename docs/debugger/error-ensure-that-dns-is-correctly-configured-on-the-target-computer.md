---
title: 确保目标计算机上正确配置了 DNS | Microsoft Docs
description: 目标计算机无法解析 Visual Studio 调试器主机计算机的名称时，会发生此错误。
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.callback_dns_failed
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
ms.openlocfilehash: 871163bb5ee4e29eebd037b1c499addc06fc8d96
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122161413"
---
# <a name="error-ensure-that-dns-is-correctly-configured-on-the-target-computer"></a>错误：确保目标计算机上正确配置了 DNS
当尝试执行远程调试时，您可能会收到如下错误信息：

```cmd
Error: The Visual Studio Remote Debugger on the target computer cannot connect back to this computer. Ensure that DNS is correctly configured on the target computer.
```

 目标计算机无法解析 Visual Studio 调试器主机计算机的名称时，会发生此错误。 检查目标计算机上的 DNS 设置。

- 有关在 Windows 8.1、Vista、Windows 7、Windows Server 2012、Windows Server 2008 或 Windows Server 2008 R2 中查看 DNS 设置的信息，请执行以下操作：在“开始”菜单上，选择“帮助和支持”，然后搜索“更改 TCP/IP 设置”  。

- 有关详细信息，请转到 [Microsoft Windows 网站](https://www.microsoft.com/windows/)并搜索“更改 TCP/IP 设置”。

  如果无法解决 DNS 问题，则可以尝试在不同帐户下运行远程调试器。 在“本地系统”帐户或“网络服务”帐户下运行远程调试器时，会发生此错误。 如果在其他帐户下运行远程调试器，它可以使用 NTLM 身份验证（这不需要 DNS）。 . 有关该过程，请参阅[错误：目标计算机上的 Visual Studio 远程调试器服务无法重新连接到此计算机](../debugger/error-the-visual-studio-remote-debugger-service-on-the-target-computer-cannot-connect-back-to-this-computer.md)。
