---
title: “监视”命令
description: 了解 Watch 命令，以及它如何创建和打开“监视”窗口的指定实例。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.watch
helpviewer_keywords:
- Watch command
- Debug.Watch command
ms.assetid: aa02e647-d9f5-4905-a651-52a8df595795
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 2258c704e8a91b2b00942a8dcae5ca5215da028d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122056038"
---
# <a name="watch-command"></a>“监视”命令
创建并打开指定“监视”  窗口的实例。 可使用“监视”窗口计算变量、表达式或寄存器的值，然后编辑这些值并保存结果。

## <a name="syntax"></a>语法

```cmd
Debug.Watch[index]
```

## <a name="arguments"></a>自变量

`index`\
必需。 监视窗口的实例数。

## <a name="remarks"></a>备注

`index` 必须为整数。 有效值为 1、2、3 或 4。

## <a name="example"></a>示例

```cmd
>Debug.Watch1
```

## <a name="see-also"></a>请参阅

- [“自动”和“局部变量”窗口](../../debugger/autos-and-locals-windows.md)
- [在 Visual Studio 中使用“监视”窗口和“快速监视”窗口对变量设置监视](../../debugger/watch-and-quickwatch-windows.md)
- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)
