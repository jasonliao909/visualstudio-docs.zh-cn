---
title: 使用项目
description: 使用技巧项目。
ms.date: 12/01/2021
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: pchapman
ms.prod: visual-studio-windows
ms.technology: vs-ide-sdk
ms.custom: cookbook
ms.openlocfilehash: ba6a40469258f733cbf4f847de0d3a39bcfdde27
ms.sourcegitcommit: a149b3a034bb555ad217656c0ec8bc1672b1e215
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2021
ms.locfileid: "133515845"
---
# <a name="working-with-projects-in-visual-studio-extensions"></a>在扩展中Visual Studio项目

下面是有关使用项目的不同方法的小代码示例的集合。

## <a name="get-project-from-contained-file"></a>从包含的文件获取项目
这是如果项目的文件，则如何从一个获取项目。

```csharp
 string fileName = "c:\\file\\in\\project.txt";
 PhysicalFile item = await PhysicalFile.FromFileAsync(fileName);
 Project project = item.ContainingProject;
```

## <a name="add-files-to-project"></a>将文件添加到项目
下面将了解如何将文件从磁盘添加到项目。

```csharp
Project project = await VS.Solutions.GetActiveProjectAsync();

var file1 = "c:\\file\\in\\project\\1.txt";
var file2 = "c:\\file\\in\\project\\2.txt";
var file3 = "c:\\file\\in\\project\\3.txt";

await project.AddExistingFilesAsync(file1, file2, file3);
```

## <a name="find-type-of-project"></a>查找项目类型
了解要处理的项目类型。

```csharp
bool isCsharp = await project.IsKindAsync(ProjectTypes.CSHARP);
```
