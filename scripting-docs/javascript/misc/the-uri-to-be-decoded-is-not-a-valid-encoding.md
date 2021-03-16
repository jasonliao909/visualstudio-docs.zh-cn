---
description: 您尝试对格式不正确的 URI 进行解码。
title: 要解码的 URI 不是有效的编码 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5025
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 029e0790-ffd1-496d-8700-3b3dbac1b6fd
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: db9d2f89a193ca4542ff5d1ca5ed5c2ae6419f53
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2021
ms.locfileid: "103571982"
---
# <a name="the-uri-to-be-decoded-is-not-a-valid-encoding"></a>要解码的 URI 不是有效编码
尝试将格式不正确的 URI 解码 (统一资源标识符) 。 Uri 具有特殊的语法;大多数非字母数字字符必须先进行编码，然后才能在 URI 中使用。 您可以使用 `encodeURI` 和 `encodeURIComponent` 方法从普通字符串创建 URI [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 。  
  
 完整的 URI 由一个组件和分隔符序列组成。 一般形式为：  
  
```JavaScript  
<Scheme>:<first>/<second>;<third>?<fourth>  
```  
  
 尖括号中的名称表示组件，"："、"/"、";" 和 "？" 是用作分隔符的保留字符。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 确保仅尝试解码有效的 Uri。 不能解码正常 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 字符串，因为它们可能包含无效字符。  
  
## <a name="see-also"></a>请参阅  
 [decodeURI 函数](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/decodeuri)   
 [decodeURIComponent 函数](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/decodeuricomponent)
