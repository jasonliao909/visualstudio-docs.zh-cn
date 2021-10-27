---
title: -DoNotLoadProjects (devenv.exe)
description: 了解如何使用 DoNotLoadProjects devenv 命令行开关在不加载任何项目的情况下打开指定的解决方案。
ms.custom: SEO-VS-2020
ms.date: 04/30/2019
ms.topic: reference
helpviewer_keywords:
- Devenv, /DoNotLoadProjects switch
- /DoNotLoadProjects Devenv switch
- DoNotLoadProjects Devenv switch
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 06e3320697acc7dac972da1233532fda06869701
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126640679"
---
# <a name="donotloadprojects-devenvexe"></a>/DoNotLoadProjects (devenv.exe)

**Visual Studio 2019 版本 16.1 中的新增功能**

打开指定的解决方案，而不加载任何项目。 有关详细信息，请参阅 [Visual Studio 中筛选的解决方案](../filtered-solutions.md)。

## <a name="syntax"></a>语法

```shell
devenv /DoNotLoadProjects SolutionName
```

## <a name="arguments"></a>自变量

*SolutionName*

必需。 要打开的解决方案的完整路径和名称。

## <a name="example"></a>示例

该示例将打开解决方案 MySln.sln 而不加载任何项目。

```shell
devenv /donotloadprojects MySln.sln
```

## <a name="see-also"></a>请参阅

- [Visual Studio 中筛选的解决方案](../filtered-solutions.md)
- [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)
