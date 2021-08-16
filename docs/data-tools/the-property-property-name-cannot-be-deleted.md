---
title: 无法删除属性
description: 无法删除 属性。 查看有关此Visual Studio 对象关系设计器 (O/R 设计器) 消息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 55873f74-7834-4ec1-8815-eeeb65618d87
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 95caaef5270b5e5a59567a8d91380347f10fef69c1b2a21de87b7030e6ce98f4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121346786"
---
# <a name="the-property-property-name-cannot-be-deleted"></a>属性 \<property name> 无法删除

无法 \<property name> 删除属性，因为它设置为 和 之间的继承的 **鉴别** 器 \<class name> 属性 \<class name>

选择的属性被设置为“鉴别器属性”，用于错误消息中所指示的类之间的继承。 如果属性参与数据类之间的继承配置，则无法删除这些属性。

将“鉴别器属性”设置为数据类的另一个属性，可以成功删除希望删除的属性。

## <a name="to-correct-this-error"></a>更正此错误

1. 在 **O/R 设计器中**，选择连接错误消息中指示的数据类的继承行。

2. 将“鉴别器”属性设置为另一个属性。

3. 再次尝试删除该属性。

## <a name="see-also"></a>另请参阅

- [LINQ to SQL工具Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)