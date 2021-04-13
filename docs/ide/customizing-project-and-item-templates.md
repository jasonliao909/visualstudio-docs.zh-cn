---
title: 自定义项目和项模板
description: 了解创建项目和项模板后如何对其进行自定义。
ms.custom: SEO-VS-2021
ms.date: 03/29/2018
ms.topic: conceptual
helpviewer_keywords:
- customizing templates [Visual Studio]
- Visual Studio templates, customizing
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.openlocfilehash: 4229b0dcaf1c1cdacd7dd5a44cbb56afdfe9707d
ms.sourcegitcommit: 9c831a7f39e5b3e3c5db000b2545715bf12225f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2021
ms.locfileid: "105933779"
---
# <a name="customize-project-and-item-templates"></a>自定义项目和项模板

即使创建项目和项模板后，仍可以对其进行进一步自定义，使其满足要求。

## <a name="customizations"></a>自定义

例如，可以执行下列任务：

- 修改并将现有模板导出为用户模板。

   有关详细信息，请参阅[如何：更新现有模板](../ide/how-to-update-existing-templates.md)。

- 将自定义参数传递给模板以替换现有值。

   有关详细信息，请参阅[如何：替换模板中的参数](../ide/how-to-substitute-parameters-in-a-template.md)。

- 自定义根据模板创建项目的向导。

   有关详细信息，请参阅[如何：使用向导来处理项目模板（扩展性）](../extensibility/how-to-use-wizards-with-project-templates.md)。

## <a name="see-also"></a>请参阅

- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [如何：对模板进行故障排除](../ide/how-to-troubleshoot-templates.md)
- [如何：创建项目模板](../ide/how-to-create-project-templates.md)
- [如何：创建项模板](../ide/how-to-create-item-templates.md)
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- <xref:Microsoft.VisualStudio.TemplateWizard.IWizard>
- [使用 `dotnet new` 命令自定义模板](/dotnet/core/tools/custom-templates/)
- [使用 `dotnet sln` 命令在 .NET 解决方案文件中列出或修改项目](/dotnet/core/tools/dotnet-sln/)
