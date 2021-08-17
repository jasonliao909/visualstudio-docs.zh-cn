---
title: 对 VSIX 包进行签名|Microsoft Docs
description: 了解对扩展程序集进行签名。 VSIX 安装程序显示一条消息，指出 VSIX 已签名，以及有关签名本身的信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- signature
- signing
- authenticode
- vsix
- packages
ms.assetid: e34cfc2c-361c-44f8-9cfe-9f2be229d248
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: c316f66a20f692ccdc20ed4b709efb0522e517d34b95f558be1e3ef30bbffe54
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121413903"
---
# <a name="signing-vsix-packages"></a>对 VSIX 包进行签名
扩展程序集无需签名，然后才能在 Visual Studio 中运行，但这样做是一种很好的做法。

 若要保护扩展并确保其未被篡改，可以将数字签名添加到 VSIX 包。 VSIX 签名后，VSIX 安装程序将显示一条消息，指示已签名，以及有关签名本身的信息。 如果 VSIX 的内容已修改，并且 VSIX 尚未再次签名，则 VSIX 安装程序将显示签名无效。 安装不会停止，但会警告用户。

> [!IMPORTANT]
> 从 Visual Studio 2015 开始，使用 SHA256 加密外的其他任何内容签名的 VSIX 包将被标识为具有无效签名。 VSIX 安装不会受阻，但会警告用户。

## <a name="signing-a-vsix-with-vsixsigntool"></a>使用 VSIXSignTool 为 VSIX 签名
 [VsixSignTool](https://www.nuget.org/packages/Microsoft.VSSDK.Vsixsigntool)上的[VisualStudioExtensibility](https://www.nuget.org/profiles/VisualStudioExtensibility) nuget.org SHA256 加密签名工具。

#### <a name="to-use-the-vsixsigntool"></a>使用 VSIXSignTool

1. 将 VSIX 添加到项目。

2. 右键单击"包"中的项目解决方案资源管理器，然后选择"**添加&#124;管理NuGet包"。**  有关创建和NuGet包NuGet，请参阅 NuGet[文档](/NuGet)和 程序包管理器[UI](/NuGet/Tools/Package-Manager-UI)主题。

3. 从 VisualStudioExtensibility 中搜索 VSIXSignTool，并安装NuGet包。

4. 现在可以从项目的本地包位置运行 VSIXSignTool。 有关 /？) 的签名方案，请参阅该工具的命令行 (VSIXSignTool.exe帮助。

   例如，使用受密码保护的证书文件进行签名：

   VSIXSignTool.exe符号 /f \<certfile> /p \<password>\<VSIXfile>

## <a name="see-also"></a>请参阅
- [传送 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)
