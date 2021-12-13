---
title: IManagedAddin 接口
description: 实现 IManagedAddin 接口以创建一个组件，该组件VSTO外接程序中加载托管组件。
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- IManagedAddin interface
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 283a8034aa49f5af06eae2c5d8176830b5f83cee
ms.sourcegitcommit: 0f2af2f1a8cf0a481fd8f673accf3aebf2e262c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2021
ms.locfileid: "134713624"
---
# <a name="imanagedaddin-interface"></a>IManagedAddin 接口
  实现 IManagedAddin 接口，以创建一个组件，该组件VSTO外接程序中加载托管组件。此接口已添加到 2007 Microsoft Office 系统中。

## <a name="syntax"></a>语法

```csharp
[
    object,
    uuid(B9CEAB65-331C-4713-8410-DDDAF8EC191A),
    pointer_default(unique),
    oleautomation
]
interface IManagedAddin : IUnknown
{
    HRESULT Load(
        [in] BSTR bstrManifestURL,
        [in] IDispatch *pdispApplication);
    HRESULT Unload();
};
```

## <a name="methods"></a>方法
 下表列出了由 IManagedAddin 接口定义的方法。

|名称|说明|
|----------|-----------------|
|[IManagedAddin::Load](../vsto/imanagedaddin-load.md)|在 Microsoft Office 应用程序加载托管 VSTO 外接程序时调用。|
|[IManagedAddin::Unload](../vsto/imanagedaddin-unload.md)|在 Microsoft Office 应用程序即将卸载 VSTO 托管外接程序时调用。|

## <a name="remarks"></a>备注
 Microsoft Office应用程序（从 2007 Microsoft Office 系统开始）使用 IManagedAddin 接口来帮助加载Office VSTO外接程序。你可以实现 IManagedAddin 接口，为托管的 VSTO 外接程序创建自己的 VSTO 外接程序加载程序和运行时，而不是使用 VSTO 外接程序加载程序 (VSTOLoader.dll *)* 和 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。 有关更多信息，请参见 [Architecture of VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md)。

## <a name="how-managed-add-ins-are-loaded"></a>如何加载托管外接程序
 应用程序启动时，会执行以下步骤：

1. 应用程序通过在以下注册表项下查找项来发现 VSTO 外接程序：

    **HKEY_CURRENT_USER\Software\Microsoft\Office\\ *\<application name>* \Addins\\**

    此注册表项下的每一项都是 VSTO 外接程序的唯一 ID。 通常情况下，这是 VSTO 外接程序程序集的名称。

2. 应用程序在每个 VSTO 外接程序的注册表项下查找 `Manifest` 项。

    托管VSTO外接程序可以将清单的完整路径存储在 `Manifest` **\\ _\<application name>_ \Addins \\ _\<add-in ID>_ 下HKEY_CURRENT_USER\Software\Microsoft\Office条目** 中。 清单是一个文件（通常是 XML 文件），提供用于帮助加载 VSTO 外接程序的信息。

3. 如果应用程序找到 `Manifest` 项，便会尝试加载托管 VSTO 外接程序加载程序组件。 应用程序通过尝试创建实现 IManagedAddin 接口的 COM 对象来实现此目的。

    [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]包括一VSTO外接程序加载程序 *(VSTOLoader.dll) ，* 或者可以通过实现 IManagedAddin 接口创建自己的加载程序组件。

4. 应用程序调用 [IManagedAddin::Load](../vsto/imanagedaddin-load.md) 方法，并传入 `Manifest` 项的值。

5. [IManagedAddin::Load](../vsto/imanagedaddin-load.md) 方法执行加载 VSTO 外接程序所需的任务，例如为正在加载的 VSTO 外接程序配置应用程序域和安全策略。

   有关应用程序用于发现和Microsoft Office托管 VSTO 外接程序的注册表项详细信息，请参阅 VSTO 外接程序 的[注册表项](../vsto/registry-entries-for-vsto-add-ins.md)。

## <a name="guidance-to-implement-imanagedaddin"></a>实现 IManagedAddin 的指南
 如果实现 IManagedAddin，则必须使用以下 CLSID 注册包含实现的 DLL：

 99D651D7-5F7C-470E-8A3B-774D5D9536AC

 Microsoft Office使用此 CLSID 创建实现 IManagedAddin 的 COM 对象。

> [!CAUTION]
> 此 CLSID 也由 中的 *VSTOLoader.dll* 使用 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。 因此，如果使用 IManagedAddin 创建自己的 VSTO 外接程序加载程序和运行时组件，则不能将组件部署到运行依赖于 的 VSTO 外接程序的计算机 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。

## <a name="see-also"></a>另请参阅
- [非托管 API 参考&#40;Office开发Visual Studio&#41;](../vsto/unmanaged-api-reference-office-development-in-visual-studio.md)
