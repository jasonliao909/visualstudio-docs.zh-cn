---
title: Debug.Print
description: 了解 Print 命令，以及它如何计算表达式或显示指定文本。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.print
helpviewer_keywords:
- Debug.Print command
- Print method
- Print command
ms.assetid: 0412d381-590a-483f-bab4-6e1cca095645
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 157f8cfe3847aadebc34edb763fdda726f7cd1eb
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126641127"
---
# <a name="print-command"></a>Print 命令

计算表达式或显示指定文本。

## <a name="syntax"></a>语法

```cmd
>Debug.Print text
```

## <a name="arguments"></a>自变量

`text`

必需。 要计算的表达式或要显示的文本。

## <a name="remarks"></a>备注

可使用问号 (?) 作为此命令的别名。 例如，命令

```cmd
>Debug.Print expA
```

也可写作

```cmd
? expA
```

此命令的这两个版本都会返回表达式 `expA` 的当前值。

## <a name="example"></a>示例

```cmd
>Debug.Print DateTime.Now.Day
```

## <a name="see-also"></a>请参阅

- [“计算语句”命令](../../ide/reference/evaluate-statement-command.md)
- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)
