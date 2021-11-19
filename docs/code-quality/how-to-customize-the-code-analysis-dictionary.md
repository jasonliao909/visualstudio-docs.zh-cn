---
title: 如何：自定义代码分析字典
ms.date: 11/04/2016
description: 了解可标识拼写和命名约定错误的代码分析字典。 了解如何创建自定义字典，以及如何将字典应用于项目。
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- code analysis dictionary
- custom dictionary, code analysis
- dictionary, code analysis
ms.assetid: 667e3b4e-beff-48be-b3d1-376e1716a895
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: f22d14e5cfeff8bc79327d62a10abd9a54c8bf2b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601306"
---
# <a name="how-to-customize-the-code-analysis-dictionary"></a>如何：自定义代码分析字典

Code Analysis 使用内置字典检查代码中的标识符，以检查 .NET 设计准则的拼写、语法情况和其他命名约定中的错误。 可以创建自定义字典 Xml 文件，以向内置字典添加、删除或修改字词、缩写和首字母缩略词。

例如，假设代码包含名为 DoorKnokker 的类。 Code Analysis 将名称标识为两个词的复合词：door 和 knokker 。 然后，它会发出警告，指出 knokker 拼写不正确。 若要强制代码分析识别拼写，可以将字词 knokker 添加到自定义字典。

## <a name="to-create-a-custom-dictionary"></a>创建自定义字典

创建名为 CustomDictionary.xml 的文件。

使用下列 XML 结构定义自定义字词：

```xml
<Dictionary>
      <Words>
         <Unrecognized>
            <Word>knokker</Word>
         </Unrecognized>
         <Recognized>
            <Word></Word>
         </Recognized>
         <Deprecated>
            <Term PreferredAlternate=""></Term>
         </Deprecated>
         <Compound>
            <Term CompoundAlternate=""></Term>
         </Compound>
         <DiscreteExceptions>
            <Term></Term>
         </DiscreteExceptions>
      </Words>
      <Acronyms>
         <CasingExceptions>
            <Acronym></Acronym>
         </CasingExceptions>
      </Acronyms>
   </Dictionary>
```

## <a name="custom-dictionary-elements"></a>自定义字典元素

可以通过在自定义词典中添加术语作为以下元素的内部文本修改 Code Analysis 字典的行为：

- [Dictionary/Words/Recognized/Word](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsRecognizedWord)

- [Dictionary/Words/Unrecognized/Word](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsUnrecognizedWord)

- [Dictionary/Words/Deprecated/Term[@PreferredAlternate]](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsDeprecatedTermPreferredAlternate)

- [Dictionary/Words/Compound/Term[@CompoundAlternate]](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsCompoundTermCompoundAlternate)

- [Dictionary/Words/DiscreteExceptions/Term](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsDiscreteExceptionsTerm)

- [Dictionary/Acronyms/CasingExceptions/Acronym](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryAcronymsCasingExceptionsAcronym)

### <a name="dictionarywordsrecognizedword"></a><a name="BKMK_DictionaryWordsRecognizedWord"></a> Dictionary/Words/Recognized/Word

若要在代码分析标识为拼写正确的术语列表中包含一个术语，请添加该词作为 Dictionary/Words/Recognized/Word 元素的内部文本。 Dictionary/Words/Recognized/Word 元素中的术语不区分大小写。

**示例**

```xml
<Dictionary>
      <Words>
         <Recognized>
            <Word>knokker</Word>
            ...
         </Recognized>
         ...
      </Words>
      ...
</Dictionary>
```

Dictionary/Words/Recognized 节点中的术语将应用于以下代码分析规则：

- [CA1701:资源字符串组合词应采用正确的大小写](../code-quality/ca1701.md)

- [CA1702:组合词应采用正确的大小写](../code-quality/ca1702.md)

- [CA1703:资源字符串应正确拼写](../code-quality/ca1703.md)

- [CA1704:标识符应正确拼写](../code-quality/ca1704.md)

- [CA1709:标识符的大小写应当正确](../code-quality/ca1709.md)

- [CA1726:使用首选词条](../code-quality/ca1726.md)

- [CA2204:文字应正确拼写](../code-quality/ca2204.md)

### <a name="dictionarywordsunrecognizedword"></a><a name="BKMK_DictionaryWordsUnrecognizedWord"></a> Dictionary/Words/Unrecognized/Word

若要在代码分析标识为拼写正确的术语列表中排除一个术语，请添加该词作为 Dictionary/Words/Unrecognized/Word 元素的内部文本进行排除。 Dictionary/Words/Unrecognized/Word 元素中的术语不区分大小写。

**示例**

```xml
<Dictionary>
      <Words>
         <Unrecognized>
            <Word>meth</Word>
            ...
         </Unrecognized>
         ...
      </Words>
      ...
</Dictionary>
```

Dictionary/Words/Unrecognized 节点中的术语将应用于以下代码分析规则：

- [CA1701:资源字符串组合词应采用正确的大小写](../code-quality/ca1701.md)

- [CA1702:组合词应采用正确的大小写](../code-quality/ca1702.md)

- [CA1703:资源字符串应正确拼写](../code-quality/ca1703.md)

- [CA1704:标识符应正确拼写](../code-quality/ca1704.md)

- [CA1709:标识符的大小写应当正确](../code-quality/ca1709.md)

- [CA1726:使用首选词条](../code-quality/ca1726.md)

- [CA2204:文字应正确拼写](../code-quality/ca2204.md)

### <a name="dictionarywordsdeprecatedtermpreferredalternate"></a><a name="BKMK_DictionaryWordsDeprecatedTermPreferredAlternate"></a> Dictionary/Words/Deprecated/Term[@PreferredAlternate]

若要在代码分析标识为已弃用的术语列表中包含一个术语，请添加该词作为 Dictionary/Words/Deprecated/Term 元素的内部文本。 已弃用的字词拼写正确但不应该使用。

若要在警告中包括建议的备用字词，请指定 Term 元素的 PreferredAlternate 特性中的备用项。 如果不想建议替代项，可以将特性值留空。

- Dictionary/Words/Deprecated/Term 元素中弃用字词不区分大小写。

- PreferredAlternate 特性值区分大小写。 对复合备用项使用 Pascal 大小写。

**示例**

```xml
<Dictionary>
      <Words>
         <Deprecated>
            <Term PreferredAlternate="LogOn">login</Term>
            ...
         </Deprecated>
         ...
      </Words>
      ...
</Dictionary>
```

Dictionary/Words/Deprecated 节点中的术语将应用于以下代码分析规则：

- [CA1701:资源字符串组合词应采用正确的大小写](../code-quality/ca1701.md)

- [CA1702:组合词应采用正确的大小写](../code-quality/ca1702.md)

- [CA1703:资源字符串应正确拼写](../code-quality/ca1703.md)

- [CA1704:标识符应正确拼写](../code-quality/ca1704.md)

- [CA1726:使用首选词条](../code-quality/ca1726.md)

### <a name="dictionarywordscompoundtermcompoundalternate"></a><a name="BKMK_DictionaryWordsCompoundTermCompoundAlternate"></a> Dictionary/Words/Compound/Term[@CompoundAlternate]

内置字典将某些字词标识为单个离散字词，而不是复合字词。 若要在代码分析标识为拼写正确的术语列表中包含一个术语，请添加该词作为 Dictionary/Words/Compound/Term 元素的内部文本。 在 Term 元素的 CompoundAlternate 特性中，通过将单个单词的第一个字母大写（Pascal 大小写），指定构成复合字词的各个单词。 请注意，内部文本中指定的字词会自动添加到 Dictionary/Words/DiscreteExceptions 列表中。

- Dictionary/Words/Compound/Term 元素中的复合词不区分大小写。

- CompoundAlternate 特性值区分大小写。 对复合备用项使用 Pascal 大小写。

**示例**

```xml
<Dictionary>
      <Words>
         <Compound>
            <Term CompoundAlternate="CheckBox">checkbox</Term>
            ...
         </Compound>
         ...
      </Words>
      ...
</Dictionary>
```

Dictionary/Words/Compound 节点中的字词将应用于以下代码分析规则：

- [CA1701:资源字符串组合词应采用正确的大小写](../code-quality/ca1701.md)

- [CA1702:组合词应采用正确的大小写](../code-quality/ca1702.md)

- [CA1703:资源字符串应正确拼写](../code-quality/ca1703.md)

- [CA1704:标识符应正确拼写](../code-quality/ca1704.md)

### <a name="dictionarywordsdiscreteexceptionsterm"></a><a name="BKMK_DictionaryWordsDiscreteExceptionsTerm"></a> Dictionary/Words/DiscreteExceptions/Term

若要在复合词的大小写规则检查字词时，排除代码分析标识为单个离散字词的字词列表中的某个字词，请添加该词作为 Dictionary/Words/DiscreteExceptions/Term 元素的内部文本。 Dictionary/Words/DiscreteExceptions/Term 元素中的复合词不区分大小写。

**示例**

```xml
<Dictionary>
      <Words>
         <DiscreteExceptions>
            <Term>checkbox</Term>
            ...
         </DiscreteExceptions>
         ...
      </Words>
      ...
</Dictionary>
```

将 Dictionary/Words/DiscreteExceptions 节点中的术语应用于以下代码分析规则：

- [CA1701:资源字符串组合词应采用正确的大小写](../code-quality/ca1701.md)

- [CA1702:组合词应采用正确的大小写](../code-quality/ca1702.md)

### <a name="dictionaryacronymscasingexceptionsacronym"></a><a name="BKMK_DictionaryAcronymsCasingExceptionsAcronym"></a> Dictionary/Acronyms/CasingExceptions/Acronym

若要在代码分析标识为拼写正确的术语列表中包含首字母缩略词，并指示复合词的大小写规则检查字词时首字母缩略词如何，请添加该词作为 Dictionary/Acronyms/CasingExceptions/Acronym 元素的内部文本。 Dictionary/Acronyms/CasingExceptions/Acronym 元素中的首字母缩略词区分大小写。

**示例**

```xml
<Dictionary>
      <Acronyms>
         <CasingExceptions>
            <Acronym>NESW</Acronym>   <!-- North East South West -->
            ...
         </CasingExceptions>
         ...
      </Acronyms>
      ...
</Dictionary>
```

将 Dictionary/Acronyms/CasingExceptions 节点中的字词应用于以下代码分析规则：

- [CA1709:标识符的大小写应当正确](../code-quality/ca1709.md)

## <a name="to-apply-a-custom-dictionary-to-a-project"></a><a name="BKMK_ToApplyACustomDictionaryToAProject"></a> 将自定义字典应用于项目

1. 在解决方案资源管理器中，使用以下过程之一：

    - 若要将字典添加到单个项目，请右键单击项目名称，然后单击“添加现有项”。 在“添加现有项”对话框中指定文件。
  
    - 若要添加在两个或多个项目之间共享的字典，请在“添加现有项”对话框中找到要共享的文件，单击“添加”按钮上的向下箭头，然后单击“添加为链接”  。

2. 在解决方案资源管理器中，右键单击“CustomDictionary.xml”文件名，然后单击“属性”  。

3. 从“生成操作”列表中，选择“CodeAnalysisDictionary” 。

4. 从“复制到输出目录”列表中，选择“不复制” 。
