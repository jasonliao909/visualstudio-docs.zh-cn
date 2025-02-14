---
title: 测试区域 1：从To-Open添加|Microsoft Docs
description: 此源代码管理插件测试区域介绍如何将解决方案或项目置于源代码管理下，以及从源代码管理中检索它们。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], adding and opening solutions
- source control plug-ins, adding and opening solutions
ms.assetid: 5b3b5b08-5e9b-41be-ac72-c63957faed22
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 1f404b2d4ff41482fa492eedb17261618366934c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122137608"
---
# <a name="test-area-1-add-toopen-from-source-control"></a>测试区域 1：添加到源代码管理/从源代码管理打开
此源代码管理插件测试区域介绍如何将解决方案或项目置于源代码管理下，以及从源代码管理中检索它们。

## <a name="command-menu-access"></a>命令菜单访问
 测试用例 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中使用了以下集成开发环境菜单路径：

- 对于 [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] ，从源代码管理打开 **：文件**、**打开** Project / **解决方案**;查看 [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] 位置。

- 对于其他源代码管理插件，请从源代码管理打开：**文件、****源代码** 管理、**从源代码管理打开**。

- 添加到源代码管理： **文件**、 **源代码** 管理、将 **解决方案添加到** 源代码管理文件、 **源代码** 管理、将 **选定项目添加到源代码管理**。

- 快捷菜单 (Project/解决方案 **) ，将解决方案添加到源代码管理**。

- 从源代码管理中添加 **：文件**、**源代码** 管理 **、从Project添加源。**

- 对于 [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] ，还可以从"文件"、"添加"和"现有Project添加";查看 [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] 位置。

  > [!NOTE]
  > 可在此测试中使用本地文件或本地 IIS (Web 服务器) 路径。

## <a name="expected-behavior"></a>预期行为

- 对于每个受支持的项目类型，用户应该能够"添加到"和"从"源代码管理打开" 。

- 将项目添加到源代码管理时，将创建相应的 \<*ProjectName*> .vspscc (Project提示) 文件。 它包含排除文件列表和连接信息。 不要删除此文件，因为它包含特定于项目的信息。

- 将解决方案添加到源代码管理时，将创建相应的 \<*SolutionName*> .vssscc (三) S 文件。 文本文件包含连接信息和排除文件列表，类似于项目提示文件。 此文件是临时的，仅存在于源代码管理数据库中。

- 从源代码管理打开解决方案时， (临时文件中) 一个 .vsscc 双 S) \<*SolutionName*> 文件。 此文件包含从解决方案连接文件夹到解决方案文件的路径。 此文件是临时的，完成"从源代码管理打开"操作后，将删除本地副本。

- 将项目添加到源代码管理后，可以针对它执行任何 (签出、获取等操作) 。

## <a name="test-cases"></a>测试用例
 以下是"添加到源代码管理"/"从源代码管理打开"测试区域的特定测试用例。

### <a name="case-1a-add-solution-to-source-control"></a>案例 1a：将解决方案添加到源代码管理中
 此测试用例侧重于向源代码管理添加解决方案。

|操作|测试步骤|要验证的预期结果|
|------------|----------------|--------------------------------|
|将包含客户端项目的解决方案添加到源代码管理|1.创建客户端项目。<br />2.将解决方案添加到源代码管理 (**文件**、源代码 **管理**、将解决方案 **添加到源代码管理) 。**|解决方案/Project添加到源代码管理。|
|将包含文件系统或本地 IIS Web 项目的解决方案添加到源代码管理|1.创建文件系统或本地 IIS Web 项目 ("浏览"按钮指向项目的位置;路径确定要创建的 Web 项目) 。<br />2.将解决方案添加到源代码管理 (**文件**、源代码 **管理**、将解决方案 **添加到源代码管理) 。**|解决方案/Project添加到源代码管理。|
|将包含远程站点网站项目的解决方案添加到源代码管理|1.创建远程站点网站项目。<br />2.将解决方案添加到源代码管理 (**文件**、源代码 **管理**、将解决方案 **添加到源代码管理) 。**<br />3.在 FrontPage 访问警告对话框中单击"确定"。|解决方案已添加到源代码管理。<br /><br /> 远程站点项目不在源代码管理下。  (远程站点项目必须从其自己的 IIS server.) |
|使用"将选定项目添加到源代码管理"将 **单个项目解决方案添加到源代码管理**。|1.创建单个项目解决方案。<br />2.仅将解决方案作为选择添加到源代码管理 (**文件、源代码** 管理、将选定项目 **添加到源代码管理) 。** 如果此步骤成功，请继续执行下一步。<br />3.将项目作为选择添加到源代码 **(、****源代码管理、** 将选定项目 **添加到源代码管理) 。**<br />4.单击 **"是** "，将项目添加到同一位置。<br />5.单击 **"签出** 以 **编辑"** 对话框。|`Result from Step 2:`<br /><br /> 项目和项目内的所有文件都有签出的源代码管理指示器，工具提示显示"不在源代码管理下"。<br /><br /> `Result from Step 5:`<br /><br /> Project和解决方案文件在源代码管理中的同一文件夹中。|
|取消将解决方案添加到源代码管理|1.创建单个项目解决方案。<br />2.尝试将项目和解决方案添加到源代码管理。 如果此步骤成功，请继续执行下一步。<br />3.在源代码管理系统中后取消。|`Result from Step 2:`<br /><br /> "设置项目位置源代码管理"对话框只显示一次。<br /><br /> `Result from Step 3:`<br /><br /> Project已取消，则项目/解决方案不在源代码管理下，并且所有"添加到源代码管理"菜单仍可用。|

### <a name="case-1b-open-solution-from-source-control"></a>案例 1b。 从源代码管理打开解决方案
 此测试用例侧重于从源代码管理打开解决方案。

|操作|测试步骤|要验证的预期结果|
|------------|----------------|--------------------------------|
|从源代码管理打开包含客户端项目的解决方案|1.创建客户端项目。<br />2.将解决方案添加到源代码管理。<br />3.关闭解决方案。<br />4.将解决方案从源代码管理打开到新位置。|解决方案/Project源代码管理打开。|
|从源代码管理打开包含本地或 IIS Web 项目的解决方案|1.创建本地或 IIS Web 项目。<br />2.将解决方案添加到源代码管理。<br />3.关闭解决方案。<br />4.将解决方案从源代码管理打开到新位置。|解决方案/Project源代码管理打开。|
|从源代码管理打开包含远程站点网站项目的解决方案|1.创建远程站点网站项目。<br />2.将解决方案添加到源代码管理。 如果此步骤成功，请继续执行下一步。<br />3.关闭解决方案。<br />4.将解决方案从源代码管理打开到新位置。|`Result from Step 2:`<br /><br /> 远程站点网站不在源代码管理下。<br /><br /> `Result from Step 4:`<br /><br /> 从源代码管理打开的解决方案。<br /><br /> 远程站点项目已加载，但它不在源代码管理下。|

### <a name="case-1c-add-solution-from-source-control"></a>案例 1c：从源代码管理添加解决方案
 此测试用例侧重于从源代码管理添加解决方案。

|操作|测试步骤|要验证的预期结果|
|------------|----------------|--------------------------------|
|添加到空解决方案 - 单个项目解决方案|1.创建单个项目解决方案。<br />2.将解决方案添加到源代码管理。<br />3.关闭解决方案。<br />4.创建第二个空解决方案。<br />5.从源代码管理中添加以前控制的解决方案 (**文件****、源代码** 管理、从源代码Project **添加) 。**|添加的项目显示在 **解决方案资源管理器并** 签入。|
|使用单个项目添加到解决方案 - 单个项目|1.使用单个项目创建解决方案。<br />2.将解决方案添加到源代码管理。<br />3.关闭解决方案。<br />4.创建第二个空解决方案。<br />5.从源代码管理中添加以前控制的解决方案 (**文件****、源代码** 管理、从源代码Project **添加) 。**|添加的项目显示在 **解决方案资源管理器并** 签入。|
|添加到解决方案 - 通过选择添加到源代码管理的解决方案|1.使用项目创建解决方案。<br />2.仅将解决方案作为选择添加到源代码管理。 如果此步骤成功，请继续执行下一步。<br />3.关闭解决方案。<br />4.创建新解决方案。<br />5.从源代码管理中添加以前控制的解决方案 (**文件****、源代码** 管理、从源代码Project **添加) 。**|`Result from Step 2:`<br /><br /> Project不在源代码管理下。<br /><br /> `Result from Step 5:`<br /><br /> 如果第一个解决方案包含解决方案项，则不能从源代码管理中添加这些项，因此它们不会出现。<br /><br /> Project解决方案中的资源显示为不可用。|

## <a name="see-also"></a>请参阅
- [源代码管理插件的测试指南](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)
