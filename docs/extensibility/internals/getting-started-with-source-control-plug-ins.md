---
title: 入门源代码管理插件|Microsoft Docs
description: 了解如何创建源代码管理插件，该插件实现源代码管理插件 API 中定义的用于源代码版本控制的函数。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, getting started
- getting started, source control plug-ins
ms.assetid: 46ac1f9f-4ecc-4a72-88d3-4c7e1647e1cb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 65972621980b311dc3a396836c4c85286e10a00e2e93589a9b3aeaffc8627528
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121337976"
---
# <a name="get-started-with-source-control-plug-ins"></a>源代码管理插件入门
若要创建源代码管理插件，必须创建一个实现源代码管理插件 API 中定义的函数的 DLL，然后向 注册 DLL，使其可用于源代码版本控制。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]

 源代码管理插件 API (1.1、1.2 和 1.3) 三个版本可用于源代码管理插件。此处介绍的源代码管理插件 API 版本为 1.3。 它旨在与支持版本 1.1 和 1.2 的源代码管理插件完全兼容。 源代码 [管理插件 API 版本 1.3](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-3.md) 中的新增功能部分详细介绍了最新版本的源代码管理插件 API 中支持的新功能。

## <a name="in-this-section"></a>本节内容
- [如何：安装源代码管理插件](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)

 介绍如何创建插入源代码管理 DLL 所需的注册表项。

- [源代码管理插件 API 版本 1.3 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-3.md)

 简要概述在版本 1.3 中对源代码管理插件 API 所做的更改。

- [源代码管理插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)

 简要概述在版本 1.2 中对源代码管理插件 API 所做的更改。

## <a name="related-sections"></a>相关章节
- [源代码管理插件](../../extensibility/source-control-plug-ins.md)

 提供源代码管理插件 API 中所有元素的完整列表。

- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)

 定义源代码管理插件 SDK 并描述包含的资源。
