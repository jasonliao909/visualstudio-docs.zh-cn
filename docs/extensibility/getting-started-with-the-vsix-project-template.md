---
title: 入门 VSIX Project模板|Microsoft Docs
description: 了解如何使用 VSIX Project模板创建扩展或打包现有扩展以用于部署。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- Visual Studio SDK, VSIX project template
ms.assetid: 89fac33e-9380-4723-9b45-048a6e16f0ed
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: c3d090a426e5e1f784202b512f8825cd7b1b429e3b63cd9ac420d14395655347
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121291514"
---
# <a name="get-started-with-the-vsix-project-template"></a>VSIX Project模板入门

可以使用 VSIX Project模板创建扩展或打包现有扩展以用于部署。 VSIX Project模板具有 Visual Basic 和 Visual C# 版本，并作为 Visual Studio SDK 的一部分进行安装。

 VSIX Project模板仅包含 *source.extension.vsixmanifest* 文件，其中包含有关扩展及其提供的资产的信息。

 若要查找 VSIX 项目模板，必须安装 Visual Studio SDK。 有关详细信息，请参阅 [Visual Studio SDK](../extensibility/visual-studio-sdk.md)。

## <a name="deploy-a-custom-project-template-using-the-vsix-project-template"></a>使用 VSIX Project模板部署自定义Project模板

 以下步骤显示如何使用 VSIX 项目打包项目模板，该项目模板可以与其他开发人员共享或上传到 Visual Studio库。

1. 创建项目模板。

    1. 打开要创建模板的项目。 此项目可以是任何项目类型。

    2. 在“项目”菜单上，单击“导出模板”。 完成向导的步骤。

         在 *.zip* *%USERPROFILE%\我的文档\Visual Studio {version}\My Exported Templates \\ 中创建一个配置文件*。

2. 创建一个空的 VSIX 项目。

     选择“文件” > “新建” > “项目”  。 在搜索框中，键入"vsix"并选择 VSIX **Visual Basic的****C#** **或 Project。**

3. 将 *.zip* 文件添加到项目。 将其" **复制到输出目录"属性** 设置为 `Copy Always` 。

4. 在 **解决方案资源管理器** 中，双击 *source.extension.vsixmanifest* 文件，在 **VSIX** 清单设计器中打开该文件，然后进行以下更改：

    - 将"**产品名称"字段** 设置为 **"我的Project模板"。**

    - 将"**产品 ID"** 字段设置为 **"MyProjectTemplate - 1"。**

    - 将" **作者"** 字段设置为 **Fabrikam**。

    - 将"**说明"** 字段设置为 **"我的项目模板"。**

    - 在 **"资产**"部分中，添加 **Microsoft.VisualStudio.ProjectTemplate** 类型，将其路径设置为 *.zip的名称。*

5. 保存并关闭 *source.extension.vsixmanifest* 文件。

6. 生成项目。

7. 在输出目录中，双击 *.vsix* 文件。

8. 将显示 **VSIX 安装程序** 消息框。 按照说明安装扩展。

9. 关闭 Visual Studio，然后重新打开它。

::: moniker range="vs-2017"

10. 在 **"工具"菜单** (**选择"扩展** 和更新") 并选择" **模板"** 类别。 可用扩展之一应为"我的Project **模板"。**

::: moniker-end

::: moniker range=">=vs-2019"

10. 在 **"扩展" (****选择**"管理扩展") 并选择"**模板"** 类别。 可用扩展之一应为"我的Project **模板"。**

::: moniker-end

11. 新项目模板显示在"新建 **Project"对话框中** 与原始项目模板相同的位置。 例如，如果从 Visual Basic 控制台应用程序创建了名为 VB **Console** 的模板，VB **控制台** 会显示在控制台Visual Basic **模板的同一窗格中**。

### <a name="to-specify-the-location-of-the-template-in-the-new-project-dialog-box"></a>在"新建模板"对话框中指定Project的位置

1. 模板文件夹位于 *{Visual Studio 安装路径}\Common7\IDE\ProjectTemplates* 和 *{Visual Studio Installation Path}\Common7\IDE\ItemTemplates* 目录中。 "新建文件夹"对话框中 **Project部分的名称** 与模板文件夹的名称不完全匹配。 如果它们不同，请使用模板文件夹的名称。

    将 *.vsix 文件* 扩展名更改为 *.zip，* 然后打开该文件。

2. 创建一个新文件夹，该文件夹的名称与模板应出现在"新建 **Project对话框部分** 的名称相同。

3. 如果模板要出现在子节中，请创建同名的子文件夹。

4. 将 *模板.zip* 文件移动到新文件夹中。

5. 将 *.zip* 扩展更改为 *.vsix*。

6. 打开 VSIX 清单。

7. 在 VSIX 清单中，更新模板的资产路径，以便它指向包含模板文件的目录树的根目录。 例如，如果模板位于 *\CSharp\Windows* 中，则引用应指向 *\CSharp*。
