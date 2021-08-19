---
title: '&lt;customErrorReporting &gt; Element (ClickOnce Deployment) |Microsoft Docs'
description: customErrorReporting 元素指定发生错误时要显示的 URI，而不是显示异常堆栈的错误对话框。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <customErrorReporting> element [ClickOnce deployment manifest]
ms.assetid: 7d31816e-c692-46b5-9cc9-753284b3bcda
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: b296e87accb896f25fe1d83d859e46b0e1d89755
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122153753"
---
# <a name="ltcustomerrorreportinggt-element-clickonce-deployment"></a>&lt;customErrorReporting &gt; 元素 (ClickOnce部署) 
指定发生错误时所显示的 URI。

## <a name="syntax"></a>语法

```xml
<customErrorReporting
   uri
/>
```

## <a name="remarks"></a>备注
 此元素为可选元素。 如果没有它 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ，将显示一个错误对话框，其中显示了异常堆栈。 如果 `customErrorReporting` 元素存在， [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 将改为显示 参数指示的 `uri` URI。 目标 URI 将包括外部异常类、内部异常类和内部异常消息作为参数。

 使用此元素将错误报告功能添加到应用程序。 由于生成的 URI 包含有关错误类型的信息，因此网站可以分析该信息并显示相应的故障排除屏幕，例如。

## <a name="example"></a>示例
 以下代码片段显示了 `customErrorReporting` 元素，以及它可能生成的 URI。

```xml
<customErrorReporting uri=http://www.contoso.com/applications/error.asp />

Example Generated Error:
http://www.contoso.com/applications/error.asp? outer=System.Deployment.Application.InvalidDeploymentException&&inner=System.Deployment.Application.InvalidDeploymentException&&msg=The%20application%20manifest%20is%20signed,%20but%20the%20deployment%20manifest%20is%20unsigned.%20Both%20manifests%20must%20be%20either%20signed%20or%20unsigned.
```

## <a name="see-also"></a>请参阅
- [ClickOnce部署清单](../deployment/clickonce-deployment-manifest.md)