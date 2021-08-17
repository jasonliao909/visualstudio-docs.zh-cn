---
title: VSCT XML 架构条件属性|Microsoft Docs
description: 了解如何将条件属性应用于 VSCT XML 架构列表和项。 属性计算结果为 true 或 false，控制生成的输出。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, conditional attributes
- conditional attributes (VSCT XML schema)
ms.assetid: 754d4f32-319b-44c9-915f-f7c60e53222e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: c56f3cd8929d9ca17b01df2e78ab6a1b8354558445450137bd2e68aa1a8785d1
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121335272"
---
# <a name="vsct-xml-schema-conditional-attributes"></a>VSCT XML 架构条件属性
可以将条件属性应用于所有列表和项。 逻辑运算符和符号扩展表达式的计算结果为 true 或 false。 如果为 true，则关联的列表或项包含在生成的输出中。

 可以针对其他标记扩展或常量测试令牌扩展。 函数 `Defined()` 测试是否已定义特定名称，即使该名称没有值。

 将 Condition 属性应用于列表时，条件将应用于列表中的每个子元素。 如果子元素本身包含 Condition 属性，则其条件通过 AND 操作与父表达式合并。

 值 1、"1"和"true"计算为 true，0、"0"和"false"计算为 false。

## <a name="operators"></a>运算符
 使用以下运算符计算条件表达式。

|操作员|定义|
|--------------|----------------|
|(,)|分组|
|!|逻辑“非”|
|\<, >, \<=, >=, ==, !=|关系式与等式|
|以及|Boolean|
|或|Boolean|

## <a name="examples"></a>示例

```xml
<Menu Condition="Defined(DEBUG)" ...
</Menu>

<Menu Condition="%(SKU_MODE) = 'Demo'" ...
</Menu>

<Menus Condition="Defined(DEBUG)">
    <Menu ...
    </Menu>
</Menus>

<Menus Condition="Defined(DEMO_SKU)">
    <Menus Condition="!Defined(DEBUG)">
        <Menu ...
        </Menu>
    </Menus>

    <Menu ...
    </Menu>
</Menus>

<Menus Condition="(Defined(DEMO_SKU) or Defined(SAMPLE_SKU))
and !Defined(DEBUG)">
    <Menu ...
    </Menu>
</Menus>
```

## <a name="see-also"></a>另请参阅
- [Visual Studio命令表 (。Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
