---
title: VSTextBuffer 对象|Microsoft Docs
description: VSTextBuffer 对象表示 Unicode 文本流，通常与文件关联。 本文列出了 VSTextBuffer 的接口。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VSTextBuffer
helpviewer_keywords:
- VSTextBuffer object, reference
- views [Visual Studio SDK], VSTextBuffer object
ms.assetid: c5f94b45-7249-4e1f-a53d-1d2a1c61e0ef
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 97af9ff3cf30954212de6918e83aaa52ef4e3852
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122028366"
---
# <a name="vstextbuffer-object"></a>VSTextBuffer 对象
文本缓冲区对象表示 Unicode 文本流，该流通常与文件关联。 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>对象可以在核心编辑器的上下文之外使用，就像在向导中一样。

 下表显示了 的接口 `VSTextBuffer` 。

|方法|说明|
|------------|-----------------|
|[IOleCommandTarget](/windows/desktop/api/docobj/nn-docobj-iolecommandtarget)|标准 OLE 接口。 用于在缓冲区中撤消/重做处理。|
|[IPersistFile](/windows/desktop/api/objidl/nn-objidl-ipersistfile)|标准 OLE 接口。|
|[IPersistStream](/windows/desktop/api/objidl/nn-objidl-ipersiststream)|标准 OLE 接口。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompoundAction>|允许创建复合 (操作，即分组到单个撤消/重做单元中的) 。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>|启用由文本缓冲区管理的文档数据的持久性。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>|提供基本服务;由许多客户端使用。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextFind>|用于搜索缓冲区。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>|使用二维坐标提供读取和写入功能。 继承自 `IVsTextBuffer`。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream>|使用一维坐标提供读写功能。 继承自 `IVsTextBuffer`。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextScanner>|提供对缓冲区中文本的快速、面向流的顺序访问。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData>|提供对属性的泛型集合的访问。 最重要的属性是缓冲区的名称或名字对象。 可以通过创建 GUID 并使用该 GUID 作为键，将自己的随机数据存储在此接口的缓冲区中。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer>|支持事件的连接点。|

## <a name="remarks"></a>备注
 `VSTextBuffer`通常通过上的 调用 `QueryInterface` 找到 `IVsTextBuffer` 。 有关详细信息，请参阅文本 [缓冲区](/previous-versions/visualstudio/visual-studio-2015/extensibility/accessing-the-text-buffer-by-using-the-legacy-api?preserve-view=true&view=vs-2015)。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>
- <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>
- [图形编辑](https://www.microsoft.com/download/details.aspx?id=55984)