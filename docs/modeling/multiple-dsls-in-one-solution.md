---
title: 一个解决方案中的多个 DSL
description: 了解如何将多个特定于域的语言打包 (DLL) 作为单个解决方案的一部分，以便它们一起安装。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: d26d321f93d3d70300c8bdfaa758ec87309840bd8d21db3341a5cf7e2040505d
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121231517"
---
# <a name="multiple-dsls-in-one-solution"></a>一个解决方案中的多个 DSL

可将多个 DSL 打包为单个解决方案的一部分，以便可同时安装它们。

可使用多种技术集成多个 DSL。 有关详细信息，请参阅使用模型[总线Visual Studio模型](../modeling/integrating-models-by-using-visual-studio-modelbus.md)和[如何：](../modeling/how-to-add-a-drag-and-drop-handler.md)添加拖放处理程序和[自定义复制行为](../modeling/customizing-copy-behavior.md)。

## <a name="build-more-than-one-dsl-in-the-same-solution"></a>在同一解决方案中生成多个 DSL

1. 创建新的 **VSIX Project** 项目。

2. 在 VSIX 解决方案目录中创建两个或多个 DSL 项目。

   - 对于每个 DSL，打开 Visual Studio 的新实例。 创建新 DSL，并指定与 VSIX 解决方案相同的解决方案目录。

   - 确保使用不同的文件名扩展创建每个 DSL。

   - 更改 **Dsl** 和 **DslPackage** 项目的名称，以便它们全部不同。 例如：`Dsl1`、`DslPackage1`、`Dsl2`、`DslPackage2`。

   - 在每个 **DslPackage \* \source.extension.tt** 中，将该行更新为正确的 Dsl 项目名称：

      `string dslProjectName = "Dsl2";`

   - 在 VSIX 解决方案中，添加 Dsl* 和 DslPackage \* 项目。 你可能想要将每一对放在其自己的解决方案文件夹中。

2. 合并 DSL 的 VSIX 清单：

   1. 打开 _YourVsixProject_**\source.extension.manifest**。

   2. 对于每个 DSL，选择" **添加内容** "并添加：

       - `Dsl*` 项目作为 **MEF 组件**

       - `DslPackage*` 项目作为 **MEF 组件**

       - `DslPackage*` 项目作为 **VS 包**

3. 生成解决方案。

   生成的 VSIX 将安装这两个 DSL。 可以使用 F5 测试它们，或部署 _YourVsixProject_**\bin\Debug \\ \* .vsix**。

## <a name="see-also"></a>请参阅

- [使用 Visual Studio Modelbus 集成模型](../modeling/integrating-models-by-using-visual-studio-modelbus.md)
- [如何：添加拖放处理程序](../modeling/how-to-add-a-drag-and-drop-handler.md)
- [自定义复制行为](../modeling/customizing-copy-behavior.md)