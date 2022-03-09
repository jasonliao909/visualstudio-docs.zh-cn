---
description: VS SDK 分析器错误 VsixCompatibility1001
title: VS SDK 分析器错误 VsixCompatibility1001
ms.date: 07/20/2015
ms.topic: error-reference
f1_keywords:
- VsixCompatibility1001
helpviewer_keywords:
- VsixCompatibility1001
- VSIX error codes, compatibility analyzer
author: ankitvarmait
ms.author: anva
manager: tinali
ms.technology: vs-ide-sdk
ms.openlocfilehash: 06aaee2fabc6b4f6f214e1c1bf2d5f7e5f86334f
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139604944"
---
# <a name="vs-sdk-analyzer-error-vsixcompatibility1001"></a>VS SDK 分析器错误 VsixCompatibility1001

由于引用不兼容的 VS SDK 版本，扩展与 Visual Studio 的目标版本不兼容。 

以下条件生成 VsixCompatibility1001：

- 正在为 Visual Studio 2022 更新或创建 Visual Studio 扩展。
- 你使用的是最新版本的 VSSDK) package (版本的 [BuildTools](https://www.nuget.org/packages/Microsoft.VSSDK.BuildTools/) 。
- 你使用的是早期版本的 [VisualStudio](https://www.nuget.org/packages/Microsoft.VisualStudio.Sdk/) (版本) 元包。

**解决方案**
- 将 [VisualStudio](https://www.nuget.org/packages/Microsoft.VisualStudio.Sdk/) 元包更新到 (版本) 的最新版本。