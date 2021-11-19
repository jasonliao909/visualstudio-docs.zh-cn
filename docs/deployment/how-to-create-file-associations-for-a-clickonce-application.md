---
title: 创建文件关联（ClickOnce 应用）
description: 了解如何将 ClickOnce 应用程序与一个或多个文件扩展名关联，以便当用户打开此类文件时，应用程序将启动。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665609"
---
# <a name="how-to-create-file-associations-for-a-clickonce-application"></a>如何：为 ClickOnce 应用程序创建文件关联
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序可以与一个或多个文件扩展名相关联，以便当用户打开这些类型的文件时，应用程序将自动启动。 向 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序添加文件扩展名支持非常简单。

### <a name="to-create-file-associations-for-a-clickonce-application"></a>创建 ClickOnce 应用程序的文件关联

1. 正常创建 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序，或使用现有的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序。

2. 使用文本或 XML 编辑器（例如记事本）打开应用程序清单。

3. 查找 `assembly` 元素。 有关详细信息，请参阅 [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)。

4. 添加一个 `fileAssociation` 元素，将其作为`assembly` 元素的子元素。 `fileAssociation` 元素具有四个属性：

   - `extension`：要与应用程序关联的文件扩展名。

   - `description`：文件类型的说明，将显示在 Windows shell 中。

   - `progid`：唯一标识文件类型的字符串，以在注册表中标记它。

   - `defaultIcon`：用于此文件类型的图标。 该图标必须添加为应用程序清单中的文件资源。 有关详细信息，请参阅[如何：将数据文件添加到 ClickOnce 应用程序中](../deployment/how-to-include-a-data-file-in-a-clickonce-application.md)。

     有关 `file` 和 `fileAssociation` 元素的示例，请参阅 [\<fileAssociation> 元素](../deployment/fileassociation-element-clickonce-application.md)。

5. 如果要将多个文件类型与应用程序关联，请添加其他 `fileAssociation` 元素。 请注意，每个文件类的 `progid` 属性应不同。

6. 完成应用程序清单后，对清单重新签名。 可以通过使用 Mage.exe 从命令行执行此操作。

    `mage -Sign WindowsFormsApp1.exe.manifest -CertFile mycert.pfx`

    有关详细信息，请参阅 [Mage.exe（清单生成和编辑工具）](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)。

## <a name="see-also"></a>另请参阅
- [\<fileAssociation> 元素](../deployment/fileassociation-element-clickonce-application.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)
- [Mage.exe（清单生成和编辑工具）](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)