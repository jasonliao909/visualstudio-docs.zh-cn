---
title: “设置基数”命令
description: 了解“设置基数”命令以及它如何设置或返回用于显示整数值的数值进制。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.setradix
helpviewer_keywords:
- Set Radix command
- Debug.SetRadix command
ms.assetid: 6ffd1554-7530-4da4-b5f5-e276a5034f3b
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: f693391cea9ccb17a5e5427d7508424c05c3d457
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126640836"
---
# <a name="set-radix-command"></a>“设置基数”命令
设置或返回用来显示整数值的数值基数。

## <a name="syntax"></a>语法

```cmd
Debug.SetRadix [10 | 16 | hex | dec]
```

## <a name="arguments"></a>参数
`10` 或 `16` 或 `hex` 或 `dec`

可选。 指示十进制（10 或 dec）或十六进制（16 或 hex）。 如果省略某个参数，则返回当前基数值。

## <a name="example"></a>示例
此示例将环境设置为以十六进制格式显示整数值。

```cmd
>Debug.SetRadix hex
```

## <a name="see-also"></a>另请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)