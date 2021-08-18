---
title: 如何：保存和编辑连接字符串
description: 了解如何在应用程序中保存和编辑Visual Studio字符串。 直接在应用程序设置中保存或编辑连接字符串。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: f8ef3a2c-029c-423b-9d9e-a4f1add4f640
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: d6ff3b07d05430ebb8ce26d4003f8ce74ab8ac4d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122059276"
---
# <a name="how-to-save-and-edit-connection-strings"></a>如何：保存和编辑连接字符串
应用程序Visual Studio中的连接字符串保存在应用程序配置文件 (也称为应用程序设置) 或直接在应用程序中硬编码。 在应用程序配置文件中保存连接字符串简化了维护应用程序的任务。 如果连接字符串需要进行更改，则可以在应用程序设置文件中对其进行更新（这与必须在源代码中对其进行更改并重新编译应用程序相反）。

将敏感信息（如密码）存储在连接字符串中可能会影响应用程序的安全性。 保存在应用程序配置文件中的连接字符串是未经加密处理的，因此其他人有可能访问该文件并查看其内容。 若要控制对数据库的访问，一种较为安全的方法是使用 Windows 集成安全性。

如果不选择使用 Windows 集成安全性，并且数据库需要用户名和密码，则可以在连接字符串中省略这些内容，但需要应用程序提供此信息才能成功连接到数据库。 例如，可以创建一个对话框提示用户提供此信息并在运行时动态生成连接字符串。 如果在发送到数据库的途中该信息被截获，则安全性将得不到保证。
有关详细信息，请参阅[保护连接信息](/dotnet/framework/data/adonet/protecting-connection-information)。

## <a name="to-save-a-connection-string-from-within-the-data-source-configuration-wizard"></a>从数据源配置向导中保存连接字符串
在 **"数据源配置向导"** 中，选择"将连接字符串保存到应用程序配置文件"页上 **保存连接** 的选项。

## <a name="to-save-a-connection-string-directly-into-application-settings"></a>将连接字符串直接保存到应用程序设置中
1. 在“解决方案资源管理器”中，双击“我的项目”图标 (Visual Basic) 或“属性”图标 (C#) 以打开项目设计器。
1. 选择“设置”选项卡。
1. 输入连接字符串的“名称”。 当在代码中访问该连接字符串时引用此名称。
1. 将“类型”设置为“连接字符串”。
1. 将“范围”保留为“应用程序”。
1. 在"值"字段中键入连接字符串，或单击"值 (...) **按钮以** 打开"连接属性"对话框以生成连接字符串。 

## <a name="edit-connection-strings-stored-in-application-settings"></a>编辑存储在应用程序设置中的连接字符串
通过使用“项目设计器”，可修改在应用程序设置中保存的连接信息。

### <a name="to-edit-a-connection-string-stored-in-application-settings"></a>编辑存储在应用程序设置中的连接字符串
1. 在“解决方案资源管理器”中，双击“我的项目”图标 (Visual Basic) 或“属性”图标 (C#) 以打开项目设计器。
1. 选择“设置”选项卡。
1. 找到要编辑的连接，然后选择"值 **"字段中的文本** 。
1. 在"值"字段中编辑连接字符串，或单击"值 (...) **按钮以** 编辑与"连接属性"对话框的连接。 

## <a name="edit-connection-strings-for-datasets"></a>编辑数据集的连接字符串
可以修改数据集中每个 TableAdapter 的连接信息。

### <a name="to-edit-a-connection-string-for-a-tableadapter-in-a-dataset"></a>编辑数据集中 TableAdapter 的连接字符串
1. 在 **解决方案资源管理器** 中，双击具有 (**连接的 .xsd**) 数据集。
1. 选择具有要编辑的连接的 **TableAdapter** 或查询。
1. 在" **属性"** 窗口中，展开"连接 **"节点**。
1. 若要快速修改连接字符串，请编辑 **ConnectionString** 属性，或单击"连接"属性上的向下 **箭头，然后选择**"新建 **连接"。**

## <a name="security"></a>安全性
将敏感信息（如密码）存储在连接字符串中可能会影响应用程序的安全性。 若要控制对数据库的访问，一种较为安全的方法是使用 Windows 集成安全性。
有关详细信息，请参阅[保护连接信息](/dotnet/framework/data/adonet/protecting-connection-information)。

## <a name="see-also"></a>请参阅

- [添加连接](../data-tools/add-new-connections.md)
