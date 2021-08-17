---
title: UsedCommand 元素|Microsoft Docs
description: UsedCommand 元素使 VSPackage 能够访问在另一个 .vsct 文件中定义的命令。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- UsedCommands element (VSCT XML schema)
- VSCT XML schema elements, UsedCommands
ms.assetid: 99cd05d3-644a-42ff-b289-8458cd1b20c0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 0333b3a83333eebdb25da83206b9da2a4c9082ad
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122049280"
---
# <a name="usedcommand-element"></a>UsedCommand 元素
使 VSPackage 能够访问在另一个 .vsct 文件中定义的命令。 例如，如果 VSPackage 使用标准 **Copy** 命令（由 shell 定义），可以将该命令添加到菜单或工具栏，而无需 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 重新实现该命令。

## <a name="syntax"></a>语法

```
<UsedCommand guid="guidMyCommandGroup" id="MyCommand" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|GUID|必需。 标识命令的 GUID ID 对的 GUID。|
|id|必需。 标识命令的 GUID ID 对的 ID。|
|条件|可选。 请参阅 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|无||

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[UsedCommands 元素](../extensibility/usedcommands-element.md)|对 UsedCommand 元素和其他 UsedCommands 分组进行分组。|

## <a name="remarks"></a>备注
 通过将命令添加到 `<UsedCommands>` 元素，VSPackage 会通知 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 环境 VSPackage 需要 命令。 应为包要求的任何命令添加一个 元素，该元素可能不会包含在包的所有版本和配置 `<UsedCommand>` Visual Studio。 例如，如果包调用特定于 Visual C++ 的命令，则除非为命令包含 元素，否则该命令将不适用于 Visual Web 开发人员 `<UsedCommand>` 的用户。

## <a name="example"></a>示例

```
<UsedCommands>
  <UsedCommand guid="guidVSStd97" id="cmdidCut"/>
  <UsedCommand guid="guidVSStd97" id="cmdidCopy"/>
  <UsedCommand guid="guidVSStd97" id="cmdidPaste"/>
</UsedCommands>
```

## <a name="see-also"></a>请参阅
- [UsedCommands 元素](../extensibility/usedcommands-element.md)
- [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
