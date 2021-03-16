---
description: 您尝试使用语句创建一个与条件编译语句一起使用的变量 @set ，但未在变量名之前放置 @ 符号 @ 符号。
title: 应为 "@" |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1032
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 82ff8b74-1710-4358-9a26-dc92ab29c53b
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e7aa02ed1e436c92014d44e57f2c71ff7db5f99b
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2021
ms.locfileid: "103570617"
---
# <a name="expected-"></a>应有“\@”
您尝试使用语句创建一个与条件编译语句一起使用的变量 `@set` ，但没有在变量名称之前加上符号 " **@** "。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- **@** 紧靠在变量名称之前添加 ""。 例如：  
  
    ```JavaScript  
    @set @myvar = 1  
    ```  
  
## <a name="see-also"></a>请参阅  
 [@set 损益](https://developer.mozilla.org/docs/Archive/Web/JavaScript/Microsoft_Extensions/at-set)   
 [条件编译](/previous-versions/windows/internet-explorer/ie-developer/scripting-articles/121hztk3(v=vs.84))   
 [条件编译变量](/previous-versions/windows/internet-explorer/ie-developer/scripting-articles/s59bkzce(v=vs.84))
