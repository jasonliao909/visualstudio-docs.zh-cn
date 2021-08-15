---
title: 测试区域6：删除 |Microsoft Docs
description: 此源代码管理测试区域涵盖 Visual Studio 源代码管理插件的解决方案资源管理器中的删除操作。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], deleting items
- source control plug-ins, deleting items
ms.assetid: 6f2e872c-5ba2-4303-9f50-a90cef9a6225
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: cd2534918bf1db69251681f282ee977dcd6efaf905f30e91fd718a4428958afd
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121336793"
---
# <a name="test-area-6-delete"></a>测试区域 6：删除
此源代码管理插件测试区域包含删除操作。

 源代码管理响应 **解决方案资源管理器** 中的删除操作。

 下面是可以删除的项列表：

- 文件

- 文件夹

- 项目

  根据项目类型，可以选择 **删除** 项目 (将文件保留在磁盘上) 或 **删除** 项目 (删除磁盘上的文件) 。 任一操作都从 **解决方案资源管理器** 中删除项目或项。

## <a name="expected-behavior"></a>预期行为
 删除测试区域中的测试用例的预期行为如下：

- **解决方案资源管理器** 中不再显示已删除的项。

- 所删除的项目或项的父项会根据需要签出 (可能有提示。 ) 

- 删除已签出或添加的项后，它不会显示在 " **挂起签入** " 窗口中。

- 项仍存在于源代码管理存储中，即使在删除后，也必须手动清除。

|操作|测试步骤|要验证的预期结果|
|------------|----------------|--------------------------------|
|删除客户端项目|1. 创建客户端项目。<br />2. 将解决方案添加到源代码管理。<br />3. 从解决方案中删除整个项目|常见的预期行为。|
|删除空文件|1. 创建客户端项目。<br />2. 将零字节文件添加到项目。<br />3. 将解决方案添加到源代码管理。<br />4. 选择文件，将其删除。|常见的预期行为。|
|删除包含一个文件的文件夹|1. 创建单个项目解决方案。<br />2. 添加文件夹。<br />3. 向文件夹添加一个文件。<br />4. 将解决方案添加到源代码管理。<br />5. 查看项目以避免出现提示。<br />6. 删除文件夹。|常见的预期行为。|
|删除文件系统 Web 项目|1. 创建文件系统 Web 项目 (使用 "浏览" 按钮指定 UNC 路径) 。<br />2. 将解决方案添加到源代码管理。<br />3. 从解决方案中删除整个项目。<br />4. 为本地 Web 项目重复步骤1到 3 (在代码中执行不同的路径，但具有相同的外部接口和行为) 。|常见的预期行为。|
|从文件系统 Web 项目中删除文件|1. 创建文件系统 Web 项目。<br />2. 将解决方案添加到源代码管理。<br />3. 从项目中删除文件。<br />4. 为本地 Web 项目重复步骤1到 3 (在代码中执行不同的路径，但具有相同的外部接口和行为) 。|常见的预期行为。|

## <a name="see-also"></a>另请参阅
- [源代码管理插件的测试指南](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)
