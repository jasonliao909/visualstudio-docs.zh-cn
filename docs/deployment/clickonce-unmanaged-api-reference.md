---
title: ClickOnce非托管 API 参考|Microsoft Docs
description: 了解 ClickOnce 中的非托管公共 API，dfshim.dll包括 CleanOnlineAppCache、GetDeploymentDataFromManifest 和 LaunchApplication。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
api_name:
- CleanOnlineAppCache
- GetDeploymentDataFromManifest
- LaunchApplication
api_location:
- dfshim.dll
api_type:
- COM
topic_type:
- apiref
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- LaunchApplication [ClickOnce unmanaged]
- ClickOnce, unmanaged APIs
- CleanOnlineAppCache [ClickOnce unmanaged]
- CleanOnlineAppCacheW interface [ClickOnce unmanaged]
- GetDeploymentDataFromManifest [ClickOnce unmanaged]
ms.assetid: ec002138-4054-456d-bcc1-79ac2f4a4fd7
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- cplusplus
ms.openlocfilehash: c78c5dc002caaa17569d3a71f01aa47e7ae901c1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122073859"
---
# <a name="clickonce-unmanaged-api-reference"></a>ClickOnce 非托管 API 参考
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 来自 dfshim.dll 中的非托管公共 API。

## <a name="cleanonlineappcache"></a>CleanOnlineAppCache
 从应用程序缓存中清理或卸载所有 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 联机应用程序。

### <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回表示失败的 HRESULT。 如果发生托管异常，则 返回0x80020009 (DISP_E_EXCEPTION) 。

### <a name="remarks"></a>备注
 如果服务尚未运行，则调用 CleanOnlineAppCache [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 将启动该服务。

## <a name="getdeploymentdatafrommanifest"></a>GetDeploymentDataFromManifest
 从清单和激活 URL 中检索部署信息。

### <a name="parameters"></a>参数

|参数|说明|类型|
|---------------|-----------------|----------|
|`pcwzActivationUrl`|指向 `ActivationURL` 的指针。|LPCWSTR|
|`pcwzPathToDeploymentManifest`|指向 `PathToDeploymentManifest` 的指针。|LPCWSTR|
|`pwzApplicationIdentity`|指向缓冲区的指针，用于接收以 NULL 结尾的字符串，该字符串指定返回的完整应用程序标识。|LPWSTR|
|`pdwIdentityBufferLength`|指向 DWORD 的指针，该 DWORD 是 `pwzApplicationIdentity` WCHAR 中缓冲区的长度。 这包括 NULL 终止字符的空间。|LPDWORD|
|`pwzProcessorArchitecture`|指向缓冲区的指针，用于从清单接收以 NULL 结尾的字符串，该字符串指定应用程序部署的处理器体系结构。|LPWSTR|
|`pdwArchitectureBufferLength`|指向 DWORD 的指针，该 DWORD 是 `pwzProcessorArchitecture` WCHAR 中缓冲区的长度。|LPDWORD|
|`pwzApplicationManifestCodebase`|指向缓冲区的指针，用于从清单接收以 NULL 结尾的字符串，该字符串指定应用程序清单的代码库。|LPWSTR|
|`pdwCodebaseBufferLength`|指向 DWORD 的指针，该 DWORD 是 `pwzApplicationManifestCodebase` WCHAR 中缓冲区的长度。|LPDWORD|
|`pwzDeploymentProvider`|指向缓冲区的指针，用于接收以 NULL 结尾的字符串，该字符串指定清单中的部署提供程序（如果存在）。 否则，将返回空字符串。|LPWSTR|
|`pdwProviderBufferLength`|指向作为 的长度的 DWORD 的指针 `pwzProviderBufferLength` 。|LPDWORD|

### <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回表示失败的 HRESULT。 如果缓冲区太小，则 (ERROR_INSUFFICIENT_BUFFER) HRESULTFROMWIN32。

### <a name="remarks"></a>备注
 指针不得为 null。 `pcwzActivationUrl``pcwzPathToDeploymentManifest`和 不得为空。

 调用方负责清理激活 URL。 例如，在需要转义字符的位置添加转义字符或删除查询字符串。

 调用方负责限制输入长度。 例如，最大 URL 长度为 2KB。

## <a name="launchapplication"></a>LaunchApplication
 使用部署 URL 启动或安装应用程序。

### <a name="parameters"></a>参数

|参数|说明|类型|
|---------------|-----------------|----------|
|`deploymentUrl`|指向以 NULL 结尾的字符串的指针，该字符串包含部署清单的 URL。|LPCWSTR|
|`data`|保留供将来使用。 必须为 NULL。|LPVOID|
|`flags`|保留供将来使用。 必须为 0。|DWORD|

### <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回表示失败的 HRESULT。 如果发生托管异常，则 返回0x80020009 (DISP_E_EXCEPTION) 。

## <a name="see-also"></a>请参阅
- <xref:System.Deployment.Application.DeploymentServiceCom.CleanOnlineAppCache%2A>