---
title: 文件和文件夹的信任设置
description: 了解如何更改文件和文件夹的信任设置以确保 Visual Studio 的安全。
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.date: 10/27/2021
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Environment.PathTrustOptions
helpviewer_keywords:
- file security
- folder security
- mark of the web
- trusted files
- trusted folders
ms.openlocfilehash: 4e92e449bf947ebbb03e676d6cb77d926c6971d8
ms.sourcegitcommit: 7a820b7698a8dcf076eb36e3d766fb0751f56bb1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2021
ms.locfileid: "131127923"
---
# <a name="configure-trust-settings-for-files-and-folders"></a>配置文件和文件夹的信任设置

::: moniker range=">=vs-2022"

在 Visual Studio 2022 中，我们改进了“信任设置”功能，以便在 IDE 中打开不受信任代码时显示警告。 

软件开发人员正面对越来越多的恶意软件。 新的“信任设置”功能旨在提高处理陌生代码的风险意识，并有助于防范恶意攻击者，这些攻击者的目标针对各种场景，从打开内容（例如，存储库、解决方案、项目和文件）到使用 Visual Studio 生成和运行应用程序等。 

默认情况下不启用“受信任位置”功能。 

## <a name="enable-trusted-locations"></a>启用受信任位置

若要启用“受信任位置”功能，请执行以下步骤：

1. 打开“工具”>“选项”>“信任设置”  。

2. 在“信任策略”窗格中，选择“打开内容之前需要信任决策” 。

:::image type="content" source="media/vs-2022/trusted-settings-options-dialog.png" alt-text="屏幕截图显示如何使用“信任设置”选项启用受信任位置。":::

> [!NOTE]
> “跳过对 Visual Studio 自动创建的临时位置的信任检查”选项默认处于启用状态，除非还启用了“打开内容前需要信任决策”选项，否则它不会产生任何影响 。

启用后，Visual Studio 会检测是否正在尝试打开未指定为“受信任”的内容，并显示一个新对话框，警告安全隐患。

:::image type="content" source="media/vs-2022/trusted-settings-warning-dialog.png" alt-text="“信任设置”警告对话框的屏幕截图。":::

## <a name="manage-trust-settings"></a>管理信任设置

下面介绍如何添加和删除受信任位置。

### <a name="add-trusted-locations"></a>添加受信任位置

启用该功能后，在添加到“受信任位置”列表中之前，使用 Visual Studio 2022 打开的所有内容都将视为不受信任。  可以直接从“警告”对话框中信任文件夹位置。 以下是操作方法：

1. 从“信任级别”下拉列表中选择要信任的文件夹（当前文件夹或父文件夹）。

   :::image type="content" source="media/vs-2022/trust-folder-trust-level.png" alt-text="屏幕截图显示如何信任警告对话框中的文件夹。":::

1. 选择对话框上的“信任和继续”按钮。

   Visual Studio 会将文件夹路径添加到“工具”>“选项”>“信任设置”中的“受信任位置”列表   。

还可以通过“信任设置”对话框将文件夹添加到“受信任位置” 。 以下是操作方法：

1. 打开“工具” > “选项” > “信任设置”  。 还可以通过从警告对话框中选择“管理信任设置”来打开“信任设置” 。

2. 在右侧的“信任策略”窗格中选择“添加文件夹” 。

3. 导航到要添加到受信任列表的文件夹并选择。

   文件夹路径将出现在“受信任位置”列表中。 你手动添加的此文件夹将列为“信任者: 本地用户” 。
   
   :::image type="content" source="media/vs-2022/trusted-locations.png" alt-text="屏幕截图显示添加到“受信任位置”的文件夹。":::

> [!NOTE]
> 启用“受信任位置”功能后，在 Visual Studio 中创建的任何内容的文件夹路径都将自动添加到“受信任位置”列表中 。 此文件夹路径将列为“信任者: 系统” 。
> 
> :::image type="content" source="media/vs-2022/trusted-by-values.png" alt-text="屏幕截图显示“受信任位置”列表中的“信任者”值：“本地用户”和“系统”。":::

### <a name="remove-trusted-locations"></a>删除受信任位置

若要删除受信任位置，请执行以下步骤：

1. 打开“工具”>“选项”>“信任设置”  。

2. 在“受信任位置”列表中，选择要删除的路径，然后单击“删除” 。

   > [!TIP]
   > 若要选择多个项，选择路径的同时按住 Shift。

   所选的路径将从“受信任位置”列表中删除。

::: moniker-end

::: moniker range="<=vs-2019"

Visual Studio 在打开具有 [Web 标记](/previous-versions/windows/internet-explorer/ie-developer/compatibility/ms537628(v=vs.85))的项目之前，将提示用户批准。 为了增强安全性，还可以配置 Visual Studio，使其在打开具有 Web 属性标记或者未指定为“受信任”的任何文件或文件夹之前提示用户批准。 默认情况下，禁用文件和文件夹检查。

> [!WARNING]
> 在审批文件、文件夹或解决方案之前，仍应先确保它们来自受信任的人员或受信任的位置。

> [!NOTE]
> 在 Visual Studio 2022 RC 中，我们改进了信任设置功能，以便在用户将要在 IDE 中打开文件、文件夹、项目和解决方案中的不受信任代码时显示警告。 默认情况下，该功能被禁用。 若要了解详细信息，请参阅此页面上的 [Visual Studio 2022 版本](?view=vs-2022&preserve-view=true)。

## <a name="configure-trust-settings"></a>配置信任设置

若要更改信任设置，请执行以下步骤：

1. 打开“工具”>“选项”> “信任设置”，然后选择右侧窗格中的“配置信任设置”链接。

2. 选择所需的文件和文件夹检查级别。 可以对每个文件和文件夹进行不同的检查。 选项包括：

   * **不验证**：Visual Studio 不执行任何检查。

   * **验证 Web 属性的标记**：如果文件或文件夹具有 Web 属性的标记，则 Visual Studio 将阻止它们并请求打开权限。

   * **验证路径是否可信**：如果文件或文件夹路径不属于“受信任路径”列表，则 Visual Studio 将阻止它们并请求打开权限。

   ![信任验证选项](media/trust-settings.png)

## <a name="add-trusted-paths"></a>添加受信任路径

若要添加受信任路径，请执行以下步骤：

1. 打开“工具”>“选项”> “信任设置”，然后选择右侧窗格中的“配置信任设置”链接。

2. 单击“信任设置”对话框中的“添加”，然后选择“文件”或“文件夹”。

3. 导航到并选择要添加到受信任列表的文件或文件夹。

   文件或文件夹路径显示在“受信任路径”列表中。

   ![已添加受信任路径](media/trusted-paths.png)

## <a name="remove-trusted-paths"></a>删除受信任路径

若要删除受信任路径，请执行以下步骤：

1. 打开“工具”>“选项”> “信任设置”，然后选择右侧窗格中的“配置信任设置”链接。

2. 在“受信任路径”列表中，选择要删除的路径，然后单击“删除”。

   > [!TIP]
   > 若要选择多个项，选择路径的同时按住 Shift。

   所选的路径都将从“受信任路径”列表中删除。

::: moniker-end

## <a name="see-also"></a>另请参阅

[在 Visual Studio 中生成应用程序](../walkthrough-building-an-application.md)
