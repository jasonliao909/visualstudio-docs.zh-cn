---
description: 您试图对非 Date 类型的对象调用 valueOf 方法，而不是对该对象调用。
title: 应输入日期对象 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5006
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: d6ab82e6-ca64-46b4-a06c-5c6b0aa057cb
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 171514ae180c2e9b24e8aee56a23c47a909bd152
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2021
ms.locfileid: "103571085"
---
# <a name="date-object-expected"></a>缺少日期对象
您尝试对类型之外的对象调用 **valueOf** **方法，而** 不是对该对象调用 `Date` 。 此类调用的对象必须是类型 `Date` 。 例如：  
  
```JavaScript  
var o = new Object;  
o.f = Date.prototype.toString;  
o.f();  
```  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 仅 **对类型** 为的对象调用 valueOf 或 `Date` 方法。  
  
## <a name="see-also"></a>请参阅  
 [Date 对象](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Date)   
 [getDate 方法 (日期) ](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Date/getdate)   
 [内部对象](https://developer.mozilla.org/docs/Learn/JavaScript/Objects)
