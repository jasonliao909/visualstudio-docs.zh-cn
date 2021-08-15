---
title: 以同步方式加载了扩展
description: 了解从 2019 Visual Studio开始的默认行为，该行为会阻止从任何扩展同步自动加载的包。
ms.custom: SEO-VS-2020
ms.date: 12/11/2019
ms.topic: conceptual
ms.assetid: 822e3cf8-f723-4ff1-8467-e0fb42358a1f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 2f30518d3720625267f0a398b22e4e7f3cf56aa5defb7598c2ec39ddb9797312
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121413864"
---
# <a name="synchronously-autoloaded-extensions"></a>以同步方式加载了扩展

同步自动加载扩展对异步自动加载Visual Studio性能产生负面影响，应将其转换为使用异步自动加载。 默认情况下，Visual Studio 2019 阻止从任何扩展同步自动加载包并通知用户。

![扩展兼容性警告](media/extension-compatibility-warning-16-1.png.png)

方法：

- 单击" **允许同步自动加载** "以允许自动加载扩展。 若要在"Visual Studio"中更改此设置，请单击"环境"，然后单击"扩展"，然后选中复选框"允许同步自动加载扩展"。 

- 单击" **管理性能** "打开" [性能管理器](#performance-manager-dialog) "对话框，显示扩展和工具窗口的性能问题。

- 单击 **"不显示当前扩展的** 此消息"，关闭通知并防止现有已安装扩展以后的通知。 如果添加以同步方式自动加载的新扩展，则此通知将再次显示。 你将继续获取有关其他新功能Visual Studio通知。

## <a name="performance-manager-dialog"></a>"性能管理器"对话框

![性能管理器对话框](media/performance-manager.png)

同步加载任何用户会话中任何包的所有扩展都显示在"已弃 **用 API"选项卡** 中。

* 单击" **有关此问题的更多信息** "，以收集有关已弃用 API 的信息。
* 有关迁移进度，请联系其扩展供应商。

## <a name="specify-synchronous-autoload-settings-using-group-policy"></a>使用组策略指定同步自动加载设置

管理员可以启用同步组策略同步自动加载。 为此，请在以下键上设置基于注册表的策略：

**HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\VisualStudio\SynchronousAutoload**

Entry = **Allowed**

值 = (DWORD)
* **0** 表示不允许同步自动加载
* **1** 是允许同步自动加载

## <a name="extension-authors"></a>扩展作者
扩展作者可以在迁移到 [AsyncPackage](https://github.com/Microsoft/VSSDK-Extensibility-Samples/tree/master/AsyncPackageMigration)中查找有关将包迁移到异步自动加载的说明。

## <a name="see-also"></a>另请参阅
有关 2019 年 1 月中同步自动加载Visual Studio，请参阅[同步自动加载行为](https://devblogs.microsoft.com/visualstudio/updates-to-synchronous-autoload-of-extensions-in-visual-studio-2019/)页。
