---
title: 在 Visual Studio 订阅中查找和声明产品密钥 | Microsoft Docs
author: evanwindom
ms.author: amast
manager: shve
ms.assetid: da8df006-4896-4ff9-b487-698d78deabc3
ms.date: 04/27/2022
ms.topic: conceptual
description: 了解如何在 Visual Studio 订阅中查找、声明和导出产品密钥
ms.openlocfilehash: 4ea850fdddbdb4e340dfa2ce12135cc7084d10cd
ms.sourcegitcommit: f0010a70e1f7f1302bd322b779ac5614ebc0f4d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/29/2022
ms.locfileid: "144390787"
---
# <a name="finding-and-claiming-product-keys-in-visual-studio-subscriptions"></a>在 Visual Studio 订阅中查找和声明产品密钥
本文介绍如何从 https://my.visualstudio.com/productkeys 中查找、声明和导出产品密钥。  有关使用密钥激活产品、密钥的零售和批量许可版本以及每日产品密钥索取上限的详细信息，请访问[产品密钥概述](product-keys.md)。

## <a name="locating-and-claiming-product-keys"></a>查找并索取产品密钥
必须登录你的 Visual Studio 订阅才能查看产品密钥。 可在如下所示的“[下载](https://my.visualstudio.com/downloads)”页中，选择某一特定产品的蓝色“获取密钥”链接来查找单个产品密钥。  所有密钥都可在“[产品密钥](https://my.visualstudio.com/productkeys?wt.mc_id=o~msft~docs)”页查找到。 如果一个产品有多个密钥，会在下载项的“注释”列中显示注释，帮助你确定应使用哪个密钥。
> [!div class="mx-imgBorder"]
> ![从“下载”页获取密钥](_img/product-keys/download-get-key.png "选择任何下载内容“信息”页上的“获取密钥”以获取该产品的密钥。")

某些产品将其多个版本捆绑到单次下载中。 在这种情况下，输入的产品密钥决定安装的产品版本。
某些密钥会自动提供，例如“静态”密钥，同一个密钥可以根据需要使用无数次，因为不需要激活。 其他密钥必须通过选择该产品的“获取密钥”链接来索取。

根据具体的产品，有多种密钥类型可供选择。

### <a name="product-key-types"></a>产品密钥类型

|  键类型   |  描述 |
|-------------|--------------|
|    不适用  | 安装此产品不需要密钥。 |
|    零售 | 零售密钥允许多次激活，并用于产品的零售版本。 在许多情况下，每个密钥允许 10 次激活，但通常在同一台计算机上允许更多激活。 |
|    多次激活 | 使用 MAK) 多个激活密钥 (，可以使用同一密钥激活产品的多个安装。 MAK 与产品的批量许可版本一起使用。 通常，每个订阅只提供一个 MAK 密钥。 |
|    静态激活密钥 | 为不需要激活的产品提供静态激活密钥。 它们可用于任意数量的安装。 |
|    自定义密钥 | 自定义密钥提供用于激活或安装产品的特殊操作或信息。 |
|    VA 1.0  |  多个激活密钥，类似于 MAK。 |
|    OEM 密钥 |  允许多次激活的原始设备制造商密钥。 |
|    DreamSpark Retail Key  | DreamSpark 的零售密钥，允许一次激活。 DreamSpark Retail 密钥按批颁发，主要用于学生消费。 |
|    DreamSpark 实验室密钥 | 实验室使用允许多个激活的 DreamSpark 程序的密钥。 DreamSpark 实验室密钥适用于大学计算机实验室方案。 |
|    DreamSpark MAK 密钥 | DreamSpark 计划客户的 MAK 密钥。 |
|

可从产品的下载页索取密钥，或者在“[产品密钥](https://my.visualstudio.com/productkeys)”页上搜索所需的密钥。

### <a name="claiming-product-keys"></a>索取产品密钥
只有拥有活动订阅的订阅者才可下载产品和索取产品密钥。  当订阅处于活动状态时，可从“[产品密钥](https://my.visualstudio.com/productkeys)”页导出索取的密钥。

索取产品密钥：
1. 登录到你的 Visual Studio 订阅。  必须登录才能下载产品或索取产品密码。
2. 选择[产品密钥](https://my.visualstudio.com/productkeys?wt.mc_id=o~msft~docs)选项卡。
3. 产品密钥根据产品名称按字母顺序列出。  可以向下滚动到所需产品的名称，也可以使用页面顶部的搜索栏进行搜索。
> [!div class="mx-imgBorder"]
> ![搜索产品密钥](_img/product-keys/search-keys.png "滚动到所需的产品，或使用搜索框快速查找任何产品。")
   
在此示例中，我们使用了搜索栏查找 Visual Studio Enterprise 2019 的产品密钥。
正如你所见，这里列出了几个版本。  已为 Visual Studio Enterprise 2019 版本 16.0 和 16.1 各声明了一个密钥。  对于这两个版本，仍然可以使用不同类型的附加密钥。 

注意，你可以在“注释”列记录有关已索取的密钥的简短说明。  可以将其与“已索取”列中的日期一起使用，以跟踪你索取的密钥。  例如，可以在使用密钥激活产品的安装时进行记录。

### <a name="exporting-your-claimed-keys"></a>导出已索取的密钥
可以导出已索取的密钥列表。  这包括众多自动标记为“已索取”的所选静态密钥和其他密钥。

> [!IMPORTANT]
> 如果订阅到期，则无法索取新的密钥或导出已索取的密钥。

若要导出密钥，请选择“产品密钥”页面最右侧的“导出所有密钥”链接。  将创建一个有权KeysExport.xml的.xml文件。   可以选择打开或保存文件。  你需要使用能够处理 .xml 文件的应用程序来打开此文件。  例如，可以在Microsoft Excel中以只读工作簿的形式打开该文件。

## <a name="resources"></a>资源
[Visual Studio 订阅支持](https://aka.ms/vssubscriberhelp)

## <a name="see-also"></a>另请参阅
+ [Visual Studio 文档](/visualstudio/)
+ [Azure DevOps 文档](/azure/devops/)
+ [Azure 文档](/azure/)
+ [Microsoft 365 文档](/microsoft-365/)

## <a name="next-steps"></a>后续步骤
当你准备好下载软件并使用密钥时，请访问 https://my.visualstudio.com/downloads 。  有关下载软件的详细信息，请参阅[下载概述](download-software.md)。