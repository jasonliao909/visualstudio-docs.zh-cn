---
title: '&lt;file&gt; 元素（ClickOnce 应用程序）| Microsoft Docs'
description: file 元素标识应用程序下载和使用的所有非程序集文件。 file 元素是可选的。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://www.w3.org/2000/09/xmldsig#Transform
- urn:schemas-microsoft-com:asm.v2#file
- http://www.w3.org/2000/09/xmldsig#DigestValue
- http://www.w3.org/2000/09/xmldsig#DigestMethod
- http://www.w3.org/2000/09/xmldsig#Transforms
- urn:schemas-microsoft-com:asm.v2#hash
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <file> element [ClickOnce application manifest]
- manifests [ClickOnce], file element
ms.assetid: 56e3490c-eed5-4841-b1bf-eefe778b6ac9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 68733629b26b4640e63919aaa4f9d07d0c70f972
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665630"
---
# <a name="ltfilegt-element-clickonce-application"></a>&lt;file&gt; 元素（ClickOnce 应用程序）
标识应用程序下载和使用的所有非程序集文件。

## <a name="syntax"></a>语法

```xml
<file
    name
    size
    group
    optional
    writeableType
>
    <typelib
        tlbid
        version
        helpdir
        resourceid
        flags
    />
    <comClass
        clsid
        description
        threadingModel
        tlbid
        progid
        miscStatus
        miscStatusIcon
        miscStatusContent
        miscStatusDocPrint
        miscStatusThumbnail
    />
    <comInterfaceExternalProxyStub
        iid
        baseInterface
        numMethods
        name
        tlbid
        proxyStubClass32
    />
    <comInterfaceProxyStub
        iid
        baseInterface
        numMethods
        name
        tlbid
        proxyStubClass32
    />
    <windowClass
        versioned
    />
</file>
```

## <a name="elements-and-attributes"></a>元素和属性
 `file` 元素是可选的。 元素具有以下属性。

|属性|说明|
|---------------|-----------------|
|`name`|必需。 标识文件的名称。|
|`size`|必需。 指定文件的大小（以字节为单位）。|
|`group`|如果指定了 `optional` 属性或将其设置为 `false`，则为可选；如果将 `optional` 设为 `true`，则是必需的。 此文件所属的组的名称。 该名称可以是开发人员选择的任何 Unicode 字符串值，随 <xref:System.Deployment.Application.ApplicationDeployment> 类一起用于按需下载文件。|
|`optional`|可选。 指定该文件是否必须在应用程序首次运行时下载，或者该文件是否应仅驻留在服务器上，直到应用程序按需请求它为止。 如果为 `false` 或未定义，则在应用程序首次运行或安装时，系统将下载该文件。 如果为 `true`，则必须指定 `group`，应用程序清单才能有效。 如果将 `writeableType` 的值指定为 `applicationData`，则 `optional` 不可能为 ture。|
|`writeableType`|可选。 指定此文件是数据文件。 当前，唯一有效的值是：`applicationData`。|

## <a name="typelib"></a>typelib
 `typelib` 元素是 file 元素的可选子元素。 此元素描述属于 COM 组件的类型库。 元素具有以下属性。

|属性|说明|
|---------------|-----------------|
|`tlbid`|必需。 分配给类型库的 GUID。|
|`version`|必需。 类型库的版本号。|
|`helpdir`|必需。 包含组件的帮助文件的目录。 长度可能为零。|
|`resourceid`|可选。 区域设置标识符 (LCID) 的十六进制字符串表示形式。 它是一到四个十六进制数字，不带 0x 前缀和前导零。 LCID 可能具有非特定子语言标识符。|
|`flags`|可选。 此类型库的类型库标志的字符串表示形式。 具体而言，它应为以下值之一：“RESTRICTED”、“CONTROL”、“HIDDEN”和“HASDISKIMAGE”。|

## <a name="comclass"></a>comClass
 `comClass` 元素是 `file` 元素的可选子元素，但如果 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序包含其打算使用免注册 COM 部署的 COM 组件，则此元素是必需的。 元素具有以下属性。

|属性|说明|
|---------------|-----------------|
|`clsid`|必需。 表示为 GUID 的 COM 组件的类 ID。|
|`description`|可选。 类名。|
|`threadingModel`|可选。 进程内 COM 类使用的线程模型。 如果此属性为 null，则不使用线程模型。 组件在客户端的主线程上进行创建，而来自其他线程的调用被封送到此线程。 以下列表显示了有效值：<br /><br /> `Apartment`、`Free`、`Both` 和 `Neutral`。|
|`tlbid`|可选。 此 COM 组件的类型库的 GUID。|
|`progid`|可选。 与 COM 组件关联的版本相关编程标识符。 `ProgID` 的格式为 `<vendor>.<component>.<version>`。|
|`miscStatus`|可选。 程序集清单中的重复项 - 由 `MiscStatus` 注册表项提供的信息。 如果找不到 `miscStatusIcon`、`miscStatusContent`、`miscStatusDocprint` 或 `miscStatusThumbnail` 属性的值，则将 `miscStatus` 中列出的相应默认值用作缺失属性的值。 该值可以是一个以逗号分隔的列表，其中包括下表中的属性值。 如果 COM 类是需要 `MiscStatus` 注册表项值的 OCX 类，则可使用此属性。|
|`miscStatusIcon`|可选。 程序集清单中的重复项 - 由 DVASPECT_ICON 提供的信息。 它可以提供对象的图标。 该值可以是一个以逗号分隔的列表，其中包括下表中的属性值。 如果 COM 类是需要 `Miscstatus` 注册表项值的 OCX 类，则可使用此属性。|
|`miscStatusContent`|可选。 程序集清单中的重复项 - 由 DVASPECT_CONTENT 提供的信息。 它可以提供可通过屏幕或打印机显示的复合文档。 该值可以是一个以逗号分隔的列表，其中包括下表中的属性值。 如果 COM 类是需要 `MiscStatus` 注册表项值的 OCX 类，则可使用此属性。|
|`miscStatusDocPrint`|可选。 程序集清单中的重复项 - 由 DVASPECT_DOCPRINT 提供的信息。 它可以提供可在屏幕上显示的对象表示形式，与在打印机上打印出的效果相同。 该值可以是一个以逗号分隔的列表，其中包括下表中的属性值。 如果 COM 类是需要 `MiscStatus` 注册表项值的 OCX 类，则可使用此属性。|
|`miscStatusThumbnail`|可选。 程序集清单中的重复项 - 由 DVASPECT_THUMBNAIL 提供的信息。 它可以提供可在浏览工具中显示的对象的缩略图。 该值可以是一个以逗号分隔的列表，其中包括下表中的属性值。 如果 COM 类是需要 `MiscStatus` 注册表项值的 OCX 类，则可使用此属性。|

## <a name="cominterfaceexternalproxystub"></a>comInterfaceExternalProxyStub
 `comInterfaceExternalProxyStub` 元素是 `file` 元素的可选子元素，但如果 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序包含其打算使用免注册 COM 部署的 COM 组件，则此元素可能就是必需的。 该元素包含以下属性。

|属性|说明|
|---------------|-----------------|
|`iid`|必需。 由此代理提供服务的接口 ID (IID)。 IID 的两边必须有大括号。|
|`baseInterface`|可选。 接口的 IID，`iid` 引用的接口是从该接口派生的。|
|`numMethods`|可选。 接口实现的方法数。|
|`name`|可选。 将在代码中显示的接口的名称。|
|`tlbid`|可选。 类型库，其中包含对 `iid` 属性指定的接口的说明。|
|`proxyStubClass32`|可选。 将 IID 映射到 32 位代理 DLL 中的 CLSID。|

## <a name="cominterfaceproxystub"></a>comInterfaceProxyStub
 `comInterfaceProxyStub` 元素是 `file` 元素的可选子元素，但如果 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序包含其打算使用免注册 COM 部署的 COM 组件，则此元素可能就是必需的。 该元素包含以下属性。

|属性|说明|
|---------------|-----------------|
|`iid`|必需。 由此代理提供服务的接口 ID (IID)。 IID 的两边必须有大括号。|
|`baseInterface`|可选。 接口的 IID，`iid` 引用的接口是从该接口派生的。|
|`numMethods`|可选。 接口实现的方法数。|
|`Name`|可选。 将在代码中显示的接口的名称。|
|`Tlbid`|可选。 类型库，其中包含对 `iid` 属性指定的接口的说明。|
|`proxyStubClass32`|可选。 将 IID 映射到 32 位代理 DLL 中的 CLSID。|
|`threadingModel`|可选。 可选。 进程内 COM 类使用的线程模型。 如果此属性为 null，则不使用线程模型。 组件在客户端的主线程上进行创建，而来自其他线程的调用被封送到此线程。 以下列表显示了有效值：<br /><br /> `Apartment`、`Free`、`Both` 和 `Neutral`。|

## <a name="windowclass"></a>windowClass
 `windowClass` 元素是 `file` 元素的可选子元素，但如果 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序包含其打算使用免注册 COM 部署的 COM 组件，则此元素可能就是必需的。 该元素指的是由 COM 组件定义的窗口类，该类必须有一个应用于它的版本。 该元素包含以下属性。

|属性|说明|
|---------------|-----------------|
|`versioned`|可选。 控制在注册中使用的内部窗口类名称是否包括含有窗口类的程序集的版本。 此属性的值可为 `yes` 或 `no`。 默认值为 `yes`。 仅当同一个窗口类由并行组件和等效的非并行组件定义，并且你想把它们当作相同的窗口类时，才应使用 `no` 值。 请注意，关于窗口类注册的常用规则适用的条件是，只有第一个注册窗口类的组件才能够注册它，因为它没有一个应用于它的版本。|

## <a name="hash"></a>hash
 `hash` 元素是 `file` 元素的可选子元素。 `hash` 元素没有属性。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使用应用程序中所有文件的算法哈希作为安全检查，以确保在部署后没有任何文件发生更改。 如果不包含 `hash` 元素，则不会执行此检查。 因此，建议不要省略 `hash` 元素。

 如果清单包含的文件未进行哈希处理，则无法对该清单进行数字签名，因为用户无法验证未经过哈希处理的文件的内容。

## <a name="dsigtransforms"></a>dsig:Transforms
 `dsig:Transforms` 元素是 `hash` 元素的必需子元素。 `dsig:Transforms` 元素没有属性。

## <a name="dsigtransform"></a>dsig:Transform
 `dsig:Transform` 元素是 `dsig:Transforms` 元素的必需子元素。 `dsig:Transform` 元素具有以下属性。

| 属性 | 说明 |
|-------------| - |
| `Algorithm` | 用于计算此文件摘要的算法。 目前 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使用的唯一值为 `urn:schemas-microsoft-com:HashTransforms.Identity`。 |

## <a name="dsigdigestmethod"></a>dsig:DigestMethod
 `dsig:DigestMethod` 元素是 `hash` 元素的必需子元素。 `dsig:DigestMethod` 元素具有以下属性。

| 属性 | 说明 |
|-------------| - |
| `Algorithm` | 用于计算此文件摘要的算法。 目前 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使用的唯一值为 `http://www.w3.org/2000/09/xmldsig#sha1`。 |

## <a name="dsigdigestvalue"></a>dsig:DigestValue
 `dsig:DigestValue` 元素是 `hash` 元素的必需子元素。 `dsig:DigestValue` 元素没有属性。 它的文本值为计算指定文件所得到的哈希。

## <a name="remarks"></a>备注
 此元素标识构成应用程序的所有非程序集文件，尤其是文件验证的哈希值。 此元素还可包括与文件关联的组件对象模型 (COM) 隔离数据。 如果文件发生更改，则还必须更新应用程序清单文件以反映这些更改。

## <a name="example"></a>示例
 下面的代码示例演示使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署的应用程序的应用程序清单中的 `file` 元素。

```xml
<file name="Icon.ico" size="9216">
  <hash>
    <dsig:Transforms>
      <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />
    </dsig:Transforms>
    <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
    <dsig:DigestValue>lVoj+Rh6RQ/HPNLOdayQah5McrI=</dsig:DigestValue>
  </hash>
</file>
```

## <a name="see-also"></a>另请参阅
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)