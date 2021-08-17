---
title: 专用库 |Microsoft Docs
description: 了解如何在 Visual Studio SDK 中共享在 SDK 中开发的控件、模板和工具，只需要将其发布到专用库即可。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSIX galleries, private
- private galleries, VSIX
ms.assetid: b6b3dee7-91c5-4556-9f69-0d56b675e83b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: b369996f59f91416cd0845e1b2b626e6dd1752d07935685a917589c382647c12
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121447819"
---
# <a name="private-galleries"></a>专用库
你可以共享你开发的控件、模板和工具，方法是将其发布到组织 intranet 上的 *专用库* ，如下所示：

- 将 Atom (RSS) 源创建到 intranet 上 (存储库) 的适当配置的中央位置。 有关详细信息，请参阅 [如何：创建专用库的 Atom 馈送](../extensibility/how-to-create-an-atom-feed-for-a-private-gallery.md)。

- 分发描述专用库的 *.pkgdef* 文件。 对于想要同时将专用库连接到多台计算机的管理员，我们建议使用此配置。

## <a name="add-a-private-gallery-to-extensions-and-updates-in-visual-studio"></a>将专用库添加到 Visual Studio 中的扩展和更新
 当专用库可用时，可以将其添加到 Visual Studio 中的 **扩展和更新** 中。

 ![“扩展管理器添加”对话框](../extensibility/media/em_adddialog.png "EM_AddDialog")

### <a name="to-add-a-private-gallery-to-extensions-and-updates"></a>向扩展和更新添加专用库

1. 在菜单栏上，依次选择“工具” > “选项” 。

2. 在 " **环境** " 节点中，选择 " **扩展和更新**"。

3. 选择“添加”按钮。

4. 在 " **名称** " 字段中，输入专用库的名称，例如 `My Gallery` 。

5. 在 " **URL** " 字段中，输入用于承载专用库的 Atom 馈送或 SharePoint 站点的 URL。

    1. 如果主机是连接到专用库的 Atom 馈送，则 URL 将如下所示： `http://www.mywebsite/mygallery/atom.xml` 。  此 URL 可以引用文件或网络路径。

    2. 如果主机是 SharePoint 站点，则 URL 将如下所示： `http://mysharepoint/sites/mygallery/forms/AllItems.aspx` 。

### <a name="manage-private-galleries"></a>管理专用库
 管理员可以通过修改每台计算机上的系统注册表，使多台计算机可以同时使用私有库。 为此，请创建一个描述新注册表项及其值的 *.pkgdef* 文件。  此文件的格式如下所示。

```
[$RootKey$\ExtensionManager\Repositories\{UniqueGUID}]
@={URI}  (REG_SZ)
Disabled=0 | 1 (DWORD)
Priority=0 (highest priority) ... MaxInt (lowest priority) (DWORD) (uint)
Protocol=Atom|Sharepoint (REG_SZ)
DisplayName={DisplayName} (REG_SZ)
DisplayNameResourceID={ID} (REG_SZ)
DisplayNamePackageGuid={GUID} (REG_SZ)

```

 有关详细信息，请参阅 [如何：使用注册表设置管理专用库](../extensibility/how-to-manage-a-private-gallery-by-using-registry-settings.md)。

## <a name="install-extensions-from-a-private-gallery"></a>从专用库安装扩展
 你可以从 "**扩展和更新**" 中的专用库搜索和安装 Visual Studio 扩展。 以下步骤使用名为的专用库 `My Gallery` 。

 ![安装专用库的扩展管理器](../extensibility/media/em_.png "EM_")

### <a name="to-search-for-and-install-extensions-from-a-private-gallery"></a>搜索并安装专用库中的扩展

1. 在菜单栏上，选择 "**工具**" "  >  **扩展和更新**"。

2. 在左窗格中，选择 " **联机扩展**"，然后选择 **"我的库**"。

3. 在右侧窗格中，选择一个扩展，然后选择 " **下载** " 按钮。

## <a name="update-extensions-from-a-private-gallery"></a>从私有库更新扩展
 在专用库中发布 Visual Studio 扩展的新版本时，可以更新已安装的扩展。 以下步骤使用名为的专用库 `My Repository` 。

 ![扩展管理器专用库更新](../extensibility/media/em_update.png "EM_Update")

### <a name="to-update-an-installed-extension-from-a-private-gallery"></a>从专用库中更新已安装的扩展

1. 在菜单栏上，选择 "**工具**" "  >  **扩展和更新**"。

2. 在左窗格中，选择 " **更新**"，然后选择 **"我的存储库**"。

3. 在右侧窗格中，选择一个扩展，然后选择 " **更新** " 按钮。

## <a name="see-also"></a>请参阅
- [查找并使用 Visual Studio 扩展](../ide/finding-and-using-visual-studio-extensions.md)
- [装运 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)
