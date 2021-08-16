---
title: Configuration 和 SelectedItem 对象的自动化 |Microsoft Docs
description: 了解如何在 Shell 互操作中使用配置和 SelectedItem 对象自动执行 Visual Studio 生成和选定项的处理。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- automation [Visual Studio SDK], SelectedItem object
- automation [Visual Studio SDK], builds
ms.assetid: 120377f1-51aa-4445-b2f7-06ab7fc2b47f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: eac3740444d1c48a196d717e073da035f5920aec468ff216ad22ebdc6cb65918
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121359749"
---
# <a name="automation-for-configuration-and-selecteditem-objects"></a>Configuration 和 SelectedItem 对象的自动化

可以在 Visual Studio 中自动执行生成和所选项的处理。

## <a name="automation-for-builds"></a>生成自动化

生成或配置具有实现时提供的自动化模型 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider> 。 有关详细信息，请参阅[了解生成配置](../../ide/understanding-build-configurations.md)。

如果创建 VSPackage 并想要控制配置选项，则必须使用自动化模型。

## <a name="automation-for-selecteditem"></a>SelectedItem 自动化

`SelectedItem`由于 Visual Studio 包含标准实现，因此不必为对象提供实现。 不过，您可以 `SelectedItem` 根据需要实现对象。 必须实现一个包含接口的对象 `SelectedItem` ，并返回对方法的调用的响应，并 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> `VSITEMID` 将设置为 [__VSHPROPID。VSHPROPID_ExtSelectedItem](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_ExtSelectedItem>)。

## <a name="see-also"></a>另请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A>
- [参与自动化模型](../../extensibility/internals/contributing-to-the-automation-model.md)
- [了解生成配置](../../ide/understanding-build-configurations.md)
