---
title: F# 不支持“编辑并继续”| Microsoft Docs
description: 在调试 F# 时不支持“编辑并继续”。 在调试期间对代码进行的编辑不会应用于源代码，因此正在调试的代码会与源代码不匹配。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Edit and Continue [F#]
- Debugging [F#], Edit and Continue
ms.assetid: 40ec77bb-07e3-4b58-9254-ae015009441c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: c37954fcb334116a81de8a29937983719f6b31ed
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122134098"
---
# <a name="edit-and-continue-not-supported-for-f"></a>F# 不支持“编辑并继续” #
在调试 F# 代码时不支持“编辑并继续”。 在调试会话期间编辑 F# 代码是可以的，但应避免这样做。 在调试会话期间不能应用代码更改。 因此，在调试期间对 F# 代码所做的任何编辑将导致源代码与正在调试的代码不匹配。
