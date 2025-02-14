---
title: 参数节点
description: 了解如何更改着色器中的参数，以根据材料属性、定向光、照相机位置和时间来改变对象的外观。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: da54db0b-3a3d-48dc-858c-7ac43aa04b13
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-designers
ms.workload:
- multiple
ms.openlocfilehash: 578c28672f9c194fa954992afd6b38db0458a1f5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126644456"
---
# <a name="parameter-nodes"></a>参数节点

在着色器设计器中，参数节点表示受应用控制、以每个绘图为基础的着色器输入，例如，材料属性、定向光、照相机位置和时间。 由于可以使用每个绘图调用更改这些参数，因此可使用相同的着色器为某个对象提供不同的外观。

## <a name="parameter-node-reference"></a>参数节点参考

|节点|详细信息|属性|
|----------|-------------|----------------|
|**照相机世界位置**|照相机在世界空间内的位置。<br /><br /> **输出：**<br /><br /> `Output`: `float4`<br /> 照相机的位置。|无|
|**灯光方向**|定义在世界空间中从光源投射出的光线方向的矢量。<br /><br /> 它可用于计算世界空间中的光照量和反射量。<br /><br /> **输出：**<br /><br /> `Output`: `float3`<br /> 从当前像素到光源的矢量。|无|
|**材料环境**|间接光照带来的当前像素的漫射颜色量。<br /><br /> 像素的漫射颜色模拟光照与粗糙表面的交互方式。 可使用材料环境参数达到近似现实世界中间接光照对某个对象造成外观上的影响的效果。<br /><br /> **输出：**<br /><br /> `Output`: `float4`<br /> 间接（即环境）光照带来的当前像素的漫射颜色。|**访问**<br /> 如果允许从模型编辑器设置属性，则为“公共”；否则为“私有”。<br /><br /> **值**<br /> 间接（即环境）光照带来的当前像素的漫射颜色。|
|**材料漫射**|一种颜色，描述当前像素如何漫射直接光照。<br /><br /> 像素的漫射颜色模拟光照与粗糙表面的交互方式。 可使用材料漫射参数以更改当前像素漫射直接光照（即定向光、点光和投射光）的方式。<br /><br /> **输出：**<br /><br /> `Output`: `float4`<br /> 一种颜色，描述当前像素如何漫射直接光照。|**访问**<br /> 如果允许从模型编辑器设置属性，则为“公共”；否则为“私有”。<br /><br /> **值**<br /> 一种颜色，描述当前像素如何漫射直接光照。|
|**材料放射**|提供自身光线的光照带来的当前像素的颜色量。<br /><br /> 可使用它来模拟发光对象，即提供自身光线的对象。 此光线不会影响到其他对象。<br /><br /> **输出：**<br /><br /> `Output`: `float4`<br /> 自发光照带来的当前像素的颜色量。|**访问**<br /> 如果允许从模型编辑器设置属性，则为“公共”；否则为“私有”。<br /><br /> **值**<br /> 自发光照带来的当前像素的颜色量。|
|**材料反射**|一种颜色，描述当前像素如何反射直接光照。<br /><br /> 像素的反射颜色模拟光照与光滑如镜的表面之间的交互方式。 可使用材料反射参数更改当前像素反射直接光照（即定向光、点光和投射光）的方式。<br /><br /> **输出：**<br /><br /> `Output`: `float4`<br /> 一种颜色，描述当前像素如何反射直接光照。|**访问**<br /> 如果允许从模型编辑器设置属性，则为“公共”；否则为“私有”。<br /><br /> **值**<br /> 一种颜色，描述当前像素如何反射直接光照。|
|**材料光泽度**|用于描述反射高光的强度的标量值。<br /><br /> 光泽度越强，反射高光则会越强烈并且越深远。<br /><br /> **输出：**<br /><br /> `Output`: `float`<br /> 一个指数项，描述当前像素上反射高光的强度。|**访问**<br /> 如果允许从模型编辑器设置属性，则为“公共”；否则为“私有”。<br /><br /> **值**<br /> 用于定义当前像素上反射高光的强度的指数。|
|**标准化时间**|以秒为单位的时间，标准化为 [0, 1] 范围，如此一来，当时间达到 1时则会重置为 0。<br /><br /> 可将其用作着色器计算中的参数，例如用来对纹理坐标、颜色值或其他属性进行动画处理。<br /><br /> **输出：**<br /><br /> `Output`: `float`<br /> 标准化时间，以秒为单位。|无|
|**时间**|时间值（以秒计）。<br /><br /> 可将其用作着色器计算中的参数，例如用来对纹理坐标、颜色值或其他属性进行动画处理。<br /><br /> **输出：**<br /><br /> `Output`: `float`<br /> 时间（以秒为单位）。|无|