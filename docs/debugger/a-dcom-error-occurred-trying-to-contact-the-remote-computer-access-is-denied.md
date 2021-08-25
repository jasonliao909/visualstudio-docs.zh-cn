---
title: 尝试联系远程计算机时出现 DCOM 错误。 拒绝访问。
titleSuffix: ''
description: “尝试联系远程计算机时出现 DCOM 错误。 拒绝访问。” 查看有关此 Visual Studio 远程调试错误引用的信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.remote.dcom_access_denied
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- remote debugging, DCOM error
- remote DCOM access denied error
- DCOM, access errors
ms.assetid: 9d7dfc1b-9fe0-4f54-9c50-9c0e0f8358c5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 53d8bbb4a4d053e4120cacfb1d44ca14295a3d22
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122052481"
---
# <a name="a-dcom-error-occurred-trying-to-contact-the-remote-computer-access-is-denied"></a>尝试联系远程计算机时出现 DCOM 错误。 拒绝访问。
在以下情况下，远程调试使用 DCOM 在本地和远程计算机之间进行通信：

- 调试器设置为了“本机兼容性模式”，或在“工具”>“选项”>“调试”页内选中了“托管兼容模式”   

- 调试的是托管 C++ (C++/CLI) 代码。

- 在 Visual Studio 2013 中，在“工具”>“选项”>“调试”页内选中了“启用本机编辑并继续”  

- 某些第三方调试方案

  当 Visual Studio 进程无法通过 DCOM 针对远程调试器进程验证自己的身份（或提供的凭据被视为不足）时，将出现此错误。 以下一个或多个解决方法可解决此问题：

- 关闭“本机兼容模式”   和“托管兼容模式”  。

- 在 Visual Studio 2013 中，关闭“启用本机编辑并继续”  。

- 重新启动这两台计算机。

- 如果远程调试要求输入凭据，则选中该选项以保存凭据。

## <a name="see-also"></a>请参阅

- [远程调试错误和疑难解答](../debugger/remote-debugging-errors-and-troubleshooting.md)
- [远程调试](../debugger/remote-debugging.md)