---
title: VSCodeWindowManager 对象|Microsoft Docs
description: 了解 VSCodeWindowManager 对象，该对象负责管理装饰，例如下拉栏。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VSCodeWindowManager
helpviewer_keywords:
- VsCodeWindowManager object
- views [Visual Studio SDK], VSCodeWindowManager object
ms.assetid: e313add5-afdb-4d8d-abd1-764e1fc10c44
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 76ab3d2a72c957b20a79850dc312f5c16de98afc
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905288"
---
# <a name="vscodewindowmanager-object"></a>VSCodeWindowManager 对象

语言服务实现代码窗口管理器，并负责管理修饰 (例如，下拉栏) 。 有关详细信息，请参阅 [使用旧版 API](/previous-versions/visualstudio/visual-studio-2015/extensibility/customizing-code-windows-by-using-the-legacy-api?preserve-view=true&view=vs-2015)自定义代码窗口。

下表显示了 对象中的 `VSCodeWindowManager` 接口。

|接口|描述|
|---------------|-----------------|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|允许在 (窗口中添加) 移除下拉条等修饰。|