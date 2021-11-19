---
title: 如何：通过使用事务来保存数据
description: 查看如何将事务与 Visual Studio 中的数据集工具结合使用来保存数据。 通过使用 System.Transactions 命名空间将数据保存在事务中。
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
ms.openlocfilehash: 238c5e82a35db0f2fbc6627bd0bb09d3af8f070b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601110"
---
# <a name="how-to-save-data-by-using-a-transaction"></a>如何：通过使用事务来保存数据

通过使用 <xref:System.Transactions> 命名空间将数据保存在事务中。 使用 <xref:System.Transactions.TransactionScope> 对象参与自动为你管理的事务。

项目不是通过对 System.Transactions 程序集的引用创建的，因此，你需要向使用事务的项目手动添加引用。

实现事务最简单的方法是在 `using` 语句中实例化 <xref:System.Transactions.TransactionScope> 对象。 （有关详细信息，请参阅 [Using 语句](/dotnet/visual-basic/language-reference/statements/using-statement)和 [Using 语句](/dotnet/csharp/language-reference/keywords/using-statement)。）在 `using` 语句中运行的代码会参与事务。

若要提交事务，请调用 <xref:System.Transactions.TransactionScope.Complete%2A> 方法作为 using 块中的最后一条语句。

若要回滚事务，请在调用 <xref:System.Transactions.TransactionScope.Complete%2A> 方法之前引发异常。

## <a name="to-add-a-reference-to-the-systemtransactionsdll"></a>添加对 System.Transactions.dll 的引用

1. 在“项目”菜单中，选择“添加引用”。

2. 在“.NET”选项卡（SQL Server 项目的“SQL Server”选项卡）上，选择“System.Transactions”，然后选择“确定”   。

     对“System.Transactions.dll”的引用会添加到项目中。

## <a name="to-save-data-in-a-transaction"></a>将数据保存在事务中

- 添加代码将数据保存在包含事务的 using 语句中。 下面的代码展示了如何在 using 语句中创建和实例化 <xref:System.Transactions.TransactionScope> 对象：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb" id="Snippet11":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs" id="Snippet11":::

## <a name="see-also"></a>另请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
- [演练：在事务中保存数据](../data-tools/save-data-in-a-transaction.md)
