---
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.openlocfilehash: c1f51f1b5540eb3272998583a4ff7d86ce9c8e3d907f0ecabb73eff884575a84
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "122058256"
---
你应能够使用你在 Visual Studio 计算机生成的符号调试你的代码。 使用本地符号时远程调试器的性能更佳。  如果必须使用远程符号，则需要告诉远程调试监视器以查找远程计算机上的符号。  

从 Visual Studio 2013 Update 2 开始，你可以使用以下 msvsmon 命令行开关来使用用于托管代码的远程符号：`Msvsmon /FallbackLoadRemoteManagedPdbs`  

有关详细信息，请参阅远程调试帮助（在远程调试器窗口中，按 F1  或依次单击“帮助”>“用法”  ）。 有关详细信息，可以参阅 [Visual Studio 2012 和 2013 中的 .NET 远程符号加载更改](https://devblogs.microsoft.com/devops/net-remote-symbol-loading-changes-in-visual-studio-2012-and-2013/)
