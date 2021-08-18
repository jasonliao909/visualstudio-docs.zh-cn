---
title: '创建应用 (ClickOnce文件) '
description: 了解如何将 ClickOnce与一个或多个文件扩展名关联，以便应用程序在用户打开此类文件时启动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- file associations, ClickOnce applications
- ClickOnce deployment, file associations
ms.assetid: 835230c8-3177-440f-85e3-e40f1d8b4f9d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: f05e61bc44f8a2db5f4a498df369131cc728df0a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122127956"
---
# <a name="how-to-create-file-associations-for-a-clickonce-application"></a>如何：为 ClickOnce 应用程序创建文件关联
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序可以与一个或多个文件扩展名相关联，以便当用户打开这些类型的文件时，应用程序将自动启动。 向应用程序添加文件扩展名 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 支持非常简单。

### <a name="to-create-file-associations-for-a-clickonce-application"></a>为应用程序创建ClickOnce关联

1. 正常 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 创建应用程序，或使用现有 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序。

2. 使用文本或 XML 编辑器打开应用程序清单，例如记事本。

3. 查找 `assembly` 元素。 有关详细信息，请参阅应用程序[ClickOnce清单](../deployment/clickonce-application-manifest.md)。

4. 添加 元素作为 `assembly` 元素的子 `fileAssociation` 元素。 元素 `fileAssociation` 有四个属性：

   - `extension`：要与应用程序关联的文件扩展名。

   - `description`：文件类型的说明，该类型将显示在 Windows shell 中。

   - `progid`：唯一标识文件类型的字符串，以在注册表中标记它。

   - `defaultIcon`：用于此文件类型的图标。 该图标必须添加为应用程序清单中的文件资源。 有关详细信息，请参阅[如何：将数据文件添加到 ClickOnce 应用程序中](../deployment/how-to-include-a-data-file-in-a-clickonce-application.md)。

     有关 和 元素 `file` `fileAssociation` 的示例，请参阅[ \<fileAssociation> 元素](../deployment/fileassociation-element-clickonce-application.md)。

5. 如果要将多个文件类型与应用程序关联，请添加其他 `fileAssociation` 元素。 请注意， `progid` 每个属性的属性应该不同。

6. 完成应用程序清单后，对清单重新签名。 可以通过使用 命令从 *命令行Mage.exe。*

    `mage -Sign WindowsFormsApp1.exe.manifest -CertFile mycert.pfx`

    有关详细信息，请参阅 [Mage.exe（清单生成和编辑工具）](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)。

## <a name="see-also"></a>请参阅
- [\<fileAssociation> 元素](../deployment/fileassociation-element-clickonce-application.md)
- [ClickOnce应用程序清单](../deployment/clickonce-application-manifest.md)
- [Mage.exe（清单生成和编辑工具）](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)