---
title: “转到”命令
description: 了解 Go To 命令，以及它如何将光标移动到指定的行。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- edit.goto
helpviewer_keywords:
- Debug.Goto command
- Go To command
ms.assetid: 201e1dd2-6701-467d-8cc1-faec2ef20511
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: ebc75b92886ea4d6938a2dd517418a3fac41e8f4
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122143828"
---
# <a name="go-to-command"></a>Go To 命令
将光标移到指定的行。

## <a name="syntax"></a>语法

```cmd
Edit.GoTo [linenumber]
```

## <a name="arguments"></a>自变量
`linenumber`\
可选。 一个表示要转到的行号的整数。

## <a name="remarks"></a>备注
行号从 1 开始。 如果 `linenumber` 的值小于 1，则显示第一行。 如果 `linenumber` 的值大于最后一行的行号，则显示最后一行。

如果未指定 `linenumber` 的值，则显示“转到行”对话框。

此命令的别名为 GoToLn。

## <a name="example"></a>示例

```cmd
>Edit.GoTo 125
```

## <a name="see-also"></a>另请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)
