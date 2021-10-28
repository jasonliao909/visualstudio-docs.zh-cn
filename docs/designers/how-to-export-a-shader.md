---
title: 如何：导出着色器
description: 了解如何使用着色器设计器来导出有向图着色器语言着色器，这样你就可以在应用中使用它。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 0bd48bf4-9792-4456-a545-e462a2be668d
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-designers
ms.workload:
- multiple
ms.openlocfilehash: b4559c7c8e2e5c77731e6a43e006556cf3ba4d75
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126737304"
---
# <a name="how-to-export-a-shader"></a>如何：导出着色器

本文演示如何使用着色器设计器导出有向图着色器语言 (DGSL) 着色器，使你能在应用中使用它。

## <a name="export-a-shader"></a>导出着色器

在使用着色器设计器创建着色器之后且在应用中使它之前，必须以图形 API 理解的格式将其导出。 可以用不同的方式导出着色器以满足不同的需求。

1. 在 Visual Studio 中，打开“视觉着色器图(.dgsl)”文件。

     如果没有要打开的“视觉着色器图 (.dgsl)”文件，请按照[如何：创建基本颜色着色器](../designers/how-to-create-a-basic-color-shader.md)中所述的步骤进行创建。

2. 在“着色器设计器”工具栏上，依次选择“高级” > “导出” > “导出为”。 显示“导出着色器”对话框。

3. 在“另存为类型”下拉列表中，选择要导出的格式。

     以下是可以选择的格式：

     **HLSL 象素着色器 (\*.hlsl)** 将着色器以高级着色器语言 (HLSL) 源代码导出。 使用此选项可随后对着色器进行修改，即使在应用中部署它后也可修改。 尽管这可以使根据最终用户问题对代码进行调试和修补更加容易，但也使用户能更容易地以你不希望的方式修改你的着色器（例如，在竞争性游戏中获得不公平的优势）。 它还会增加着色器的加载时间。

     **编译的象素着色器 (\*.cso)** 将着色器以 HLSL 字节码导出。 使用此选项可随后对着色器进行修改，即使在应用中部署它后也可修改。 它可以使根据最终用户问题对代码进行调试和修补更加容易，但由于着色器是预编译的，因此当应用加载该着色器时，它不会产生额外的运行时开销。 技术娴熟的用户仍然可以以你不希望的方式修改着色器，但编译着色器会大大增强其难度。

     **C++ 标头 (\*.h)** 将着色器以 C 样式标头导出，其定义包含 HLSL 字节码的字节数组。 此选项可能会使根据最终用户问题对代码进行调试和修补更加耗时，因为必须重新编译应用才能测试修补程序。 然而，因为此选项让用户难以（存在可能性）在着色器部署到应用后对其进行修改，因此也让用户难以以你不希望的方式修改着色器。

4. 在“文件名”组合框中，为导出的着色器指定名称，然后选择“保存”按钮。

## <a name="see-also"></a>另请参阅

- [如何：创建基本颜色着色器](../designers/how-to-create-a-basic-color-shader.md)
- [着色器设计器](../designers/shader-designer.md)
