---
title: 用于更新 Visual Studio 扩展的 ImageOptimizer 示例
description: 通过示例了解如何更新 Visual Studio 扩展以与 Visual Studio 2022 结合使用。
ms.date: 06/08/2021
ms.topic: sample
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
monikerRange: vs-2022
ms.workload:
- vssdk
feedback_system: GitHub
ms.openlocfilehash: cb8a893ae22daae80d8fb1b4a301f6f62ed7021c
ms.sourcegitcommit: 67dc39e93c86ba50eb5ca877b0471fb8ab8475ac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/08/2021
ms.locfileid: "132001178"
---
# <a name="imageoptimizer---update-a-visual-studio-extension-step-by-step"></a>ImageOptimizer - 按步骤更新 Visual Studio 扩展

[!INCLUDE [preview-note](../includes/preview-note.md)]

本指南将以案例研究的形式介绍添加 Visual Studio 2022 支持同时使用图像优化器扩展维护 Visual Studio 2019 支持所需的所有步骤。  
该指南非常完整，包含各个步骤的 Git 提交链接，但你也可在此处查看最终 PR：[https://github.com/madskristensen/ImageOptimizer/pull/46](https://github.com/madskristensen/ImageOptimizer/pull/46)。

本指南还在末尾处提供了[其他示例](#other-samples)。

## <a name="step-1---modernize-the-project"></a>步骤 1 - 对项目进行现代化改造

请参阅[对项目进行现代化改造](update-visual-studio-extension.md#modernize-your-vsix-project)。

[Git 提交 e052465](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/e052465f30e6bed37e6d76eac016047095e8e18b)

首先，在项目的“属性”页下将 VSIX 和单元测试项目提升至 .NET 4.7.2：

   ![Framework 版本提升](media/samples/framework-bump.png)

映像优化器引用一些旧版的自定义 14.* 和 15.* 包，而我们将安装合并所有所需引用的 [`Microsoft.VisualStudio.Sdk`NuGet 包](https://www.nuget.org/packages/microsoft.visualstudio.sdk)。

```Diff
-  <ItemGroup>
-    <PackageReference Include="Madskristensen.VisualStudio.SDK">
-      <Version>14.0.0-beta4</Version>
-    </PackageReference>
-    <PackageReference Include="Microsoft.VSSDK.BuildTools">
-      <Version>15.8.3247</Version>
-      <IncludeAssets>runtime; build; native; contentfiles; analyzers</IncludeAssets>
-      <PrivateAssets>all</PrivateAssets>
-    </PackageReference>
-  </ItemGroup>

+  <ItemGroup>
+    <PackageReference Include="Microsoft.VisualStudio.SDK">
+      <Version>16.9.31025.194</Version>
+    </PackageReference>
+  </ItemGroup>
```

生成项目成功，我们收到一些线程警告。 修复这些警告，方法是单击 `ctrl` 和 `.` 并使用 IntelliSense 添加缺少的线程切换行。

## <a name="step-2---refactor-source-code-into-a-shared-project"></a>步骤 2 - 将源代码重构到共享项目中

请参阅[共享项目](update-visual-studio-extension.md#use-shared-projects-for-multi-targeting)。

支持 Visual Studio 2022 需要添加新的共享项目，该项目将包含要在 Visual Studio 2019 和 Visual Studio 2022 VSIX 项目之间共享的扩展源代码。

1. 将新的共享项目添加到解决方案

   [Git 提交 abf249d](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/abf249d5a4bed9010652f3f3fc4753c7c771c892)

   ![添加共享项目](media/samples/add-shared-project.png)

1. 向 VSIX 项目添加对共享项目的引用。

   [Git 提交 e8e941e](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/e8e941e5a5482cc15f5b9e7e4f1727f5cab5b12c)

   :::image type="content" source="media/update-visual-studio-extension/add-shared-project-reference.png" alt-text="添加共享项目引用" lightbox="media/update-visual-studio-extension/add-shared-project-reference.png":::

1. 将源代码文件（cs、xaml、resx）移动到新的共享项目，以下文件除外：
    - `source.extension.vsixmanifest`
    - 扩展元数据文件（图标、许可证、发行说明等）
    - VSCT 文件
    - 链接文件
    - 需要包含在 VSIX 中的外部工具或库

   [Git 提交 f31f051](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/f31f0515305623988f2c355ed3bf5952fc8f1d9e)

   ![将文件移动到共享项目](media/samples/move-to-shared-project.png)

1. 现在将所有元数据、VSCT 文件、链接文件和外部工具/库移动到共享位置，并将它们作为链接项添加回 VSIX 项目。 请勿删除 `source.extension.vsixmanifest`。

   [Git 提交 73ba920 - 移动文件](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/73ba920b7db0bdb7c4d66aa9bc932c268efd49cb)

   [Git 提交 d5e36b2 - 添加外部工具/库](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/d5e36b2d047290d38ffc977511510bc03e257f13)

   1. 对于此项目，我们需要将扩展图标、VSCT 文件和外部工具移动到新文件夹 `ImageOptimizer\Resources`。 将它们复制到共享文件夹，并从 VSIX 项目中删除它们。
   1. 将它们作为链接项添加回来，如果这些项已经为链接项，则保持原样即可（例如许可证）。
   1. 通过选择每项并检查属性工具窗口，验证是否在添加的链接文件中正确设置生成操作和其他属性。 对于我们的项目，必须完成以下设置：
       - 将 `icon.png` 生成操作设置为 `Content`，并将已标记的“VSIX 中包含”设置为 `true`
       - 将 `ImageOptimizer.vsct` 生成操作设置为 `VSCTComplile`，并将“VSIX 中包含”设置为 `false`
       - 将 `Resources\Tools` 下文件的所有生成操作都设置为 `Content`，并将标记的“VSIX 中包括”设置为 `true`

           ![将链接文件添加到 VSIX 项目](media/samples/add-linked-files.png)

       - 此外，`ImageOptimizer.cs` 是 `ImageOptimizer.vsct` 的一个依赖项，因此必须将此依赖项手动添加到 csproj 文件：

          ```diff  
          - <Content Include="..\SharedFiles\ImageOptimizer.vsct">
          -   <Link>ImageOptimizer.vsct</Link>
          - </Content>
          - <Compile Include="..\SharedFiles\ImageOptimizer.cs">
          -   <Link>ImageOptimizer.cs</Link>
          - </Compile>

          + <VSCTCompile Include="..\SharedFiles\ImageOptimizer.vsct">
          +   <ResourceName>Menus.ctmenu</ResourceName>
          +   <Generator>VsctGenerator</Generator>
          +   <LastGenOutput>..\SharedFiles\ImageOptimizer.cs</LastGenOutput>
          + </VSCTCompile>
          + <Compile Include="..\SharedFiles\ImageOptimizer.cs">
          +   <AutoGen>True</AutoGen>
          +   <DesignTime>True</DesignTime>
          +   <DependentUpon>..\SharedFiles\ImageOptimizer.vsct</DependentUpon>
          + </Compile>
          ```

       - 如果属性工具窗口阻止你设置特定的生成操作，可以按上述方式手动修改 csproj，根据需要设置生成操作。

1. 生成项目以验证更改并修复错误/问题。 请查看[常见问题解答](update-visual-studio-extension.md#q--a)部分，了解常见问题。

## <a name="step-3---add-a-visual-studio-2022-vsix-project"></a>步骤 3 - 添加 Visual Studio 2022 VSIX 项目

请参阅[添加 Visual Studio 2022 目标](update-visual-studio-extension.md#add-a-visual-studio-2022-target)。

1. 将新的 VSIX 项目添加到解决方案。
1. 删除新项目中除 `source.extension.vsixmanifest.` 以外的所有其他源代码

   ![创建新的 VSIX 项目](media/samples/visual-studio-2022-vsix-initial.png)

1. 添加对共享项目的引用。

   [Git 提交 dd49cb2](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/dd49cb227b52c46206bf4be5c25790ac0377568d)

   :::image type="content" source="media/update-visual-studio-extension/add-shared-project-reference.png" alt-text="添加对共享项目的引用" lightbox="media/update-visual-studio-extension/add-shared-project-reference.png":::

1. 从 Visual Studio 2019 VSIX 项目添加链接文件，并验证这些文件的“生成操作”和“在 VSIX 中包括”属性是否匹配。 此外，请复制 `source.extension.vsixmanifest` 文件，稍后我们将对其进行修改，以支持 Visual Studio 2022。

   [Git 提交 98c43ee](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/98c43ee6fbe912c38a1275542c44c65e11d7dbd9)

   ![将链接文件添加到 VSIX 项目](media/samples/visual-studio-2022-add-linked-files.png)

1. 尝试的生成显示缺少对 `System.Windows.Forms` 的引用。 只需将其添加到我们的 Visual Studio 2022 项目并进行重新生成。

   [Git 提交 de71ccd](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/de71ccd9baff703aa6679392ad41a2cfe7bd7d72)

   ```Diff
   + <Reference Include="System.Windows.Forms" />
   ```

1. 升级对 Visual Studio 2022 版本的 `Microsoft.VisualStudio.SDK` 和 `Microsoft.VSSDK.BuildTools` 包引用。

   [Git 提交 d581fc3](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/d581fc3c954974124dc7e31e5ecc85f78f7828ab)

   > [!NOTE]
   > 这些是编写本指南时可用的最新版本。 建议获取可用的最新版本。
   >
   > ```diff
   > -<PackageReference Include="Microsoft.VisualStudio.SDK" Version="16.0.206" />
   > +<PackageReference Include="Microsoft.VisualStudio.SDK" Version="17.0.0-preview-1-31216-1036" />
   > -<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="16.10.32" />
   > +<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="17.0.63-Visual Studio 2022-g3f11f5ab" />
   > ```

1. 编辑 `source.extension.vsixmanifest` 文件以反映目标为 Visual Studio 2022。

   [Git 提交 9d393c7](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/9d393c708c04ac4af48d1eb9ce3da4470db5d5cc)
   1. 设置 `<InstallationTarget>` 标记以反映 2022 并指示 amd64 有效负载：

      ```xml
      <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[17.0,18.0)">
          <ProductArchitecture>amd64</ProductArchitecture>
      </InstallationTarget>
      ```

   1. 修改“先决条件”，以仅包括 Visual Studio 2022 及更高版本：

      ```Diff
      - <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[15.0,)" DisplayName="Visual Studio core editor" />
      + <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[17.0,)" DisplayName="Visual Studio core editor" />
      ```

大功告成！

这样一来，生成现在会生成 Visual Studio 2019 和 Visual Studio 2022 VSIX。

## <a name="other-samples"></a>其他示例

- [ProPower 工具](https://github.com/microsoft/VS-PPT/pull/244)
  - PeekF1
    - 支持在 Web 浏览器中查看所选类/对象的帮助信息。
  - FixMixedTabs
    - 扫描文档，将制表符替换为空格，或将空格替换为制表符

## <a name="next-steps"></a>后续步骤

请阅读此[完整流程指南](update-visual-studio-extension.md)，为更新扩展做好准备。
