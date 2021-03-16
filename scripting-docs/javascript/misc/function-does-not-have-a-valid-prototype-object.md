---
description: 您尝试使用 instanceof 来确定对象是否是从特定函数类派生的，但您将对象的原型属性重新定义为 null，或是 (不是有效的 JavaScript 对象) 的外部对象类型。
title: 函数没有有效的原型对象 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5023
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: b9e34652-190f-4b57-b253-df2e8c4d09c6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0356ac9ef7c63c77c0cc0dfca623ff24d3de24af
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2021
ms.locfileid: "103571410"
---
# <a name="function-does-not-have-a-valid-prototype-object"></a>函数没有有效的原型对象
您尝试使用 **instanceof** 来确定对象是否派生自特定函数类，但您将对象的属性重新定义 `prototype` 为 `null` 或外部对象类型 (不是有效的 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 对象) 。 外部对象可以是宿主对象模型中的对象 (例如，Internet Explorer 的文档或窗口对象) 或外部 COM 对象。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 确保函数的 `prototype` 属性引用有效的 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 对象。  
  
## <a name="see-also"></a>请参阅  
 [Function 对象](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Function)   
 [prototype 属性 (Object)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)
