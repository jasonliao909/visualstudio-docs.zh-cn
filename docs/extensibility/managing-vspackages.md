---
title: 管理 VSPackages |Microsoft Docs
description: 了解如何管理 VSPackage，以便知道何时只需使用由 Visual Studio 提供的默认 VSPackage 管理，以及如何以及何时对其进行自定义。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, autoloading
- VSPackages, delayed loading
- delay loading
- VSPackages, loading
ms.assetid: 386e0ce5-4107-4164-b0cd-1cf43eb5e7cf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: af813e57420cfcb5c583af18790f5399cb54be47f1f1dc959ec1d6d451951711
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121401058"
---
# <a name="manage-vspackages"></a>管理 VSPackage
在大多数情况下，无需担心如何管理 VSPackage，因为项目和项模板会自动注册和加载包。 但是，在某些情况下，可能需要了解一些知识才能管理包。

## <a name="use-the-experimental-instance"></a>使用实验实例
 若要了解有关实验实例的更多信息，请参阅 [实验实例](../extensibility/the-experimental-instance.md)。

## <a name="register-and-unregister-vspackages"></a>注册和注销 VSPackage
 若要了解如何注册和注销 VSPackage 和其他类型的扩展，请参阅注册和[注销 VSPackage。](../extensibility/registering-and-unregistering-vspackages.md)

## <a name="load-a-vspackage"></a>加载 VSPackage
 VSPackages 可以设置为在打开特定 CMDUICONTEXT GUID 时自动加载。 有关详细信息，请参阅加载[VSPackage。](../extensibility/loading-vspackages.md)

## <a name="use-asyncpackage-to-load-vspackages-in-the-background"></a>使用 AsyncPackage 在后台加载 VSPackage
 类 `AsyncPackage` 允许在后台线程上加载包，以更好地在 Visual Studio。 有关详细信息，请参阅[如何：使用 AsyncPackage 在后台加载 VSPackage。](../extensibility/how-to-use-asyncpackage-to-load-vspackages-in-the-background.md)

## <a name="rule-based-ui-context-for-extensions"></a>扩展的基于规则的 UI 上下文
 基于规则的 UI 上下文允许扩展作者定义激活 UI 上下文和加载关联的 VSPackage 的精确条件。 有关详细信息，请参阅[如何：将基于规则的 UI](../extensibility/how-to-use-rule-based-ui-context-for-visual-studio-extensions.md)上下文用于Visual Studio扩展。

## <a name="diagnose-extension-performance"></a>诊断扩展性能
扩展可能会影响启动和解决方案加载性能。 了解如何Visual Studio扩展影响，以及如何在本地分析扩展，以测试扩展是否显示为影响性能的扩展。 有关详细信息，请参阅 [如何：诊断扩展性能](how-to-diagnose-extension-performance.md)。

## <a name="troubleshoot-vspackages"></a>VSPackage 故障排除
 了解排查未加载或遇到错误的 [VSPackage 的方法：VSPackages 疑难解答](../extensibility/troubleshooting-vspackages.md)

## <a name="see-also"></a>请参阅
- [VSPackages](../extensibility/internals/vspackages.md)
