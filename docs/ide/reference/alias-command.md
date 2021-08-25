---
title: “别名”命令
description: 了解如何使用“别名”命令为完整命令、完整命令和参数或另一个别名创建新别名。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- tools.alias
helpviewer_keywords:
- aliases, Visual Studio commands
- commands, aliases
- Tools.Alias command
- command aliases
- alias command
ms.assetid: bdf857df-b5d5-450f-8c10-a6fd4dccc130
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: f5c1b3f07a563484b70e36ed4257ee4dac005faf
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122101630"
---
# <a name="alias-command"></a>“别名”命令
为完整命令、完整命令和参数或另一个别名创建新别名。

> [!TIP]
> 键入 `>alias` 但不带任何参数会显示别名及其定义的当前列表。

## <a name="syntax"></a>语法

```cmd
Tools.Alias [/delete] [/reset] [aliasname] [aliasstring]
```

## <a name="arguments"></a>自变量
`aliasname`\
可选。 新别名的名称。 如果不为 `aliasname` 提供任何值，则显示当前别名及其定义的列表。

`aliasstring`\
可选。 完整命令名称、现有别名或想创建为别名的任何参数。 如果不为 `aliasstring` 提供任何值，则显示指定别名的名称和字符串。

## <a name="switches"></a>交换机
/delete 或 /del 或 /d\
可选。 删除指定别名，将其从自动补全中删除。

/reset\
可选。 将预定义别名的列表重置为其原始设置。 即还原所有预定义别名，并删除所有用户定义的别名。

## <a name="remarks"></a>注解
别名表示命令，因此别名必须位于命令行的开头。

发出此命令时，应将开关紧跟在命令（而不是别名）之后，否则开关本身会被视为别名字符串。

`/reset` 开关会在还原别名之前要求确认。 `/reset` 没有缩写形式。

## <a name="examples"></a>示例
此示例会为完整命令 Edit.MakeUpperCase 创建一个新别名 `upper`。

```cmd
>Tools.Alias upper Edit.MakeUpperCase
```

此示例会删除别名 `upper`。

```cmd
>Tools.alias /delete upper
```

此示例会显示所有当前别名和定义的列表。

```cmd
>Tools.Alias
```

## <a name="see-also"></a>另请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)
