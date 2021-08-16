---
title: 如何：更新 Visual Studio 扩展|Microsoft Docs
description: 了解如何使用扩展Visual Studio更新版本在系统上更新扩展。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- update package
- update extension
- new package version
ms.assetid: 93f79774-7b79-4dd6-94ad-13698f72c257
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 8b1dce6d9f8e410f4cf0b642a2f50eeb864a0d54d7fedafa3a524e76615ebb83
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121401591"
---
# <a name="how-to-update-a-visual-studio-extension"></a>如何：更新 Visual Studio 扩展
可以使用扩展Visual Studio更新来安装更新的版本，在系统上更新扩展。 如果创建扩展的更新版本，可以通过递增 VSIX 清单中的版本号来将扩展表示为已更新。

 当传入扩展的 VSIX 清单与已安装的清单相同且编号较高时 `ID` ，将安装 `Version` 更新。 如果 `Version` 数字相同或更低，则不能安装包。 如果 `ID` 值不匹配，则尚未安装的包被识别为单独的扩展。

 为了帮助防止开发期间发生冲突，建议卸载正在进行中的早期版本的扩展，并卸载或禁用任何其他可能冲突的扩展。

## <a name="to-update-an-extension-on-your-system"></a>更新系统上的扩展

1. 在“工具”菜单上，单击“扩展和更新”。

2. 在左窗格中，单击"更新 **"。**

3. 在中间窗格中，单击要安装的更新。

     更新的扩展的版本号将连同其他信息一起显示在右窗格中。

4. 在右窗格底部，单击"更新 **"。**

## <a name="to-publish-an-update-of-an-extension"></a>发布扩展的更新

1. 在Visual Studio中，打开要更新的扩展的解决方案。 进行更改。

    > [!IMPORTANT]
    > 未签名的每个用户扩展不会自动更新。 应始终对扩展进行签名。

2. 在 **解决方案资源管理器** 中，打开 *source.extension.manifest*。

3. 在清单设计器中，增加"版本"字段中 **数字** 的值。

4. 保存并生成解决方案。

5. Upload新的 *.vsix* (项目 *\bin\Debug 文件夹中) 到 Visual Studio \* [Marketplace](https://marketplace.visualstudio.com/vs)网站。

     当具有早期版本的扩展的用户打开"扩展和更新"时，新版本将显示在"更新"列表中，只要该工具设置为自动查找更新。

     可以在"更新"窗格底部启用或禁用自动更新检查 (启用 **/** 禁用对可用更新的自动检测) ，这将更改"工具""选项""环境扩展和更新"中的"检查更新"  >    >    >  **设置**。

    > [!NOTE]
    > 从 Visual Studio 2015 Update 2 开始，可以在"工具""选项""环境扩展和更新") 中指定" ("，无论是否要自动更新每用户扩展、所有用户扩展或两者 (默认设置  >    >    >  ) 。

## <a name="see-also"></a>另请参阅
- [VSIX 包剖析](../extensibility/anatomy-of-a-vsix-package.md)
- [查找和使用Visual Studio扩展](../ide/finding-and-using-visual-studio-extensions.md)
