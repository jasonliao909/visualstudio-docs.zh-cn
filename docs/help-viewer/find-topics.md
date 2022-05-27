---
title: 搜索主题（帮助查看器）
description: 了解如何在 Microsoft Help Viewer 中搜索主题。 使用通配符表达式、逻辑运算符和高级搜索运算符自定义搜索。
ms.date: 05/17/2022
ms.topic: how-to
ms.assetid: 683f1b0c-1551-4bba-91fe-3855f03fdd69
author: jasonchlus
ms.author: jasonchlus
manager: jmartens
ms.technology: vs-help-viewer
ms.custom: kr2b-contr-experiment
ms.workload:
- multiple
ms.openlocfilehash: aecc0e7a5ece465f7a7ae0e7da2da9c7622ade05
ms.sourcegitcommit: 2e205fdee00c245816f3eb7b606cf3d91214cb19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2022
ms.locfileid: "145892654"
---
# <a name="how-to-search-for-topics-in-help-viewer"></a>如何：在帮助查看器中搜索主题

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]

可以使用 Microsoft 帮助查看器的全文搜索功能来查找包含特定字词的所有主题。 还可以通过使用通配符表达式、逻辑运算符和高级搜索运算符优化与自定义搜索。

## <a name="to-perform-a-full-text-search"></a>执行全文搜索

1. 使用以下方法之一打开“帮助查看器 **搜索** ”选项卡：

   - 在 **“帮助查看器** ”窗口中，选择“ **搜索** ”选项卡。
   - 在键盘上，选择 **Ctrl**+**E**。

1. 在搜索框中，输入要查找的单词。

1. 在搜索查询中，指定要应用于搜索的任何逻辑或高级搜索运算符。 若要搜索所有可用帮助，请勿使用运算符。

    > [!NOTE]
    > 在 **“查看器选项** ”对话框中，可以指定其他首选项，例如一次显示的最大搜索结果数，以及在主要区域设置不是英语的情况下是否包含英语内容。

1. 选择 **Enter** 键。

     默认情况下，一次搜索最多返回 200 个命中结果，并显示在搜索结果区域中。 每个结果的版本信息可能会显示，具体取决于内容。

1. 若要查看主题，请从结果列表中选择其标题。

## <a name="full-text-search-tips"></a>全文搜索提示

了解语法对查询的影响后，可以让搜索目的性更强，仅返回你感兴趣的主题。 语法包括特殊字符、保留字和筛选器。 本部分提供提示、过程和详细的语法信息，帮助你更好地制定查询。

### <a name="general-guidelines"></a>一般指南

下表包括在帮助中进行搜索查询的一些基本规则和指南。

|语法|说明|
|------------|-----------------|
|事例敏感性|搜索不区分大小写。 使用大写或小写字符开发搜索条件。 例如，“OLE”和“ole”返回相同的结果。|
|字符组合|不能仅搜索单个字母 (a-z) 或单个数字 (0-9)。 如果尝试搜索某些保留字词，例如“and”、“from”和“with”，则将被忽略。 有关详细信息，请参阅本文后面的 [搜索中忽略的单词](#words-ignored-in-searches-stop-words) 。|
|计算顺序|搜索查询从左到右进行求值。|

### <a name="search-syntax"></a>搜索语法

可以输入包含多个字词的搜索字符串，例如“word1 word2”。 该字符串等效于键入“word1 AND word2”。 使用 AND 运算符的搜索仅返回包含搜索字符串中所有单个字词的主题。

> [!IMPORTANT]
> - 不支持短语搜索。 如果在搜索字符串中指定多个单词，则返回的主题包含你指定的所有单词，但不一定是指定的确切短语。
> - 使用逻辑运算符指定搜索短语中各单词之间的关系。 可以使用逻辑运算符（如 AND、OR NOT 和 NEAR）进一步优化搜索。 例如，如果搜索“声明 NEAR 联合”，搜索结果包括包含单词“声明”和“union”的主题，这些主题彼此之间不超过几个单词。 有关详细信息，请参阅[搜索表达式中的逻辑运算符](../help-viewer/logical-operators-search-expressions.md)。

### <a name="filters"></a>筛选器

可利用高级搜索运算符进一步限制搜索结果。 “帮助”包括三类用于筛选全文搜索结果的方式：标题、代码和关键字。

### <a name="ranking-of-search-results"></a>搜索结果排名

搜索算法应用特定条件在结果列表中对搜索结果进行排名。 一般而言：

- 标题中包含搜索词的内容排名高于标题中不包含搜索词的内容。

- 搜索词紧挨的内容高于搜索词较远的内容。

- 包含较多搜索词的内容排名高于包含较少搜索词的内容。

### <a name="words-ignored-in-searches-stop-words"></a>搜索中忽略的字（停用字）

全文索引搜索期间，会自动忽略经常出现的单词或数字（有时也称停用字）。 例如，如果搜索短语“传递”，搜索结果将显示包含单词“pass”但不包含“through”的主题。

## <a name="see-also"></a>另请参阅

- [逻辑运算符和高级运算符](../help-viewer/logical-operators-search-expressions.md)
- [如何：在索引中查找主题](../help-viewer/find-topics-index.md)
- [如何：在 TOC 中查找主题](../help-viewer/find-topics-toc.md)
- [Microsoft Help Viewer](../help-viewer/overview.md)