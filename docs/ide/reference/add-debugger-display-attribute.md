---
title: 添加 DebuggerDisplay 属性
description: 了解如何添加 DebuggerDisplay 属性，以控制调试器变量窗口显示对象、属性或字段的方式。
ms.custom: SEO-VS-2020
ms.date: 05/12/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- dotnet
ms.openlocfilehash: 5e72c2ddba9bfbca2c3fdaa43ae1f278009e3960
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126737069"
---
# <a name="add-debuggerdisplay-attribute"></a>添加 DebuggerDisplay 属性

此代码生成适用于：

- C#

**功能：** [DebuggerDisplay 属性](../../debugger/using-the-debuggerdisplay-attribute.md)控制对象、属性或字段在调试器变量窗口中的显示方式。

**使用时机：** 你希望在代码中以编程方式在调试器中 [固定属性](../../debugger/view-data-values-in-data-tips-in-the-code-editor.md#pin-properties-in-datatips)。

操作原因：固定属性使你能够，通过将对象属性向上浮升到调试器中对象属性列表的顶部，来按属性快速检查对象。 

## <a name="how-to"></a>操作说明

1. 将光标置于类型、委托、属性或字段上。 

2. 按“Ctrl”+ **。** 触发“快速操作和重构”菜单，然后选择“添加 DebuggerDisplay 属性”。

    ![生成比较运算符](media/add-debugger-display-attribute.png)

3. DebuggerDisplay 属性将与返回默认 ToString() 的自动方法一起添加。 

## <a name="see-also"></a>请参阅

- [代码生成](../code-generation-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)