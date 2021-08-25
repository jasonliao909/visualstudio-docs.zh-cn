---
title: 实用程序节点
description: 了解着色器设计器中的实用工具节点，它表示不适合完全归入其他类别的常见且实用的着色器计算。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: ff732221-b731-424c-ad5b-82ef5f21dff5
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-designers
ms.workload:
- multiple
ms.openlocfilehash: 924ab14d01c82879ae728b2acb6323740dce49bb
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122035444"
---
# <a name="utility-nodes"></a>实用程序节点

在着色器设计器中，实用程序节点表示不适合归入其他类别的常见且有用的着色器计算。 某些实用程序节点执行简单的操作，如将矢量追加在一起或有条件地选择结果；其他节点执行复杂的操作，如根据常用的照明模型计算照明量。

## <a name="utility-node-reference"></a>实用程序节点引用

|节点|详细信息|属性|
|----------|-------------|----------------|
|**追加矢量**|通过将指定的输入追加在一起，创建矢量。<br /><br /> **输入：**<br /><br /> `Vector`：`float`、`float2` 或 `float3`<br /> 要追加到其中的值。<br /><br /> `Value to Append`: `float`<br /> 要追加的值。<br /><br /> **输出：**<br /><br /> `Output`：`float2`、`float3` 或 `float4`，具体取决于输入 `Vector` 的类型<br /> 新的矢量。|无|
|**菲涅耳**|基于指定的表面法线计算菲涅耳衰减。<br /><br /> 菲涅耳衰减值表示当前像素的表面法线与视图矢量的一致程度。 在矢量对齐时，函数的结果为 0；矢量越不相似，结果越大，且当矢量正交时，达到其最大值。 可将此用于基于当前像素的方向和照相机之间的关系，生成更清晰或更模糊的效果。<br /><br /> **输入：**<br /><br /> `Surface Normal`: `float3`<br /> 当前像素的表面法线，在当前像素的切线空间中定义。 可将此用于干扰明显的表面法线，如法线贴图所示。<br /><br /> **输出：**<br /><br /> `Output`: `float`<br /> 当前像素的反射率。|**指数**<br /> 用于计算菲涅尔衰减的指数。|
|**If**|有条件地选择每个分量的三个可能结果之一。 该条件由两个其他指定输入之间的关系来定义。<br /><br /> 对于结果的每个分量，将根据前两个输入的对应分量之间的关系选择三个可能结果之一的对应分量。<br /><br /> **输入：**<br /><br /> `X`：`float`、`float2`、`float3` 或 `float4`<br /> 要比较的左侧值。<br /><br /> `Y`：与输入 `X` 类型相同<br /> 要比较的右侧值。<br /><br /> `X > Y`：与输入 `X` 类型相同<br /> 在 `X` 大于 `Y` 时所选的值。<br /><br /> `X = Y`：与输入 `X` 类型相同<br /> 在 `X` 等于 `Y` 时所选的值。<br /><br /> `X < Y`：与输入 `X` 类型相同<br /> 在 `X` 小于 `Y` 时所选的值。<br /><br /> **输出：**<br /><br /> `Output`: `float3`<br /> 对每个分量所选的结果。|无|
|**朗伯**|通过使用指定的表面法线，根据朗伯照明模型计算当前像素的颜色。<br /><br /> 该颜色是直接照明下，环境颜色和漫射照明量的总和。 环境颜色近似于间接照明的总量，但如果没有其他照明的帮助，看起来单调且平淡。 漫射照明有助于向对象添加形状和深度。<br /><br /> **输入：**<br /><br /> `Surface Normal`: `float3`<br /> 当前像素的表面法线，在当前像素的切线空间中定义。 可将此用于干扰明显的表面法线，如法线贴图所示。<br /><br /> `Diffuse Color`: `float3`<br /> 当前像素的漫射颜色，通常为 **点颜色**。 如果未提供任何输入，则默认值为白色。<br /><br /> **输出：**<br /><br /> `Output`: `float3`<br /> 当前像素的漫射颜色。|无|
|**遮罩向量**|指定矢量的遮罩分量。<br /><br /> 可将此用于从某个颜色值中移除特定颜色通道，或阻止特定分量对后续计算产生影响。<br /><br /> **输入：**<br /><br /> `Vector`: `float4`<br /> 要遮罩的矢量。<br /><br /> **输出：**<br /><br /> `Output`: `float4`<br /> 已遮罩的矢量。|**红色/X**<br /> 若要遮住红色 (x) 分量，则为 **False**；否则为 **True**。<br /><br /> **绿色/Y**<br /> 若要遮住绿色 (y) 分量，则为 **False**；否则为 **True**。<br /><br /> **蓝色/Z**<br /> 若要遮住蓝色 (z) 分量，则为 **False**；否则为 **True**。<br /><br /> **Alpha/W**<br /> 若要遮住 alpha (w) 分量，则为 **False**；否则为 **True**。|
|**反射矢量**|基于照相机的位置，计算正切空间中当前像素的反射矢量。<br /><br /> 可以将此用于计算反射、立方体贴图坐标和反射照明量<br /><br /> **输入：**<br /><br /> `Tangent Space Surface Normal`: `float3`<br /> 当前像素的表面法线，在当前像素的切线空间中定义。 可将此用于干扰明显的表面法线，如法线贴图所示。<br /><br /> **输出：**<br /><br /> `Output`: `float3`<br /> 反射矢量。|无|
|**反射**|通过使用指定的表面法线，根据 Phong 照明模型计算反射照明量。<br /><br /> 反射照明赋予对象（例如水、塑料或金属）闪亮、反光的外观。<br /><br /> **输入：**<br /><br /> `Surface Normal`: `float3`<br /> 当前像素的表面法线，在当前像素的切线空间中定义。 可将此用于干扰明显的表面法线，如法线贴图所示。<br /><br /> **输出：**<br /><br /> `Output`: `float3`<br /> 反射高光的颜色量。|无|