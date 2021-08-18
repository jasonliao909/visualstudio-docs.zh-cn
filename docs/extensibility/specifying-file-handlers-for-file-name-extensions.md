---
title: 指定文件扩展名的文件处理程序|Microsoft Docs
description: 了解如何使用 OpenWithList 和 OpenWithProgids 确定在 Visual Studio SDK 中处理文件扩展名的应用程序。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- file extensions, specifying file handlers
ms.assetid: e3de4730-a95c-465a-b3b2-92ca85364ad7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 752d34734537d46681a3a5a116640c24adaffb41
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122137569"
---
# <a name="specifying-file-handlers-for-file-name-extensions"></a>指定文件扩展名的文件处理程序
有许多方法可以确定处理具有特定文件扩展名的文件的应用程序。 OpenWithList 和 OpenWithProgids 谓词是两种在文件扩展名的注册表项下指定文件处理程序的方法。

## <a name="openwithlist-verb"></a>OpenWithList 谓词
 在资源管理器中右键单击Windows，会看到"打开 **"** 命令。 如果多个产品与扩展相关联，则会看到 Open **With** 子menu。

 可以通过在 HKEY_CLASSES_ROOT 中设置文件扩展名的 OpenWithList 键来注册不同的应用程序以打开HKEY_CLASSES_ROOT。 文件扩展名的此键下列出的应用程序显示在"打开方式"对话框中的"推荐程序 **"** 标题下。 以下示例演示注册以打开 .vcproj 文件扩展名的应用程序。

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)="VisualStudio.vcproj.14.0"
      OpenWithList\
         devenv.exe
```

> [!NOTE]
> 指定应用程序的键来自"应用程序"下HKEY_CLASSES_ROOT\Applications。

 通过添加 OpenWithList 密钥，可以声明应用程序支持文件扩展名，即使另一个应用程序取得扩展名的所有权。 这可能是应用程序或另一个应用程序的未来版本。

## <a name="openwithprogids"></a>OpenWithProgIDs
 ProgID (编程) 标识应用程序或 COM 对象的版本的 ClassID 的友好版本。 每个可共同创建的对象都应有其自己的 ProgID。 例如，VisualStudio.DTE.7.1 Visual Studio .NET 2003 启动，而 VisualStudio.DTE.10.0 启动 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 作为项目类型或项目项类型的所有者，必须为文件扩展名创建特定于版本的 ProgID。 由于多个 ProgID 可以启动同一应用程序，因此这些 ProgID 可能是冗余的。 有关详细信息，请参阅 [为文件扩展名 注册谓词](../extensibility/registering-verbs-for-file-name-extensions.md)。

 对版本控制的文件 ProgID 使用以下命名约定，以避免与其他供应商注册重复：

|文件扩展名|版本控制 ProgID|
|--------------------|----------------------|
|.extension|ProductName。 extension.versionMajor.versionMinor|

 可以通过向 \\ \OpenWithProgids 密钥添加版本控制 ProgID 作为值来注册能够打开特定文件扩展名HKEY_CLASSES_ROOT *\<extension>* 应用程序。 此注册表项包含与文件扩展名关联的备用 ProgID 的列表。 与列出的 ProgID 关联的应用程序显示在"使用产品名称打开 _"_ 子项中。 如果在 和 键中指定了同一 `OpenWithList` `OpenWithProgids` 应用程序，操作系统将合并重复项。

> [!NOTE]
> 密钥 `OpenWithProgids` 仅在 Windows XP 中受支持。 由于其他操作系统忽略此密钥，因此请勿将其用作文件处理程序的唯一注册。 使用此密钥在 Windows XP 中提供更好的用户体验。

 将所需的 ProgID 添加为类型为 REG_NONE。 以下代码提供了为文件扩展名注册 ProgID 的示例 (。*ext*) 。

```
HKEY_CLASSES_ROOT\
   .ext\
      (default)="MyProduct.ext.14.0"
      OpenWithProgids
         progid        REG_NONE (zero-length binary value)
         otherprogid   REG_NONE (zero-length binary value)
```

 指定为文件扩展名默认值的 ProgID 是默认文件处理程序。 如果修改以前版本的 的文件扩展名的 ProgID，或者由其他应用程序接管的文件扩展名，则必须注册文件扩展名的密钥，并指定列表中的新 ProgID 以及支持的旧 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] `OpenWithProgids` ProgID。 例如：

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)="VisualStudio.vcproj.14.0"
      OpenWithProgids
         vcprojfile              //old progid
         VisualStudio.vcproj.12.0 //old progid
         VisualStudio.vcproj.14.0 //new progid
```

 如果旧的 ProgID 具有与之关联的谓词，则这些谓词也会显示在快捷菜单中的"使用产品名称打开"下。

## <a name="see-also"></a>请参阅
- [关于文件扩展名](../extensibility/about-file-name-extensions.md)
- [注册文件扩展名的谓词](../extensibility/registering-verbs-for-file-name-extensions.md)
