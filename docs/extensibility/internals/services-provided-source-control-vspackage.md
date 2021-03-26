---
title: " (源代码管理) 提供的服务 |Microsoft Docs"
description: 了解 Vspackage 如何通过服务共享功能，包括与 Visual Studio IDE 及其 Vspackage 交互。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- services, source control packages
- source control packages, services
ms.assetid: 9db07d70-87d2-4401-bc88-e3a49d81e9a2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fe1d9ee9805e6e86595f3f7f3cf640114c7030b9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080809"
---
# <a name="services-provided-source-control-vspackage"></a>提供的服务（源代码管理 VSPackage）
服务是一种主要机制，通过该机制，Vspackage 和 Visual Studio 集成开发环境 (IDE) 及其安装的 Vspackage 之间共享功能。 有关服务及其在 Visual Studio IDE 中的重要性的详细说明，请参阅[使用和提供服务](../../extensibility/using-and-providing-services.md)。

## <a name="the-source-control-service"></a>源代码管理服务
 Visual Studio 提供了两个服务层： IDE 级服务和包级服务。 Visual Studio IDE 本身提供 IDE 级服务。 源代码管理包使用其中的一些服务。 作为 VSPackage 的源代码管理包通过提供自己的专用源代码管理服务来共享其源代码管理功能。 源代码管理包以可供 Visual Studio IDE 使用的协定的形式封装由其实现的与源代码管理相关的接口集。

## <a name="see-also"></a>另请参阅
- [设计元素](../../extensibility/internals/source-control-vspackage-design-elements.md)
