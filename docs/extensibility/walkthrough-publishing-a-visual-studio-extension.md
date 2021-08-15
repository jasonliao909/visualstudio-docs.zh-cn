---
title: 演练：发布Visual Studio扩展|Microsoft Docs
description: 了解如何将扩展Visual Studio发布到 Visual Studio Marketplace，使开发人员能够浏览新的和更新的扩展。
ms.custom: SEO-VS-2020
ms.date: 01/15/2021
ms.topic: how-to
helpviewer_keywords:
- publishing web controls
- web controls, publishing
ms.assetid: a7816161-0490-4043-86f5-0f7331ed83b3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: f5ae3c9664bca8540ead29e6b646aa61a5698cd9d683013ec42996a5c5ef8acd
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121320331"
---
# <a name="walkthrough-publish-a-visual-studio-extension"></a>演练：发布Visual Studio扩展

本演练演示如何将 Visual Studio 扩展发布到 Visual Studio Marketplace。 将扩展添加到市场Visual Studio，开发人员可以使用扩展和更新来浏览新的和更新的扩展。

## <a name="prerequisites"></a>先决条件

 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="create-a-visual-studio-extension"></a>创建Visual Studio扩展

本文使用默认的 VSPackage 扩展，但这些步骤对每种扩展都有效。

- 在具有菜单命令的 C# 中创建名为 `TestPublish` 的 VSPackage。 有关详细信息，请参阅创建[第一个扩展：Hello World。](../extensibility/extensibility-hello-world.md)

## <a name="package-your-extension"></a>打包扩展

1. 使用有关产品名称、作者和版本的正确信息更新扩展 *.vsixmanifest。*

   ![更新扩展 vsixmanifest](media/update-extension-vsixmanifest.png)

2. 在发布模式下 **生成** 扩展。 现在，扩展打包为 \bin\Release 文件夹中的 VSIX。

3. 可以双击 VSIX 来验证安装。

## <a name="test-the-extension"></a>测试扩展

 在分发扩展之前，请生成并测试它，以确保该扩展已正确安装在 Visual Studio。

1. 在Visual Studio中，开始调试以打开 Visual Studio。

2. 在实验实例中，转到"工具 **"菜单**，然后单击"**扩展和更新"。** TestPublish 扩展应显示在中心窗格中并启用。

3. 在" **工具** "菜单上，确保看到测试命令。

## <a name="publish-the-extension-to-visual-studio-marketplace"></a>将扩展发布到 Visual Studio Marketplace

1. 请确保已生成扩展的发布版本，并且该版本是最新的。

2. 在 Web 浏览器中，转到["Visual Studio市场"。](https://marketplace.visualstudio.com/vs)

3. 在右上角，单击"**登录"。**

4. 使用您的 Microsoft 帐户登录。 如果没有此Microsoft 帐户，此时可以创建一个。

5. 单击 **"发布扩展"。** 此选项将导航到所有扩展的"管理"页。 如果没有发布者帐户，此时系统会提示你创建一个。

   ![Upload市场](media/upload-to-marketplace.png)

6. 选择要用于上传扩展的发布者。 可以通过单击左侧列出的发布者名称来更改发布者。 单击 **"新建扩展**"并选择 **"Visual Studio"。**

7. 在 **1：Upload** 扩展中，可以选择将 VSIX 文件直接上传到 Visual Studio Marketplace，或者只需添加指向你自己的网站的链接。 此示例上传了扩展 *TestPublish.vsix。* 拖放扩展名或使用单击 **链接** 浏览文件。 在项目的 \bin\Release 文件夹中查找扩展。  单击 **“继续”** 。

8. 在 **2：提供扩展详细信息** 中，某些字段从扩展名的 *source.extension.vsixmanifest* 文件中自动填充。 在下面查找有关每个项的更多详细信息：

    * **内部** 名称用于扩展详细信息页的 URL。 例如，发布发布者名称"myname"下的扩展，将内部名称指定为"my extension"会导致扩展详细信息页的 URL 为"marketplace.visualstudio \. com/items？itemName=myname.myextension"。

    * **显示扩展** 插件的名称。 此名称从 *source.extension.vsixmanifest* 文件中自动填充。

    * **要** 上传的扩展的版本号。 此版本从 *source.extension.vsixmanifest* 文件中自动填充。

    * **VSIX ID** 是扩展Visual Studio的唯一标识符。 如果希望自动更新扩展，则此标识符是必需的。 此标识符从 *source.extension.vsixmanifest* 文件中自动填充。

    * **用于** 扩展的徽标。 如果提供，则从 *source.extension.vsixmanifest* 文件中自动填充此徽标。

    * **扩展** 功能简短说明。 此说明从 *source.extension.vsixmanifest* 文件中自动填充。

    * **概述** 是一个不错的位置，可以包括有关扩展功能屏幕截图和详细信息。

    * **使用Visual Studio版本**，可以选择扩展Visual Studio版本。 扩展仅安装到这些版本。

    * **通过Visual Studio版本**，可以选择扩展Visual Studio版本。 扩展仅安装到这些版本。

    * **类型**。 最常见的扩展类型是"工具 **"。**

    * **类别**。 最多选择三个最适合你的扩展。

    * **标记** 是可帮助用户查找扩展的关键字。 标记可帮助提高扩展在 Visual Studio 的相关性。

    * **定价** 类别是扩展的成本。

    * **源代码存储库** 允许与社区共享源代码链接。

    * **"允许&的问答** "允许用户在扩展输入页上提问。

9. 单击"**保存& Upload"。** 此选项将返回到发布者管理页。 扩展尚未发布。

10. 若要发布扩展，请右键单击扩展并选择"**公开"。** 若要查看扩展在市场中的外观，Visual Studio"**查看扩展"。** 对于采购编号，请单击"报表 **"。** 若要对扩展进行更改，请单击"编辑 **"。**

    ![扩展条目菜单](media/extension-entry-menu.png)

11. 单击 **"公开"，** 扩展现已公开。 在Visual Studio市场中搜索扩展。

## <a name="update-a-published-extension-in-visual-studio-marketplace"></a>更新 Visual Studio 市场中的已发布扩展

在开始之前，请确保已生成扩展的新版本，并且它是最新的。

1.  在 Web 浏览器中，转到["Visual Studio市场"。](https://marketplace.visualstudio.com/vs)

1.  在右上角，单击" **登录"，** 然后使用Microsoft 帐户。

    :::image type="content" source="media/marketplace-upload-extension.png" alt-text="屏幕截图显示了如何选择已上传的扩展文件资源管理器。":::

1.  单击 **"发布扩展**"，然后选择要用于上传更新的扩展的发布者。

    :::image type="content" source="media/marketplace-select-extension-version.png" alt-text="&quot;Visual Studio&quot;的屏幕截图，其中突出显示了&quot;发布扩展&quot;链接。":::

1.  在要更新的扩展旁边，将鼠标悬停在三个水平点上，然后选择"编辑 **"。**

    :::image type="content" source="media/marketplace-select-extension.png" alt-text="显示选择要编辑的扩展的屏幕截图。":::

1.  在 **"1：Upload** 扩展名"中，单击 VSIX 文件名后，单击铅笔图标以编辑已发布的扩展名。

     :::image type="content" source="media/marketplace-edit-extension-details.png" alt-text="显示单击铅笔图标以编辑扩展的屏幕截图。":::

1.  浏览到更新的扩展 VSIX 文件。 单击该文件，然后单击"打开 **"。**

    已更新的扩展将上传。

    :::image type="content" source="media/marketplace-upload-extension-notification.png" alt-text="上传编辑的扩展后上传文件通知的屏幕截图。":::

1. 在 **2 中**：提供扩展详细信息，某些详细信息对于扩展更新是只读的，或者从扩展中的 *source.extension.vsixmanifest* 文件中自动填充。 下面是有关扩展详细信息的详细信息：

    - **内部名称** \*在扩展的详细信息页的 URL 中使用。 例如，在发布者名称"myname"下发布扩展，将内部名称指定为"my extension"会导致扩展详细信息页的 URL 为"marketplace.visualstudio.com/items?itemName=myname.myextension"。

    - **显示名称** \*扩展的 。 此名称从 *source.extension.vsixmanifest* 文件中自动填充。

    - **版本** \*要上传的扩展插件数。 此版本从 *source.extension.vsixmanifest* 文件中自动填充。

    - **VSIX ID** \*是扩展Visual Studio的唯一标识符。 如果希望自动更新扩展，则此标识符是必需的。 此标识符从 *source.extension.vsixmanifest* 文件中自动填充。

    - **徽标** \*用于扩展的 。 如果提供，则从 *source.extension.vsixmanifest* 文件中自动填充此徽标。

    - **简短说明** \*扩展功能。 此说明从 *source.extension.vsixmanifest* 文件中自动填充。

    - **概述** 是一个不错的位置，可以包括有关扩展功能屏幕截图和详细信息。

    - **支持Visual Studio版本** \*允许你选择扩展Visual Studio版本。 扩展仅安装到这些版本。

    - **支持Visual Studio版本** \*允许你选择扩展Visual Studio版本。 扩展仅安装在这些版本上。

    - **类型**。 最常见的扩展类型是"工具 **"。**

    - **类别**。 最多选择三个最适合你的扩展。

    - **标记** 是可帮助用户查找扩展的关键字。 标记可帮助提高扩展在市场中的搜索Visual Studio相关性。

    - **定价** 类别是扩展的成本。

    - **源代码存储库** 允许与社区共享源代码链接。

    - **"允许&的问答** "允许用户在扩展输入页上提问。

       \* 无法更改扩展更新的此详细信息。

1. 单击"**保存& Upload"。** 此选项将返回到发布者管理页。 扩展尚未发布。

1. 若要发布扩展，请右键单击扩展并选择"**公开"。** 若要查看扩展在市场中的显示Visual Studio，请选择"查看 **扩展"。** 对于采购编号，请单击"报表 **"。** 若要对扩展进行更改，请单击"编辑 **"。**

## <a name="add-additional-users-to-manage-your-publisher-account"></a>添加其他用户以管理发布者帐户

Visual Studio市场支持向其他用户授予访问和管理发布者帐户的权限。

1. 导航到要添加其他用户的发布者帐户。

2. 选择 **"成员**"，然后单击"**添加"。**

   ![添加其他用户](media/add-users.png)

3. 然后，可以在"选择角色"下指定要添加的用户的电子邮件地址，并 **授予适当的访问权限级别**。  可从以下选项中进行选择：

   * **创建者**：用户可以发布扩展，但不能查看或管理其他用户发布的扩展。

   * **读者**：用户可以查看扩展，但不能发布或管理扩展。

   * **参与者**：用户可以发布和管理扩展，但不能编辑发布者设置或管理访问权限。

   * **所有者**：用户可以发布和管理扩展、编辑发布者设置以及管理访问权限。

## <a name="install-the-extension-from-visual-studio-marketplace"></a>从 Visual Studio Marketplace 安装扩展

发布扩展后，请在 Visual Studio 中进行安装和测试。

1. 在 Visual Studio 的“工具”菜单中，单击“扩展和更新” 。

2. 单击 **"联机**"，然后搜索 **"TestPublish"。**

3. 单击“下载”。 然后计划安装扩展。

4. 若要完成安装，请关闭 Visual Studio 的所有实例。

## <a name="remove-the-extension"></a>删除扩展

可以从市场和计算机Visual Studio扩展。

### <a name="to-remove-the-extension-from-visual-studio-marketplace"></a>从市场中删除Visual Studio扩展

1. 转到["Visual Studio市场"。](https://marketplace.visualstudio.com/vs)

2. 在右上角，单击" **发布扩展** "。 选择用于发布 **TestPublish 的发布服务器**。 将显示 **TestPublish** 的列表。

3. 右键单击扩展条目，然后单击"删除 **"。** 系统要求确认是否要删除扩展。 单击“确定”。

### <a name="to-remove-the-extension-from-your-computer"></a>从计算机中删除扩展

1. 在 Visual Studio 的“工具”菜单中，单击“扩展和更新” 。

2. 选择 **"测试""发布"，** 然后单击"**卸载"。** 然后计划卸载扩展。

3. 若要完成卸载，请关闭 Visual Studio 的所有实例。
