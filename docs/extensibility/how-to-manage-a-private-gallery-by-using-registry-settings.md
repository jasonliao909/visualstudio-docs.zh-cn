---
title: 使用注册表设置管理专用库
description: 了解如何控制对库、示例库或专用库中Visual Studio、模板和工具的访问。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- VSIX private galleries, managing
- managing VSIX private galleries
ms.assetid: 86b86442-4293-4cad-9fe2-876eef65f426
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 38cc90f557bb901f2ef9710bc1cd129e471a3781
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122124928"
---
# <a name="how-to-manage-a-private-gallery-by-using-registry-settings"></a>如何：使用注册表设置管理专用库
如果你是独立 Shell 扩展的管理员或开发人员，可以控制对 Visual Studio 库、示例库或专用库中的控件、模板和工具的访问。 若要使库可用或不可用，请创建一个 *.pkgdef* 文件，用于描述修改后的注册表项及其值。

## <a name="manage-private-galleries"></a>管理专用库
 可以创建 *.pkgdef* 文件来控制对多台计算机上库的访问。 此文件必须采用以下格式。

```
[$RootKey$\ExtensionManager\Repositories\{UniqueGUID}]
@={URI}  (REG_SZ)
Disabled=0 | 1 (DWORD)
Priority=0 (highest priority) ... MaxInt (lowest priority) (DWORD) (uint)
Protocol=Atom Feed|Sharepoint (REG_SZ)
DisplayName={DisplayName} (REG_SZ)
DisplayNameResourceID={ID} (REG_SZ)
DisplayNamePackageGuid={GUID} (REG_SZ)

```

 `Repositories`键是指要启用或禁用的库。 示例Visual Studio库和示例库使用以下存储库 GUID：

- Visual Studio库：0F45E408-7995-4375-9485-86B8DB553DC9

- 示例库：AEB9CB40-D8E6-4615-B52C-27E307F8506C

  该值 `Disabled` 是可选的。 默认情况下，库已启用。

  `Priority`值确定库在"选项"对话框中 **的列出** 顺序。 Visual Studio库的优先级为 10，示例库的优先级为 20。 专用库从优先级 100 开始。 如果多个库具有相同的优先级值，则它们的显示顺序取决于其本地化 `DisplayName` 属性的值。

  `Protocol`基于 Atom 的库或基于 Atom 的库SharePoint值。

  必须 `DisplayName` 指定 或 `DisplayNameResourceID` 同时 `DisplayNamePackageGuid` 指定 和 。 如果指定了所有 ，则 `DisplayNameResourceID` 使用 `DisplayNamePackageGuid` 和 对。

## <a name="disable-the-visual-studio-gallery-using-a-pkgdef-file"></a>使用 .pkgdef 文件Visual Studio库
 可以在 *.pkgdef* 文件中禁用库。 以下条目禁用Visual Studio库：

```
[$RootKey$\ExtensionManager\Repositories\{0F45E408-7995-4375-9485-86B8DB553DC9}]
"Disabled"=dword:00000001

```

 以下条目禁用示例库：

```
[$RootKey$\ExtensionManager\Repositories\{AEB9CB40-D8E6-4615-B52C-27E307F8506C}]
"Disabled"=dword:00000001

```

## <a name="see-also"></a>请参阅
- [专用库](../extensibility/private-galleries.md)
