---
title: 测试区域 2：从源代码管理|Microsoft Docs
description: 此测试区域涵盖使用 Get 从版本存储中检索项的测试用例。 这些测试用例可同时应用于本地和 Web 项目。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, getting items from source control
- source control [Visual Studio SDK], getting items from
ms.assetid: cbd345c5-ca43-4630-b7a4-85564f4e2090
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: b7feb73cddacc15eeba1bd617f8beaa28a7e068d481290852c2d4e6c2b67801b
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121336819"
---
# <a name="test-area-2-get-from-source-control"></a>测试区域 2：从源代码管理获取
此测试区域涵盖通过 Get 命令从版本存储检索项的测试用例。 这些测试用例可同时应用于本地和 Web 项目。

## <a name="command-menu-access"></a>命令菜单访问
 以下 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 集成开发环境菜单路径用于测试用例。

##### <a name="get-latest-version"></a>获取最新版本：

- **文件**、**源代码管理、****获取最新版本**。

- **文件**， **获取最新版本**。

- 快捷菜单"**获取最新版本"。**

- 获取：**文件**、**源代码管理、****获取**。

## <a name="expected-behavior"></a>预期行为

##### <a name="get-latest-version"></a>获取最新版本：
 执行无提示 (，) 从版本存储区检索项的最新版本。

##### <a name="get"></a>获取：
 显示 **"** 获取"对话框，允许用户对将检索的文件集进行更改，以及修改影响文件检索方式的选项。

## <a name="test-cases"></a>测试用例

|操作|测试步骤|要验证的预期结果|
|------------|----------------|--------------------------------|
|获取本地不存在的文件的最新版本|1.创建项目。<br />2.向项目添加项。<br />3.将项目置于源代码管理下。<br />4.删除项的本地副本。<br />5.获取项的最新版本 (快捷菜单，**获取最新版本) 。**|在本地检索项文件。|
|获取本地不存在的文件|1.创建项目。<br />2.向项目添加项。<br />3.将项目置于源代码管理下。<br />4.删除项的本地副本。<br />5.获取"文件 (**源代码管理"和**"**获取** \<item>) "项。|在本地检索项文件。|
|获取已以独占方式签出并在本地修改的文件|1.创建项目。<br />2.向项目添加项。<br />3.将项目置于源代码管理下。<br />4.以独占方式签出项目项。<br />5.修改本地副本。<br />6.获取文件的项的 **(，****获取最新版本** \<item>) 。 如果此步骤成功，请继续执行下一步。<br />7.单击 **警告** 对话框中的"替换"按钮。|**步骤 6 中的 ReResult**`:`<br /><br /> "警告"对话框指示文件已签出。<br /><br /> **步骤 7 中的 ReResult：**<br /><br /> 修改的本地文件将替换为版本存储区中的原始版本。<br /><br /> 文件是读/写。|
|获取和替换在本地签出、共享和修改的文件|1.创建新项目。<br />2.向项目添加项。<br />3.将项目置于源代码管理下。<br />4.将项目项作为共享项签出。<br />5.修改本地副本。<br />6.获取文件的项的 **(，****获取最新版本** \<item>) 。 如果此步骤成功，请继续执行下一步。<br />7.单击 **警告** 对话框中的"替换"。|**步骤 6 的结果：**<br /><br /> "警告"对话框指示文件已签出。<br /><br /> **步骤 7 的结果：**<br /><br /> 修改的本地文件将替换为版本存储区中的原始版本。<br /><br /> 文件是读/写。|
|获取本地存在的文件，该文件与版本存储中的最新版本相同|1.创建新项目。<br />2.向项目添加项。<br />3.将项目置于源代码管理下。<br />4.获取"文件 (**源代码管理"和**"**获取** \<item>) "。|本地文件保持不变。|
|获取具有一个项目的解决方案|1.创建具有一个项目的解决方案。<br />2.将解决方案放在源代码管理下。<br />3.在本地删除所有项目文件。<br />4.获取解决方案 (**文件、****源代码管理、****获取**) 。|所有已删除的文件都在本地还原。|

## <a name="see-also"></a>请参阅
- [源代码管理插件的测试指南](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)
