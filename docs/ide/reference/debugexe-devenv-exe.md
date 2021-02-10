---
title: -DebugExe (devenv.exe)
description: 了解如何使用 DebugExe devenv 命令行开关打开要调试的指定可执行文件。
ms.custom: SEO-VS-2020
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- Devenv, /DebugExe switch
- DebugExe switch
- /DebugExe [devenv.exe]
- debugging executables
ms.assetid: cd700006-1648-418f-924b-4b1e5c1412ab
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 5cdf770446b78b1a1bb4b55d61f4c3e9f50c4035
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894603"
---
# <a name="debugexe-devenvexe"></a>/DebugExe (devenv.exe)

打开要调试的指定可执行文件。

## <a name="syntax"></a>语法

```shell
devenv /DebugExe ExecutableFile
```

## <a name="arguments"></a>参数

- ExecutableFile

  必需。 `.exe` 文件的路径和文件名。 如果 `.exe` 文件找不到或不存在，Visual Studio 不会显示任何警告或错误，而是正常启动。

## <a name="remarks"></a>备注

ExecutableFile 参数后跟的任何字符串都作为参数传递到相应文件。

## <a name="example"></a>示例

以下示例打开文件 `MyApplication.exe` 进行调试。

```shell
devenv /debugexe MyApplication.exe
```

## <a name="see-also"></a>另请参阅

- [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)
