---
title: 一个解决方案中的多个 DSL
description: 了解如何将多个特定于域的语言 (Dsl) 打包为一个解决方案的一部分，以便将它们一起安装。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 967d8190b488bf4b10a9f01739e52e93fac5bb3b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663942"
---
# <a name="multiple-dsls-in-one-solution"></a>一个解决方案中的多个 DSL

可将多个 DSL 打包为单个解决方案的一部分，以便可同时安装它们。

可使用多种技术集成多个 DSL。 有关详细信息，请参阅[使用 Visual Studio Modelbus 集成模型](../modeling/integrating-models-by-using-visual-studio-modelbus.md)和[如何：添加拖放处理程序](../modeling/how-to-add-a-drag-and-drop-handler.md)和[自定义复制行为](../modeling/customizing-copy-behavior.md)。

## <a name="build-more-than-one-dsl-in-the-same-solution"></a>在同一个解决方案中构建多个 DSL

1. 创建新的 **VSIX Project** 项目。

2. 在 VSIX 解决方案目录中创建两个或多个 DSL 项目。

   - 对于每个 DSL，打开 Visual Studio 的新实例。 创建新 DSL，并指定与 VSIX 解决方案相同的解决方案目录。

   - 确保使用不同的文件名扩展创建每个 DSL。

   - 更改 **Dsl** 和 **DslPackage** 项目的名称，使其完全不同。 例如：`Dsl1`、`DslPackage1`、`Dsl2`、`DslPackage2`。

   - 在每个 **DslPackage \* \ source.extension.tt** 中，将以下行更新为正确的 Dsl 项目名称：

      `string dslProjectName = "Dsl2";`

   - 在 VSIX 解决方案中，添加 Dsl * 和 DslPackage \* 项目。 你可能想要将每一对放在其自己的解决方案文件夹中。

2. 合并 DSL 的 VSIX 清单：

   1. 打开 _YourVsixProject_**\source.extension.manifest**。

   2. 对于每个 DSL，选择 " **添加内容** " 并添加：

       - `Dsl*`作为 **MEF 组件** 的项目

       - `DslPackage*`作为 **MEF 组件** 的项目

       - `DslPackage*` 项目即 **VS 包**

3. 生成解决方案。

   生成的 VSIX 将安装这两个 DSL。 可以使用 F5 测试它们，或部署 _YourVsixProject_**\bin\Debug \\ \***。

## <a name="see-also"></a>另请参阅

- [使用 Visual Studio Modelbus 集成模型](../modeling/integrating-models-by-using-visual-studio-modelbus.md)
- [如何：添加拖放处理程序](../modeling/how-to-add-a-drag-and-drop-handler.md)
- [自定义复制行为](../modeling/customizing-copy-behavior.md)