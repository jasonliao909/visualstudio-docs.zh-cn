---
description: 您尝试对除枚举器之外的类型的对象调用 atEnd、moveFirst 或方法，或对该方法调用的枚举器。
title: 应为枚举器对象 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5015
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: dc6e32c1-a6e6-4e12-ac99-e3f65f91c8d7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9fc48ca3e0f17d97af3d538033c2319538afc079
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2021
ms.locfileid: "103571046"
---
# <a name="enumerator-object-expected"></a>缺少枚举器对象
您试图对非类型的对象调用 **atEnd、moveFirst、或** 方法的调用程序，则不能调用该方法的 **方法。** `Enumerator` 此类调用的对象必须是类型 `Enumerator` 。 下面是中断此规则的代码示例：  
  
```JavaScript  
var o = new Object;  
o.f = Enumerator.prototype.atEnd;  
o.f();  
```  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 仅对类型为的对象调用 **atEnd**、 moveFirst、**或** 方法，然后 **调用枚举器** `Enumerator` 方法。 若要确定对象是否为 `Enumerator` 对象，请使用：  
  
    ```js
    if(x instanceof Enumerator)  
    ```  
  
## <a name="see-also"></a>请参阅  
 [Enumerator 对象](https://developer.mozilla.org/docs/Archive/Web/JavaScript/Microsoft_Extensions/Enumerator)
