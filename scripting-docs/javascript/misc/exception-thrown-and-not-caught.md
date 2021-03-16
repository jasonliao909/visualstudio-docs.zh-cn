---
description: 你在代码中包含了 throw 语句，但它未包含在 try 块中，或者没有关联的 catch 块捕获该错误。
title: 引发了异常且未被捕获 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5022
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: b5235490-a8e7-42e3-804e-d85235bc6f05
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b8abcfced6dfe78dc18f4e31d2bd90d5e5a45a4a
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2021
ms.locfileid: "103570630"
---
# <a name="exception-thrown-and-not-caught"></a>引发了异常且未被捕获
你在代码中包含了一个 `throw` 语句，但该语句未包含在 **try** 块中，或者没有关联的 **catch** 块捕获该错误。 使用 **throw** 语句从 **try** 块内部引发异常，并使用 **catch** 语句在 **try** 块外捕获异常。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 将可以在 **try** 块中引发异常的代码括起来，并确保存在相应的 **catch** 块。  
  
- 请确保 catch 语句需要正确的异常形式。  
  
- 如果重新引发异常，请确保有另一个相应的 catch 语句。  
  
## <a name="see-also"></a>请参阅  
 [Error 对象](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Error)   
 [throw 语句](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/throw)   
 [尝试 .。。catch .。。finally 语句](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/try...catch)
