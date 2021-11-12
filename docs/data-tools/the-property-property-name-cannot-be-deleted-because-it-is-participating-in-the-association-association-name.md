---
title: 属性参与关联
description: 无法删除属性，因为该属性正在参与关联。 查看此对象关系设计器（O/R 设计器）消息的相关信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 389873cc-92dd-48da-bfca-0f6c8e0ae3c2
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: dc732273719484b7f2f3eaf26a39a8ff518ee3dc
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601081"
---
# <a name="the-property-ltproperty-namegt-cannot-be-deleted-because-it-is-participating-in-the-association-ltassociation-namegt"></a>无法删除属性 &lt;属性名称&gt;，原因是它参与了关联 &lt;关联名称&gt;

选择的属性被设置为错误消息中指示的类之间关联的“关联属性”。 如果属性参与了数据类之间的关联，则无法删除。

将“关联属性”设置为数据类的另一个属性，可以成功删除希望删除的属性。

## <a name="to-correct-this-error"></a>更正此错误

1. 在 O/R 设计器中选择连接错误消息中指示的数据类的关联连线。

2. 双击该连线以打开“关联编辑器”对话框。

3. 从“关联属性”中移除该属性。

4. 再次尝试删除该属性。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)