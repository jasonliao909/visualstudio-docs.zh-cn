---
title: '&lt;PackageFiles&gt; 元素（引导程序）| Microsoft Docs'
description: 了解 PackageFiles 元素，它包含 PackageFile 元素，这些元素定义作为 Command 元素的结果执行的安装包。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <PackageFiles> element [bootstrapper]
ms.assetid: 3ea252d7-18a3-47d8-af83-47feebcfe82b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: d986c13a4c575fa70dd4496c0b87073baa1615f7
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663812"
---
# <a name="ltpackagefilesgt-element-bootstrapper"></a>&lt;PackageFiles&gt; 元素（引导程序）
`PackageFiles` 元素包含 `PackageFile` 元素，这些元素定义作为 `Command` 元素的结果执行的安装包。

## <a name="syntax"></a>语法

```xml
<PackageFiles
    CopyAllPackageFiles
>
    <PackageFile
        Name
        HomeSite
        CopyOnBuild
        PublicKey
        Hash
    />
</PackageFiles>
```

## <a name="elements-and-attributes"></a>元素和属性
 `PackageFiles` 元素具有以下属性。

|属性|说明|
|---------------|-----------------|
|`CopyAllPackageFiles`|可选。 如果设置为 `false`，则安装程序将仅下载从 `Command` 元素引用的文件。 如果设置为 `true`，将下载所有文件。<br /><br /> 如果设置为 `IfNotHomesite`，则安装程序的行为与 `False` 相同（如果 `ComponentsLocation` 设置为 `HomeSite`），否则其行为与 `True` 相同。 此设置对于允许本身是引导程序的包在 HomeSite 场景中执行它们自己的行为很有用。<br /><br /> 默认为 `true`。|

## <a name="packagefile"></a>PackageFile
 `PackageFile` 元素是 `PackageFiles` 元素的一个子元素。 一个 `PackageFiles` 元素必须至少有一个 `PackageFile` 元素。

 `PackageFile` 具有以下属性。

| 属性 | 说明 |
|---------------| - |
| `Name` | 必需。 包文件的名称。 这是 `Command` 元素在定义安装包的条件时将引用的名称。 此值还用作 `Strings` 表中的键，用于检索工具（如 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]）将用于描述包的本地化名称。 |
| `HomeSite` | 可选。 包在远程服务器上的位置（如果未包含在安装程序中）。 |
| `CopyOnBuild` | 可选。 指定引导程序是否应在生成时将包文件复制到磁盘上。 默认值为 true。 |
| `PublicKey` | 包的证书签名者加密公钥。 如果使用 `HomeSite`，则是必需的；否则为可选。 |
| `Hash` | 可选。 包文件的 SHA1 哈希。 这用于在安装时验证文件的完整性。 如果无法从包文件中计算相同的哈希，则不会安装包。 |

## <a name="example"></a>示例
 下面的代码示例定义 .NET Framework 可再发行包及其依赖项（如 Windows Installer）的包。

```xml
<PackageFiles>
    <PackageFile Name="instmsia.exe" HomeSite="InstMsiAExe" PublicKey="3082010A0282010100AA99BD39A81827F42B3D0B4C3F7C772EA7CBB5D18C0DC23A74D793B5E0A04B3F595ECE454F9A7929F149CC1A47EE55C2083E1220F855F2EE5FD3E0CA96BC30DEFE58C82732D08554E8F09110BBF32BBE19E5039B0B861DF3B0398CB8FD0B1D3C7326AC572BCA29A215908215E277A34052038B9DC270BA1FE934F6F335924E5583F8DA30B620DE5706B55A4206DE59CBF2DFA6BD154771192523D2CB6F9B1979DF6A5BF176057929FCC356CA8F440885558ACBC80F464B55CB8C96774A87E8A94106C7FF0DE968576372C36957B443CF323A30DC1BE9D543262A79FE95DB226724C92FD034E3E6FB514986B83CD0255FD6EC9E036187A96840C7F8E203E6CF050203010001"/>
    <PackageFile Name="WindowsInstaller-KB884016-v2-x86.exe" HomeSite="Msi30Exe" PublicKey="3082010A0282010100B22D8709B55CDF5599EB5262E7D3F4E34571A932BF94F20EE90DADFE9DC7046A584E9CA4D1D84441FB647E0F65EEC817DA4DDBD9D650B40C565B6C16884BBF03EE504883EC4F88939A51E394197FFAB397A5CE606D9FDD4C9338BDCD345971E686CEE98399A096B8EAE0445B1342B93A484E5472F70896E400C482017643AF61C2DBFAE5C5F00213DDF835B40F0D5236467443B1A2CA9CDD7E99F1351177FB1526018ECFE0B804782A15FD72C66076910CE74FB218181B6989B4F12F211B66EACA91C7460DB91758715856866523D10232AE64A06FDA5295FDFBDD8D34F5C10C35A347D7E91B6AFA0F45B4E8321D7019BDD1F9E5641FEB8737EA6FD40D838FFD0203010001"/>
    <PackageFile Name="dotnetfx.exe" HomeSite="DotNetFXExe" PublicKey="3082010A0282010100B22D8709B55CDF5599EB5262E7D3F4E34571A932BF94F20EE90DADFE9DC7046A584E9CA4D1D84441FB647E0F65EEC817DA4DDBD9D650B40C565B6C16884BBF03EE504883EC4F88939A51E394197FFAB397A5CE606D9FDD4C9338BDCD345971E686CEE98399A096B8EAE0445B1342B93A484E5472F70896E400C482017643AF61C2DBFAE5C5F00213DDF835B40F0D5236467443B1A2CA9CDD7E99F1351177FB1526018ECFE0B804782A15FD72C66076910CE74FB218181B6989B4F12F211B66EACA91C7460DB91758715856866523D10232AE64A06FDA5295FDFBDD8D34F5C10C35A347D7E91B6AFA0F45B4E8321D7019BDD1F9E5641FEB8737EA6FD40D838FFD0203010001"/>
    <PackageFile Name="dotnetchk.exe"/>
</PackageFiles>
```

## <a name="see-also"></a>另请参阅
- [\<Product> 元素](../deployment/product-element-bootstrapper.md)
- [\<Package> 元素](../deployment/package-element-bootstrapper.md)
- [产品和包架构引用](../deployment/product-and-package-schema-reference.md)