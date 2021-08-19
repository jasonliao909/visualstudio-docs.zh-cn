---
title: 公开Project对象|Microsoft Docs
description: 了解如何通过提供允许使用自动化接口访问项目的自动化对象，在 Visual Studio 中公开自定义项目类型的对象。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- project objects, exposing
- extensibility, project objects
ms.assetid: 5bb24967-434a-4ef4-87a0-2f3250c9e22d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6fd2a7f85569bcaa63b4efef80deb564ee1e2ecb
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122094823"
---
# <a name="expose-project-objects"></a>公开项目对象

自定义项目类型可以提供自动化对象，以允许使用自动化接口访问项目。 每个项目类型应提供从 访问的标准自动化对象，该对象包含 IDE 中打开的所有 <xref:EnvDTE.Project> <xref:EnvDTE.Solution> 项目的集合。 项目中的每个项预期由使用 访问 <xref:EnvDTE.ProjectItem> 的对象公开 `Project.ProjectItems` 。 除了这些标准自动化对象，项目还可以选择提供特定于项目的自动化对象。

你可以创建自定义根级自动化对象，这些对象可以使用 或 从根 DTE 对象访问后期 `DTE.<customObjectName>` 绑定 `DTE.GetObject("<customObjectName>")` 。 例如，Visual C++创建一个 C++ 项目特定的项目集合，名为 *VCProjects，* 可以使用 或 `DTE.VCProjects` 访问 `DTE.GetObject("VCProjects")` 它。 还可以创建一个 ，它对于项目类型是唯一的，一个 ，可查询其派生最大的对象，以及一个 ，它 `Project.Object` `Project.CodeModel` 公开 和 `ProjectItem` `ProjectItem.Object` `ProjectItem.FileCodeModel` 。

这是项目的常见约定，用于公开特定于项目的自定义项目集合。 例如， [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 创建一个 C++ 特定的项目集合，然后可以使用 或 访问 `DTE.VCProjects` 该集合 `DTE.GetObject("VCProjects")` 。 还可以创建一个 ，它对于项目类型是唯一的、一个 ，可针对其派生最大的对象进行查询、一个公开 的 `Project.Object` `Project.CodeModel` 和 `ProjectItem` `ProjectItem.Object` `ProjectItem.FileCodeModel` 。

## <a name="to-contribute-a-vspackage-specific-object-for-a-project"></a>为项目提供特定于 VSPackage 的对象

1. 将相应的密钥添加到 VSPackage 的 *.pkgdef* 文件。

     例如，下面是 C++ 语言项目的 *.pkgdef* 设置：

    ```
    [$RootKey$\Packages\{F1C25864-3097-11D2-A5C5-00C04F7968B4}\Automation]
    "VCProjects"=""
    [$RootKey$\Packages\{F1C25864-3097-11D2-A5C5-00C04F7968B4}\AutomationEvents]
    "VCProjectEngineEventsObject"=""
    ```

2. 在 方法中 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> 实现代码，如以下示例所示。

    ```cpp
    STDMETHODIMP CVsPackage::GetAutomationObject(
    /* [in]  */ LPCOLESTR       pszPropName,
    /* [out] */ IDispatch **    ppIDispatch)
    {
    ExpectedPtrRet(pszPropName);
    ExpectedPtrRet(ppIDispatch);
    *ppIDispatch = NULL;

        if (m_fZombie)
            return E_UNEXPECTED;

        if (_wcsicmp(pszPropName, g_wszAutomationProjects) == 0)
        {
            return GetAutomationProjects(ppIDispatch);
        }
        else if (_wcsicmp(pszPropName, g_wszAutomationProjectsEvents) == 0)
        {
            return CAutomationEvents::GetAutomationEvents(ppIDispatch);
        }
        else if (_wcsicmp(pszPropName, g_wszAutomationProjectItemsEvents) == 0)
        {
            return CAutomationEvents::GetAutomationEvents(ppIDispatch);
        }
        return E_INVALIDARG;
    }
    ```

     在代码中， `g_wszAutomationProjects` 是项目集合的名称。 方法创建一个 实现 接口的对象，并返回指向调用对象的指针 `GetAutomationProjects` `Projects` `IDispatch` ，如下面的代码示例所示。

    ```cpp
    HRESULT CVsPackage::GetAutomationProjects(/* [out] */ IDispatch ** ppIDispatch)
    {
        ExpectedPtrRet(ppIDispatch);
        *ppIDispatch = NULL;

        if (!m_srpAutomationProjects)
        {
            HRESULT hr = CACProjects::CreateInstance(&m_srpAutomationProjects);
            IfFailRet(hr);
            ExpectedExprRet(m_srpAutomationProjects != NULL);
        }
        return m_srpAutomationProjects.CopyTo(ppIDispatch);
    }
    ```

     为自动化对象选择唯一名称。 名称冲突不可预测，如果多个项目类型使用相同的名称，则冲突会导致任意引发冲突的对象名称。 应在自动化对象的名称中包括公司名称或产品名称的某个独特方面。

     自定义 `Projects` 集合对象是项目自动化模型其余部分的便利入口点。 还可以从项目集合访问项目 <xref:EnvDTE.Solution> 对象。 创建为使用者提供集合对象的适当代码和注册表项后，实现必须为项目模型提供 `Projects` 剩余的标准对象。 有关详细信息，请参阅 Project[建模](../../extensibility/internals/project-modeling.md)。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>
