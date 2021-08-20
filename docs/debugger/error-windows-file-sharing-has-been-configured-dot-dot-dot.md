---
description: 已配置 Windows 文件共享，因此您将使用另一不同的用户名连接到远程计算机。
title: 已配置 Windows 文件共享... | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.remote_credentials_prohibited
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
ms.openlocfilehash: 2c0ea67f32474b124d4f6e4987de6a0491b6aaba
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122154351"
---
# <a name="error-windows-file-sharing-has-been-configured"></a>错误：已配置 Windows 文件共享...
已配置 Windows 文件共享，因此您将使用另一不同的用户名连接到远程计算机。 这与远程调试不兼容

 当前文件共享配置设置为使用另一用户名连接到远程计算机。 在这种情况下不能进行远程调试。

 若要更正此错误，请使用其他帐户名登录到计算机上，或是更改文件共享以使用要用来进行调试的帐户名。

 如果要使用此用户名连接到远程计算机，则必须首先从远程计算机断开连接。

### <a name="to-correct-this-error"></a>更正此错误

1. 使用其他帐户名登录到本地计算机（要从其进行调试的计算机）上。

     \- 或 -

     . 中断与远程计算机的连接，然后重新配置文件共享，以便使用您的帐户名称连接至其他计算机：

    1. 在“开始”菜单上，指向“附件”，然后单击“命令提示”  。

    2. 在 Windows 命令提示符中，键入：

         `net use /delete computer_name`

    3. 使用 Windows 帮助中介绍的任一方法更改文件共享设置。
