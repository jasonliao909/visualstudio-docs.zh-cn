---
title: 为并行 ID 注册文件名扩展名
description: 了解如何为并行部署注册文件扩展名，以便用户可以在相应版本的 Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- file extensions, registering for side-by-side
ms.assetid: 9ab046a2-147d-4167-aa14-7d661b1eaaa5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: be7c5c2a45d42840c41b5860596cc4fd8c883bf0
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600689"
---
# <a name="register-file-name-extensions-for-side-by-side-deployments"></a>为并行部署注册文件扩展名
对于并行环境中部署的 VSPackage，必须注册文件扩展名，以将文件与正确版本的 关联 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 除非使用版本特定的文件扩展名，否则注册允许用户在 的适当版本中打开项目和项目项文件 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

## <a name="in-this-section"></a>本节内容
- [关于文件扩展名](../extensibility/about-file-name-extensions.md) 讨论如何注册文件扩展名。

- [指定文件扩展名的文件处理程序](../extensibility/specifying-file-handlers-for-file-name-extensions.md) 提供有关如何注册可以打开、编辑特定文件扩展名等的应用程序的信息。

- [为文件扩展名注册谓词](../extensibility/registering-verbs-for-file-name-extensions.md) 讨论如何注册谓词。

- [管理并行文件关联](../extensibility/managing-side-by-side-file-associations.md) 讨论如何处理并行安装，其中应调用 的特定版本以 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 打开文件。

## <a name="related-sections"></a>相关章节
- [支持多个版本的Visual Studio](../extensibility/supporting-multiple-versions-of-visual-studio.md)介绍在开发和部署到最终用户期间与 多个版本的 和 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] VSPackage 相关的问题。
