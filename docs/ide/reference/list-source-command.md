---
title: “列出源”命令
description: 了解 List Source 命令，以及它如何显示源代码的指定行。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- Debug.ListSource
helpviewer_keywords:
- Debug.ListSource command
- list source command
- ListSource command
ms.assetid: e45f08d2-f4a3-49c3-9452-aa60508e2f74
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 03f62140322bca8efb3a3f8ba006293ab52ce665
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126641784"
---
# <a name="list-source-command"></a>“列出源”命令
显示源代码的指定行。

## <a name="syntax"></a>语法

```
Debug.ListSource [/Count:number] [/Current] [/File:filename]
[/Line:number] [/ShowLineNumbers:yes|no]
```

## <a name="switches"></a>交换机
/Count:`number`

可选。 指定要显示的行的编号。

/Current

可选。 显示当前行。

/File:`filename`

可选。 要显示的文件的路径。 如果未指定文件名，该命令会显示当前语句所在行的源代码。

/Line:`number`

可选。 显示特定行号。

/ShowLineNumbers:`yes|no`

可选。 指定是否显示行号。

## <a name="example"></a>示例
此示例列出文件 Form1.vb 第 4 行的源代码，并显示行号。

```
Debug.ListSource /File:"C:\Visual Studio Projects\Form1.vb" /Line:4 /ShowLineNumbers:yes
```

## <a name="see-also"></a>另请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)