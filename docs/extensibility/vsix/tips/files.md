---
title: 使用文件
description: 使用技巧文件。
ms.date: 12/01/2021
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: pchapman
ms.prod: visual-studio-windows
ms.technology: vs-ide-sdk
ms.custom: cookbook
ms.openlocfilehash: 80d0c7265be8bb833ef07fcde8e0baaa0ec8eb2a
ms.sourcegitcommit: a149b3a034bb555ad217656c0ec8bc1672b1e215
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2021
ms.locfileid: "133515813"
---
# <a name="working-with-files-and-documents-in-visual-studio-extensions"></a>使用扩展插件中的Visual Studio文档

下面是有关使用文件和文档的不同方法的小代码示例的集合。

## <a name="get-active-text-view"></a>获取活动文本视图
获取当前活动文本视图以操作其文本缓冲区文本。

```csharp
DocumentView docView = await VS.Documents.GetActiveDocumentViewAsync();
if (docView?.TextView == null) return; //not a text window
SnapshotPoint position = docView.TextView.Caret.Position.BufferPosition;
docView.TextBuffer?.Insert(position, "some text"); // Inserts text at the caret
```

## <a name="file-icon-associations"></a>文件图标关联
若要将图标与 解决方案资源管理器扩展名关联，请向包 `[ProvideFileIcon()]` 类添加 属性。

```csharp
[ProvideFileIcon(".abc", "KnownMonikers.Reference")]
public sealed class MyPackage : ToolkitPackage
{
    ...
}
```

使用 `KnownMonikers` KnownMonikers Explorer 工具窗口查看集合中的数千个可用图标。 在主菜单中 **的">"Windows"** 其他选项"下找到它。

## <a name="open-file"></a>打开文件
使用 `Microsoft.VisualStudio.Shell.VsShellUtilities` 帮助程序类。

```csharp
string fileName = "c:\\file.txt";
await VS.Document.OpenAsync(fileName);
```

## <a name="open-file-via-project"></a>通过项目打开文件
如果打开的文件是解决方案的一部分，请使用此方法。

```csharp
string fileName = "c:\\file.txt";
await VS.Documents.OpenViaProjectAsync(fileName);
```

## <a name="open-file-in-preview-tab"></a>在"预览"选项卡中打开文件
"预览"选项卡（也称为"临时"选项卡）是在文档右侧打开的临时选项卡。 在"预览"选项卡中打开任何文件，如下所示：

```csharp
string fileName = "c:\\file.txt";
await VS.Documents.OpenInPreviewTabAsync(fileName);
```

## <a name="get-file-name-from-itextbuffer"></a>从 ITextBuffer 获取文件名
使用位于 `buffer.GetFileName()` 命名空间中的扩展 `Microsoft.VisualStudio.Text` 方法。

```csharp
string fileName = buffer.GetFileName();
```

## <a name="solutionitem-from-file"></a>来自文件的 SolutionItem
从 `SolutionItem` 绝对文件路径查找 。

```csharp
string fileName = "c:\\file.txt";
PhysicalFile item = await PhysicalFile.FromFileAsync(fileName);
```
