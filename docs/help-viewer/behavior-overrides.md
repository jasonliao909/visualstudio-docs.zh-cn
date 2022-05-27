---
title: 替代帮助查看器默认值
description: 了解 Help Content Manager 重写，它们可以更改 Visual Studio IDE 中的 Help Viewer 和帮助相关功能的默认行为。
ms.date: 05/17/2022
ms.topic: conceptual
ms.assetid: 95fe6396-276b-4ee5-b03d-faacec42765f
author: jasonchlus
ms.author: jasonchlus
manager: jmartens
ms.technology: vs-help-viewer
ms.custom: kr2b-contr-experiment
ms.workload:
- multiple
ms.openlocfilehash: a50b97c26eac92db23c4a9fc5ffd4ee1f5b6b7ce
ms.sourcegitcommit: 2e205fdee00c245816f3eb7b606cf3d91214cb19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2022
ms.locfileid: "145892691"
---
# <a name="override-help-viewer-defaults"></a>替代帮助查看器默认值

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]

可以在 Visual Studio IDE 中更改 Microsoft 帮助查看器的默认行为和帮助相关功能。

帮助内容管理器是一种工具，可用于部署和管理本地帮助查看器内容。 若要更改帮助查看器行为，可以替代帮助内容管理器可执行程序的默认设置，HlpCtntMgr.exe。

可通过不同的方法设置帮助内容管理器选项：

- 创建 . [pkgdef 文件](https://devblogs.microsoft.com/visualstudio/whats-a-pkgdef-and-why/) 以设置注册表项值。
- 直接在注册表中设置选项。

## <a name="use-a-pkgdef-file-to-change-help-viewer-behavior"></a>使用 .pkgdef 文件更改帮助查看器行为

.pkgdef 文件存储帮助查看器使用的配置信息。 可以使用 .pkgdef 文件调整下表列出了的注册表项值：

|注册表项值|类型|数据|说明|
|------------------|----|----|-----------|
|NewContentAndUpdateService|字符串|\<service endpoint URL\>|定义唯一的服务终结点|
|UseOnlineHelp|dword|`0` 指定本地帮助，`1` 指定联机帮助|定义联机或脱机帮助（默认）|
|OnlineBaseUrl|字符串|\<service endpoint URL\>|定义唯一的 F1 终结点|
|OnlineHelpPreferenceDisabled|dword|`0` 启用或 `1` 禁用联机帮助首选项|禁用联机帮助首选项|
|DisableManageContent|dword|`0` 启用或 `1` 禁用 Help Viewer 中的“管理内容”选项卡|禁用“管理内容”选项卡|
|DisableFirstRunHelpSelection|dword|`0` 启用或 `1` 禁用在 Visual Studio 首次启动时配置的帮助功能|禁用首次启动 Visual Studio 时的内容安装|

若要在 .pkgdef 文件中设置注册表项值，请执行以下步骤：

1. 创建新文件，并为其指定扩展名 *.pkgdef*。

1. 将以下文本添加到文件的第一行：

   `[$RootKey$\Help]`

1. 在单独的行上，添加上一个表描述的任何注册表项值。 例如，可以添加此行来配置 `UseOnlineHelp` 值：

   `"UseOnlineHelp"=dword:00000001`

1. 将文件复制到安装Visual Studio的 *CommonExtensions* 文件夹。 例如：

   - 如果使用 Visual Studio 2017 Community 版本，请将 .pkgdef 文件添加到此文件夹：

     *C：\Program Files (x86) \Microsoft Visual Studio\2017\Community\Common7\IDE\CommonExtensions*

   - 如果使用 Visual Studio 2022 Community 版本，请将 .pkgdef 文件添加到此文件夹：

     *C：\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\CommonExtensions*

1. 在开发人员命令提示符处运行以下命令：

   `devenv /updateconfiguration`

### <a name="example-pkgdef-file-contents"></a>示例 .pkgdef 文件内容

```pkgdef
[$RootKey$\Help]
"NewContentAndUpdateService"="https://some.service.endpoint"
"UseOnlineHelp"=dword:00000001
"OnlineBaseUrl"="https://some.service.endpoint"
"OnlineHelpPreferenceDisabled"=dword:00000000
"DisableManageContent"=dword:00000000
"DisableFirstRunHelpSelection"=dword:00000001
```

## <a name="use-registry-editor-to-change-help-viewer-behavior"></a>使用注册表编辑器更改帮助查看器的行为

可以通过在注册表编辑器中设置注册表项值来控制以下行为类型。

|任务|注册表项|Value|数据|
|----------|-----|------|----|
|替代 BITS 作业优先级|HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node（64 位计算机上）\Microsoft\Help\v2.3|BITSPriority|**foreground**、**high**、**normal** 或 **low**|
|指向网络共享上的本地内容存储区|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\ v2.3\Catalogs\VisualStudio15|LocationPath|*ContentStoreNetworkShare*|

## <a name="see-also"></a>另请参阅

- [Help Viewer 管理员指南](../help-viewer/administrator-guide.md)
- [Help Content Manager 的命令行参数](../help-viewer/command-line-arguments.md)
- [Microsoft Help Viewer](../help-viewer/overview.md)