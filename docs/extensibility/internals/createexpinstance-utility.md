---
title: CreateExpInstance 实用工具|Microsoft Docs
description: 了解 CreateExpInstance 实用工具，该实用工具可用于创建、重置或删除数据库的实验Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- experimental builds
- experimental hive
- experimental instance
- createexpinstance
- createexpinst
ms.assetid: 03779774-9401-49ae-997c-0c3ab25ed0d5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 91046edab4693adee21b13616ab8d2f2c1259f11053829bdad23ebcb797bc9ca
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121448177"
---
# <a name="createexpinstance-utility"></a>CreateExpInstance 实用工具
使用 **CreateExpInstance** 实用工具创建、重置或删除 Visual Studio。 可以使用实验实例来调试和测试Visual Studio扩展，而无需更改基础产品。

## <a name="syntax"></a>语法

```
CreateExpInstance.exe [/Create | /Reset | /Clean] /VSInstance=VsInstance /RootSuffix=Suffix
```

## <a name="parameters"></a>参数
 **/Create** 创建实验实例。

 **/Reset** 删除实验实例，然后创建一个新实例。

 **/Clean** 删除实验实例。

 **/VSInstance** 包含要复制的基实例Visual Studio的名称。

 **/RootSuffix** 要追加到实验实例目录名称的后缀。

## <a name="remarks"></a>备注
 处理扩展时，Visual Studio F5 打开默认实验实例并安装当前扩展。 如果没有可用的实验实例，Visual Studio创建一个具有默认设置的实例。

 试验实例的默认位置取决于Visual Studio版本号。 例如，对于 2015 Visual Studio，位置为 *%localappdata%\Microsoft\VisualStudio\14.0Exp \\*。 目录位置的所有文件都被视为该实例的一部分。 除非目录名称更改为默认位置，否则Visual Studio不会加载任何其他实验实例。

 Visual Studio打开实验实例时，它无法访问系统注册表。 这不同于早期版本的 Visual Studio，该版本使用了注册表配置单元的实验版本。

 **CreateExpInstance** 实用工具替换 **VsRegEx** 实用工具。

 以下示例重置实例的默认实验Visual Studio：

 **CreateExpInstance.exe /Reset /VSInstance=14.0 /RootSuffix=Exp**

## <a name="see-also"></a>另请参阅
- [VSPackages](../../extensibility/internals/vspackages.md)
