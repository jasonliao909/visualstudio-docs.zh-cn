---
description: 您尝试对不是布尔值的类型的对象调用 valueOf 方法或布尔方法。
title: 应为布尔值 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5010
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 35d71b7f-53fd-44c4-a7c7-b1550c65cfd4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1ceaddc9341d67ac60326fa7121c32655ab6a3f6
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2021
ms.locfileid: "103571436"
---
# <a name="boolean-expected"></a>缺少布尔值
您尝试对类型之外的对象调用 **valueOf** 方法，而不是 **调用的方法** `Boolean` 。 此类调用的对象必须是类型 `Boolean` 。 例如：

```JavaScript
var o = new Object;
o.f = Boolean.prototype.toString;
o.f();
```

## <a name="to-correct-this-error"></a>更正此错误

- 仅对 **布尔** 类型的对象调用 **valueOf** **方法或布尔** 方法。

## <a name="see-also"></a>请参阅

- [Boolean 对象](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)
- [数据类型](https://developer.mozilla.org/docs/Web/JavaScript/Data_structures)
- [控制程序流](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Control_flow_and_error_handling)
- [复制、传递和比较数据](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Functions)
