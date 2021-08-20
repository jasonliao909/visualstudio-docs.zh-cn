---
title: 测试区域8：插件切换 |Microsoft Docs
description: 此源代码管理测试区域为在 Visual Studio 中选取要用于解决方案源代码管理的插件的过程提供测试用例。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], switching plug-ins
- source control plug-ins, switching
ms.assetid: 01370792-b5da-4e46-9ce2-7dd326587141
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: de08444c91ed0ab9bebc828873b7485ba97e6584
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122158627"
---
# <a name="test-area-8-plug-in-switching"></a>测试区域 8：插件切换
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成开发环境 (IDE) 使用户界面 (UI) 以更改当前源代码管理插件。 此测试区域为选择用于解决方案源代码管理的插件提供了测试用例。

## <a name="command-menu-access"></a>命令菜单访问
 以下 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 集成开发环境菜单路径用于测试用例。

- 当前源代码管理插件：**工具**  ->  **选项**  ->  **源代码管理**  ->  **插件选择**。

- 更改源代码管理绑定：**文件**  ->  **源控件**  ->  **更改源代码管理**.。。

## <a name="common-expected-behavior"></a>常见的预期行为
 无需退出 Visual Studio 或重新加载解决方案，即可更改解决方案的源代码管理插件。 此外，在加载解决方案时，当前源代码管理插件会自动更改为解决方案使用的插件。

## <a name="test-cases"></a>测试用例
 下面是插件切换测试区域的特定测试用例。

### <a name="case-8a-automatic-change"></a>案例 8a：自动更改

#### <a name="expected-behavior"></a>预期行为
 当用户加载受源代码管理的解决方案时，将自动加载解决方案，并选择相应的源代码管理插件作为 "当前"。

| 操作 | 测试步骤 | 要验证的预期结果 |
| - | - | - |
| 自动源代码管理插件更改 | 1. 选择 "测试" 下的插件作为当前 (**工具**  ->  **选项**  ->  **源代码管理**  ->  **插件选择**。 ) <br />2. 创建一个新项目。<br />3. 将解决方案添加到源代码管理。<br />4. 选择另一个插件 (例如 [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)]) 。<br />5. 接受卸载解决方案提示。<br />6. 从磁盘重新打开解决方案。 | 解决方案已打开。<br /><br /> 正在测试的插件是当前源代码管理插件。 |

### <a name="case-8b-solution-based-change"></a>案例 8b：基于解决方案的更改

#### <a name="expected-behavior"></a>预期行为
 解决方案可以更改其关联的源代码管理插件。

| 操作 | 测试步骤 | 要验证的预期结果 |
|----------------------------------| - | - |
| 更改解决方案的插件 | 1. 选择 "测试" 下的插件作为当前 (**工具**  ->  **选项**  ->  **源代码管理**  ->  **插件选择**) 。<br />2. 创建新的项目和解决方案。<br />3. 将解决方案添加到源代码管理。<br />4. 使用 " **更改源代码管理** " 对话框) 将解决方案从源代码管理取消绑定 (。<br />5. 选择另一个插件 (例如 [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)]) 。<br />6. 如果卸载，请从磁盘重新加载解决方案。<br />7. 将解决方案添加到源代码管理。<br />8. 使用 " **更改源代码管理** " 对话框) 将解决方案从源控件取消绑定 (。<br />9. 再次选择 "测试"。<br />10. 如果卸载，请从磁盘重载解决方案。<br />11. 使用 " **更改源代码管理** " 对话框) 将解决方案绑定到原始位置 (。 | 使用所选插件将解决方案添加到源代码管理。 |

## <a name="see-also"></a>请参阅
- [源代码管理插件的测试指南](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)
