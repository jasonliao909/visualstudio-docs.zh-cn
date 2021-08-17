---
title: 开发最佳做法：COM、VSTO、& VBA 外接程序Office
description: 了解开发 COM、VSTO 和 VBA 外接程序时建议Microsoft Office。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 07/25/2017
ms.topic: conceptual
dev_langs:
- ''
helpviewer_keywords:
- ''
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 523f339fb26ea12e8e737772a59002001d6302bb
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122106466"
---
# <a name="development-best-practices-for-com-vsto-and-vba-add-ins-in-office"></a>适用于 COM、VSTO 和 VBA 外接程序的开发最佳做法Office
  如果要开发 COM、VSTO或 VBA 外接程序Office，请遵循本文中所述的开发最佳做法。   这有助于确保：

- 不同版本和不同部署版本的外接程序的兼容性Office。
- 降低了用户和 IT 管理员的外接程序部署的复杂性。
- 不会发生外接程序意外安装或运行时故障。

>注意[：桌面桥为](/windows/uwp/porting/desktop-to-uwp-root)Windows Store 准备 COM、VSTO或 VBA 外接程序。 COM、VSTO 和 VBA 加载项不能分发到 Windows Store 或 Office Store 中。

## <a name="do-not-check-for-office-during-installation"></a>在安装过程中，Office检查是否安装
 建议不要在外接程序安装过程中检测Office是否安装了该加载项。 如果未Office，可以安装外接程序，并且用户能够在安装外接程序后Office它。

## <a name="use-embedded-interop-types-nopia"></a>将嵌入式互操作类型 (NoPIA) 
如果解决方案使用 .NET 4.0 或更高版本，请使用嵌入式互操作类型 (NoPIA) ，而不是依赖于 Office 主互操作程序集 (PIA) 可再发行组件。 使用类型嵌入可减少解决方案的安装大小，并确保将来的兼容性。 Office 2010 是交付 PIA 可再发行Office的最后一个版本。 有关详细信息，请参阅[演练：](/previous-versions/ee317478(v=vs.140))嵌入来自Microsoft Office的类型信息和类型[等效和嵌入的互操作类型](/windows/uwp/porting/desktop-to-uwp-root)。

如果解决方案使用早期版本的 .NET，建议将解决方案更新为使用 .NET 4.0 或更高版本。 使用 .NET 4.0 或更高版本可减少较新版本的 Windows。

## <a name="avoid-depending-on-specific-office-versions"></a>避免依赖于特定的Office版本
如果解决方案使用仅在较新版本的 Office 中提供的功能，请验证该功能是否存在于 (（如果可能）（例如，使用异常处理或检查版本) ）运行时)  (的功能级别。 使用对象模型中支持的 API（如 [Application.Version](<xref:Microsoft.Office.Interop.Excel._Application.Version%2A>)属性 ）验证最低版本，而不是特定版本。 建议不要依赖于二进制Office、安装路径或注册表项，因为它们在安装、环境和版本之间可能会更改。

## <a name="enable-both-32-bit-and-64-bit-office-usage"></a>启用 32 位和 64 位Office使用情况
默认生成目标应同时支持 32 位 (x86) 和 64 位 (x64) ，除非解决方案依赖于仅适用于特定位的库。 64 位版本的 Office在采用中不断增加，尤其是在大数据环境中。 支持 32 位和 64 位可让用户更轻松地在 32 位和 64 位版本的 Office。

编写 VBA 代码时，请使用 64 位安全声明语句，并适当地转换变量。 此外，通过提供每个位的代码，确保可在运行 32 位或 64 位版本的 Office 之间共享文档。 有关详细信息，请参阅[64 位Visual Basic应用程序概述](/office/vba/Language/Concepts/Getting-Started/64-bit-visual-basic-for-applications-overview)。

## <a name="support-restricted-environments"></a>支持受限环境
解决方案不应要求用户帐户提升或管理员权限。 此外，解决方案不应依赖于设置或更改：

- 当前工作目录。
- DLL 加载目录。
- PATH 变量。

## <a name="change-the-save-location-of-shared-data-and-settings"></a>更改共享数据和设置的保存位置
如果解决方案由外接程序和 Office 外部的进程组成，请不要使用用户的应用程序数据文件夹或注册表在外接程序和外部进程之间交换数据或设置。 请考虑改为使用用户的临时文件夹、文档文件夹或解决方案的安装目录。

## <a name="increment-the-version-number-with-each-update"></a>每次更新时递增版本号
设置解决方案中二进制文件的版本号，并随每个更新递增版本号。 这样，用户就更容易识别版本之间的更改并评估兼容性。

## <a name="provide-support-statements-for-the-latest-versions-of-office"></a>为最新版本的 Office
客户要求 ISV 为在 Office 中运行的 COM、VSTO 和 VBA 外接程序提供支持声明。 列出显式支持声明可帮助使用企业就绪Microsoft 365应用的客户了解你的支持。

若要为 Office 客户端应用程序（例如 Word 或 Excel) ）提供支持语句 (，请首先验证加载项是否在当前 Office 版本中运行，然后承诺在外接程序在将来版本中中断时提供更新。 当 Microsoft 发布新版本或更新外接程序时，不需要测试Office。 Microsoft 很少更改 VSTO 中的 COM、VSTO 和 VBA 扩展性Office，这些更改将记录在文件中。

>重要提示：Microsoft 维护就绪情况报告和 ISV 联系信息支持的外接程序列表。 若要列出外接程序，请参阅 [/configmgr/desktop-analytics/ready-for-windows](/configmgr/desktop-analytics/ready-for-windows)。

## <a name="use-process-monitor-to-help-debug-installation-or-loading-issues"></a>使用进程监视器帮助调试安装或加载问题
如果外接程序在安装或加载过程中有兼容性问题，则这些问题可能与文件或注册表访问问题相关。 使用 [进程监视器](/sysinternals/downloads/procmon) 或类似调试工具记录行为并将其与工作环境进行比较，以帮助识别问题。