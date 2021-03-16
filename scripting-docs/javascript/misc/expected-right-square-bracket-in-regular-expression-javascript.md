---
description: 试图为正则表达式匹配创建字符类，但未包含右大括号。
title: 正则表达式中需要 "]" (JavaScript) |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5019
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 1ca2079a-44dd-479f-a1e3-e04a14d0739e
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6b5e7a25f6fbef3bf87d084b149ee9f356981600
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2021
ms.locfileid: "103570942"
---
# <a name="expected--in-regular-expression-javascript"></a>正则表达式中应有“]”(JavaScript)
试图为正则表达式匹配创建字符类，但未包含右大括号。 可以通过将各个文本字符组合放在方括号中来将它们组合到字符类中。 字符类与它所包含的任何一个字符匹配。 例如，/[abc]/匹配任何字母 "a"、"b" 或 "c"。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 向正则表达式添加右括号。  
  
    > [!NOTE]
    > 如果要匹配单个方括号，请使用反斜杠对其进行转义- \\ [-因此，它不会被解释为特殊字符 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 。  
  
## <a name="see-also"></a>请参阅  
 [正则表达式对象](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/RegExp)   
 [JavaScript)  (正则表达式语法 ](/previous-versions/1400241x(v=vs.100))
