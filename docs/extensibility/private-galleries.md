---
title: 专用库|Microsoft Docs
description: 了解如何通过将控件、模板和工具发布到专用库来共享在 Visual Studio SDK 中开发的工具。
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
ms.openlocfilehash: ae9a2683cf7f80b415b81a2f3f96d940ff62dc99
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122102137"
---
# <a name="private-galleries"></a>专用库
可以通过将控件、模板和工具发布到组织的 Intranet 上的专用库来共享开发控件、模板和工具，如下所示：

- 创建 Atom (RSS) 源，以在 Intranet 上 (配置) 中心位置。 有关详细信息，请参阅 [如何：为专用库创建 Atom 源](../extensibility/how-to-create-an-atom-feed-for-a-private-gallery.md)。

- 分发 *描述专用库的 .pkgdef* 文件。 对于想要同时将专用库连接到多台计算机的管理员，建议采用此配置。

## <a name="add-a-private-gallery-to-extensions-and-updates-in-visual-studio"></a>将专用库添加到扩展和更新Visual Studio
 当专用库可用时，可以将其添加到"扩展和更新"Visual Studio。 

 ![“扩展管理器添加”对话框](../extensibility/media/em_adddialog.png "EM_AddDialog")

### <a name="to-add-a-private-gallery-to-extensions-and-updates"></a>将专用库添加到扩展和更新

1. 在菜单栏上，依次选择“工具” > “选项” 。

2. 在"**环境"** 节点中，选择 **"扩展和更新"。**

3. 选择“添加”按钮。

4. 在 **"名称** "字段中，输入专用库的名称，例如 `My Gallery` 。

5. 在 **"URL"** 字段中，输入托管专用库SharePoint Atom 源或源站点的 URL。

    1. 如果主机是连接到专用库的 Atom 源，则 URL 将类似于 `http://www.mywebsite/mygallery/atom.xml` ：。  此 URL 可以引用文件或网络路径。

    2. 如果主机是SharePoint站点，则 URL 将类似于 `http://mysharepoint/sites/mygallery/forms/AllItems.aspx` ：。

### <a name="manage-private-galleries"></a>管理专用库
 管理员可以通过修改每台计算机上的系统注册表，使专用库同时可供多台计算机使用。 为此，请创建一个 *.pkgdef* 文件，用于描述新的注册表项及其值。  此文件的格式如下所示。

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

 有关详细信息，请参阅 [如何：使用注册表](../extensibility/how-to-manage-a-private-gallery-by-using-registry-settings.md)设置 管理专用库。

## <a name="install-extensions-from-a-private-gallery"></a>从专用库安装扩展
 可以在"扩展和更新"Visual Studio专用库中搜索和安装 **扩展**。 以下步骤使用名为 的专用库 `My Gallery` 。

 ![安装专用库的扩展管理器](../extensibility/media/em_.png "EM_")

### <a name="to-search-for-and-install-extensions-from-a-private-gallery"></a>从专用库搜索和安装扩展

1. 在菜单栏上，选择"**工具**  >  **扩展和更新"。**

2. 在左窗格中，选择"**联机扩展"，** 然后选择"**我的库"。**

3. 在右窗格中，选择一个扩展，然后选择"下载 **"** 按钮。

## <a name="update-extensions-from-a-private-gallery"></a>从专用库更新扩展
 当新版本的 Visual Studio扩展发布在专用库中时，可以更新已安装的扩展。 以下步骤使用名为 的专用库 `My Repository` 。

 ![扩展管理器专用库更新](../extensibility/media/em_update.png "EM_Update")

### <a name="to-update-an-installed-extension-from-a-private-gallery"></a>从专用库更新已安装的扩展

1. 在菜单栏上，选择"**工具**  >  **扩展和更新"。**

2. 在左窗格中，选择"**更新"，** 然后选择"**我的存储库"。**

3. 在右窗格中，选择一个扩展，然后选择"更新 **"** 按钮。

## <a name="see-also"></a>请参阅
- [查找和使用Visual Studio扩展](../ide/finding-and-using-visual-studio-extensions.md)
- [提供Visual Studio扩展](../extensibility/shipping-visual-studio-extensions.md)
