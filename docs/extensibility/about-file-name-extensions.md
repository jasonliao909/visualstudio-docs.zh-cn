---
title: 关于文件扩展名 |Microsoft Docs
description: 了解如何为 Vspackage 注册文件扩展名，并将其与特定版本的 Visual Studio 关联。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- file extensions
- file name extensions
ms.assetid: 99f4f9ff-fb84-4258-9787-6890f308a57f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 75629d0f559db2dac717d44eb3dc59b23c8af9e0
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122127787"
---
# <a name="about-file-name-extensions"></a>关于文件扩展名
注册 VSPackage 的文件扩展名时，可以将其与的版本相关联 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 如果在计算机上安装了多个版本的，则这一点非常重要 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

 Vspackage 的文件扩展名在 **HKEY_CLASSES_ROOT** 键下注册，其默认值指向关联的编程标识符 (ProgID) 。

 下面的示例显示了 *vcproj* 文件扩展名的注册信息：

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)=" VisualStudio.vcproj.8.0"
```

 与关联的文件 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 必须具有一个版本控制的 ProgID，如 `VisualStudio.vcproj.8.0` 。 版本控制的 ProgID 允许并行安装产品以维护产品版本之间的文件扩展名关联。 使用版本特定的 ProgID，还可以使用标准谓词（如 "打开"、"编辑" 等），而无需考虑覆盖或被其他应用程序或版本覆盖的问题 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

 在某些情况下，不应更改与文件扩展名关联的 ProgID。 例如，在操作系统的多个位置对 *.htm* 文件扩展名 (progid = htmlfile) 进行硬编码，这是众所周知的，并用于与 *.htm* 和 *.html* 文件关联。

## <a name="see-also"></a>请参阅
- [为并行部署注册文件扩展名](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)
- [指定文件扩展名的文件处理程序](../extensibility/specifying-file-handlers-for-file-name-extensions.md)
