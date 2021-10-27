---
title: -ResetSettings (devenv.exe)
description: 了解如何使用 ResetSettings devenv 命令行开关来还原 Visual Studio 默认设置并自动启动 Visual Studio IDE。
ms.custom: SEO-VS-2020
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- Devenv, /ResetSettings switch
- ResetSettings switch
- /ResetSettings Devenv switch
- settings [Visual Studio], resetting
ms.assetid: 1d41021c-6f58-4bd5-b122-d1c995812192
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: cbc3b329b4a525a525823169d63ebbda2770727e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126640858"
---
# <a name="resetsettings-devenvexe"></a>/ResetSettings (devenv.exe)

还原 Visual Studio 的默认设置，自动启动 Visual Studio IDE。 此开关视需要将这些设置重置为指定的设置文件 (`*.vssettings`)。

默认设置来自在 Visual Studio 首次启动时被选择的配置文件。

> [!TIP]
> 若要了解如何使用集成开发环境 (IDE) 重置设置，请参阅[重置设置](../environment-settings.md#reset-settings)。

## <a name="syntax"></a>语法

```shell
devenv /ResetSettings [SettingsFile|DefaultCollectionSpecifier]
```

## <a name="arguments"></a>参数

- *SettingsFile*

  可选。 应用于 Visual Studio 的 `.vssettings` 文件的完整路径和文件名。

- DefaultCollectionSpecifier

  可选。 表示要还原的默认设置集合的说明符。 从表中列出的默认集合说明符中选择一个。

  | 默认集合名称 | 集合说明符 |
  | --- | --- |
  | **常规** | `General` |
  | **JavaScript** | `JavaScript` |
  | **Visual Basic** | `VB` |
  | **Visual C#** | `CSharp` |
  | **Visual C++** | `VC` |
  | **Web 开发** | `Web` |
  | **Web 开发（仅代码）** | `WebCode` |

## <a name="remarks"></a>备注

如果没有指定 SettingsFile，IDE 使用现有设置打开。 


## <a name="example"></a>示例

第一个示例应用文件 `MySettings.vssettings` 中存储的设置。

第二个示例还原 Visual C# 默认配置文件。

第三个示例也将在应用设置后关闭 Visual Studio。 可以追加 `/Command "File.Exit"`。

```shell
devenv /ResetSettings "%USERPROFILE%\MySettings.vssettings"

devenv /ResetSettings CSharp

devenv /NoSplash /ResetSettings General /Command Exit 
```

## <a name="see-also"></a>另请参阅

- [环境设置](../environment-settings.md)
- [个性化设置 Visual Studio IDE](../../ide/personalizing-the-visual-studio-ide.md)
- [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)
