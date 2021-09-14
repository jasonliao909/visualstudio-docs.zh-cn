---
title: 无法删除属性
description: 不能删除该属性。 查看有关此 Visual Studio 的信息对象关系设计器 (O/R 设计器) 消息。
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
ms.openlocfilehash: 307e0f7bf52ed7e95536a13b4b292fda90ef4be1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601078"
---
# <a name="the-property-property-name-cannot-be-deleted"></a>属性 \<property name> 无法删除

\<property name>无法删除属性，因为它被设置为与之间的继承的 **鉴别** 器属性 \<class name>\<class name>

选择的属性被设置为“鉴别器属性”，用于错误消息中所指示的类之间的继承。 如果属性参与数据类之间的继承配置，则无法删除这些属性。

将“鉴别器属性”设置为数据类的另一个属性，可以成功删除希望删除的属性。

## <a name="to-correct-this-error"></a>更正此错误

1. 在 **O/R 设计器** 中，选择连接错误消息中指示的数据类的继承连线。

2. 将“鉴别器”属性设置为另一个属性。

3. 再次尝试删除该属性。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)