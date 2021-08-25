---
title: 调试数据绑定 ActiveX 控件 | Microsoft Docs
description: 了解如何通过创建容器应用程序进行调试，从而调试绑定到数据源控件的 ActiveX 控件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- data-bound controls, ActiveX
- ActiveX controls, debugging
- controls [Visual Studio], ActiveX
ms.assetid: 9f6e1f00-e25b-48a9-8484-7e67a1232461
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: b3153eb383e3e4ea3b0495319e8acb3904995897
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122030995"
---
# <a name="debugging-a-data-bound-activex-control"></a>调试数据绑定 ActiveX 控件
如果开发的是将被绑定到数据源控件的 ActiveX 控件，可以通过创建自己的容器应用程序并将该容器用于调试该 ActiveX 控件。

 例如，创建基于对话的 MFC 应用程序并将数据绑定控件和数据源控件放在该对话框上。 可将该 MFC 应用程序用于运行时测试和用作调试数据绑定 ActiveX 控件的容器可执行文件。

## <a name="using-the-test-container"></a>使用测试容器
 如果需要可以轻松修改以支持控件或容器上的各种接口的容器，则将 ActiveX 测试容器用作调试会话的可执行文件。 在 ActiveX 测试容器中，从“容器”菜单上单击“选项”以启用各种接口 。 有关详细信息，请参阅[使用测试容器测试属性和事件](/cpp/mfc/testing-properties-and-events-with-test-container)。

 如果在调试时需要单步执行容器的代码，请使用容器的调试版本或者使用 ActiveX 测试容器的调试版本。 有关详细信息，请参阅 [TSTCON 示例：ActiveX 控件测试容器](/previous-versions/f9adb5t5(v=vs.100))。

## <a name="see-also"></a>请参阅
- [调试 COM 和 ActiveX](../debugger/com-and-activex-debugging.md)
- [ActiveX 控件](/cpp/mfc/activex-controls)