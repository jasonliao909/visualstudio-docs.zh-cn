---
description: 正在调用数组构造函数时使用的参数不是整数 (整数包含零加上一组正整数) 。
title: 数组长度必须为有限正整数 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5029
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 1a467040-4702-4178-848f-418a5974e907
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 49d3d2985706ad6cfca9b6ac441baa039ccf04af
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2021
ms.locfileid: "103572112"
---
# <a name="array-length-must-be-a-finite-positive-integer"></a>数组长度必须为有限正整数
正在调用 **数组** 构造函数时使用的参数不是整数 (整数包含零加上一组正整数) 。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 仅在创建新对象时使用正整数 `Array` 。 如果要创建一个数组，该数组包含不是整数的单个元素，请在两个步骤中执行此操作。 首先创建一个具有一个元素的数组，然后将该值放在第一个元素 (数组 [0] ) 。 下面是生成此错误的示例。  
  
    ```JavaScript  
    var piArray = new Array(3.14159);  
    ```  
  
     下面的示例演示了使用单个数值元素指定数组的正确方法。  
  
    ```JavaScript  
    var piArray = new Array(1);  
    piArray [0] = 3.14159;  
    ```  
  
     除了最大整数值 (大约 4000000000) 以外，数组大小没有上限。  
  
## <a name="see-also"></a>请参阅  
 [使用数组](https://developer.mozilla.org/docs/Learn/JavaScript/First_steps/Arrays)
