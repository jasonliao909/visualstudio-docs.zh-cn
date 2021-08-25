---
title: 在 UWP 应用中使用预提取的内容进行调试 | Microsoft Docs
description: 若要使 UWP 应用更具响应性，请使用 ContentPrefetcher 请求 Windows 预提取 Web 内容。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- uwp
ms.openlocfilehash: 60ec12f554c900aac74f63f463f4ea2c8276b66a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122105192"
---
# <a name="debug-uwp-apps-using-prefetched-content-in-visual-studio"></a>在 Visual Studio 中使用预提取的内容调试 UWP 应用

 若要使 UWP 应用能够更快地响应，可以请求 Windows 将一些 Web 内容（如网页或 Web 图像）预加载到应用的 [WinINet](/windows/desktop/WinInet/about-wininet) 缓存中。 此功能称为“预提取”。 这对于启动时使用的内容特别有效，但也可以预提取其他常用内容。 利用 [Windows.Networking.BackgroundTransfer.ContentPrefetcher](/uwp/api/Windows.Networking.BackgroundTransfer.ContentPrefetcher) 类的方法，可以指定要预加载的内容的 URI。 有关如何将 ContentPrefetcher 功能添加到应用程序的示例，请参阅 [Windows SDK 内容预提取示例](https://code.msdn.microsoft.com/windowsapps/ContentPrefetcher-Sample-432c8309)。

 Windows 使用试探法来确定何时及是否应进行预提取，以及将下载哪些资源。 试探法将考虑系统网络和电源情况、用户应用使用情况历史记录和之前预提取尝试的结果。 在 Visual Studio 中，可以使用“触发 Microsoft Store 应用预提取”命令来强制 Windows 忽略 ContentPrefetcher 试探法并预加载所有指定的 Web 内容。 若要在已知状态（已加载或未加载）下使用要预提取的内容测试应用程序的行为或性能，这会很有用。

## <a name="to-force-preloading-of-contentprefetcher-specified-resources"></a>强制预加载 ContentPrefetcher 指定的资源
 此过程假定你已在应用程序项目中设置 ContentPrefetcher 功能并指定预加载的内容 URI。 若要在指定资源为新的或已修改的资源时强制预加载内容，必须在选择“触发 Microsoft Store 应用预提取”命令之前启动和停止此应用程序。 先运行应用程序以注册 URI。 然后，“触发 Microsoft Store 应用预提取”命令将强制 ContentPrefetcher 下载此内容并将其添加到缓存。 在应用程序的后续运行中，你可以假定已预加载此内容。

1. 启动应用程序以将预提取内容 URI 注册到应用程序。 在“调试”菜单上，选择“启动调试”（键盘快捷键 ：F5）。

2. 在“调试”菜单上，选择“停止调试”（键盘快捷方式： Shift + F5）。

3. 在“调试”菜单上，选择“其他调试目标”，然后选择“触发 Microsoft Store 应用预提取”  。

   现在可以利用预提取的 Web 资源来调试、测试或分析应用程序。

> [!NOTE]
> 当你添加或修改指定的 Web 内容时，请重复上述步骤。

## <a name="see-also"></a>请参阅
- [博客文章：在 Visual Studio 2013 Update 2 中触发 Windows 应用商店应用的预提取](https://devblogs.microsoft.com/devops/triggering-prefetch-for-windows-store-apps-in-visual-studio-2013-update-2/)