---
title: 创建扩展包
description: 了解如何使用扩展包项模板创建扩展包
ms.custom: SEO-VS-2020
ms.date: 07/27/2018
ms.topic: tutorial
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: 5388EEBA-211D-4114-8CD9-70C899919F7E
author: leslierichardson95
ms.author: lerich
manager: Meng
ms.workload:
- vssdk
ms.openlocfilehash: 213e3e71503ebea8074594bbc88a06980e3e64b4
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905132"
---
# <a name="walkthrough-create-an-extension-pack"></a>演练：创建扩展包

扩展包是一组可以一起安装的扩展。 借助扩展包，可以轻松地与其他用户共享你喜欢的扩展，或将一组扩展捆绑到一起，以用于特定场景。

## <a name="prerequisites"></a>先决条件

从 Visual Studio 2015 开始，Visual Studio SDK 作为可选功能包含在 Visual Studio 设置中。 也可稍后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

从 Visual Studio 15.8 预览版 2 开始提供扩展包功能。

## <a name="create-an-extension-with-an-extension-pack-item-template"></a>使用扩展包项模板创建扩展

扩展包项模板会创建一个扩展包，该扩展包具有一组可以一起安装的扩展。

1. 在“新建项目”对话框中，搜索“vsix”并选择“VSIX 项目” 。 对于“项目名称”，请键入“测试扩展包”。 选择“创建”。

2. 在“解决方案资源管理器”中，右键单击项目节点并选择“添加” > “新建项”  。 转到“Visual C# 扩展性”节点，然后选择“扩展包” 。 保留默认文件名 (ExtensionPack1.cs)。

3. 添加了 ExtensionPack1.vsext 文件，其中包含以下代码

   ```json
   {
    "id": "ExtensionPack1",
    "name": "ExtensionPack1",
    "description": "Read about creating extension packs at https://aka.ms/vsextpack",
    "version": "1.0.0.0",
    "extensions": [  // List of extensions that are included in the Extension Pack.
      {
        "vsixId": "41858b2d-ff0b-4a43-80b0-f1b2d6084935", // The vsix id of the extension you want to   include.
        "name": "AlignAssignments"
      },
      {
          "vsixId": "42374550-426a-400e-96f9-237682e8dea6",
        "name": "CopyAsHtml"
      }
    ]
   }
   ```

4. 可在 [Visual Studio Marketplace](https://marketplace.visualstudio.com/) 中找到要包含在扩展包中的扩展的 vsixid。 找到要包含的扩展，然后单击“复制 ID”。 可以更新上述文件的现有 vsixId 或将其他扩展添加到列表中。

    ![从 Marketplace 复制 VsixId](media/vsixid-marketplace.png)

5. 生成项目，将扩展上传到 Marketplace。 请参阅[发布 Visual Studio 扩展](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)。

> [!NOTE]
> 扩展包只能安装 [Visual Studio Marketplace](https://marketplace.visualstudio.com/) 或[专用库](../extensibility/how-to-create-an-atom-feed-for-a-private-gallery.md)中提供的扩展。

## <a name="install-the-extension-pack-from-the-visual-studio-marketplace"></a>安装 Visual Studio Marketplace 中的扩展包

发布扩展后，请在 Visual Studio 中进行安装和测试。

::: moniker range="vs-2017"

1. 在 Visual Studio 的“工具”菜单中，单击“扩展和更新” 。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在 Visual Studio 的“扩展”菜单上，单击"托管扩展" 。

::: moniker-end

2. 单击“联机”，然后搜索“测试扩展包”。

3. 单击“下载”。 扩展包中包含的扩展及其扩展列表将按计划安装。

4. 下面是“管理扩展”对话框的示例扩展包下载视图。 如果希望仅安装扩展包中包含的某些扩展，可以在“计划安装”中修改扩展列表。

    ![从 Marketplace 下载扩展包](media/vside-extensionpack.png)

5. 若要完成安装，请关闭 Visual Studio 的所有实例。

## <a name="remove-the-extension"></a>删除扩展

若要从计算机中删除扩展，请执行以下操作：

::: moniker range="vs-2017"

1. 在 Visual Studio 的“工具”菜单中，单击“扩展和更新” 。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在 Visual Studio 的“扩展”菜单上，单击"托管扩展" 。

::: moniker-end

2. 选择“测试扩展包”，然后单击“卸载” 。 扩展包中包含的扩展及其扩展列表将按计划卸载。

3. 若要完成卸载，请关闭 Visual Studio 的所有实例。
