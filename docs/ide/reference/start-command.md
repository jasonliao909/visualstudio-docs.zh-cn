---
title: “启动”命令
description: 了解“启动”命令以及它如何开始调试启动项目。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.start
helpviewer_keywords:
- Start command
- Debug.Start command
ms.assetid: dc4e4aa2-b0ab-4e00-92db-6dc3058ddc21
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: f5eb9036b12d066e03eb6e4de346d99f78b04c79
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122048695"
---
# <a name="start-command"></a>“启动”命令
开始调试启动项目。

## <a name="syntax"></a>语法

```cmd
Debug.Start [address]
```

## <a name="arguments"></a>自变量
`address`

可选。 程序挂起执行的地址，类似于源代码中的断点。 此参数仅在调试模式下有效。

## <a name="remarks"></a>备注
“启动”命令在执行时会对指定的地址执行 RunToCursor 操作。

## <a name="example"></a>示例
此示例启动调试器并忽略任何发生的异常。

```cmd
>Debug.Start
```

## <a name="see-also"></a>另请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)
