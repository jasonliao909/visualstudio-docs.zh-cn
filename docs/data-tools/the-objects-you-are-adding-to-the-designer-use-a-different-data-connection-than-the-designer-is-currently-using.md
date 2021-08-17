---
title: 对象使用不同的连接
description: 要添加到设计器的对象使用的数据连接与设计器不同。 查看有关此Visual Studio O/R 设计器消息的信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 332ed2f3-3377-4d51-8e3b-fdb98231978e
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: c4ac9e9426d782c32a4cd75fb73a29f2839edf35ba8f94b8bd8708cc3223a622
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121346773"
---
# <a name="the-objects-you-are-adding-to-the-designer-use-a-different-data-connection-than-the-designer"></a>要添加到设计器的对象使用的数据连接与设计器不同

要添加到设计器中的对象使用的数据连接与设计器当前所用的数据连接不同。 是否要替换设计器使用的连接?

在 **O/R 设计器对象关系设计器 (项** 时) 项都使用一个共享数据连接。   (设计图面表示 ，它针对 surface 上的所有对象使用单个连接。) 如果将对象添加到使用与设计器当前使用的数据连接不同的数据连接的设计器中，则 <xref:System.Data.Linq.DataContext> 会出现此消息。 若要解决此错误，可以选择保持现有连接。 如果选择这样做，则不会添加所选对象。 您也可以选择添加对象并将 <xref:System.Data.Linq.DataContext> 连接重置为新的连接。

## <a name="connection-options"></a>连接选项

- 若要将现有连接替换为所选对象使用的连接，请单击"是 **"。**

   所选对象将添加到 **O/R 设计器** *，DataContext.Connection* 设置为新连接。

   > [!NOTE]
   > 如果单击 **"是****"，O/R** 设计器上的所有实体类将映射到新连接。

- 若要继续使用现有连接并取消添加所选对象，请单击"否 **"。**

   操作被取消。 *DataContext.Connection* 仍设置为现有连接。

## <a name="see-also"></a>请参阅

- [LINQ to SQL工具Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
