---
title: 创建扩展包
description: 创建扩展包以与他人轻松共享你最喜爱的扩展，或将一组扩展捆绑在一起。
ms.date: 12/01/2021
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: pchapman
ms.prod: visual-studio-windows
ms.technology: vs-ide-sdk
ms.custom: cookbook
ms.openlocfilehash: 57dd6c11b75725e13d52e120f547ed47774e41a5
ms.sourcegitcommit: a149b3a034bb555ad217656c0ec8bc1672b1e215
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2021
ms.locfileid: "133515828"
---
# <a name="create-an-extension-pack"></a>创建扩展包

本文演示如何创建扩展包。 扩展包是一组可以一起安装的扩展。 借助扩展包，可以轻松地与其他用户共享你喜欢的扩展，或将一组扩展捆绑到一起，以用于特定场景。

以下视频介绍了如何创建扩展包。
> [!VIDEO https://www.microsoft.com/videoplayer/embed/RWP8KA]

## <a name="create-from-project-template"></a>从项目模板创建
扩展包项目模板创建一个扩展包，该扩展包具有一组可以一起安装的扩展。

在"**新建Project** 对话框中，搜索 *扩展并选择*"扩展 **包"。** 对于 **Project，** 请输入 *"测试扩展包"。* 选择“创建”。

Visual Studio中打开项目解决方案资源管理器编辑器中打开 **文件 Extensions.vsext。**

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
在"解决方案资源管理器"中，右键单击项目节点，然后选择">**项"。** 转到 **"Visual C# 扩展性"节点**，然后选择"**扩展包"。** 保留默认文件名 (ExtensionPack1.cs)。

项目根目录中的 .vsext 文件将项目转换为扩展包。 只需确保"生成 *操作* "设置为" *内容* "，并且 *"在 VSIX* 中包括"设置为 *True，* 如下所示。

![包括在 VSIX 中](../media/include-in-vsix.png)
