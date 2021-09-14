---
title: 将数据持久保存MSBuild Project文件|Microsoft Docs
description: 了解如何将数据保留到项目文件中，并使用 IPersistXMLFragment 跨项目子类型聚合级别维护项目文件的数据。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project files, persisting data in
ms.assetid: 6a920cb7-453d-4ffd-af1c-6f3084bd03f7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: a5147eed5026f010811905fa693baccb4352010e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664337"
---
# <a name="persisting-data-in-the-msbuild-project-file"></a>保留 MSBuild 项目文件中的数据
项目子类型可能需要将特定于子类型的数据保留到项目文件中，供以后使用。 项目子类型使用项目文件持久性来满足以下要求：

1. 保留生成项目时所使用的数据。  (有关此Microsoft 生成引擎，[请参阅MSBuild](../../msbuild/msbuild.md).) 生成相关信息：

    1. 与配置无关的数据。 也就是说，存储在具有空白或MSBuild的元素中存储的数据。

    2. 依赖于配置的数据。 也就是说，存储在特定MSBuild配置的条件的元素中存储的数据。 例如：

        ```
        <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">
        ```

2. 保留与生成不相关的数据。 此数据可以自由格式的 XML 表示，该 XML 未根据 XML 架构进行验证。

    1. 与配置无关的数据。

    2. 依赖于配置的数据。

## <a name="persisting-build-related-information"></a>保留Build-Related信息
 对生成项目有用的数据的持久性通过MSBuild。 系统MSBuild维护生成相关信息的主表。 Project子类型负责访问此数据以获取和设置属性值。 Project子类型还可以通过添加要持久化的其他属性和删除属性来增强与生成相关的数据表，以便它们不会持久化。

 若要修改MSBuild，项目子类型负责通过 从MSBuild检索属性对象 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> 。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> 是在核心项目系统上实现的接口，并且聚合项目子类型通过运行 来查询它 `QueryInterface` 。

 以下过程概述了使用 删除属性的步骤 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> 。

#### <a name="to-remove-a-property-from-an-msbuild-project-file"></a>从项目文件中删除MSBuild属性

1. 对 `QueryInterface` 项目 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> 子类型调用 。

2. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.RemoveProperty%2A> `pszPropName` ，将 设置为要删除的属性。

### <a name="persisting-non-build-related-information"></a>保留非生成相关信息
 项目文件中与生成不重要的数据的持久性通过 进行处理 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> 。

 可以在主 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> 对象和 `project subtype aggregator` /或 `project subtype project configuration` 对象上实现 。

 以下几点概述了有关非生成相关信息持久性的主要概念。

- 基本项目对主项目子类型 (（即最外层项目子类型) 聚合器对象）调用 以加载和保存与配置无关的数据，并调用项目子类型项目配置对象以加载或保存与配置相关的数据。

- 基础项目针对每个级别的项目子类型聚合多次调用 方法， <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> 并传递每个级别的 GUID。

- 基础项目传递或接收专用于特定项目子类型的 XML 片段，并使用此机制作为在聚合级别之间持久保存状态的方法。

- 基础项目调用在 GUID 中传递的最外层 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> 项目子类型的实现。 如果 GUID 属于最外层的项目子类型，则它处理调用本身;否则，它将调用委托给内部项目子类型等，直到找到 GUID 所对应的项目子类型。

- 项目子类型还可以在将调用委托给内部项目子类型之前或之后修改 XML 片段。 以下示例显示了项目文件的摘录，其中包含特定于项目子类型的属性的文件的名称传递给该项目子类型。

    ```
    <ProjectExtensions>
        <VisualStudio>
          <FlavorProperties GUID="{<FlavorGUID>}">
            <FlavorProject TestFileFolder="TestFile" />
          </FlavorProperties>
        </VisualStudio>
      </ProjectExtensions>
    ```

## <a name="see-also"></a>另请参阅
- [项目子类型](../../extensibility/internals/project-subtypes.md)
