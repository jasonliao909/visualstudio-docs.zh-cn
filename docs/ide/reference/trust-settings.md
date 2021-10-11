---
title: 文件和文件夹的信任设置
description: 了解如何更改文件和文件夹的信任设置以确保 Visual Studio 的安全。
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.date: 09/15/2021
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Environment.PathTrustOptions
helpviewer_keywords:
- file security
- folder security
- mark of the web
- trusted files
- trusted folders
ms.openlocfilehash: cde67d54f7c70935f6012542406834ba6c423d78
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128430650"
---
# <a name="configure-trust-settings-for-files-and-folders"></a>配置文件和文件夹的信任设置

::: moniker range=">=vs-2022"

在 Visual Studio 2022（预览版 2）中，我们改进了信任设置功能，以便在用户将要在 IDE 中打开文件、文件夹、项目和解决方案中的不受信任的代码时显示警告。

:::image type="content" source="media/vs-2022/trusted-settings-warning-message.png" alt-text="信任设置警告消息的屏幕截图":::

我们将继续更新此功能，并随之在此页面中添加更多信息。 同时，若要了解最新咨询，请查看我们最新的博客文章，[通过 Visual Studio 2022 提高开发人员的安全性](https://devblogs.microsoft.com/visualstudio/improving-developer-security-with-visual-studio-2022/)。

::: moniker-end

::: moniker range="<=vs-2019"

Visual Studio 在打开具有 [Web 标记](/previous-versions/windows/internet-explorer/ie-developer/compatibility/ms537628(v=vs.85))的项目之前，将提示用户批准。 为了增强安全性，还可以配置 Visual Studio，使其在打开具有 Web 属性标记或者未指定为“受信任”的任何文件或文件夹之前提示用户批准。 默认情况下，禁用文件和文件夹检查。

> [!WARNING]
> 在审批文件、文件夹或解决方案之前，仍应先确保它们来自受信任的人员或受信任的位置。

> [!NOTE]
> 在 Visual Studio 2022（预览版）中，我们改进了信任设置功能，以便在用户将要在 IDE 中打开文件、文件夹、项目和解决方案中的不受信任的代码时显示警告。 有关详细信息，请参阅最近发布的[使用 Visual Studio 2022 提高开发人员安全性](https://devblogs.microsoft.com/visualstudio/improving-developer-security-with-visual-studio-2022/)博客文章。

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
