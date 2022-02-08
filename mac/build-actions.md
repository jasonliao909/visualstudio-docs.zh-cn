---
title: 设置生成操作
description: 本文介绍可用于 C# 项目的各种生成操作
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 09/18/2019
ms.topic: conceptual
ms.assetid: 5399BCB1-E317-4C7B-87B1-C531E985DE6E
ms.openlocfilehash: 219d16b4b9f383f771e67c2b1c737ca1830bea5a
ms.sourcegitcommit: 782992423db6e1cbbf206715c9b3b400c80052a9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2022
ms.locfileid: "138100925"
---
# <a name="configure-build-actions"></a>配置生成操作

Visual Studio for Mac 项目中的所有文件都具有生成操作。 生成操作控制编译项目时文件发生的情况。 

>[!NOTE]
>本主题适用于 Visual Studio for Mac。 对于 Windows 上的 Visual Studio，请参阅[生成操作](/visualstudio/ide/build-actions)。

## <a name="set-a-build-action"></a>设置生成操作

若要在 Visual Studio for Mac 中设置文件的生成操作，可右键单击任意文件并浏览到“生成操作”，如下所示：

![从解决方案资源管理器选择编译生成操作](media/projects-and-solutions-image1.png)

此文件的生成操作将显示在弹出菜单中。 

## <a name="build-action-values"></a>生成操作值

可在 Visual Studio for Mac 中生成的项目的一些常见生成操作包括：

|生成操作 | 项目类型 | 说明 |
|--|--|--|
| **Compile** | any | 文件被传递到 C# 编译器作为源文件。|
| **内容** | .NET、Xamarin | 对于 ASP.NET 项目，在部署站点时包含这些文件，作为站点的一部分。 对于 Xamarin.iOS 和 Xamarin.Mac 项目，它们会被包含在应用程序包中。|
| **嵌入式资源** | .NET | 文件被传递到 C# 编译器作为嵌入程序集中的资源。 来自 `System.Reflection` 命名空间的 [Assembly.GetManifestResourceStream](/dotnet/api/system.reflection.assembly.getmanifestresourcestream) 可用于从程序集中读取文件。|
| **无** | any | 该文件不以任何形式包含在生成中，且它包括在项目中是为了便于从 IDE 轻松访问。 例如，此值可用于文档文件，例如“ReadMe”文件。|

> [!NOTE]
> 可以为特定项目类型定义其他生成操作，因此，生成操作列表取决于项目类型，可能出现不在此列表中的值。  

Xamarin.iOS 项目具有 BundleResource 生成操作，用于将文件添加为应用程序包的一部分。 有关 Xamarin.Android 特定生成操作的信息，请参阅[生成过程](/xamarin/android/deploy-test/building-apps/build-process#Build_Actions)指南。

还可在解决方案资源管理器中选择多个文件，这样便可同时设置多个文件的生成操作。

## <a name="see-also"></a>另请参阅

- [生成操作（Windows 上的 Visual Studio）](/visualstudio/ide/build-actions)
