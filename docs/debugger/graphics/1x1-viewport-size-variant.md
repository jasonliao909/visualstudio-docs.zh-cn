---
title: 1x1 视区大小变体 | Microsoft Docs
description: 应用 1x1 视区大小变体，将所有呈现器目标上的视区尺寸缩小为 1x1 像素。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 3dbc3247-00f5-4644-8ff9-72e9febcf09a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: bf619c6f9499916971620e3d428cf3545fd4cea1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126642018"
---
# <a name="1x1-viewport-size-variant"></a>1x1 视口大小变量
将所有呈现器目标上的视口尺寸缩小为 1x1 像素。

## <a name="interpretation"></a>解释
 较小视区会减少必须遮盖的像素数。 但是，较小视区不减少必须处理的顶点数。 将视口尺寸设置为 1x1 像素可有效地消除应用中的像素着色。

 如果此变体显示较大的性能提升，则可能表示你的应用使用了太多填充率。 此外，分辨率对于目标平台而言可能太高，或者你的应用可能花费了大量时间来为之后覆盖（也称为过度绘制）的像素着色。 较小帧缓冲区或减少过度绘制量将提升应用的性能。

## <a name="remarks"></a>备注
 在每次调用 `ID3D11DeviceContext::OMSetRenderTargets` 或 `ID3D11DeviceContext::RSSetViewports` 之后，视口尺寸将重置为 1x1 像素。

## <a name="example"></a>示例
 可以通过以下代码重现此变体：

```cpp
D3D11_VIEWPORT viewport;
viewport.TopLeftX = 0;
viewport.TopLeftY = 0;
viewport.Width = 1;
viewport.Height = 1;
d3d_context->RSSetViewports(1, &viewport);
```
