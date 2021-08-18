---
title: 为解决方案创建父容器|Microsoft Docs
description: 了解如何使用源代码管理插件 API 版本 1.2 为解决方案内的所有 Web 项目指定单个根源代码管理目标。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions, creating parent containers
- source control plug-ins, creating parent containers
ms.assetid: 961e68ed-2603-4479-a306-330eda2b2efa
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 88ae7686af37b601ef6c5093a035d58281f2bdca
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122086698"
---
# <a name="create-parent-container-folders-for-solutions"></a>为解决方案创建父容器文件夹
在源代码管理插件 API 版本 1.2 中，用户可以为解决方案内的所有 Web 项目指定单个根源代码管理目标。 此单一根称为超级统一根 (SUR) 。

 在源代码管理插件 API 版本 1.1 中，如果用户向源代码管理添加了多项目解决方案，系统会提示用户为每个 Web 项目指定一个源代码管理目标。

## <a name="new-capability-flags"></a>新功能标志
 `SCC_CAP_CREATESUBPROJECT`

 `SCC_CAP_GETPARENTPROJECT`

## <a name="new-functions"></a>新函数
- [SccCreateSubProject](../../extensibility/scccreatesubproject-function.md)

- [SccGetParentProjectPath](../../extensibility/sccgetparentprojectpath-function.md)

 将 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 解决方案添加到源代码管理时，IDE 几乎总是创建一个 SUR 文件夹。 具体而言，它在下列情况下会这样做：

- 该项目是文件共享 Web 项目。

- 项目和解决方案文件有不同的驱动器。

- 项目和解决方案文件有不同的共享。

- 在源代码管理的解决方案 (单独添加了项目) 。

在 中，建议 SUR 文件夹的名称与不带扩展 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 名的解决方案名称相同。 下表总结了这两个版本的行为。

|特征|源代码管理插件 API 版本 1.1|源代码管理插件 API 版本 1.2|
|-------------| - | - |
|将解决方案添加到 SCC|SccInitialize () <br /><br /> SccGetProjPath () <br /><br /> SccGetProjPath () <br /><br /> SccOpenProject () |SccInitialize () <br /><br /> SccGetProjPath () <br /><br /> SccCreateSubProject () <br /><br /> SccCreateSubProject () <br /><br /> SccOpenProject () |
|将项目添加到源代码管理的解决方案|SccGetProjPath () <br /><br /> OpenProject () |SccGetParentProjectPath () <br /><br /> SccOpenProject () <br /><br />  **注意**：Visual Studio假定解决方案是 SUR 的直接子级。  |

## <a name="examples"></a>示例
 下表列出了两个示例。 在这两种情况下，系统会提示用户输入源代码管理下解决方案的目标位置，user_choice指定为 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 目标。  指定user_choice时，将添加解决方案和两个项目，而不会提示用户输入源代码管理目标。

|解决方案包含|在磁盘位置|数据库默认结构|
|-----------------------|-----------------------|--------------------------------|
|*sln1.sln*<br /><br /> Web1<br /><br /> Web2|*C：\Solutions\sln1*<br /><br /> *C：\Inetpub\wwwroot\Web1*<br /><br /> \\\server\wwwroot$\Web2|$/<user_choice>/sln1<br /><br /> $/<user_choice>/C/Web1<br /><br /> $/<user_choice>/Web2|
|*sln1.sln*<br /><br /> Web1<br /><br /> Win1|*C：\Solutions\sln1*<br /><br /> *D：\Inetpub\wwwroot\Web1*<br /><br /> *C：\solutions\sln1\Win1*|$/<user_choice>/sln1<br /><br /> $/<user_choice>/D/web1<br /><br /> $/<user_choice>/sln1/win1|

 无论操作是因错误而取消还是失败，都会创建 SUR 文件夹和子文件夹。 它们不会自动在取消或错误条件下删除。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 如果源代码管理插件不返回 功能标志，则 默认为版本 1.1 `SCC_CAP_CREATESUBPROJECT` `SCC_CAP_GETPARENTPROJECT` 行为。 此外， 的用户可以通过将以下键的值设置为 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] *dword：00000001 来选择还原到* 版本 1.1 行为：

 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl] DoNotCreateSolutionRootFolderInSourceControl**  = *dword：00000001*

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
