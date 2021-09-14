---
title: 网站支持模板 |Microsoft Docs
description: 了解网站支持模板。 Visual Studio 网站项目和项模板提供可重用且可自定义的网站项目和项存根。
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
ms.openlocfilehash: d6aea0846a8811956bb022975c8efd0fa80a1044
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600693"
---
# <a name="web-site-support-templates"></a>网站支持模板
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 网站项目和项模板提供可重用且可自定义的网站项目和项存根，可通过无需从头开始创建新的网站项目和项来加速开发过程。 有关模板的详细信息 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，请参阅[创建 Project 和项模板](../../ide/creating-project-and-item-templates.md)。

## <a name="project-template-folder"></a>Project模板文件夹
 web 项目模板通常安装在 [*Visual Studio 安装路径*] \Common7\IDE\ProjectTemplates\Web 上 \\ ，每个模板都在以 Web 编程语言命名的子文件夹中。

## <a name="project-file"></a>项目文件
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成开发环境 (IDE) 需要项目文件扩展名才能将模板映射到正确的项目类型。 由于 Web 项目没有项目文件，因此会注册虚拟项目文件 .webproj，以将模板映射到项目类型。

 （可选）可以将语言名称字符串添加到模板，使 Web 项目系统可以在基于模板的项的 " **添加新项** " 对话框中设置语言默认值。 字符串必须是文件的第一行。 它必须与 IntelliSense 引擎注册中 AddItemLanguageName 下注册的名称匹配，并且必须在 (.vstemplate) Project 子类型下注册的名称。 有关详细信息，请参阅网站 [支持属性](../../extensibility/internals/web-site-support-attributes.md)。

 如果不存在该字符串，则 Web 项目系统将尝试根据 Project 模板添加到 Web 项目的页的语言属性和文件扩展名来确定默认语言。

## <a name="project-templates"></a>项目模板
 网站项目模板用于生成新网站，以响应 "**文件**" 菜单上的 "**新建网站**" 命令。 当前支持三个网站项目类型：

- 空网站项目

- 网站项目

- Web 服务项目

### <a name="empty-web-site-projects"></a>空网站项目
 这些文件会创建一个新的空网站来响应 **空** 的网站命令，该命令在选择 "**文件**" "新建网站" 后提供  >  ：

- EmptyWeb

     指导创建新的空网站的模板文件。

- EmptyWeb. .webproj

     此文件是项目模板系统的项目。 它满足 EmptyWeb 文件中的项目文件引用。

### <a name="web-site-projects"></a>网站项目
 这些文件会创建一个新网站来响应 **ASP.NET** 网站命令，该命令在选择 "**文件**" "新建网站" 后提供  >  ：

- Default.aspx

     新网站的默认主页。 Language 特性指定了代码隐藏语言，而 CodeFile 特性指定了包含与此页关联的代码隐藏代码的依赖文件。

- Default.aspx。*扩展*

     包含默认主页的代码隐藏代码的依赖文件。 代码隐藏语言确定此文件的 *扩展名* 。

- web.config

     根 web.site 配置文件。

- WebApplication

     确定网站解决方案内容并强制创建 App_Data 文件夹的模板文件。

- WebApplication. .webproj

     此文件是项目模板系统的项目。 它满足 WebApplication 文件中的项目文件引用。

### <a name="web-service-projects"></a>Web 服务项目
 在选择 "**文件**" "新建网站" 后，这些文件会创建一个新网站来响应 **ASP.NET Web 服务** 命令，该命令可用  >  ：

- 服务 .asmx

     新 Web 服务的 HTML 页。 Language 特性指定了代码隐藏语言，而代码隐藏特性指定了包含与此服务关联的代码隐藏代码的依赖文件。

- Service。 *extension*

     实现服务类的依赖文件。 代码隐藏语言确定此文件的 *扩展名* 。

- web.config

- 根 web.site 配置文件。

- WebService

     确定网站解决方案内容并强制创建 App_Data 和 App_Code 文件夹的模板文件。 服务。*扩展* 文件将复制到 App_Code 文件夹。

- WebService. .webproj

     此文件是项目模板系统的项目。 它满足 WebService 文件中的项目文件引用。

## <a name="project-item-template-folder"></a>Project项模板文件夹
 Web 项目-项模板通常安装在 [*Visual Studio 安装路径*] \Common7\IDE\ItemTemplates\Web 中 \\ ，每个模板都在以其 Web 编程语言命名的子文件夹中。

## <a name="project-item-templates"></a>Project项模板
 网站项目项模板用于向网站添加新网页，以响应 " **添加现有项** " 命令。 当前支持这些类型的网页：

- 新类

- 新 HTML 页面

- 新建 Web 窗体

- 新母版页

### <a name="new-class"></a>新类
 此模板创建一个新的源文件，该文件定义一个空类以响应 " **添加新类** " 命令。

- 类。 *extension*

     实现空类的源文件。 代码隐藏语言确定此文件的 *扩展名* 。

- 类 .vstemplate

     用于创建源文件并确定其内容的模板文件。

### <a name="new-html-page"></a>新 HTML 页面
 此模板创建一个新网页，以响应 " **添加新的 HTML 页** " 命令。

- HTMLPage.htm

     网页的起始内容。 此网页通常没有关联的代码隐藏依赖文件。 若要创建具有关联的代码隐藏文件的智能页面，请改用 Web 窗体模板。

- Html 页

     用于创建网页并确定其内容的模板文件。

### <a name="new-webform"></a>新 WebForm
 此模板创建一个新的智能网页，以响应 " **添加新 Web 窗体** " 命令。

 若要创建依赖的代码隐藏源文件，请选择 " **将代码放在单独的文件中**"。 否则，将创建一个具有空脚本块且没有 \<% Page %> 用于挂钩依赖文件的指令的单个网页。

 若要为所选母版页创建内容页，请选择 " **选择母版页**"。

- WebForm .aspx

     网页的起始内容。 此网页没有关联的代码隐藏依赖文件。

- WebForm_cb .aspx

     网页的起始内容。 此网页包含关联的代码隐藏依赖文件。

- Codebehind. *extension*

     实现 webform 类的依赖文件。 代码隐藏语言确定此文件的 *扩展名* 。

- ContentPage .aspx

     作为内容页的网页的起始内容。 此网页没有关联的代码隐藏依赖文件。

- ContentPage_cb .aspx

     作为内容页的网页的起始内容。 此网页包含关联的代码隐藏依赖文件。

- WebForm

     确定新网页的内容及其依赖文件（如果有）的模板文件。

### <a name="new-master-page"></a>新母版页
 此模板创建一个新的母版页，以响应 " **添加新的母版页** " 命令。

 若要创建依赖的代码隐藏源文件，请选择 " **将代码放在单独的文件中**"。 否则，将创建一个具有空脚本块且没有 \<% Page %> 用于挂钩依赖文件的指令的单个网页。

- MasterPage

     母版页的起始内容。 此母版页没有关联的代码隐藏依赖文件。

- MasterPage_cb master

     母版页的起始内容。 此母版页具有关联的代码隐藏依赖文件。

- Codebehind.*扩展*

     实现母版页类的依赖文件。 代码隐藏语言确定此文件的 *扩展名* 。

- MasterPage

     确定新母版页的内容及其依赖文件（如果有）的模板文件。

## <a name="see-also"></a>另请参阅
- [网站支持](../../extensibility/internals/web-site-support.md)
