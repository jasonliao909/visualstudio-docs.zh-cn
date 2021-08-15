---
title: Web Project Essentials |Microsoft Docs
description: 了解有关 Web 项目在项目中如何工作的内部Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- web projects, essentials
ms.assetid: ca2f4e43-322c-4431-8680-52da846940bc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 23290b0cccaef596ac2a5d55623f3ddd7ef02ff259e5aba81475bfb638d263e4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121337846"
---
# <a name="web-project-essentials"></a>Web 项目基础知识
Web 项目创建 Web 应用程序。 可以使用 Web 项目创建具有智能网页的 Web 应用程序。 智能网页具有服务器端代码，可按需呈现网页。

 使用传统编程语言（如 或 ）可以创建智能网页，以收集和处理用户的信息、将信息存储在数据库中 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 等。

- 代码隐藏模型将依赖源代码文件与文件扩展名 .aspx 或 .asmx 的网页关联。 例如，hello.aspx 可能有从属源代码文件 hello.aspx.cs。

- 与智能网页关联的服务器端代码编译为位于网站 /bin 文件夹中的可执行文件。

- 其他源代码文件（如不与特定网页关联的帮助程序类）位于网站 /App_Code 文件夹中。

  - WSP (网站) 每个智能网页生成一个可执行文件。 其他可执行文件从 /App_Code 文件夹中的任何源代码文件生成。

  - WAP (Web 应用程序) 生成一个可执行文件，该文件合并所有智能网页的代码以及 /App_Code 文件夹中的所有源文件。

- Web 项目的解决方案文件独立于网站本身。 默认情况下，解决方案文件位于 \Documents，设置 \\ *YourAccount*\我的文档 \\ *\<Visual Studio ####>* \Projects \\ *YourWebSite。*

  > [!NOTE]
  > 如果要将解决方案文件与网站一起保留，只需将其移动到该位置，然后重新打开它。

- 如果打开的网站上没有解决方案Visual Studio，系统会自动为该网站生成一个新的解决方案文件。

- Web 项目没有项目文件。 Project存储在解决方案文件、web.config文件和其他位置。

- 将全局属性添加到 Web 项目会自动在 Web 项目解决方案文件夹中创建存储文件。

- 智能网页可以使用 Page 指令或 标记与服务器端编程语言 \<script runat="server"> 相关联。

- 此外，网页可以具有以任何脚本语言编写的任意数目的客户端脚本块。

- 网站项目系统通过向项目添加项目和项模板以及注册实现 [!INCLUDE[vwprvw](../../extensibility/internals/includes/vwprvw_md.md)] 。

- WAP 系统作为项目子类型实现，也称为项目风格。 项目 [!INCLUDE[vwprvw](../../extensibility/internals/includes/vwprvw_md.md)] 由 WAP 子类型进行风格化，以创建 WAP 系统。 有关项目子类型详细信息，请参阅 Project[子类型](../../extensibility/internals/project-subtypes.md)。

- 智能网页将 HTML 与服务器端编程语言相结合。 服务器端语言称为包含语言。 若要支持包含的语言，Web 项目系统必须实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage> 接口系列。

  - 若要在编辑器中支持包含的语言，HTML 语言服务必须将包含的语言代码显示到包含的语言服务。

  - 应 (编辑器的主缓冲区) 创建红色锯齿的错误标记。

## <a name="see-also"></a>另请参阅
- [Web 项目](../../extensibility/internals/web-projects.md)
