---
title: 管理 Xamarin 应用资源
description: 本文提供各种描述如何在 Visual Studio for Mac 中为各种平台管理应用资源的指南链接
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 05/06/2018
ms.assetid: 61EAAB8F-3C32-4574-924F-CFC616604089
ms.topic: overview
ms.openlocfilehash: d1e2e24d87acea7ec94d5b25b35a8229db347e29
ms.sourcegitcommit: fcf47a9c356df7e9636bcab92186923e5c9b8892
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2022
ms.locfileid: "144516218"
---
# <a name="managing-app-resources"></a>管理应用资源

 [!INCLUDE [Visual Studio for Mac](~/includes/applies-to-version/vs-mac-only.md)]

应用资源文件（如图像、文本文件和音频文件）对你的应用程序是必要的，但它们不使用应用程序进行编译。 Visual Studio for Mac 支持的每个平台以不同的方式处理这些资源，如以下指南中所述：

## <a name="xamarinforms"></a>Xamarin.Forms

Xamarin.Forms 代码在多个平台上运行 - 其中每个平台都具有其自己的文件系统，且每个文件系统指示如何读取和写入到文件。 在 Xamarin.Forms 中，可以使用每个平台上的本机文件 API 或通过将文件添加为嵌入的资源来管理应用资源。

* [使用图像](https://developer.xamarin.com/guides/xamarin-forms/user-interface/images/)
* [使用文件]( https://developer.xamarin.com/guides/xamarin-forms/application-fundamentals/files/)

## <a name="xamarinios"></a>Xamarin.iOS

* [使用资源](https://developer.xamarin.com/guides/ios/application_fundamentals/working_with_resources/)
* [使用图像](https://developer.xamarin.com/guides/ios/application_fundamentals/working_with_images/)
* [使用文件系统](https://developer.xamarin.com/guides/ios/application_fundamentals/working_with_the_file_system/)

## <a name="xamarinandroid"></a>Xamarin.Android

* [Android 资源](https://developer.xamarin.com/guides/android/application_fundamentals/resources_in_android/)

## <a name="xamarinmac"></a>Xamarin.Mac

* [使用图像](https://developer.xamarin.com/guides/mac/application_fundamentals/working-with-images/)

## <a name="see-also"></a>请参阅

- [管理应用程序资源（Windows 上的 Visual Studio）](/visualstudio/ide/managing-application-resources-dotnet)
