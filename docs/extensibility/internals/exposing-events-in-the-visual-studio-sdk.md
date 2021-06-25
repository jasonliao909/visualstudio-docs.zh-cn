---
title: 公开 Visual Studio SDK |Microsoft Docs
description: 了解公开Visual Studio项的事件的 SDK 方法和注册表项。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- events [Visual Studio], exposing
- automation [Visual Studio SDK], exposing events
ms.assetid: 70bbc258-c221-44f8-b0d7-94087d83b8fe
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 99298329b969df3b9d7dbb46a3f4b9e7d4ed7091
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898323"
---
# <a name="expose-events-in-the-visual-studio-sdk"></a>公开 Visual Studio SDK 中的事件
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 允许使用自动化来源事件。 建议为项目和项目项源事件。

 自动化使用者从 对象或对象中检索事件 <xref:EnvDTE.DTEClass.Events%2A> (<xref:EnvDTE.DTEClass.GetObject%2A> 例如 `GetObject("EventObjectName")` ，) 。 环境通过使用 `IDispatch::Invoke` 或 `DISPATCH_METHOD` `DISPATCH_PROPERTYGET` 标志调用 以返回事件。

 以下过程说明如何返回特定于 VSPackage 的事件。

1. 环境启动。

2. 它从注册表中读取所有 VSPackage的 **Automation、AutomationEvents** 和 **AutomationProperties** 键下的所有值名称，并存储这些名称。

3. 自动化使用者调用 （本示例中为 `DTE.Events.AutomationProjectsEvents` ）或 `DTE.Events.AutomationProjectItemsEvents` 。

4. 环境在表中查找字符串参数并加载相应的 VSPackage。

5. 环境通过使用在调用中传递的名称来调用 方法; <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> 本示例中为 或 `AutomationProjectsEvents` `AutomationProjectItemsEvents` 。

6. VSPackage 创建一个根对象，该对象具有 和 等方法，然后返回指向该对象的 `get_AutomationProjectsEvents` `get_AutomationProjectItemEvents` IDispatch 指针。

7. 环境根据传递到自动化调用中的名称调用适当的方法。

8. `get_`方法创建另一个基于 IDispatch 的事件对象，该对象实现 接口和 接口，并 `IConnectionPointContainer` `IConnectionPoint` `IDispatchpointer` 返回给 对象。

   若要使用自动化公开事件，必须响应并监视添加到注册表的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> 字符串。 在基本项目示例中，字符串为 *BscProjectsEvents* 和 *BscProjectItemsEvents*。

## <a name="registry-entries-from-the-basic-project-sample"></a>基本项目示例中的注册表项
 本部分显示在何处向注册表添加自动化事件值。

 **[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Packages<\\ PkgGUID \> \AutomationEvents]**

 **AutomationProjectEvents** = 返回 `AutomationProjectEvents` 对象。

 **AutomationProjectItemEvents** = 返回 `AutomationProjectItemsEvents` 对象。

|名称|类型|范围|描述|
|----------|----------|-----------|-----------------|
|默认 (@) |REG_SZ|未使用|未使用。 可以将数据字段用于文档。|
|*AutomationProjectsEvents*|REG_SZ|事件对象的名称。|仅密钥名称相关。 可以将数据字段用于文档。<br /><br /> 此示例来自基本项目示例。|
|*AutomationProjectItemEvents*|REG_SZ|事件对象的名称|仅密钥名称相关。 可以将数据字段用于文档。<br /><br /> 此示例来自基本项目示例。|

 当自动化使用者请求任何事件对象时，请创建一个根对象，该对象包含 VSPackage 支持的任何事件的方法。 环境对此对象 `get_` 调用适当的方法。 例如， `DTE.Events.AutomationProjectsEvents` 如果调用 ， `get_AutomationProjectsEvents` 则调用根对象上的 方法。

 ![Visual Studio项目事件](../../extensibility/internals/media/projectevents.gif "ProjectEvents") 事件的自动化模型

 类 `CProjectEventsContainer` 表示 *BscProjectsEvents* 的源对象，并 `CProjectItemsEventsContainer` 表示 *BscProjectItemsEvents 的源对象*。

 在大多数情况下，必须返回每个事件请求的新对象，因为大多数事件对象都使用筛选器对象。 在事件被调用时，请检查此筛选器以验证是否正在调用事件处理程序。

 *AutomationEvents.h* 和 *AutomationEvents.cpp* 包含下表中类的声明和实现。

|类|描述|
|-----------|-----------------|
|`CAutomationEvents`|实现从 对象检索的事件根 `DTE.Events` 对象。|
|`CProjectsEventsContainer` 和 `CProjectItemsEventsContainer`|实现可发射相应事件的事件源对象。|

 下面的代码示例演示如何响应对事件对象的请求。

```cpp
STDMETHODIMP CVsPackage::GetAutomationObject(
    /* [in]  */ LPCOLESTR       pszPropName,
    /* [out] */ IDispatch **    ppIDispatch)
{
    ExpectedPtrRet(ppIDispatch);
    *ppIDispatch = NULL;

    if (_wcsicmp(pszPropName, g_wszAutomationProjects) == 0)
        //Is the requested name our Projects object?
    {
        return GetAutomationProjects(ppIDispatch);
        // Gets our Projects object.
    }
    else if (_wcsicmp(pszPropName, g_wszAutomationProjectsEvents) == 0)
        //Is the requested name our ProjectsEvents object?
    {
        return CAutomationEvents::GetAutomationEvents(ppIDispatch);
          // Gets our ProjectEvents object.
    }
    else if (_wcsicmp(pszPropName, g_wszAutomationProjectItemsEvents) == 0)  //Is the requested name our ProjectsItemsEvents object?
    {
        return CAutomationEvents::GetAutomationEvents(ppIDispatch);
          // Gets our ProjectItemsEvents object.
    }
    return E_INVALIDARG;
}
```

 在以上代码中， 是项目集合 `g_wszAutomationProjects` 的名称 (*FigProjects*) 、 (`g_wszAutomationProjectsEvents` *FigProjectsEvents*) 和 `g_wszAutomationProjectItemsEvents` (*FigProjectItemEvents*) 是项目事件和项目项事件的名称，这些事件来自 VSPackage 实现。

 从同一中心位置（即 对象）检索事件 `DTE.Events` 对象。 这样，所有事件对象都组合在一起，以便最终用户无需浏览整个对象模型来查找特定事件。 这还允许提供特定的 VSPackage 对象，而无需为系统范围事件实现自己的代码。 但是，对于最终用户（必须查找接口的事件）来说，无法立即从检索 `ProjectItem` 该事件对象的地方进行清除。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>
