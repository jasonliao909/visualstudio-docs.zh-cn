---
title: 创建扩展包
description: 按照视频操作或使用说明创建一个扩展包，其中包含你最喜欢的扩展或将一组扩展组合在一起。
ms.date: 12/01/2021
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: pchapman
ms.prod: visual-studio-windows
ms.technology: vs-ide-sdk
ms.custom: cookbook, kr2b-contr-experiment
ms.openlocfilehash: d75baf221506077586a1ad358509f145685b8413
ms.sourcegitcommit: fec993dbfc5cbe94ca5c5845cb6c1b17b46160fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2022
ms.locfileid: "145859261"
---
# <a name="create-an-extension-pack"></a>创建扩展包

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]

本文介绍如何创建扩展包。 扩展包是一组可以一起安装的扩展。 借助扩展包，可以轻松地与其他用户共享你喜欢的扩展，或将一组扩展捆绑到一起，以用于特定场景。

以下视频介绍了如何创建扩展包。
> [!VIDEO https://www.microsoft.com/videoplayer/embed/RWP8KA]

## <a name="create-from-project-template"></a>从项目模板创建
扩展包项目模板创建一个扩展包，其中包含一组可以一起安装的扩展。

在“**新建Project**”对话框中，搜索 *扩展* 并选择“**扩展包**”。 对于 **Project** 名称，请输入 *测试扩展包*。 选择“创建”。

Visual Studio在解决方案资源管理器中打开项目，并在编辑器中打开文件扩展名 **.vsext**。

```json
{
  "version": "1.0.0.0",
  "extensions": [
    {
      "vsixId": "OneDarkPro.e1e706e2-05d3-4da9-8754-652cd8ab65f4",
      "name": "One Dark Pro"
    },
    {
      "vsixId": "7fa839e2-b938-4b1c-9277-edaebe6fdeb5",
      "name": "Winter is Coming"
    }
  ]
}
```

## <a name="add-to-existing-extension"></a>添加到现有扩展
在解决方案资源管理器中，右键单击项目节点，然后选择“**添加新项”>**。 转到 **Visual C# 扩展性** 节点并选择 **“扩展包**”。 保留默认文件名 (ExtensionPack1.cs)。

项目的根目录中的 .vsext 文件将项目转换为扩展包。 只需确保其 *生成操作* 设置为 *“内容* ”， *VSIX 中的“包含* ”设置为 *True* ，如下所示。

![“属性”对话框的屏幕截图。 突出显示了“生成”操作和“在 V S I X 中包含”。](../media/include-in-vsix.png)
