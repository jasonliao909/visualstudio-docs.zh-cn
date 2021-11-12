---
title: 缺少连接属性
description: 应用程序设置文件中缺少连接属性或连接属性不正确。 查看此 Visual Studio O/R 设计器消息的相关信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 77724510-ff59-4d43-b933-a0434e1ac597
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 228d938cd056d1d65430abab6386388b68a8d79e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601093"
---
# <a name="the-connection-property-in-the-application-settings-file-is-missing-or-incorrect"></a>应用程序设置文件中的连接属性缺失或不正确

应用程序设置文件中缺少连接属性或连接属性不正确。 已使用 .dbml 文件中的连接字符串来替代它。

.dbml 文件包含对应用程序设置文件中某连接字符串的引用，但无法找到该连接字符串。 此消息是通知性消息；单击“确定”后将创建该连接字符串设置。

若要相应此消息，请选择“确定”。 .dbml 文件中包含的连接信息将添加到应用程序设置中。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
