---
title: 使用纹理和图像
description: 了解如何使用 Visual Studio 中的图像编辑器来创建和修改纹理和图像，它们的格式就像在 DirectX 应用开发中使用的一样。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: b9fbc8fa-66d1-4055-8460-24d8b8fbe43e
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-designers
ms.workload:
- multiple
ms.openlocfilehash: 37a5d3b0766013b127aa939943f7811202d935db
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122035340"
---
# <a name="work-with-textures-and-images"></a>使用纹理和图像

可以在 Visual Studio 中使用图像编辑器来创建和修改纹理与图像。 如同用 DirectX 应用程序开发的应用程序一样，图像编辑器支持丰富的纹理和图像格式。

> [!NOTE]
> 图像编辑器不支持低色彩图像，例如图标或光标。 若要创建或修改这种图像，请使用[图标的图像编辑器 (C++)](/cpp/windows/image-editor-for-icons)。

## <a name="textures-and-images"></a>纹理和图像

简单地说，纹理和图像只是用于在图形应用中提供可视细节的数据表。 纹理或图像提供的细节取决于其用法，颜色样本、Alpha（透明度）值、法线与高度值是常见的示例。 纹理与图像之间的主要差别在于，前者连同形状的表示形式（通常是三维模型）来呈现整个对象或场景，而图像通常是对象或场景的独立表示形式。

可以通过与纹理包含的数据类型或者与纹理维度或“形状”正交的方法来编码和压缩任何纹理。 但是，不同的编码和压缩方法可为不同类型的数据产生更好的效果。

你可以使用图像编辑器来创建和修改纹理和图像，就像使用其他图像编辑器一样。 图像编辑器还提供用于处理 3D 图形的 mipmap 及其他功能，并支持 DirectX 所支持的许多高度压缩与硬件加速的纹理格式。

纹理的常见类型包括：

### <a name="texture-maps"></a>纹理图

纹理图包含已组织成一维、二维或三维矩阵的颜色值。 它们用于针对受影响的对象提供颜色细节。 颜色一般使用 RGB（红、绿、蓝）颜色通道来编码，可能包含表示透明度的第四个通道，即 Alpha。 较不常见的情况是，颜色可能以其他颜色方案来编码，或者第四个通道可能包含 Alpha 以外的数据，例如高度。

### <a name="normal-maps"></a>法线图

法线图包含曲面法线。 它们用于针对受影响的对象提供照明细节。 法线通常使用红、绿、蓝分量进行编码，以存储向量的 x、y 和 z 维。 但是，还有其他编码 - 例如，基于极坐标的编码。

### <a name="height-maps"></a>高度图

高度图包含高度字段数据。 它们用于针对受影响的对象提供几何细节 - 使用着色器代码计算所需的效果 - 或者提供用例的数据点，例如地形生成。 高度值通常使用纹理中的一个通道进行编码。

### <a name="cube-maps"></a>立方体图

立方体图可能包含不同类型的数据（例如，颜色或法线），但是已在立方体的表面组织成六个纹理。 因此，对立方体图进行采样的方式不是通过提供纹理坐标，而是提供原点在立方体中心的向量；样本是取自向量与立方体交集的点。 使用立方体图可以提供用于计算反射的环境近似值（称为 *环境映射*），或者提供失真度比基本、二维纹理低的纹理给球面对象。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[图像编辑器](../designers/image-editor.md)|介绍如何使用图像编辑器处理纹理和图像。|
|[图像编辑器示例](../designers/how-to-create-a-basic-texture.md)|提供演示如何使用图像编辑器执行常见图像处理任务的主题的链接。|
