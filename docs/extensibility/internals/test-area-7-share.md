---
title: 测试区域 7：共享|Microsoft Docs
description: 此源代码管理测试区域介绍如何使用源代码管理插件的 Share 命令在Visual Studio项。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], sharing items
- source control plug-ins, sharing items
ms.assetid: 6ec4780a-bda4-4327-bb3e-c6c9e7eabf35
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 23b5564470551b1732e57e4cf07cbd191c069d21afd6ac1f0b563f596c852fcd
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121431768"
---
# <a name="test-area-7-share"></a>测试区域 7：共享
此测试区域介绍如何通过 Share 命令在位置 **之间共享** 项。

 hhare 操作是源代码管理文件层次结构中两个或多个位置之间的文件和文件夹项明显重复。 在服务器上实际上不会发生重复，但用户确实在两个或多个指定位置看到相同的文件。 每当更改任何共享项时，这些更改都会显示在所有其他共享位置中。

 如果选择一个文件夹，其中至少有一个文件位于源代码管理下，则共享到文件夹中有效。 在下列情况下禁用共享命令：

- 如果所选文件夹为空文件夹。

- 如果存在实际文件夹，但它不包含源代码管理文件。

- 如果存在虚拟文件夹，则源代码管理下的文件是否位于该文件夹中。

- 如果存在远程站点网站项目。

## <a name="command-menu-access"></a>命令菜单访问
 以下 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 集成开发环境菜单路径用于测试用例。

 共享： -> **文件源代码管理** -> **共享**。

## <a name="expected-behavior"></a>预期行为

- 共享文件显示在共享位置。

- 查看源代码管理版本存储历史记录会显示 (共享) 文件。

- 编辑共享文件会编辑文件的两个位置。

## <a name="test-cases"></a>测试用例
 以下是共享测试区域的特定测试用例。

|操作|测试步骤|要验证的预期结果|
|------------|----------------|--------------------------------|
|将一个文件从源代码管理下的一个已加载项目共享到另一个加载的项目|1.创建新项目。<br />2.向解决方案添加第二个项目。<br />3.创建第二个项目中名称不位于第一个项目的文件。<br />4.将解决方案添加到源代码管理。<br />5.选择第一个项目。<br />6."**打开** 共享"对话框 (  ->  **源代码管理**  ->  **共享) 。**<br />7.将文件从第二个项目共享到第一个项目。<br />8.如果 **系统提示，则** 接受签出。|常见预期行为。|
|将文件从一个项目共享到另一个项目|1.创建新项目。<br />2.将其添加到源代码管理。<br />3.关闭解决方案。<br />4.创建新解决方案 (另一个项目。) <br />5.将解决方案添加到源代码管理。<br />6.选择项目。<br />7.打开"**共享**"对话框  ->  **("文件源代码管理**  ->  **共享") 。**<br />8.将以前添加的项目中的文件共享到打开的项目。<br />9.如果 **系统提示，则** 接受签出。|常见预期行为。|
|将不是项目一部分的文件从源代码管理共享到当前加载的项目|1.创建新项目。<br />2.将解决方案添加到源代码管理。<br />3.将文件添加到不是项目或解决方案的一部分的源代码管理。<br />4.选择项目，然后打开"文件共享 **" ("文件共享**  ->    ->  **") 。**<br />5.选择当前项目或解决方案中不存在的"共享"对话框中的文件，并共享该文件。<br />6.如果 **系统提示，则** 接受签出。|源代码管理存储已执行 Get，因此文件现在位于项目的本地位置。|
|将同一项目中的文件共享到其他文件夹|1.在 **"工具选项""源代码****管理"中选择"**  ->    ->  **自动签出"。**<br />2.创建新项目并将其添加到源代码管理。<br />3.向项目添加文件夹。<br />4.将文件添加到 文件夹并签入文件夹。<br />5.选择文件夹。<br />6."**打开** 共享"对话框 (  ->  **源代码管理**  ->  **共享) 。**<br />7.将文件共享到所选文件夹。|常见预期行为。<br /><br /> 必须先将文件夹与文件一起签入，然后才能用于共享。|
|将文件夹共享到已加载Project — 递归|1.创建新项目。<br />2.将解决方案添加到源代码管理。<br />3.选择项目。<br />4.打开"**文件共享**"对话框  ->  **("文件源代码管理**  ->  **共享) 。**<br />5.选择文件夹。<br />6.以递归将文件夹共享到项目中。|常见预期行为。|
|将多个文件从一个项目共享到另一个项目|1.创建一个包含多个文件的新项目。<br />2.将解决方案添加到源代码管理。<br />3.关闭解决方案。<br />4.在新的解决方案中创建新项目。<br />5.将解决方案添加到源代码管理。<br />6.选择项目。<br />7.打开"**共享**"对话框  ->  **("文件源代码管理**  ->  **共享") 。**<br />8.将以前创建的项目中的多个文件共享到当前打开的项目。|常见预期行为。|

## <a name="see-also"></a>请参阅
- [源代码管理插件的测试指南](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)
