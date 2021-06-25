---
title: 向导 (。Vsz) File |Microsoft Docs
description: 了解 IDE 用于启动向导的 .vsz 文件。 这些文件包含有关要调用的向导以及要传递给向导的内容的信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- .vsz files
- vsz files
- wizards, files
ms.assetid: 72e1d0f3-eef1-455e-b803-96827f030f50
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: de687dae79fa1613090fb400f73ab658ee5d66cb
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900649"
---
# <a name="wizard-vsz-file"></a>向导 (.Vsz) 文件

IDE (集成) 使用 .vsz 文件启动向导。 这些 .vsz 文件包含 IDE 用于确定要调用的向导以及要传递给向导的信息的信息。

.vsz 文件是包含.ini的格式化文本文件的版本。 IDE 已知的信息存储在文件的开头。 这提供了 IDE 调用的向导与 .vsz 文件中要传递给 IDE 的参数之间的链接。 文件的其余部分提供特定于向导的参数，这些参数由 IDE 收集并传递给特定向导。

以下示例显示 .vsz 文件的内容。

```
VSWizard 8.0
Wizard=VsWizard.CBlankSiteWizard -or- {123-1234556-123334}
Param="WIZARDNAME = Wizard One"
Param="WIZARDUI = FALSE"
```

下面是 .vsz 文件中的各个部分。

|组成部分|描述|
|----------|-----------------|
|VSWizard|文件的第一个参数是模板文件格式的版本号。 此版本号必须为 6.0、7.0、7.1 或 8.0。 其他数字无法启动，导致格式无效错误。|
|向导|此字段包含向导的 OLE ProgID，或者包含由 IDE 共同创建向导的 CLSID 的 GUID 字符串表示形式。|
|Param|这些部分是可选的。 可根据需要添加多个 。|

这些参数使 .vsz 文件能够将其他自定义参数传递给向导。 每个值作为变体数组中的字符串元素传递给向导。 有关详细信息，请参阅 [自定义参数](../../extensibility/internals/custom-parameters.md)。

若要将默认区域设置 ID 添加到 .vsz 文件，请指定 =xxxx，其中 xxxx 是区域设置 `FALLBACK_LCID` ID，例如，1033 表示英语。 定义 `FALLBACK_LCID` 参数时，如果找不到当前 ID，向导将使用提供的回退区域设置 ID。

## <a name="see-also"></a>另请参阅

- [自定义参数](../../extensibility/internals/custom-parameters.md)
- [向导](../../extensibility/internals/wizards.md)
- [模板目录说明 (.Vsdir) 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)
