---
title: 如何：导出包含自左乘的 Alpha 的纹理
description: 了解图像内容管道如何从源图像生成更易于使用且更可靠的预乘 Alpha 纹理。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 05348afa-f079-4f53-a05b-ecd91d13adab
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-designers
ms.workload:
- multiple
ms.openlocfilehash: 7f21aa94786fb9914bd72dfccfa9a59b8469d09f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122073638"
---
# <a name="how-to-export-a-texture-that-has-premultiplied-alpha"></a>如何：导出包含自左乘的 Alpha 的纹理

图像内容管道可从源图像生成预乘 Alpha 纹理。 这些纹理比不包含预乘 alpha 的纹理更易于使用且更可靠。

本文档演示了这些活动：

- 将源映像配置为由图像内容管道进行处理。

- 配置图像内容管道以生成预乘 alpha。

## <a name="premultiplied-alpha"></a>预乘 Alpha
预乘 Alpha 相对于常规非预乘 Alpha 来说具有若干优点，因为它通过透明度（允许通过的底色的量）来分离纹素添加的颜色（纹素添加到场景中的颜色），更好的体现了现实世界与物理材质的光线交互。 使用预乘 Alpha 的一些优点为：

- 与预乘 Alpha 混合的是一种结合性运算，无论按何种顺序混合纹理，混合多个半透明纹理的结果都是相同的。

- 因为混合预乘 Alpha 具有结合性，所以简化了半透明对象的多通渲染。

- 通过使用预乘 Alpha，可以同时实现纯附加混合（通过将 Alpha 设置为零）和线性内插混合。 例如，在粒子系统中，附加混合火粒子可能会成为通过使用线性内插混合成的半透明烟粒子。 如果没有预乘 Alpha，将需要在烟粒子之外单独绘制火粒子，并修改绘图调用间的呈现状态。

- 使用预乘 Alpha 时，纹理拥有更高的压缩质量，并且它们不显示变色的边缘（或“晕轮效应”），这种边缘会在混合不使用预乘 alpha 的纹理时出现。

#### <a name="to-create-a-texture-that-uses-premultiplied-alpha"></a>创建使用预乘 Alpha 的纹理

1. 从基本纹理开始。 加载现有图像文件，或根据[如何：创建基本纹理](../designers/how-to-create-a-basic-texture.md)所述，创建一个纹理。

2. 配置纹理文件，使其由图像内容管道进行处理。 在“解决方案资源管理器”中，打开纹理文件的快捷菜单，然后选择“属性”。 在“配置属性” > “常规”页上，将“项目类型”属性设置为“图像内容管道”   。 请确保将“内容”属性设置为“是”，并且将“从生成中排除”设置为“否”，然后选择“应用”按钮。 将出现“图像内容管道”配置属性页。

3. 配置图像内容管道，生成预乘 Alpha。 在“配置属性” > “图像内容管道” > “常规”页上，将“转换为预乘 Alpha 格式”属性设置为“是 (/generatepremultipliedalpha)”    。

4. 选择 **“确定”** 按钮。

   生成项目后，图像内容管道将源图像从工作格式转换为指定的输出格式，其中包括将图像转换为预乘 Alpha 格式，该结果将复制到项目的输出目录中。