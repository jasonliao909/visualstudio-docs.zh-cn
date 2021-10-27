---
title: “设置当前线程”命令
description: 了解“设置当前线程”命令，以及它如何将指定的线程设置为当前线程。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.setcurrentthread
helpviewer_keywords:
- Set Current Thread command
- Debug.SetCurrentThread command
ms.assetid: 9917ed1d-6c30-4d94-b2f0-69acce74f1b2
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 302dd26541c49c4cd8f84da437c298dca40421ba
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126640839"
---
# <a name="set-current-thread-command"></a>“设置当前线程”命令
将指定的线程设置为当前线程。

## <a name="syntax"></a>语法

```
Debug.SetCurrentThread index
```

## <a name="arguments"></a>自变量
`index`

必需。 按线程的索引选择线程。

## <a name="example"></a>示例

```
>Debug.SetCurrentThread 1
```

## <a name="see-also"></a>另请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)