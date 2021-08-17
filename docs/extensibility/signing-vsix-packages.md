---
title: 为 VSIX 包签名 |Microsoft Docs
description: 了解如何对扩展程序集进行签名。 VSIX 安装程序显示一条消息，指出 VSIX 已签名，并显示有关签名本身的信息。
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
ms.openlocfilehash: c8d82d1e4839a4830eb9a2ac0ac49f80f8e80138
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122028613"
---
# <a name="signing-vsix-packages"></a>对 VSIX 包进行签名
在 Visual Studio 中运行扩展程序集之前，不需要对其进行签名，但这是一种很好的做法。

 如果你想要保护你的扩展，并确保其未被篡改，你可以将数字签名添加到 VSIX 包。 当对 VSIX 进行签名时，VSIX 安装程序将显示一条消息，指示该消息已签名，还会显示有关签名本身的详细信息。 如果已修改 VSIX 的内容，并且 VSIX 未再次进行签名，则 VSIX 安装程序会显示签名无效。 安装未停止，但会警告用户。

> [!IMPORTANT]
> 从 Visual Studio 2015 开始，使用 SHA256 加密以外的任何内容签名的 VSIX 包都将标识为具有无效的签名。 VSIX 安装未被阻止，但会警告用户。

## <a name="signing-a-vsix-with-vsixsigntool"></a>使用 VSIXSignTool 为 VSIX 签名
 Nuget.org 上的 [VisualStudioExtensibility](https://www.nuget.org/profiles/VisualStudioExtensibility) 中提供了一个 SHA256 加密签名工具 [VsixSignTool](https://www.nuget.org/packages/Microsoft.VSSDK.Vsixsigntool)。

#### <a name="to-use-the-vsixsigntool"></a>使用 VSIXSignTool

1. 将 VSIX 添加到项目。

2. 右键单击 "解决方案资源管理器中的项目节点，选择"**添加 &#124; 管理 NuGet 包**"。  有关 NuGet 和添加 NuGet 包的详细信息，请参阅[NuGet 文档](/NuGet)和[程序包管理器 UI](/NuGet/Tools/Package-Manager-UI)主题。

3. 从 VisualStudioExtensibility 搜索 VSIXSignTool 并安装 NuGet 包。

4. 你现在可以从项目的本地包位置中运行 VSIXSignTool。 有关签名方案，请参阅该工具的命令行帮助 (VSIXSignTool.exe/？ ) 。

   例如，使用受密码保护的证书文件进行签名：

   VSIXSignTool.exe sign/f \<certfile> /p \<password>\<VSIXfile>

## <a name="see-also"></a>请参阅
- [传送 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)
