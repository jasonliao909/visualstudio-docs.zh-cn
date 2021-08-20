---
title: 将成员设为静态成员
description: 了解如何使用“快速操作和重构”菜单将成员设为静态成员。
ms.custom: SEO-VS-2020
ms.date: 02/19/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
ms.technology: vs-ide-general
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 215004e6de9cad6988707c5584ba1ff33663396d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122151309"
---
# <a name="make-member-static"></a>将成员设为静态成员

此重构适用于：

- C#

**功能：** 将成员设为静态成员。

**使用时机：** 在你希望非静态成员为静态成员时。

操作原因：静态成员可提高可读性：已知特定代码是隔离的，使其更易于理解、重新读取和重用。 

## <a name="how-to"></a>操作说明

1. 将脱字号放置在成员名称上。

2. 按“Ctrl”  + **。** （句点）触发“快速操作和重构”菜单。

   ![将成员设为静态成员](media/make-member-static.png)

3. 选择“设为静态”。

## <a name="see-also"></a>另请参阅

- [重构](../refactoring-in-visual-studio.md)
