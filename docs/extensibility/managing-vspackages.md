---
title: 管理 Vspackage |Microsoft Docs
description: 了解如何管理 vspackage，以了解何时可以使用 Visual Studio 提供的默认 VSPackage 管理以及如何以及何时对其进行自定义。
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
在大多数情况下，你无需担心如何管理 Vspackage，因为项目和项模板会自动注册并加载包。 但是，在某些情况下，你可能需要更多地了解，才能管理包。

## <a name="use-the-experimental-instance"></a>使用实验实例
 若要了解有关实验实例的详细信息，请参阅 [实验实例](../extensibility/the-experimental-instance.md)。

## <a name="register-and-unregister-vspackages"></a>注册和注销 Vspackage
 若要了解如何注册和注销 Vspackage 和其他类型的扩展，请参阅 [注册和注销 vspackage](../extensibility/registering-and-unregistering-vspackages.md)。

## <a name="load-a-vspackage"></a>加载 VSPackage
 当启用特定 CMDUICONTEXT GUID 时，可以将 Vspackage 设置为 autoload。 有关详细信息，请参阅 [Load vspackage](../extensibility/loading-vspackages.md)。

## <a name="use-asyncpackage-to-load-vspackages-in-the-background"></a>使用 AsyncPackage 在后台加载 Vspackage
 `AsyncPackage`类在后台线程上启用包加载，以便在 Visual Studio 中获得更好的 UI 响应能力。 有关详细信息，请参阅 [如何：使用 AsyncPackage 在后台加载 vspackage](../extensibility/how-to-use-asyncpackage-to-load-vspackages-in-the-background.md)。

## <a name="rule-based-ui-context-for-extensions"></a>用于扩展的基于规则的 UI 上下文
 基于规则的 UI 上下文允许扩展创作者定义激活 UI 上下文以及 Vspackage 加载关联的精确条件。 有关详细信息，请参阅[如何：将基于规则的 UI 上下文用于 Visual Studio 扩展](../extensibility/how-to-use-rule-based-ui-context-for-visual-studio-extensions.md)。

## <a name="diagnose-extension-performance"></a>诊断扩展性能
扩展可能会影响启动和解决方案加载性能。 了解如何计算 Visual Studio 扩展影响，以及如何在本地对其进行分析，以测试是否可以将某个扩展显示为性能影响的扩展。 有关详细信息，请参阅 [如何：诊断扩展性能](how-to-diagnose-extension-performance.md)。

## <a name="troubleshoot-vspackages"></a>Vspackage 故障排除
 了解故障排除 Vspackage 的技术，这些技术无法加载或遇到错误： [疑难解答 vspackage](../extensibility/troubleshooting-vspackages.md)

## <a name="see-also"></a>另请参阅
- [VSPackages](../extensibility/internals/vspackages.md)
