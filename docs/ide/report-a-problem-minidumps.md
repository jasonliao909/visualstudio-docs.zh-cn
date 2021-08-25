---
title: 使用所有调用堆栈创建小型转储
description: 了解如何创建包含所有调用堆栈信息的 Visual Studio 进程小型转储。
ms.custom: SEO-VS-2020
ms.date: 06/27/2019
ms.topic: how-to
helpviewer_keywords:
- minidumps for Visual Studio issues"
author: corob-msft
ms.author: corob
manager: jmartens
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.description: Collect minidumps to send to Microsoft for help with troubleshooting issues with Visual Studio
ms.openlocfilehash: 169401462589b12c9d0d337d442c4288bf4e16ad
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122048578"
---
# <a name="create-minidumps-for-a-visual-studio-process-with-all-call-stacks"></a>使用所有调用堆栈为 Visual Studio 进程创建小型转储

在某些情况下，Microsoft 可能会要求提供正在运行的 Visual Studio 进程的小型转储，其中包含所有调用堆栈的信息。 要收集此信息，请执行以下步骤：

## <a name="create-the-minidump-file"></a>创建小型转储文件

1. 启动 Visual Studio 的新实例。
1. 从主菜单中，选择“调试” > “附加到进程”。
1. 勾选相关的“托管”和“本机”复选框，然后按“附加”。

   ![附加到进程](../ide/media/attach-to-process.png)

1. 从正在运行的进程列表中选择要附加的其他 Visual Studio 实例。
1. 从主菜单中，选择“调试” > “全部中断”。
1. 从主菜单中，选择“调试” > “将转储另存为”。

## <a name="get-the-call-stacks-from-the-minidump"></a>从小型转储中获取调用堆栈

1. 在 Visual Studio 中打开转储文件。
1. 转到“工具” > “选项” > “调试” > “符号”，确保在“符号文件(.pdb) 位置”中勾选“Microsoft 符号服务器”     。
1. 打开“命令”窗口（“视图” > “其他窗口” > “命令窗口”）
1. 键入“~*k”。 此窗口会显示所有线程的调用堆栈。
1. 从命令窗口中复制所有文本并保存到文本文件中。
1. 将 txt 文件附加到 bug。
