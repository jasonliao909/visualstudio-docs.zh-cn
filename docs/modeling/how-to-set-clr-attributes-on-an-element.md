---
title: 如何：在元素上设置 CLR 特性
description: 了解如何添加从 System.Attribute 类继承的任何属性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.dsltools.EditAttributesDialog
helpviewer_keywords:
- Domain-Specific Language, custom attrributes
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: b6b11d186ea6c4831679c111a632ffe710a6b886
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122143360"
---
# <a name="how-to-set-clr-attributes-on-an-element"></a>如何：在元素上设置 CLR 特性
自定义属性是可添加到域元素、形状、连接器和关系图的特殊属性。 可以添加从 类继承的任何 `System.Attribute` 属性。

### <a name="to-add-a-custom-attribute"></a>添加自定义属性

1. 在 **DSL 资源管理器** 中，选择要将自定义属性添加到的元素。

2. 在"**属性"** 窗口中的"自定义属性"属性旁边，单击"浏览 **(...)** 图标。

     " **编辑属性"** 对话框随即打开。

3. 在" **名称** "列中， **\<add attribute>** 单击并键入属性的名称。 按 Enter。

4. 属性名称下的行显示括号。 在此行中，键入属性参数类型的 (例如，) ，然后 `string` 按 ENTER。

5. 在" **名称属性** "列中，键入适当的名称，例如 `MyString` 。

6. 单击“确定”。

     " **自定义属性"** 属性现在按以下格式显示属性：

     `[`*AttributeName* `(`*ParameterName* `=`*类型*`)]`

## <a name="see-also"></a>请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))