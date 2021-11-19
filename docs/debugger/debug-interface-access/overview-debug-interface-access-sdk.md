---
description: 使用 DIA SDK 访问 Microsoft 调试信息。
title: 概述 (调试接口访问 SDK) |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- user-defined types
- .dbg files
- modules
- interfaces [DIA SDK]
- DBG files
- procedures [DIA SDK]
- executable files
- COM objects, in DIA SDK
- compilands
- executable images
ms.assetid: 720b4479-a8bc-4fec-860e-80c1a0780405
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 3df38213785f1d7eb6231df82df01a25c00c3223
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832804"
---
# <a name="overview-debug-interface-access-sdk"></a>概述（调试接口访问 SDK）
使用 DIA SDK 访问 Microsoft 调试信息。 DIA SDK 提供了基于 COM 的 API 集，无需在 Microsoft 更改调试信息格式时重写代码。 使用 DIA SDK 还可以读取一组以前版本的调试信息，这些信息位于 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 版本5.0 及更高版本生成的 .pdb 和 dbg 文件中。

 DIA SDK 中的每个接口都表示不同的 COM 对象，但在其他情况下除外。 附加接口，因此其他对象是通过显式查询（如 [IDiaDataSource：： openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md) 或 [IDiaSession：： findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)）创建的，而不是通过调用现有的 `QueryInterface` 接口指针来创建的。

## <a name="see-also"></a>另请参阅
- [IDiaDataSource::openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
