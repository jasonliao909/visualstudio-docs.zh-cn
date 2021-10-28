---
title: 升级 Dotfuscator Community
ms.date: 03/28/2019
ms.devlang: dotnet
ms.topic: conceptual
keywords: Dotfuscator, Dotfuscator Community, Dotfuscator CE, PreEmptive, PreEmptive Solutions, PreEmptive Protection, 保护, 社区版, 模糊处理, .NET, 免费, Visual Studio 2019, Visual Studio 2017, Visual Studio, 升级, 命令行
helpviewer_keywords:
- PreEmptive Protection Dotfuscator
- Dotfuscator Community Edition
- Dotfuscator CE
- Dotfuscator Community
- Dotfuscator
- obfuscation
- protection
- Dotfuscator upgrade
- upgrade Dotfuscator
- upgrading Dotfuscator
- register Dotfuscator
- registering Dotfuscator
- Dotfuscator command line
- Dotfuscator Professional
description: 了解如何升级 Visual Studio 中包含的免费 Dotfuscator Community 副本。
ms.assetid: c7c60904-27f9-4f1f-b79b-ddf65041b810
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.openlocfilehash: ef784a6c0d0816fdbf2ff93c5d4de09c2e4a40a5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126642194"
---
# <a name="upgrade-dotfuscator-community"></a>升级 Dotfuscator Community

Dotfuscator Community 直接向使用 Microsoft Visual Studio 的所有开发人员提供许多应用程序保护和强化功能。
升级 Dotfuscator 版本的用户还可使用更多功能。

本用户指南涵盖了 PreEmptive Protection - Dotfuscator Community 6。
根据你的安装历史记录和 Visual Studio 的版本，你当前可能正在运行 Dotfuscator Community 5，即之前的主版本。
如果是这样，那么应进行升级，因为[必须确保为代码提供最新的保护措施][always-improving]。
升级是免费的。

本页介绍如何确定当前拥有的版本，如何升级到版本 6（如有必要），以及这两个版本之间不同的已替换或删除的功能。

## <a name="determining-dotfuscators-version"></a>确定 Dotfuscator 的版本

如果不确定正在运行哪个 Dotfuscator 版本，可以通过执行以下操作之一来确定版本：

* 通过转到 Visual Studio 的“工具”菜单并选择“PreEmptive Protection - Dotfuscator Community”启动 Dotfuscator Community [图形用户界面][gui] (GUI) 。
  从 Dotfuscator GUI，打开“帮助”菜单，并选择“关于...”以显示“关于”屏幕 。
  此屏幕将列出 Dotfuscator 的版本。

* 如果[命令行接口][cli]（如 [Xamarin][xamarin] 应用中的）的生成中集成了 Dotfuscator，还可以查看某一行的生成日志，如下所示：

  ```no-highlight
  Dotfuscator Community Version 5.42.0.9514-e0e25f754
  ```

  可能需要增加生成的详细程度才能看到此文本。
  对于 Visual Studio，请参阅[详细程度设置][verbosity]。

版本的第一个整数（第一个点 `.` 之前）指示 Dotfuscator 的主要版本。
如果这是 `5`，则应在此页上执行升级步骤，以便可以利用最新 Dotfuscator 6 功能和保护更新。

## <a name="upgrade-instructions"></a>升级说明

本部分包含一组说明，说明如何将 Dotfuscator Community 的典型用法从版本 5 升级到版本 6。

### <a name="installing-dotfuscator-6"></a>安装 Dotfuscator 6

Dotfuscator Community 作为 Visual Studio 的扩展进行分发。
Dotfuscator 6 的安装说明具体取决于所具有的 Visual Studio 版本：

* **Visual Studio 2019**。
  Dotfuscator Community 6 包含在更高版本的 Visual Studio 2019（版本 16.10.0 及更高版本）中。
  [ Visual Studio 2019 升级][vs-update]至最新版本。
  这会自动将任何 Dotfuscator Community 5 安装升级到 Dotfuscator Community 6。

    * 如果尚未安装 Dotfuscator，请先更新 Visual Studio，然后参阅[安装][install]。

    * 除了 Visual Studio 的发布版本外，还可以从 [Dotfuscator 下载][download]页获得最新版本的 Dotfuscator Community。

* Visual Studio 2017。
  此版本的 Visual Studio 仅随 Dotfuscator Community 5 一起提供。
  但是，可以通过转到 [Dotfuscator 下载][download]页并选择相应的下载链接，来安装或升级到 Dotfuscator Community 6。

  运行下载的 `.vsix` 文件，然后按照提示将 Dotfuscator Community 6 安装到 Visual Studio。
  这将升级现有 Dotfuscator Community 5 安装。

* Visual Studio 早期版本。
  这些版本的 Visual Studio 不支持 Dotfuscator Community 6。
  建议升级到更新的 Visual Studio 版本，或[从 Dotfuscator Community 升级到 Dotfuscator Professional][pro]。

如果之前已[注册][register] Dotfuscator Community 5，则首次运行 Dotfuscator Community 6 时，会自动转换该注册。

### <a name="updating-paths-to-the-command-line-interface"></a>更新命令行接口的路径

对于 CLI 更新说明，请参阅完整 Dotfuscator Community 用户指南的 [Updating from Community 5][up-com] 页。

### <a name="upgrading-dotfuscator-config-files"></a>升级 Dotfuscator 配置文件

对于配置文件升级说明，请参阅完整 Dotfuscator Community 用户指南的 [Updating from Community 5][up-com-d] 页。

### <a name="updating-xamarin-integration"></a>更新 Xamarin 集成

对于 Xamarin 集成升级说明，请参阅完整 Dotfuscator Community 用户指南的 [Updating from Community 5][up-com-xa] 页

### <a name="updating-references-to-attribute-libraries"></a>更新对属性库的引用

有关“属性库参考”更新说明，请参阅完整 Dotfuscator Community 用户指南的[更新自 Community 5][up-com-li] 页。

## <a name="removed-features"></a>已删除的功能

Dotfuscator Community 6 引入了 Dotfuscator Community 5 中的中断性变更。
如果你一直在使用 Dotfuscator Community 5，本部分将介绍如何处理可能需要修改生成或影响 Dotfuscator 输出的更改。
可在[更改日志][changelog]中查看更改的完整列表。

## <a name="registering-dotfuscator-community"></a>注册 Dotfuscator Community

Dotfuscator Community 的注册用户可以访问其他功能（如[命令行支持][cli]），将 Dotfuscator Community 轻松集成到自动生成过程中。 注册后还可以访问一款用于[解码混淆堆栈跟踪][decode-obfuscated]的内置工具。

注册快速、简单而且免费。
若要注册 Dotfuscator Community，请参阅[完整 Dotfuscator Community 用户指南中的说明][register-ce]。

## <a name="upgrading-to-dotfuscator-professional"></a>升级到 Dotfuscator Professional

虽然 Dotfuscator Community 提供了基本级别的保护，但如果升级到 PreEmptive Protection - Dotfuscator Professional，你将能够使用增强的模糊处理转换和保护功能。 其中包括：

* *知识产权保护*
  * 其他重命名选项，包括 Enhanced Overload Induction™ 和随机标识符选择。
  * 访问企业级模糊处理转换，包括[以破坏自动化代码反编译为目标的转换][control-flow]。
  * 能够[隐匿敏感字符串][string-encryption]因此不可能对反编译代码进行简单搜索。
  * 能够[将所有权和分发字符审慎串嵌入程序集][watermarking]（软件水印），因此可以确定未经授权的软件泄漏的根源。
  * 能够[将多个程序集组合成一个][linking]，不再分离关注点，让攻击者更加难以确定代码元素的角色。
  * 能够[自动删除应用程序中未使用的代码][pruning]，减少附带的敏感代码量。
* *应用程序完整性保护*
  * 其他[应用程序防御行为][check-actions]。
  * 能够将防篡改和反调试代码注入 `.dll` 程序集。
  * 能够在应用程序生命周期截止前提供警告期。
  * 能够在生命周期警告期内或在截止时间后通知应用程序代码。

Dotfuscator Professional 是行业标准的 [.NET 模糊处理程序][net-obfuscator]，适用于需要持续支持、维护和产品更新的企业开发人员。
此外，Dotfuscator Professional 提供与 Visual Studio 的更紧密集成，并获得商业使用许可。

有关 Dotfuscator Professional 的高级应用程序保护功能的详细信息，请访问 [Dotfuscator 概述页][product-about]和[将 Dotfuscator Professional 与 Dotfuscator Community 进行比较][product-compare]。

[可在 preemptive.com 上请求获取完整支持的 Dotfuscator Professional 试用版。][eval]

## <a name="see-also"></a>请参阅

[升级 Dotfuscator Community][full]

<!-- Copyright © 2021 PreEmptive Solutions, LLC -->

[control-flow]:  https://www.preemptive.com/products/dotfuscator/features#controlflow
[string-encryption]:  https://www.preemptive.com/products/dotfuscator/features#string
[watermarking]:  https://www.preemptive.com/products/dotfuscator/features#watermarking
[linking]:  https://www.preemptive.com/products/dotfuscator/features#linking
[pruning]:  https://www.preemptive.com/products/dotfuscator/features#pruning

[check-actions]:  https://www.preemptive.com/dotfuscator/pro/userguide/en/protection_checks_overview.html#actions

[net-obfuscator]:  https://www.preemptive.com/products/dotfuscator/overview
[eval]:  https://www.preemptive.com/eval-request

[product-about]:  https://www.preemptive.com/products/dotfuscator/overview
[product-compare]:  https://www.preemptive.com/products/dotfuscator/compare-editions

[cli]:  https://www.preemptive.com/dotfuscator/ce/docs/help/intro_cli.html
[register-ce]:  https://www.preemptive.com/dotfuscator/ce/docs/help/gui_getstarted.html#register

[full]:  https://www.preemptive.com/dotfuscator/ce/docs/help/intro_upgrades.html
[decode-obfuscated]:  https://www.preemptive.com/dotfuscator/ce/docs/help/gui_decode_stack_trace.html

[Dotfuscator Community 用户指南][home]

[always-improving]:  https://www.preemptive.com/always-improving
[gui]:  https://www.preemptive.com/dotfuscator/ce/docs/help/getting_started_gui.html
[xamarin]:  https://www.preemptive.com/dotfuscator/ce/docs/help/getting_started_xamarin.html
[verbosity]:  ../how-to-view-save-and-configure-build-log-files.md?view=vs-2019&preserve-view=true#to-change-the-amount-of-information-included-in-the-build-log
[vs-update]:  ../../install/update-visual-studio.md?view=vs-2019&preserve-view=true
[install]:  https://www.preemptive.com/dotfuscator/ce/docs/help/intro_install.html
[download]:  https://www.preemptive.com/products/dotfuscator/downloads
[pro]:  https://www.preemptive.com/dotfuscator/ce/docs/help/intro_upgrades.html
[register]:  https://www.preemptive.com/dotfuscator/ce/docs/help/intro_register.html
[up-com]:  https://www.preemptive.com/dotfuscator/ce/docs/help/intro_upgrade_from_5.html#pctoc-updating-paths-to-the-command-line-interface
[up-com-d]:  https://www.preemptive.com/dotfuscator/ce/docs/help/intro_upgrade_from_5.html#pctoc-upgrading-dotfuscator-config-files
[up-com-xa]:  https://www.preemptive.com/dotfuscator/ce/docs/help/intro_upgrade_from_5.html#pctoc-updating-xamarin-integration
[up-com-li]:  https://www.preemptive.com/dotfuscator/ce/docs/help/intro_upgrade_from_5.html#pctoc-updating-references-to-attribute-libraries
[changelog]:  https://www.preemptive.com/support/dotfuscator-support/dotfuscator-ce-change-log
[home]:  https://www.preemptive.com/dotfuscator/ce/docs/help/index.html