---
title: 为文件扩展名注册谓词|Microsoft Docs
description: 了解如何使用 Shell 密钥注册与文件扩展名的编程标识符关联的谓词。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- verbs, registering
ms.assetid: 81a58e40-7cd0-4ef4-a475-c4e1e84d6e06
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 00359f3d7d367333af8796b8d1a6ece104287539
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122124485"
---
# <a name="register-verbs-for-file-name-extensions"></a>为文件扩展名注册谓词
文件扩展名与应用程序的关联通常具有用户双击文件时发生的首选操作。 此首选操作链接到对应于该操作的谓词（例如 open）。

 可以使用位于 **HKEY_CLASSES_ROOT \{ progid}\shell** 的 Shell 密钥为扩展注册与编程标识符 (ProgID) 关联的谓词。 有关详细信息，请参阅 [文件类型](/windows/desktop/shell/fa-file-types)。

## <a name="register-standard-verbs"></a>注册标准谓词
 操作系统可识别以下标准谓词：

- 打开

- 编辑

- 显示

- 打印

- 预览

  如果可能，请注册标准谓词。 最常见的选择是 Open 谓词。 仅在打开文件与编辑文件之间存在明显差异时，才使用"编辑谓词"。 例如， *打开.htm文件* 会在浏览器中显示该文件， *而* 编辑.htm文件将启动 HTML 编辑器。 标准谓词使用操作系统区域设置进行本地化。

> [!NOTE]
> 注册标准谓词时，请勿设置 Open 键的默认值。 默认值包含菜单上的显示字符串。 操作系统为标准谓词提供此字符串。

 Project用户打开文件时，应注册新文件以 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 启动 的新实例。 下面的示例演示了项目的标准谓词 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 注册。

```
[HKEY_CLASSES_ROOT\.csproj]
@="VisualStudio.csproj.8.0"

[HKEY_CLASSES_ROOT\.csproj\OpenWithList]
[HKEY_CLASSES_ROOT\.csproj\OpenWithList\VSLauncher.exe]
@=""

[HKEY_CLASSES_ROOT\.csproj\OpenWithProgids]
"VisualStudio.csproj.8.0"=""

[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe]
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe\Shell]
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe\Shell\Open]
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe\Shell\Open\Command]
@="C:\\Program Files\\Common Files\\Microsoft Shared\\MSEnv\\VSLauncher.exe \"%1\""

[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0]
@="C# Project file"

[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\DefaultIcon]
@="C:\\VisualStudioPath\\VC#\\VCSPackages\\csproj.dll,0"

[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\shell]
[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\shell\Open]
[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\shell\Open\Command]
@="\"C:\\Program Files\\Common Files\\Microsoft Shared\\MSEnv\\VSLauncher.exe\" \"%1\""
```

 若要在 的现有实例中打开文件 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ，请注册 DDEEXEC 密钥。 下面的示例演示 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] *.cs* 文件的标准谓词注册。

```
[HKEY_CLASSES_ROOT\.cs]
@="VisualStudio.cs.8.0"

[HKEY_CLASSES_ROOT\.cs\OpenWithList]
[HKEY_CLASSES_ROOT\.cs\OpenWithList\devenv.exe]
@=""

[HKEY_CLASSES_ROOT\.cs\OpenWithProgids]
"VisualStudio.cs.8.0"=""

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0]
@="C# Source file"

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\DefaultIcon]
@="C:\\VisualStudioPath\\VC#\\VCSPackages\\csproj.dll,1"

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell]
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open]
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\Command]
@="\"C:\\VisualStudioPath\\Common7\\IDE\\devenv.exe\" /dde \"%1\""

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\ddeexec]
@="Open(\"%1\")"

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\ddeexec\Application]
@="VisualStudio.8.0"

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\ddeexec\Topic]
@="system"
```

## <a name="set-the-default-verb"></a>设置默认谓词
 默认谓词是当用户双击资源管理器中的文件时Windows操作。 默认谓词是指定为 **\\ *progid*\Shell** 键HKEY_CLASSES_ROOT默认值的谓词。 如果未指定值，则默认谓词是 **\\ *progid*\Shell** HKEY_CLASSES_ROOT中指定的第一个谓词。

> [!NOTE]
> 如果计划在并行部署中更改扩展的默认谓词，请考虑对安装和删除的影响。 在安装过程中，将覆盖原始默认值。

## <a name="see-also"></a>请参阅
- [管理并行文件关联](../extensibility/managing-side-by-side-file-associations.md)
