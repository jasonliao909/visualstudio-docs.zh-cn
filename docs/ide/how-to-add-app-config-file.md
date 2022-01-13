---
title: 如何将 app.config 文件添加到项目
description: 了解如何将 app.config 文件添加到 C# 项目中，以自定义公共语言运行时定位和加载程序集文件的方式。
ms.custom: SEO-VS-2020
ms.date: 01/12/2022
ms.topic: how-to
dev_langs:
- CSharp
helpviewer_keywords:
- app.config files, adding to C# projects
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- dotnet
ms.openlocfilehash: 426750ded6c14dfc2015bfc5ab1e8b73d92eaa88
ms.sourcegitcommit: 9b1c1cceab4c59f0b91e19ae46a51969f72fcc34
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2022
ms.locfileid: "136801222"
---
# <a name="how-to-add-an-application-configuration-file-to-a-c-project"></a>如何：向 C# 项目添加应用程序配置文件

通过将应用程序配置文件（app.config 文件）添加到 C# 项目中，可自定义公共语言运行时定位和加载程序集文件的方式。 有关应用程序配置文件的详细信息，请参阅[运行时如何定位程序集 (.NET Framework)](/dotnet/framework/deployment/how-the-runtime-locates-assemblies)。

> [!NOTE]
> UWP 应用不包含 app.config 文件。

生成项目时，开发环境会自动复制 app.config 文件，更改副本的文件名以匹配可执行文件，然后将副本移动到“bin”目录。

## <a name="to-add-an-application-configuration-file-to-a-c-project"></a>若要向 C# 项目添加应用程序配置文件

::: moniker range="vs-2017"

1. 在菜单栏上，选择 " **Project** " > **添加新项**"。

     此时会显示“添加新项”对话框。

1. 展开 " **已安装** > 的 **Visual c # 项**"，然后选择 " **应用程序配置文件** " 模板。

1. 在“名称”文本框中输入名称，然后选择“添加”按钮。

     项目中将添加名为 app.config 的文件。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在 **解决方案资源管理器** 中，右键单击项目节点，然后选择 " **添加** > **新项**"。

     此时会显示“添加新项”对话框。

1. 展开 " **已安装** > 的 **Visual c # 项**"。

1. 在中间窗格中，选择 " **应用程序配置文件** " 模板。

1. 选择“添加”按钮。

     名为 *App.config* 的文件将添加到你的项目中。

::: moniker-end

## <a name="see-also"></a>另请参阅

- [管理应用程序设置 (.NET)](../ide/managing-application-settings-dotnet.md)
- [配置文件架构 (.NET Framework)](/dotnet/framework/configure-apps/file-schema/index)
- [配置应用 (.NET Framework)](/dotnet/framework/configure-apps/index)
