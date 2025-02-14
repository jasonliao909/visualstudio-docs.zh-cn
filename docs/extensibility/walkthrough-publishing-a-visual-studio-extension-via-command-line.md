---
title: 使用命令行发布扩展
description: 了解如何使用命令行将扩展发布到 Visual Studio Marketplace，使开发人员能够浏览新的和更新的扩展。
ms.custom: SEO-VS-2020
ms.date: 07/12/2018
ms.topic: how-to
helpviewer_keywords:
- publishing extensions
- extension, publishing
ms.assetid: 6ff9efc4-919d-4071-a80d-6dbdd2ceb2f8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: b7cac2a9f5aa59bb3305f96340a987569e18a1a5
ms.sourcegitcommit: 23b0ef3815833426933ff6491271034658683f9d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2022
ms.locfileid: "137983814"
---
# <a name="walkthrough-publishing-a-visual-studio-extension-via-command-line"></a>演练：通过Visual Studio发布扩展

本演练演示如何使用命令行将 Visual Studio扩展发布到 Visual Studio Marketplace。 将扩展添加到市场时，开发人员可以使用"扩展和更新"对话框[](../ide/finding-and-using-visual-studio-extensions.md)在市场中浏览新的和更新的扩展。

VsixPublisher.exe是命令行工具，用于将Visual Studio发布到市场。 可以从 ${VSInstallDir}\VSSDK\VisualStudioIntegration\Tools\Bin\VsixPublisher.exe。 此工具上可用的命令包括： **publish**、 **deletePublisher**、 **deleteExtension**、 **login**、 **logout**。

## <a name="commands"></a>命令

### <a name="publish"></a>发布

将扩展发布到市场。 扩展可以是 vsix、exe/msi 文件或链接。 如果已存在同一版本的扩展，它将覆盖该扩展。 如果扩展不存在，它将创建一个新的扩展。

|命令选项 |说明 |
|---------|---------|
|所需的 (负载)  | 要发布的有效负载的路径或用作"更多信息 URL"的链接。 |
|publishManifest (必需)  | 要使用的发布清单文件的路径。 |
|ignoreWarnings | 发布扩展时要忽略的警告列表。 发布扩展时，这些警告显示为命令行消息。  ("VSIXValidatorWarning01， VSIXValidatorWarning02") 
|personalAccessToken | 个人访问令牌 (PAT) ，用于对发布者进行身份验证。 如果未提供，则从登录用户获取 PAT。 |

```
VsixPublisher.exe publish -payload "{path to vsix}" -publishManifest "{path to vs-publish.json}" -ignoreWarnings "VSIXValidatorWarning01,VSIXValidatorWarning02"
```

### <a name="deletepublisher"></a>deletePublisher

删除市场中的发布者。

|命令选项 |说明 |
|---------|---------|
|publisherName (必需)  | 发布服务器的名称 (例如，标识符) 。 |
|需要 (personalAccessToken)  | 用于对发布者进行身份验证的个人访问令牌。 |

```
VsixPublisher.exe deletePublisher -publisherName "{Publisher Name}" -personalAccessToken "{Personal Access Token}"
```

### <a name="deleteextension"></a>deleteExtension

从市场中删除扩展。

|命令选项 |说明 |
|---------|---------|
|extensionName (必需)  | 要删除的扩展的名称。 |
|publisherName (必需)  | 发布服务器的名称 (例如，标识符) 。 |
|personalAccessToken | 用于对发布者进行身份验证的个人访问令牌。 如果未提供，则从登录用户获取 pat。 |

```
VsixPublisher.exe deleteExtension -extensionName "{Extension Name}" -publisherName "{Publisher Name}"
```

### <a name="login"></a>登录

将发布服务器记录到计算机中。

|命令选项 |说明 |
|---------|---------|
|需要 personalAccessToken ( | 用于对发布者进行身份验证的个人访问令牌。 |
|publisherName (必需)  | 发布服务器的名称 (例如，标识符) 。 |
|overwrite | 指定任何现有发布者都应使用新的个人访问令牌覆盖。 |

```
VsixPublisher.exe login -personalAccessToken "{Personal Access Token}" -publisherName "{Publisher Name}"
```

### <a name="logout"></a>logout

将发布服务器记录到计算机外。

|命令选项 |说明 |
|---------|---------|
|publisherName (必需)  | 发布服务器的名称 (例如，标识符) 。 |
|ignoreMissingPublisher | 指定如果指定的发布服务器尚未登录，则该工具不应出错。 |

```
VsixPublisher.exe logout -publisherName "{Publisher Name}"
```

### <a name="createpublisher"></a>createPublisher
> [!Caution]
> 此命令不再可用。 可以通过导航到"市场"来创建新的[Visual Studio发布者](https://marketplace.visualstudio.com/manage/publishers)。

## <a name="publishmanifest-file"></a>publishManifest 文件

publishManifest 文件由 **publish 命令** 使用。 它表示有关市场需要知道的扩展的所有元数据。 如果要上传的扩展来自 VSIX 扩展，则"identity"属性必须仅设置"internalName"。 这是因为可以从 vsixmanifest 文件生成其余"标识"属性。 如果扩展是 msi/exe 或链接扩展，则用户必须在"identity"属性中提供必填字段。 清单的其余部分包含特定于市场 (的信息，例如类别、&问答功能等) 。

VSIX 扩展 publishManifest 文件示例：

```json
{
    "$schema": "http://json.schemastore.org/vsix-publish",
    "categories": [ "build", "coding" ],  // The categories of the extension. Between 1 and 3 categories are required.
    "identity": {
        "internalName": "MyVsixExtension" // If not specified, we try to generate the name from the display name of the extension in the vsixmanifest file.
                                            // Required if the display name is not the actual name of the extension.
    },
    "overview": "overview.md",            // Path to the "readme" file that gets uploaded to the Marketplace. Required.
    "priceCategory": "free",              // Either "free", "trial", or "paid". Defaults to "free".
    "publisher": "MyPublisherName",       // The name of the publisher. Required.
    "private": false,                     // Specifies whether or not the extension should be public when uploaded. Defaults to false.
    "qna": true,                          // Specifies whether or not the extension should have a Q&A section. Defaults to true.
    "repo": "https://github.com/MyPublisherName/MyVsixExtension" // Not required.
}
```

MSI/EXE 或 LINK publishManifest 文件示例：

```json
{
    "$schema": "http://json.schemastore.org/vsix-publish",
    "categories": [ "build", "coding" ],
    "identity": {
        "description": "My extension.", // The description of the extension. Required for non-vsix extensions.
        "displayName": "My Extension",  // The display name of the extension. Required for non-vsix extensions.
        "icon": "\\path\\to\\icon.ico", // The path to an icon file (can be relative to the json file location). Required for non-vsix extensions.
        "installTargets": [             // The installation targets for the extension. Required for non-vsix extensions.
            {
                "sku": "Microsoft.VisualStudio.Community",
                "version": "[10.0, 16.0)"
            }
        ],
        "internalName": "MyExtension",
        "language": "en-US",            // The default language id of the extension. Can be in the "1033" or "en-US" format. Required for non-vsix extensions.
        "tags": [ "tag1", "tag2" ],     // The tags for the extension. Not required.
        "version": "3.7.0",             // The version of the extension. Required for non-vsix extensions.
        "vsixId": "MyExtension",        // The vsix id of the extension. Not required but useful for showing updates to installed extensions.
    },
    "overview": "overview.md",
    "priceCategory": "free",
    "publisher": "MyPublisherName",
    "private": false,
    "qna": true,
    "repo": "https://github.com/MyPublisherName/MyVsixExtension"
}
```

## <a name="asset-files"></a>资产文件

可以针对在自述文件中嵌入图像等内容提供资产文件。 例如，如果扩展具有以下"概述"Markdown 文档：

```markdown
TestExtension
...
This is test extension.
![Test logo](images/testlogo.png "Test logo")
```

为了解析上一示例中的"images/testlogo.png"，用户可以在其发布清单中提供"assetFiles"，如下所示：

```json
{
    "assetFiles": [
        {
            "pathOnDisk": "\\path\\to\\logo.png",
            "targetPath": "images/logo.png"
        }
    ],
    // other required fields
}
```

## <a name="publishing-walkthrough"></a>发布演练

### <a name="prerequisites"></a>先决条件

要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

### <a name="create-a-visual-studio-extension"></a>创建Visual Studio扩展

在这种情况下，我们将使用默认的 VSPackage 扩展，但相同的步骤对于每一种扩展都有效。

1. 在具有菜单命令的 C# 中创建名为"TestPublish"的 VSPackage。 有关详细信息，请参阅创建 [第一个扩展：Hello World](../extensibility/extensibility-hello-world.md)。

### <a name="package-your-extension"></a>打包扩展

1. 使用有关产品名称、作者和版本的正确信息更新扩展 vsixmanifest。

   ![更新扩展 vsixmanifest](media/update-extension-vsixmanifest.png)

2. 在发布模式下 **生成** 扩展。 现在，扩展将打包为 \bin\Release 文件夹中的 VSIX。

3. 可以双击 VSIX 来验证安装。

### <a name="test-the-extension"></a>测试扩展

 在分发扩展之前，请生成并测试它，以确保该扩展正确安装在 Visual Studio。

1. 在Visual Studio中，开始调试。 打开 的实验Visual Studio。

2. 在实验实例中，转到"工具 **"菜单** ，然后单击" **扩展和更新..."**。TestPublish 扩展应显示在中心窗格中并启用。

3. 在" **工具** "菜单上，确保看到测试命令。

### <a name="publish-the-extension-to-the-marketplace-via-command-line"></a>通过命令行将扩展发布到市场

1. 请确保已生成扩展的发布版本，并且该版本是最新的。

2. 确保已创建 publishmanifest.json overview.md 文件。

3. 打开命令行并导航到 ${VSInstallDir}\VSSDK\VisualStudioIntegration\Tools\Bin\ 目录。

4. 若要发布新扩展，请使用以下命令：

   ```
   VsixPublisher.exe publish -payload "{Path to vsix file}"  -publishManifest "{path to publishManifest file}"  -personalAccessToken "{Personal Access Token that is used to authenticate the publisher. If not provided, the pat is acquired from the logged-in users.}"
   ```

5. 成功发布扩展后，将看到以下命令行消息：

   ```
   Uploaded 'MyVsixExtension' to the Marketplace.
   ```

6. 可以通过导航到"市场"来验证发布[Visual Studio扩展](https://marketplace.visualstudio.com/)

### <a name="install-the-extension-from-the-visual-studio-marketplace"></a>从 Visual Studio Marketplace 安装扩展

发布扩展后，请在 Visual Studio 中进行安装和测试。

1. 在Visual Studio"工具"**菜单上，** 单击"**扩展和更新..."**。

2. 单击 **"联机** "，然后搜索"TestPublish"。

3. 单击“下载”。 然后，将计划安装该扩展。

4. 若要完成安装，请关闭 Visual Studio 的所有实例。

## <a name="remove-the-extension"></a>删除扩展

可以从 Visual Studio 市场和计算机中删除该扩展。

### <a name="to-remove-the-extension-from-the-marketplace-via-command-line"></a>通过命令行从市场中删除扩展

1. 如果要删除扩展，请使用以下命令：

   ```
   VsixPublisher.exe deleteExtension -publisherName "TestVSIXPublisher" -extensionName "MyVsixExtension"
   ```

2. 成功删除扩展后，将看到以下命令行消息：

   ```
   Removed 'MyVsixExtension' from the Marketplace.
   ```

### <a name="to-remove-the-extension-from-your-computer"></a>从计算机中删除扩展

1. 在 Visual Studio 的“工具”菜单中，单击“扩展和更新” 。

2. 选择"MyVsixExtension"，然后单击"卸载 **"**。 然后，将计划卸载扩展。

3. 若要完成卸载，请关闭 Visual Studio 的所有实例。
