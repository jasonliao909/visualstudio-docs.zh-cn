---
description: 您尝试对不是函数对象的对象调用某个函数原型方法，或在函数调用上下文中使用了对象。
title: 应为函数 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5002
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: f62ade94-9f6f-4832-9b9b-49a06a385bbe
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 99e354118844d7e57f708cf3f2d5653ee1c0fc65
ms.sourcegitcommit: 3a855d3513407ea78336386dc3be0b75142614b0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/17/2021
ms.locfileid: "103622603"
---
# <a name="function-expected"></a>缺少函数
尝试对不是对象的对象调用某个 **函数原型** 方法 `Function` ，或在函数调用上下文中使用了对象。 例如，以下代码会产生此错误，因为 **示例** 不是函数。  
  
```JavaScript  
var example = new Object();  // Create a new object called "example".  
var x = example();           // Try and call example as if it were a function.  
```  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 仅对对象调用 **函数原型** 方法 `Function` 。  
  
- 确保使用函数调用运算符 `()` 来仅调用函数。  
  
## <a name="see-also"></a>另请参阅  
 [Function 对象](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Function)   
 [prototype 属性 (Object)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)
