---
title: 检测系统要求 |Microsoft Docs
description: 了解如何配置 Microsoft Windows Installer 以检测系统要求，例如安装的 Visual Studio 版本。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- setup, VSPackages
- launch conditions
ms.assetid: 0ba94acf-bf0b-4bb3-8cca-aaac1b5d6737
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 09c83eabb15c1ba4573bc35925529f46d4fb9ad6
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122069960"
---
# <a name="detect-system-requirements"></a>检测系统要求
除非安装 Visual Studio，否则 VSPackage 无法正常工作。 使用 Microsoft Windows Installer 管理 VSPackage 的安装时，可以配置安装程序以检测是否安装了 Visual Studio。 你还可以将其配置为检查系统中是否有其他要求，例如 Windows 的特定版本或特定的 RAM 量。

## <a name="detect-visual-studio-editions"></a>检测 Visual Studio 版本
 若要确定是否安装了某个版本的 Visual Studio，请验证 **安装** 注册表项的值是否 (在相应文件夹中 *REG_DWORD) 1* ，如下表所示。 请注意，有 Visual Studio 版本的层次结构：

1. 企业

2. Professional

3. 社区

安装较新版本时，会添加该版本的注册表项以及早期版本的注册表项。 也就是说，如果安装了 Enterprise 版，则 Enterprise 以及 Professional 和 Community 版本的 **安装** 密钥设置为 *1* 。 因此，只需要检查所需的最新版本。

> [!NOTE]
> 在64位版本的注册表编辑器中，32位密钥显示在 " **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\\**" 下。 Visual Studio 项在 **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\DevDiv\vs\Servicing\\** 下。

|产品|键|
|-------------|---------|
|Visual Studio Enterprise 2015|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\enterprise|
|Visual Studio Professional 2015|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\professional|
|Visual Studio Community 2015|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\community|
|Visual Studio 2015 Shell (集成和隔离) |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\isoshell|

## <a name="detect-when-visual-studio-is-running"></a>检测 Visual Studio 何时运行
 如果安装 VSPackage 时 Visual Studio 正在运行，则无法正确注册 VSPackage。 安装程序必须检测 Visual Studio 正在运行的时间，然后拒绝安装该程序。 Windows安装程序不允许使用表项来启用此类检测。 相反，您必须创建自定义操作，如下所示：使用 `EnumProcesses` 函数检测 *devenv.exe* 进程，然后设置在启动条件中使用的安装程序属性，或按条件显示一个对话框，提示用户关闭 Visual Studio。

## <a name="see-also"></a>请参阅
- [安装 vspackage 与 Windows Installer](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
