---
title: 获取旧版代码片段 (代码) |Microsoft Docs
description: 了解如何获取特定语言 GUID 的所有代码片段。 这些代码片段的快捷方式可以插入到 IntelliSense 完成列表中。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- snippets, retrieving list
- code snippets, retrieving list
- GetSnippets method
ms.assetid: 7d142f8b-35b1-44c4-a13e-f89f6460c906
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 051f356e7b6b6f1a92ba475617f48e5c6074f402
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898869"
---
# <a name="walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation"></a>演练：获取包含已安装的代码片段的列表（旧版实现）
代码片段是一段代码，可以使用菜单命令 (（允许从已安装的代码片段列表) 或从 IntelliSense 完成列表中选择代码片段快捷方式）插入到源缓冲区中。

 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionManager.EnumerateExpansions%2A>方法获取特定语言 GUID 的所有代码片段。 这些代码片段的快捷方式可以插入到 IntelliSense 完成列表中。

 请参阅 [对旧版语言服务](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md) 中的代码片段的支持，详细了解如何通过 MPF 语言服务在托管包框架中 (代码) 代码片段。

### <a name="to-retrieve-a-list-of-code-snippets"></a>检索代码片段列表

1. 下面的代码演示如何获取给定语言的代码片段列表。 结果存储在 结构的数组 <xref:Microsoft.VisualStudio.TextManager.Interop.VsExpansion> 中。 此方法使用静态 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 方法从 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager> 服务获取 <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> 接口。 但是，也可使用为 VSPackage 给定的服务提供程序并调用 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> 方法。

    ```csharp
    using System;
    using System.Collections;
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio.Package;
    using Microsoft.VisualStudio.Shell;
    using Microsoft.VisualStudio.TextManager.Interop;

    [Guid("00000000-0000-0000-0000-000000000000")] //create a new GUID for the language service
    namespace TestLanguage
    {
        class TestLanguageService : LanguageService
        {
            private void GetSnippets(Guid languageGuid,
                                     ref ArrayList expansionsList)
            {
                IVsTextManager textManager = (IVsTextManager)Package.GetGlobalService(typeof(SVsTextManager));
                if (textManager != null)
                {
                    IVsTextManager2 textManager2 = (IVsTextManager2)textManager;
                    if (textManager2 != null)
                    {
                        IVsExpansionManager expansionManager = null;
                        textManager2.GetExpansionManager(out expansionManager);
                        if (expansionManager != null)
                        {
                            // Tell the environment to fetch all of our snippets.
                            IVsExpansionEnumeration expansionEnumerator = null;
                            expansionManager.EnumerateExpansions(languageGuid,
                            0,     // return all info
                            null,    // return all types
                            0,     // return all types
                            1,     // include snippets without types
                            0,     // do not include duplicates
                            out expansionEnumerator);
                            if (expansionEnumerator != null)
                            {
                                // Cache our expansions in a VsExpansion array
                                uint count   = 0;
                                uint fetched = 0;
                                VsExpansion expansionInfo = new VsExpansion();
                                IntPtr[] pExpansionInfo   = new IntPtr[1];

                                // Allocate enough memory for one VSExpansion structure. This memory is filled in by the Next method.
                                pExpansionInfo[0] = Marshal.AllocCoTaskMem(Marshal.SizeOf(expansionInfo));

                                expansionEnumerator.GetCount(out count);
                                for (uint i = 0; i < count; i++)
                                {
                                    expansionEnumerator.Next(1, pExpansionInfo, out fetched);
                                    if (fetched > 0)
                                    {
                                        // Convert the returned blob of data into a structure that can be read in managed code.
                                        expansionInfo = (VsExpansion)Marshal.PtrToStructure(pExpansionInfo[0], typeof(VsExpansion));

                                        if (!String.IsNullOrEmpty(expansionInfo.shortcut))
                                        {
                                            expansionsList.Add(expansionInfo);
                                        }
                                    }
                                }
                                Marshal.FreeCoTaskMem(pExpansionInfo[0]);
                            }
                        }
                    }
                }
            }
        }
    }
    ```

### <a name="to-call-the-getsnippets-method"></a>调用 GetSnippets 方法

1. 下面的方法演示如何在完成 `GetSnippets` 分析操作时调用 方法。 <xref:Microsoft.VisualStudio.Package.LanguageService.OnParseComplete%2A>在以 原因启动的分析操作之后调用 方法 <xref:Microsoft.VisualStudio.Package.ParseReason> 。

> [!NOTE]
> `expansionsList`出于性能原因，将缓存数组列表。 对代码片段的更改不会反映在列表中，除非停止语言服务并重新加载 (，例如停止并重启 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]) 。

```csharp
class TestLanguageService : LanguageService
{
    private ArrayList expansionsList;

    public override void OnParseComplete(ParseRequest req)
    {
        if (this.expansionsList == null)
        {
            this.expansionsList = new ArrayList();
            GetSnippets(this.GetLanguageServiceGuid(),
                ref this.expansionsList);
        }
    }
}
```

### <a name="to-use-the-snippet-information"></a>使用代码片段信息

1. 下面的代码演示如何使用 方法返回的代码片段 `GetSnippets` 信息。 从分析器调用 方法，以响应用于填充代码片段列表的任何 `AddSnippets` 分析原因。 这应在首次完成完整分析后发生。

     `AddDeclaration`方法生成声明列表，该列表稍后将显示在完成列表中。

     `TestDeclaration`类包含可在完成列表中显示的所有信息以及声明的类型。

    ```csharp
    class TestAuthoringScope : AuthoringScope
    {
        public void AddDeclarations(TestDeclaration declaration)
        {
            if (m_declarations == null)
                m_declarations = new List<TestDeclaration>();
            m_declarations.Add(declaration);
         }
    }
    class TestDeclaration
    {
        private string m_name;
        private string m_description;
        private string m_type;

        public TestDeclaration(string name, string desc, string type)
        {
            m_name = name;
            m_description = desc;
            m_type = type;
        }

    class TestLanguageService : LanguageService
    {
        internal void AddSnippets(ref TestAuthoringScope scope)
        {
            if (this.expansionsList != null && this.expansionsList.Count > 0)
            {
                int count = this.expansionsList.Count;
                for (int i = 0; i < count; i++)
                {
                    VsExpansion expansionInfo = (VsExpansion)this.expansionsList[i];
                    scope.AddDeclaration(new TestDeclaration(expansionInfo.title,
                         expansionInfo.description,
                         "snippet"));
                }
            }
        }
    }

    ```

## <a name="see-also"></a>另请参阅
- [旧版语言服务中的代码片段支持](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)
