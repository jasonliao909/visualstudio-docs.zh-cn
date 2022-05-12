---
title: 使用文件 IO 提高应用的性能
description: 使用文件 IO 工具可在分析会话期间查看文件读取和写入信息。
ms.custom: SEO-VS-2020
ms.date: 04/26/2022
ms.topic: how-to
ms.assetid: 7501a20d-04a1-480f-a69c-201524aa709d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: '>= vs-2022'
ms.workload:
- multiple
ms.openlocfilehash: afd08cfaf77f6610da1951f60fc3987a04bcf264
ms.sourcegitcommit: ffde8e1b7a5f0b14026b82aef2ce0c8fc19fb7b0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2022
ms.locfileid: "144845846"
---
# <a name="view-file-read-and-write-information-to-help-improve-performance"></a>查看文件读取和写入信息，以帮助提高性能

文件 IO 工具通过在分析会话期间读取文件来提供文件读取和写入信息。 这些文件在经过收集之后在报告中自动生成，并按其目标进程排列，同时显示聚合信息。 

## <a name="setup"></a>安装

1. 在 Visual Studio 中选择“Alt+F2”打开性能探查器。

1. 选中“文件 IO”复选框。

   ![显示已选择文件 IO 工具的屏幕截图。](./media/vs-2022/file-io-launch.png "已选择文件 IO 工具")

   > [!NOTE]
   > 如果无法选择该工具，请清除所有其他工具的复选框，因为某些工具需要单独运行。 若要详细了解如何一起运行工具，请查看[显示如何通过命令行使用分析工具的屏幕截图](../profiling/using-the-profiling-tools-from-the-command-line.md)。
   >
   > 如果该工具仍不可用，请检查项目是否满足前面的要求。 请确保项目处于“发布”模式，以便捕获最准确的数据。

1. 选择“开始”按钮以运行该工具。

1. 出现提示时选择“是”。

1. 在此工具开始运行后，在应用中完成要探查的方案。 然后，选择“停止收集”或关闭应用，以查看数据。

![显示已停止文件 IO 工具的屏幕截图。](./media/vs-2022/file-io-after.png "已停止文件 IO 工具")

## <a name="analyze-the-file-io-report"></a>分析文件 IO 报告
选择“文件读取”以在单页上查看所有文件读取内容，选择“文件读取”以查看写入内容 。 如果右键单击其中一行，则可以转到代码中的源。 如果多次读取了某个聚合行，请将其展开，以查看针对该文件的单个读取操作及其频率（如果已多次读取）。

![显示已选择“文件读取”的屏幕截图。](./media/vs-2022/file-io-reads.png "已选择文件读取")

单个文件读取的重复因子是从文件读取的字节数除以文件大小的结果。 对于聚合读取，重复因子是从文件读取的总字节数除以所有读取操作中文件的平均大小的结果。 相同的逻辑适用于文件写入。 重复因子显示从文件中读取或写入的内容是否超过所需的内容。 如果重复因子为 3x，这意味着从文件中读取的字节数是文件本身大小的 3 倍，这可能表明你正在读取和处理的内容比你认为的更多。 这可以表明缓存文件读取和处理结果的位置可以提高应用的性能。

![显示已选择“重复因子”的屏幕截图。](./media/vs-2022/file-io-duplication-factor.png "已选择重复因子")

双击任何文件都会使其加载到回溯视图中。 此视图可加载读取或写入的任何文件，使你能够查看代码中发生读取或写入的位置。

![显示已选择回溯视图的屏幕截图。](./media/vs-2022/file-io-backtraces.png "已选择回溯视图")

 > [!NOTE]
 > 目前仅支持数据读取、数据写入和计数。
 > 
 > [!NOTE] 
 > 缓存读取的文件不是正确的解决方法，因为 OS 已采取此操作。 应缓存文件读取内容转换后的内容。

## <a name="see-also"></a>另请参阅
- [CPU 采样初学者指南](../profiling/beginners-guide-to-cpu-sampling.md)
- [分析数据库](../profiling/analyze-database.md)
