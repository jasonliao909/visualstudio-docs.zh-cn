---
title: 代码图速度缓慢
description: 了解如何提高代码图性能，以及如何最大限度地减少完成呈现所需的时间。
ms.custom: SEO-VS-2020
ms.date: 05/16/2018
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 74c600fecf01290bd6d00ae0472b061402ceb4ee
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122055557"
---
# <a name="improve-performance-for-code-maps"></a>提高代码图的性能

在首次生成代码图时，Visual Studio 会将其找到的所有依赖关系都编入索引中。 此过程可能需要一些时间，尤其是对于大型解决方案，但会提高以后的性能。 如果更改了代码，Visual Studio 只会将已更新的代码重新编入索引。 若要最大程度地减少地图完成呈现所花时间，请考虑以下建议：

- 仅映射你感兴趣的依赖关系。

- 在生成整个解决方案的代码图之前，缩小解决方案范围。

- 通过在代码图工具栏上选择"跳过生成 **"，** 关闭解决方案的自动生成。

- 通过在代码图工具栏上选择"包括父级" **来** 关闭父项的自动添加。

   ![跳过“生成和包括父项”按钮](../modeling/media/codemapsfilterskipbuildicons.png)

- 直接编辑代码图文件，以删除不需要的节点和链接。 更改代码图不会影响基础代码。 请参阅 [Customize code maps by editing the DGML files](../modeling/customize-code-maps-by-editing-the-dgml-files.md)。

当项目项的"复制到输出目录"属性 **设置为**"始终复制"时，可能需要解决方案资源管理器创建映射或将项添加到 **映射中。** 若要提高性能，请将此属性更改为“如果较新则复制”  或 `PreserveNewest`。 请参阅 [增量生成](../msbuild/incremental-builds.md)。

已完成的映射只显示成功生成代码的依赖项。 如果某些组件出现生成错误，这些错误会出现在代码图上。 在基于代码图做出体系结构决策时，请确保组件实际生成并且具有依赖项。
