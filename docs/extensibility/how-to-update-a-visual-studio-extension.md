---
title: 如何：更新 Visual Studio 扩展 |Microsoft Docs
description: 了解如何使用扩展和更新来更新系统上的 Visual Studio 扩展，以便安装更新的版本。
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
你可以使用 "**扩展和更新**" 来更新系统上的 Visual Studio 扩展，以便安装更新的版本。 如果你创建扩展的更新版本，则可以通过在 VSIX 清单中递增版本号来将其表示为已更新。

 当传入扩展的 VSIX 清单 `ID` 与安装的扩展具有相同和更高的数目时，会安装更新 `Version` 。 如果 `Version` 数字相同或更低，则无法安装包。 如果 `ID` 值不匹配，则表示尚未安装的包被识别为单独的扩展。

 为了帮助防止开发过程中发生冲突，我们建议你卸载正在进行的较早版本的扩展，同时卸载或禁用任何其他可能存在冲突的扩展。

## <a name="to-update-an-extension-on-your-system"></a>更新系统上的扩展

1. 在“工具”菜单上，单击“扩展和更新”。

2. 在左窗格中，单击 " **更新**"。

3. 在中间窗格中，单击要安装的更新。

     更新的扩展的版本号将显示在右窗格中，以及其他信息。

4. 在右窗格的底部，单击 " **更新**"。

## <a name="to-publish-an-update-of-an-extension"></a>发布扩展的更新

1. 在 Visual Studio 中，打开要更新的扩展的解决方案。 进行更改。

    > [!IMPORTANT]
    > 无符号的所有用户扩展都不会自动更新。 应始终对扩展进行签名。

2. 在 **解决方案资源管理器** 中，打开 *源扩展名 .manifest*。

3. 在清单设计器中，增加 " **版本** " 字段中的数字值。

4. 保存并生成解决方案。

5. Upload 项目) 的 * \bin\Debug 文件夹中的新 *.vsix* 文件 (\* 到 [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs)网站。

     当具有较早版本的扩展的用户打开 " **扩展和更新**" 时，新版本将出现在 **更新** 列表中，前提是该工具设置为 "自动查找更新"。

     你可以启用或禁用 "**更新**" 窗格底部的 "自动检查更新" (**启用/禁用可用更新的自动检测**) ，这将更改 "**工具** 选项"   >    >  **环境**  >  **扩展和更新** 中的 "检查更新" 设置。

    > [!NOTE]
    > 从 Visual Studio 2015 Update 2 开始，你可以在 "**工具**  >  **选项**"  >  **环境**  >  **扩展和更新** 中指定 (，) 是要将每用户扩展的自动更新、所有用户扩展或两者 (默认设置) 。

## <a name="see-also"></a>请参阅
- [VSIX 包的解析](../extensibility/anatomy-of-a-vsix-package.md)
- [查找并使用 Visual Studio 扩展](../ide/finding-and-using-visual-studio-extensions.md)
