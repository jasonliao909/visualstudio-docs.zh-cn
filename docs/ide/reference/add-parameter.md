---
title: “向方法添加参数”快速操作
description: 了解如何根据使用情况使用快速操作自动向方法添加并声明参数。
ms.custom: SEO-VS-2020
ms.date: 09/28/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- dotnet
ms.openlocfilehash: c48e062ec4187fad479f5013fb8786c7eb018cc2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122123965"
---
# <a name="add-a-parameter-to-a-method-using-a-quick-action"></a>使用快速操作向方法添加参数

此代码生成适用于：

- C#

- Visual Basic

**用途：** 便于用户根据使用情况，自动向方法添加参数。

**适用情况：** 需要向方法添加参数，并希望以适当方式自动声明它。

**原因：** 虽然可以在调用方法前向方法声明添加参数，但此功能可根据方法调用自动添加参数。

## <a name="how-to-use-it"></a>如何使用它

1. 向方法调用添加额外参数。

   调用的方法的名称下方显示红色波形曲线。

2. 将指针悬停在红色波形曲线上，直到显示“快速操作”菜单。 选择“快速操作”菜单中的“向下箭头”，再选择“向 [方法] 添加参数”。

   ![Visual Studio 中的“向方法添加参数”快速操作](media/add-parameter-to-method.png)

   > [!TIP]
   > 也可以通过下列方式访问“快速操作”菜单：将光标悬停在方法调用行上，再按 Ctrl+.， （句点）或选择文件边距中的灯泡图标。

   此时，Visual Studio 会向方法声明添加新参数。

> [!NOTE]
> 如果对相应方法有其他调用，可能会在使用此快速操作后看到错误消息，因为其他调用没有为新添加的形参指定实参。

## <a name="see-also"></a>另请参阅

- [向构造函数添加参数](generate-constructor.md#addparameter)
