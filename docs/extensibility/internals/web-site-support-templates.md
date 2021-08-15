---
title: 网站支持模板|Microsoft Docs
description: 了解网站支持模板。 Visual Studio网站项目和项模板提供可重用且可自定义的网站项目和项存根。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- we site projects, templates
ms.assetid: 37173c97-486b-4b3c-8ed3-cf5890c4de23
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6480b21cc4907e45b174b69418f1d10177f36440597949fd8a1806246016dc27
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121414150"
---
# <a name="web-site-support-templates"></a>网站支持模板
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 网站项目和项模板提供可重用且可自定义的网站项目和项存根，无需从头开始创建新的网站项目和项，从而加快开发过程。 有关模板的详细信息 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，请参阅 Creating [Project 和 Item Templates。](../../ide/creating-project-and-item-templates.md)

## <a name="project-template-folder"></a>Project模板文件夹
 Web 项目模板通常安装在 [*Visual Studio 安装* 路径 ]\Common7\IDE\ProjectTemplates\Web 上，每个模板都安装在以 Web 编程语言命名的子文件夹 \\ 内。

## <a name="project-file"></a>项目文件
 IDE (集成) 需要项目文件扩展名，才能将模板 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 映射到正确的项目类型。 由于 Web 项目没有项目文件，因此将注册虚拟项目文件扩展名 .webproj，以将模板映射到项目类型。

 （可选）可以将语言名称字符串添加到模板，使 Web 项目系统能够基于模板为项设置"添加新项"对话框中的语言默认值。 字符串必须是文件的第一行。 它必须匹配在 IntelliSense 引擎注册中的 AddItemLanguageName 下注册的名称，以及 VsTemplate Project 子 (注册) 。 有关详细信息，请参阅 [网站支持属性](../../extensibility/internals/web-site-support-attributes.md)。

 如果字符串不存在，则 Web 项目系统会尝试根据 Web 模板添加到 Web 项目的页的 Language 属性和文件扩展名来确定Project语言。

## <a name="project-templates"></a>项目模板
 网站项目模板用于生成新网站，以响应"文件"菜单 **上的** "新建网站 **"** 命令。 目前支持三种网站项目类型：

- 空网站项目

- 网站项目

- Web 服务项目

### <a name="empty-web-site-projects"></a>空网站项目
 这些文件会创建一个新的空网站以响应"空 **网站**"命令，该命令在选择"文件""新建网站"  >  **后可用**：

- EmptyWeb.vstemplate

     指导新建空网站的模板文件。

- EmptyWeb.webproj

     此文件是项目模板系统的项目。 它满足 EmptyWeb.vstemplate 文件中项目文件引用。

### <a name="web-site-projects"></a>网站项目
 这些文件会创建一个新网站以响应 ASP.NET **网站命令**，该命令在选择"文件""新建网站"  >  **后可用**：

- Default.aspx

     新网站的默认主页。 Language 属性指定代码后发语言，CodeFile 属性指定包含与此页关联的代码后发代码的依赖文件。

- Default.aspx。*扩展*

     包含默认主页的代码后发代码的依赖文件。 代码后发语言确定 *此文件* 的扩展名。

- web.config

     根 web.site 配置文件。

- WebApplication.vstemplate

     用于确定网站解决方案的内容并强制创建 App_Data 文件的模板文件。

- WebApplication.webproj

     此文件是项目模板系统的项目。 它满足 WebApplication.vstemplate 文件中项目文件引用。

### <a name="web-service-projects"></a>Web 服务项目
 这些文件创建新的网站以响应 ASP.NET Web 服务命令，该命令在选择 **"文件""新建** 网站"  >  **后可用**：

- Service.asmx

     新 Web 服务的 HTML 页。 Language 属性指定代码后发语言，CodeBehind 属性指定包含与此服务关联的代码后发代码的依赖文件。

- Service。 *extension*

     实现服务类的依赖文件。 代码后发语言确定 *此文件* 的扩展名。

- web.config

- 根 web.site 配置文件。

- WebService.vstemplate

     模板文件，用于确定网站解决方案的内容并强制创建App_Data App_Code文件夹。 服务。*扩展* 文件将复制到 App_Code 文件夹。

- WebService.webproj

     此文件是项目模板系统的项目。 它满足 WebService.vstemplate 文件中项目文件引用。

## <a name="project-item-template-folder"></a>Project项模板文件夹
 Web 项目项模板通常安装在 [ Visual Studio *安装* 路径 ]\Common7\IDE\ItemTemplates\Web 中，每个模板都安装在以 Web 编程语言命名的子文件夹 \\ 内。

## <a name="project-item-templates"></a>Project项模板
 网站项目项模板用于向网站添加新网页，以响应" **添加现有项"** 命令。 目前支持以下类型的网页：

- 新类

- "新建 HTML"页

- 新建 Web 窗体

- 新建母版页

### <a name="new-class"></a>新类
 此模板创建一个新的源文件，该文件定义一个空类以响应 **"添加新类"** 命令。

- 类。 *extension*

     实现空类的源文件。 代码后发语言确定 *此文件* 的扩展名。

- Class.vstemplate

     创建源文件并确定其内容的模板文件。

### <a name="new-html-page"></a>"新建 HTML"页
 此模板创建一个新网页以响应" **添加新 HTML 页面"** 命令。

- HTMLPage.htm

     网页的起始内容。 此网页通常没有关联的代码后发依赖文件。 若要创建包含关联代码后发文件的智能页面，请改为使用 Web 窗体模板。

- HTMLPage.vstemplate

     创建网页并确定其内容的模板文件。

### <a name="new-webform"></a>新建 WebForm
 此模板创建新的智能网页以响应"添加新 **Web 窗体"** 命令。

 若要创建依赖代码后发源文件，请选择"**将代码放在单独的文件中"。** 否则，将创建一个包含空脚本块且没有用于挂钩依赖 \<% Page %> 文件的指令的网页。

 若要为所选母版页创建内容页，请选择"**选择母版页"。**

- WebForm.aspx

     网页的起始内容。 此网页没有关联的代码后发依赖文件。

- WebForm_cb.aspx

     网页的起始内容。 此网页具有关联的代码后发依赖文件。

- Codebehind。 *extension*

     实现 Webform 类的依赖文件。 代码后发语言确定 *此文件* 的扩展名。

- ContentPage.aspx

     网页作为内容页的起始内容。 此网页没有关联的代码后发依赖文件。

- ContentPage_cb.aspx

     网页作为内容页的起始内容。 此网页具有关联的代码后发依赖文件。

- WebForm.vstemplate

     用于确定新网页的内容及其依赖文件的模板文件（如果有）。

### <a name="new-master-page"></a>新建母版页
 此模板创建新的母版页以响应"添加新 **母版页"** 命令。

 若要创建依赖代码后发源文件，请选择"**将代码放在单独的文件中"。** 否则，将创建一个包含空脚本块且没有用于 \<% Page %> 挂钩依赖文件的指令的网页。

- MasterPage.master

     母版页的起始内容。 此母版页没有关联的代码后发依赖文件。

- MasterPage_cb.master

     母版页的起始内容。 此母版页具有关联的代码后发依赖文件。

- Codebehind。*扩展*

     实现母版页类的依赖文件。 代码后发语言确定 *此文件* 的扩展名。

- MasterPage.vstemplate

     用于确定新母版页的内容及其依赖文件的模板文件（如果有）。

## <a name="see-also"></a>另请参阅
- [网站支持](../../extensibility/internals/web-site-support.md)
