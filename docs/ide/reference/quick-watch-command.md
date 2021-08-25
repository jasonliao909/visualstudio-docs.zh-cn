---
title: “快速监视”命令
description: 了解 Quick Watch 命令，以及它如何在“快速监视”窗口的“表达式”字段中显示选定文本或指定文本。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.quickwatch
helpviewer_keywords:
- Quick Watch command
- Debug.Quickwatch command
ms.assetid: 9670ac3a-8f2f-4874-974d-cb87d3b0cde1
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 3b47b34fafce8acf2eebaf01257e76df5b195c14
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122056155"
---
# <a name="quick-watch-command"></a>“快速监视”命令
在[快速监视](../../debugger/watch-and-quickwatch-windows.md)窗口的“表达式”字段中显示选定或指定的文本。 可使用此对话框计算调试器所识别的变量或表达式的当前值或计算寄存器的内容。 此外，可更改任何非常量变量的值或任何寄存器的内容。

## <a name="syntax"></a>语法

```cmd
Debug.QuickWatchq [text]
```

## <a name="arguments"></a>自变量

`text`\
可选。 要添加到“快速监视”对话框的文本。

## <a name="remarks"></a>备注

如果忽略了 `text`，则光标处当前选中的文本或字词将添加到“监视”窗口。

## <a name="example"></a>示例

```cmd
>Debug.QuickWatch
```

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中使用“监视”窗口和“快速监视”窗口对变量设置监视](../../debugger/watch-and-quickwatch-windows.md)
- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)
