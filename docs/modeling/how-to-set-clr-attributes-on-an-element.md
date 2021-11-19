---
title: 如何：在元素上设置 CLR 特性
description: 了解如何添加任何继承自 System.Attribute 类的特性。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665994"
---
# <a name="how-to-set-clr-attributes-on-an-element"></a>如何：在元素上设置 CLR 特性
自定义属性是可以添加到域元素、形状、连接器和关系图中的特殊特性。 可以添加任何继承自 `System.Attribute` 类的特性。

### <a name="to-add-a-custom-attribute"></a>添加自定义属性

1. 在“DSL 资源管理器”中，选择要向其添加自定义属性的元素。

2. 在“属性”窗口中，单击“自定义属性”属性旁边的浏览 (…) 图标  。

     “编辑特性”对话框随即打开。

3. 在“名称”列中，单击 \<add attribute> 并键入特性的名称 。 按 Enter。

4. 特性名称下面的行显示括号。 在此行上，键入特性的参数类型（例如 `string`），然后按 Enter。

5. 在“为属性命名”列中，键入适当的名称，例如 `MyString`。

6. 单击 **“确定”** 。

     “自定义属性”属性现在按以下格式显示特性：

     `[` AttributeName `(` ParameterName `=` Type `)]`  

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))