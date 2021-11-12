---
title: '&lt;entryPoin&gt; 元素（ClickOnce 应用程序） | Microsoft Docs'
description: entryPoint 元素标识在客户端计算机上运行 ClickOnce 应用程序时应执行的程序集。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#commandLine
- urn:schemas-microsoft-com:asm.v2#entryPoint
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <entryPoint> element [ClickOnce application manifest]
- manifests [ClickOnce], entryPoint element
ms.assetid: 10ad3083-10c1-4189-a870-9bba2eab244f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: a6268f2ff1c8d60184ddb290260fa33c841b1d51
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665631"
---
# <a name="ltentrypointgt-element-clickonce-application"></a>&lt;entryPoint&gt; 元素（ClickOnce 应用程序）
标识在客户端计算机上运行 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时应执行的程序集。

## <a name="syntax"></a>语法

```xml
<entryPoint
   name
>
   <assemblyIdentity
      name
      version
      processorArchitecture
      language
   />
   <commandLine
      file
      parameters
   />
   <customHostRequired />
   <customUX />
</entryPoint>
```

## <a name="elements-and-attributes"></a>元素和属性
 `entryPoint` 元素是必需的，它位于 `urn:schemas-microsoft-com:asm.v2` 命名空间中。 在应用程序清单中定义的 `entryPoint` 元素可能只有一个。

 `entryPoint` 元素具有以下属性。

|属性|说明|
|---------------|-----------------|
|`name`|可选。 .NET Framework 不使用此值。|

 `entryPoint` 具有下列元素。

## <a name="assemblyidentity"></a>assemblyIdentity
 必需。 `assemblyIdentity` 的角色及其属性在 [\<assemblyIdentity>](../deployment/assemblyidentity-element-clickonce-application.md) 中定义。

 此元素的 `processorArchitecture` 属性与应用程序清单中其他位置的 `assemblyIdentity` 中定义的 `processorArchitecture` 属性必须匹配。

## <a name="commandline"></a>commandLine
 必需。 必须作为 `entryPoint` 元素的子元素。 它没有子元素但具有以下属性。

| 属性 | 说明 |
|--------------| - |
| `file` | 必需。 对 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序的启动程序集的本地引用。 此值不能包含正斜杠 (/) 或反斜杠 (\\) 路径分隔符。 |
| `parameters` | 必需。 描述要对入口点执行的操作。 唯一有效的值为 `run`；如果提供了空白字符串，则采用 `run`。 |

## <a name="customhostrequired"></a>customHostRequired
 可选。 如果包含，则指定此部署包含将在自定义主机内部署的组件，且不是独立应用程序。

 如果此元素存在，则不能同时存在 `assemblyIdentity` 和 `commandLine` 元素。 如果这两个元素存在，[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 在安装过程中将引发验证错误。

 此元素没有属性和任何子元素。

## <a name="customux"></a>customUX
 可选。 指定应用程序由自定义安装程序安装和维护，并且不创建“开始”菜单项、快捷方式或“添加或删除程序”项。

```xml
<customUX xmlns="urn:schemas-microsoft-com:clickonce.v1" />
```

 包含 customUX 元素的应用程序必须提供一个使用 <xref:System.Deployment.Application.InPlaceHostingManager> 类的自定义安装程序来执行安装操作。 包含此元素的应用程序无法通过双击其清单或 setup.exe 必备组件引导程序来安装。 自定义安装程序可以创建“开始”菜单条目、快捷方式和“添加或删除程序”条目。 如果自定义安装程序不创建“添加或删除程序”项，则它必须存储 <xref:System.Deployment.Application.GetManifestCompletedEventArgs.SubscriptionIdentity%2A> 属性提供的订阅标识符，并使用户能够在以后通过调用 <xref:System.Deployment.Application.InPlaceHostingManager.UninstallCustomUXApplication%2A> 方法来卸载应用程序。 有关详细信息，请参阅[演练：为 ClickOnce 应用程序创建自定义安装程序](../deployment/walkthrough-creating-a-custom-installer-for-a-clickonce-application.md)。

## <a name="remarks"></a>备注
 此元素标识 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序的程序集和入口点。

 你无法在运行时使用 `commandLine` 将参数传递到应用程序中。 可以从应用程序的 <xref:System.AppDomain> 访问 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署的查询字符串参数。 有关详细信息，请参阅[如何：在联机 ClickOnce 应用程序中检索查询字符串信息](../deployment/how-to-retrieve-query-string-information-in-an-online-clickonce-application.md)。

## <a name="example"></a>示例
 下面的代码示例展示 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序的清单中的 `entryPoint` 元素。 此代码示例摘自为 [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)主题提供的一个更大的示例。

```xml
<!-- Identify the main code entrypoint. -->
<!-- This code runs the main method in an executable assembly. -->
  <entryPoint>
    <assemblyIdentity
      name="MyApplication"
      version="1.0.0.0"
      language="neutral"
      processorArchitecture="x86" />
    <commandLine file="MyApplication.exe" parameters="" />
  </entryPoint>
```

## <a name="see-also"></a>另请参阅
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)
