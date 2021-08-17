---
title: 如何：通过使用事务来保存数据
description: 查看如何在数据集中通过 DataSet 工具使用事务保存Visual Studio。 使用 System.Transactions 命名空间将数据保存在事务中。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- saving data, using transactions
- System.Transactions namespace
- transactions, saving data
- data [Visual Studio], saving
ms.assetid: 8b835e8f-34a3-413d-9bb5-ebaeb87f1198
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 5acc25ecb9a370317170d6d419a931414a7dee11ed0b4bcf1c1b4442248d109a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121346903"
---
# <a name="how-to-save-data-by-using-a-transaction"></a>如何：通过使用事务来保存数据

使用 命名空间将数据保存在事务 <xref:System.Transactions> 中。 使用 <xref:System.Transactions.TransactionScope> 对象参与自动管理的事务。

项目不是使用对 *System.Transactions* 程序集的引用创建的，因此你需要手动添加对使用事务的项目的引用。

实现事务的最简单方法是在 语句中 <xref:System.Transactions.TransactionScope> 实例化 `using` 对象。  (有关详细信息，请参阅 [Using 语句](/dotnet/visual-basic/language-reference/statements/using-statement)和 [Using](/dotnet/csharp/language-reference/keywords/using-statement)语句 .) 语句中运行的代码 `using` 参与事务。

若要提交事务，请调用 <xref:System.Transactions.TransactionScope.Complete%2A> 方法作为 using 块中的最后一个语句。

若要回滚事务，在调用 方法之前引发 <xref:System.Transactions.TransactionScope.Complete%2A> 异常。

## <a name="to-add-a-reference-to-the-systemtransactionsdll"></a>添加对引用System.Transactions.dll

1. 在“项目”菜单中，选择“添加引用”。

2. 在 **".NET"** 选项卡 (SQL Server"SQL Server"选项卡) "System.Transactions"，然后选择"确定 **"。**

     对 *System.Transactions.dll的引用* 将添加到项目中。

## <a name="to-save-data-in-a-transaction"></a>在事务中保存数据

- 添加代码以在包含事务的 using 语句中保存数据。 以下代码演示如何在 using 语句中创建 <xref:System.Transactions.TransactionScope> 和实例化 对象：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb" id="Snippet11":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs" id="Snippet11":::

## <a name="see-also"></a>请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
- [演练：在事务中保存数据](../data-tools/save-data-in-a-transaction.md)
