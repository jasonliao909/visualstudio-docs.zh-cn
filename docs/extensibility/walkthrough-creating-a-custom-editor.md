---
title: 演练：创建自定义编辑器|Microsoft Docs
description: 了解如何通过本演练使用 VSPackage 项目模板在 C++ 中创建简单的自定义编辑器。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], custom - create
ms.assetid: d090abb6-d99f-4083-a3db-cd16bf81ce7d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 8b2c06afa6391ea516d29e244ee869e21272bf0d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122157925"
---
# <a name="walkthrough-create-a-custom-editor"></a>演练：创建自定义编辑器
VSPackage 项目模板可以在 C++ 中创建一个简单的自定义编辑器。 VSPackage 项目模板不再支持 C# 或Visual Basic项目。 有关详细信息，请参阅 [Visual Studio SDK](../extensibility/visual-studio-sdk.md)。

## <a name="prerequisites"></a>先决条件
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="the-visual-studio-package-project-template"></a>"Visual Studio包"项目模板
 可以在 C++ 扩展Visual Studio下的"新建 **Project"对话框中** 找到"包 **"项目** 模板。

### <a name="to-create-a-vspackage-using-the-visual-studio-package-template"></a>使用 Visual Studio 包模板创建 VSPackage

1. 使用"包Visual Studio创建项目。

2. 选择"**自定义编辑器"** 选项，然后单击"下一 **步"。** 将显示 **"编辑器选项** "页。

3. 在"编辑器名称"框中键入 **编辑器** 的名称。 在"文件扩展名"框中键入要与编辑器关联的 **文件** 扩展名。 编辑器可用于具有此扩展名的文件。 文件扩展名仅针对 Visual Studio注册，而不是为 Windows。 在"默认文件名"框中，键入使用编辑器创建的新 **文档的默认** 文件名。

4. 单击“完成”  以在指定的文件夹中创建 VSPackage。

### <a name="to-test-your-custom-editor"></a>测试自定义编辑器

1. 在"**文件"** 菜单上，指向"**新建"，** 然后单击"文件 **"。**

2. 在"**新建文件"** 对话框的"已安装模板"窗格中，选择文件模板，然后选择注册的文件类型。

3. 单击 **"** 打开"查看和编辑文档。

     编辑器支持剪切和粘贴、查找和替换以及打开和加载操作。

## <a name="see-also"></a>请参阅
- [VSPackages](../extensibility/internals/vspackages.md)
