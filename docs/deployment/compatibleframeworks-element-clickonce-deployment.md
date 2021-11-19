---
title: '&lt;compatibleFrameworks&gt; 元素（ClickOnce 部署）| Microsoft Docs'
description: compatibleFrameworks 元素会标识此应用程序可在其上安装和运行的 .NET Framework 版本。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <compatibleFrameworks> element [ClickOnce deployment manifest]
ms.assetid: f6c3ee55-9e65-403d-8664-3ebde872c7d4
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: ed84d7f7ed60a95baba293a33059a05093400bbb
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666951"
---
# <a name="ltcompatibleframeworksgt-element-clickonce-deployment"></a>&lt;compatibleFrameworks&gt; 元素（ClickOnce 部署）
标识此应用程序可在其上安装和运行的 .NET Framework 版本。

> [!NOTE]
> 使用 [MageUI.exe](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client) 保存已用证书签名的应用程序清单时，[MageUI.exe](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client) 不支持 `compatibleFrameworks` 元素 。 这种情况下必须使用 [Mage.exe](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)。

## <a name="syntax"></a>语法

```xml
<compatibleFrameworks
      SupportUrl> 
   <framework
      targetVersion
      profile
      supportedRuntime
   /> 
</ compatibleFrameworks>
```

## <a name="elements-and-attributes"></a>元素和属性
 对于面向 .NET Framework 4 或更高版本提供的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 运行时的部署清单，需要 `compatibleFrameworks` 元素。 `compatibleFrameworks` 元素包含一个或多个 `framework` 元素，这些元素指定此应用程序可在其上运行的 .NET Framework 版本。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 运行时将在此列表中第一个可用的 `framework` 上运行应用程序。

 下表列出了 `compatibleFrameworks` 元素支持的属性。

|属性|说明|
|---------------|-----------------|
|`S` `upportUrl`|可选。 指定可在其中下载首选兼容 .NET Framework 版本的 URL。|

## <a name="framework"></a>框架
 必需。 下表列出了 `framework` 元素支持的属性。

|属性|说明|
|---------------|-----------------|
|`targetVersion`|必需。 指定目标 .NET Framework 的版本号。|
|`profile`|必需。 指定目标 .NET Framework 的配置文件。|
|`supportedRuntime`|必需。 指定与目标 .NET Framework 关联的运行时的版本号。|

## <a name="remarks"></a>备注

## <a name="example"></a>示例
 下面的代码示例演示了 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署清单中的 `compatibleFrameworks` 元素。 此部署可以在 [!INCLUDE[net_client_v40_long](../deployment/includes/net_client_v40_long_md.md)] 上运行。 它还可以在 .NET Framework 4 上运行，因为它是 [!INCLUDE[net_client_v40_long](../deployment/includes/net_client_v40_long_md.md)] 的超集。

```xml
<compatibleFrameworks xmlns="urn:schemas-microsoft-com:clickonce.v2">
  <framework
      targetVersion="4.0"
      profile="Client"
      supportedRuntime="4.0.30319" />
</compatibleFrameworks>
```

## <a name="see-also"></a>另请参阅
- [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)