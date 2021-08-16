---
title: 提高外接程序VSTO性能
description: 了解如何优化VSTO应用程序创建的外接程序Office，以便快速启动、关闭、打开项和执行其他任务。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 669e690059acb6854eceee224b5439e07c08072d26ba08b3aa69c7fab0a8fe0f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121267723"
---
# <a name="improve-the-performance-of-a-vsto-add-in"></a>提高外接程序VSTO性能
  可以通过优化为 Office 应用程序创建的 VSTO 外接程序为用户提供更好的体验，以便他们快速启动、关闭和打开项，以及执行其他任务。 如果你的 VSTO 外接程序是用于 Outlook 的，则还可以降低由于性能不佳而禁用 VSTO 外接程序的风险。 可以通过实现以下策略来提高 VSTO 外接程序的性能：

- [按需VSTO加载外接程序](#Load)。

- [使用 Office 安装程序 发布Windows解决方案](#Publish)。

- [绕过功能区反射](#Bypass)。

- [在单独的执行线程 中执行成本高昂的操作](#Perform)。

  若要详细了解如何优化外接程序Outlook VSTO，请参阅使外接程序保持VSTO[的性能条件](/previous-versions/office/jj228679(v=office.15)#performance-criteria-for-keeping-add-ins-enabled)。

## <a name="load-vsto-add-ins-on-demand"></a><a name="Load"></a>按需VSTO加载项
 可以将 VSTO 外接程序配置为仅在下列情况下加载：

- 安装 VSTO外接程序后，用户第一次启动应用程序时。

- 随后任何时间启动应用程序后，用户与 VSTO 外接程序第一次交互时。

  例如，VSTO外接程序在用户选择标记为"获取我的数据"的自定义按钮时，可能会 **使用数据填充工作表**。 应用程序必须至少加载VSTO外接程序一次，以便"获取 **我的数据**"按钮可以显示在功能区中。 但是，VSTO下次启动应用程序时，不会再次加载外接程序。 VSTO 外接程序仅在用户选择 **“获取我的数据”** 按钮时加载。

### <a name="to-configure-a-clickonce-solution-to-load-vsto-add-ins-on-demand"></a>配置 ClickOnce 解决方案以按需加载 VSTO 外接程序

1. 在 **“解决方案资源管理器”** 中，选择项目节点。

2. 在菜单栏上，依次选择“查看”   > “属性页”  。

3. 在 **“发布”** 选项卡上，选择 **“选项”** 按钮。

4. 在 **“发布选项”** 对话框中，选择 **“Office 设置”** 列表项，选择 **“按需加载”** 选项，然后选择 **“确定”** 按钮。

### <a name="to-configure-a-windows-installer-solution-to-load-vsto-add-ins-on-demand"></a>配置 Windows Installer 解决方案以按需加载 VSTO 外接程序

1. 在注册表中，将 `LoadBehavior` **_根_\Software\Microsoft\Office \\ _ApplicationName_\Addins \\ _外接程序 ID_** 项的条目设置为0x10。

     有关详细信息，请参阅外接程序 的[VSTO项](../vsto/registry-entries-for-vsto-add-ins.md)。

### <a name="to-configure-a-solution-to-load-vsto-add-ins-on-demand-while-you-debug-the-solution"></a>将解决方案配置为在调试解决方案时按需加载 VSTO 外接程序

1. 创建一个脚本，用于将 `LoadBehavior` **_根_\Software\Microsoft\Office \\ _ApplicationName_\Addins \\ _外接程序 ID_** 键的 **条目** 0x10。

     下面的代码演示了此脚本的一个示例。

    ```cmd/sh
    [HKEY_CURRENT_USER\Software\Microsoft\Office\Excel\Addins\MyAddIn]
    "Description"="MyAddIn"
    "FriendlyName"="MyAddIn"
    "LoadBehavior"=dword:00000010
    "Manifest"="c:\\Temp\\MyAddIn\\bin\\Debug\\MyAddIn.vsto|vstolocal"

    ```

2. 创建一个使用脚本更新注册表的生成后事件。

     下面的代码演示了可添加到生成后事件的命令字符串的示例。

    ```cmd/sh
    regedit /s "$(SolutionDir)$(SolutionName).reg"

    ```

     若要了解如何在 C# 项目中创建生成后事件，请参阅如何：指定 C &#40;[生成&#35;&#41;。 ](../ide/how-to-specify-build-events-csharp.md)

     若要了解如何在项目中创建生成后Visual Basic，请参阅如何：为 指定[生成&#40;Visual Basic&#41;。 ](../ide/how-to-specify-build-events-visual-basic.md)

## <a name="publish-office-solutions-by-using-windows-installer"></a><a name="Publish"></a>使用 Office 安装程序发布 Windows 解决方案
 如果使用 Windows 安装程序发布解决方案，Visual Studio 2010 Tools for Office 运行时将在加载 VSTO 外接程序时跳过以下步骤。

- 验证清单架构。

- 自动检查更新。

- 验证部署清单的数字签名。

  > [!NOTE]
  > 如果将外接程序部署到用户计算机上的VSTO位置，此方法不是必需的。

  有关详细信息，请参阅使用 Office[安装程序部署Windows解决方案](../vsto/deploying-a-vsto-solution-by-using-windows-installer.md)。

## <a name="bypass-ribbon-reflection"></a><a name="Bypass"></a> 绕过功能区反射
 如果使用 生成解决方案，请确保用户在部署解决方案时已安装 Visual Studio [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)] 2010 Tools for Office 运行时的最新版本。 旧版本的运行时VSTO反映在解决方案程序集中，以查找功能区自定义项。 此过程可导致 VSTO 外接程序加载变慢。

 或者，可以阻止任何版本的 Visual Studio 2010 Tools for Office 运行时使用反射来标识功能区自定义项。 若要遵循此策略，请重写 `CreateRibbonExtensibility` 方法，并显式返回功能区对象。 如果VSTO外接程序不包含任何功能区自定义项，则返回 `null` 方法内部。

 下面的示例基于字段的值返回功能区对象。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_ribbon_choose_ribbon_4/ThisWorkbook.vb" id="Snippet1":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_ribbon_choose_ribbon_4/ThisWorkbook.cs" id="Snippet1":::

## <a name="perform-expensive-operations-in-a-separate-execution-thread"></a><a name="Perform"></a> 在单独的执行线程中执行成本高昂的操作
 请考虑在单独的线程中执行耗时的任务（如长时间运行的任务、数据库连接或其他类型的网络调用）。 有关详细信息，请参阅 中的[线程Office。](../vsto/threading-support-in-office.md)

> [!NOTE]
> 调入 Office 对象模型的所有代码都必须在主线程中执行。

## <a name="see-also"></a>请参阅

- [外接程序VSTO加载](/archive/blogs/andreww/demand-loading-vsto-add-ins)
- [延迟加载 Office 外接程序中的 CLR](/archive/blogs/andreww/delay-loading-the-clr-in-office-add-ins)
- [使用 Visual Studio 创建 VSTO 外接程序](create-vsto-add-ins-for-office-by-using-visual-studio.md)