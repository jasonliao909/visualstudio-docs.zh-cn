---
title: “列出反汇编”命令
description: 了解 List Disassembly 命令，以及它如何开始调试过程并允许你指定处理错误的方式。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.listdisassembly
helpviewer_keywords:
- Debug.ListDisassembly command
- list disassembly command
ms.assetid: eb363e35-e86a-4121-966f-991210c27e2a
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: f41021b3b0d8c4dd0d0d688573bdc2e5c37da8f6
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122143802"
---
# <a name="list-disassembly-command"></a>“列出反汇编”命令
开始调试进程，并允许指定如何处理错误。

## <a name="syntax"></a>语法

```cmd
Debug.ListDisassembly [/count:number] [/endaddress:expression]
[/codebytes:yes|no] [/source:yes|no] [/symbolnames:yes|no]
[/linenumbers:yes|no]
```

## <a name="switches"></a>交换机
每个开关都可以使用其完整形式或缩写形式来调用。

/count: `number` [or] /c: `number` [or] /length: `number` [or] /l: `number`

可选。 要显示的指令数。 默认值为 8。

/endaddress: `expression` [or] /e: `expression`

可选。 停止反汇编的地址。

/codebytes:`yes`&#124;`no` [or] /bytes:`yes`&#124;`no` [or] /b:`yes`&#124;`no`

可选。 指示是否显示代码字节。 默认值为 `no`。

/source:`yes`&#124;`no` [or] /s:`yes`&#124;`no`

可选。 指示是否显示源代码。 默认值为 `no`。

/symbolnames:`yes`&#124;`no` [or] /names:`yes`&#124;`no` [or] /n:`yes`&#124;`no`

可选。 指示是否显示符号名称。 默认值为 `yes`。

 [/linenumbers:`yes`&#124;`no`]

可选。 启用查看与源代码关联的行号。 /source 开关必须具有 `yes` 的值来使用 /linenumbers 开关。

## <a name="example"></a>示例

```cmd
>Debug.ListDisassembly
```

## <a name="see-also"></a>请参阅

- [“列出调用堆栈”命令](../../ide/reference/list-call-stack-command.md)
- [“列出线程”命令](../../ide/reference/list-threads-command.md)
- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)