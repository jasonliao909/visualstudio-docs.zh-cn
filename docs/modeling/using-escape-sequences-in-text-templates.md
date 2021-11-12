---
title: 在文本模板中使用转义序列
description: 了解如何在文本模板中使用转义序列来生成文本模板标记，并仅在 C# 代码中对控制字符和引号进行转义。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, escape sequences
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: e5d77665ddc8f08a5efe2594fb41a8f7424e67b2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665514"
---
# <a name="use-escape-sequences-in-text-templates"></a>在文本模板中使用转义序列

你可以在文本模板中使用转义序列来生成文本模板标记，并（仅在 C# 代码中）对控制字符和引号进行转义。

若要将标准代码块的开始和结束标记输出到输出文件，请对标记进行转义，如下所示：

```
\<# ... \#>
```

可以使用其他文本模板指令和代码块标记执行相同的操作。

如果文本块包含用于对文本模板标记进行转义的字符串，你可以使用以下转义序列：

- 如果文本模板标记前面有偶数个转义 (\\) 字符，则模板分析器将包含一半转义符，并将序列作为文本模板标记包含在内。 例如，如果文本模板中有四个转义字符，则生成的文件中将有两个“\\”字符。

- 如果文本模板标记前面有奇数个转义 (\\) 字符，则模板分析器将包含一半“\\”字符以及标记本身 (\<# or #>)。 不会将该标记视为文本模板标记。

- 如果转义 (\\) 字符出现在序列（仅在 C# 中）对控制字符或引号进行转义的位置之外的任何序列中的任何其他位置，将直接输出该字符。

## <a name="see-also"></a>另请参阅

- [如何：使用转义序列基于模板生成模板](../modeling/how-to-generate-templates-from-templates-by-using-escape-sequences.md)
