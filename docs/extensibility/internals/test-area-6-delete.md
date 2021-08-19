---
title: 测试区域 6：删除|Microsoft Docs
description: 此源代码管理测试区域介绍了解决方案资源管理器源代码Visual Studio插件的删除操作。
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
ms.openlocfilehash: dd27a0ac99faf9ec2ab4b53fcbae31257e72202f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122158744"
---
# <a name="test-area-6-delete"></a>测试区域 6：删除
此源代码管理插件测试区域涵盖删除操作。

 源代码管理响应中的删除 **解决方案资源管理器。**

 下面是可删除的项的列表：

- 文件

- 文件夹

- Project

  根据项目类型，可以选择"删除项目 (将文件保留) 或删除项目 (删除磁盘上的文件) 。  操作从 中删除项目或 **解决方案资源管理器。**

## <a name="expected-behavior"></a>预期行为
 删除测试区域中测试用例的预期行为是：

- 已删除的项不再显示在 **解决方案资源管理器。**

- 根据需要签出已删除项目或项的父级， (prompt.) 

- 删除签出或添加的项后，它不会出现在"挂起 **的签入"** 窗口中。

- 该项仍然存在于源代码管理存储中，即使在删除后，也必须手动清除。

|操作|测试步骤|要验证的预期结果|
|------------|----------------|--------------------------------|
|删除客户端项目|1.创建客户端项目。<br />2.将解决方案添加到源代码管理。<br />3.从解决方案中删除整个项目|常见预期行为。|
|删除空文件|1.创建客户端项目。<br />2.向项目添加零字节文件。<br />3.将解决方案添加到源代码管理。<br />4.选择文件，将其删除。|常见预期行为。|
|删除包含一个文件的文件夹|1.创建单个项目解决方案。<br />2.添加文件夹。<br />3.将一个文件添加到 文件夹。<br />4.将解决方案添加到源代码管理。<br />5.签出项目以避免出现提示。<br />6.删除文件夹。|常见预期行为。|
|删除文件系统 Web 项目|1.创建文件系统 Web 项目 ("浏览"按钮指定 UNC 路径) 。<br />2.将解决方案添加到源代码管理。<br />3.从解决方案中删除整个项目。<br />4.对本地 Web 项目重复步骤 1 到 3 (通过代码练习不同的路径，但具有相同的外部接口和行为) 。|常见预期行为。|
|从文件系统 Web 项目中删除文件|1.创建文件系统 Web 项目。<br />2.将解决方案添加到源代码管理。<br />3.从项目中删除文件。<br />4.对本地 Web 项目重复步骤 1 到 3 (通过代码练习不同的路径，但具有相同的外部接口和行为) 。|常见预期行为。|

## <a name="see-also"></a>请参阅
- [源代码管理插件的测试指南](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)
