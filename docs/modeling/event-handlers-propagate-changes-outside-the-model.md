---
title: 事件处理程序在模型外部传播更改
description: 了解在可视化和建模 SDK 中，可以定义存储事件处理程序，以将更改传播到存储外部的资源。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain models
- Domain-Specific Language, events
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 0617021a5184b3812a88c26dce2c142b1d769544
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671860"
---
# <a name="event-handlers-propagate-changes-outside-the-model"></a>事件处理程序在模型外部传播更改

在可视化和建模 SDK 中，可以定义存储事件处理程序，以将更改传播到存储外部的资源，例如非存储变量、文件、其他存储中的模型或其他 Visual Studio 扩展。 存储事件处理程序在触发事件的事务结束之后执行。 它们也会在 Undo 或 Redo 操作中执行。 因此，与存储规则不同，存储事件最适用于更新存储外部的值。 与 .NET 事件不同，存储事件处理程序注册为侦听类：不需要为每个实例注册单独的处理程序。 若要详细了解如何在处理更改的不同方式之间做出选择，请参阅[响应和传播更改](../modeling/responding-to-and-propagating-changes.md)。

图形图面和其他用户界面控件是可由存储事件处理的外部示例资源。

### <a name="to-define-a-store-event"></a>定义存储事件

1. 选择要监视的事件类型。 如需完整列表，请查看 <xref:Microsoft.VisualStudio.Modeling.EventManagerDirectory> 的属性。 每个属性对应于一种类型的事件。 最常用的事件类型包括：

    - `ElementAdded` - 创建模型元素、关系链接、形状或连接器时触发。

    - ElementPropertyChanged - 更改 `Normal` 域属性的值时触发。 仅在新值和旧值不相等时，才触发该事件。 该事件不能应用于计算和自定义存储属性。

         它不能应用于与关系链接对应的角色属性。 请改用 `ElementAdded` 来监视域关系。

    - `ElementDeleted` - 删除模型元素、关系、形状或连接器后触发。 你仍可以访问元素的属性值，但它与其他元素没有任何关系。

2. 在 DslPackage 项目的单独代码文件中为 YourDslDocData 添加分部类定义 。

3. 将事件的代码编写为方法，如以下示例所示。 它可以是 `static`，除非你想要访问 `DocData`。

4. 重写 `OnDocumentLoaded()` 以注册处理程序。 如果具有多个处理程序，可以在同一位置注册所有处理程序。

注册代码的位置并不重要。 `DocView.LoadView()` 是一个可选位置。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.VisualStudio.Modeling;

namespace Company.MusicLib
{
  partial class MusicLibDocData
  {
    // Register store events here or in DocView.LoadView().
    protected override void OnDocumentLoaded()
    {
      base.OnDocumentLoaded(); // Don't forget this.

      #region Store event handler registration.
      Store store = this.Store;
      EventManagerDirectory emd = store.EventManagerDirectory;
      DomainRelationshipInfo linkInfo = store.DomainDataDirectory
          .FindDomainRelationship(typeof(ArtistAppearsInAlbum));
      emd.ElementAdded.Add(linkInfo,
          new EventHandler<ElementAddedEventArgs>(AddLink));
      emd.ElementDeleted.Add(linkInfo,
          new EventHandler<ElementDeletedEventArgs>(RemoveLink));

      #endregion Store event handlers.
    }

    private void AddLink(object sender, ElementAddedEventArgs e)
    {
      ArtistAppearsInAlbum link = e.ModelElement as ArtistAppearsInAlbum;
      if (link != null)
            ExternalDatabase.Add(link.Artist.Name, link.Album.Title);
    }
    private void RemoveLink(object sender, ElementDeletedEventArgs e)
    {
      ArtistAppearsInAlbum link = e.ModelElement as ArtistAppearsInAlbum;
      if (link != null)
            ExternalDatabase.Delete(link.Artist.Name, link.Album.Title);
    }
  }
}
```

## <a name="use-events-to-make-undoable-adjustments-in-the-store"></a>使用事件在存储中进行可撤消的调整

存储事件通常不用于传播存储中的更改，因为事件处理程序在提交事务后执行。 相反，将使用存储规则。 有关详细信息，请参阅[模型中的规则传播更改](../modeling/rules-propagate-changes-within-the-model.md)。

但是，如果希望用户能够独立于原始事件撤消其他更新，可以使用事件处理程序对存储进行其他更新。 例如，假设小写字符是发行集标题的常用约定。 可以编写一个存储事件处理程序，在用户以大写键入标题后将标题更正为小写。 但用户可以使用 Undo 命令取消更正，从而还原大写字符。 第二次 Undo 操作将删除用户的更改。

相反，如果你编写了一个存储规则来执行相同的操作，则用户的更改和你的更正将在同一事务中，这样用户就无法在不丢失原始更改的情况下撤消调整。

```csharp
partial class MusicLibDocView
{
    // Register store events here or in DocData.OnDocumentLoaded().
    protected override void LoadView()
    {
      /* Register store event handler for Album Title property. */
      // Get reflection data for property:
      DomainPropertyInfo propertyInfo =
        this.DocData.Store.DomainDataDirectory
        .FindDomainProperty(Album.TitleDomainPropertyId);
      // Add to property handler list:
      this.DocData.Store.EventManagerDirectory
        .ElementPropertyChanged.Add(propertyInfo,
        new EventHandler<ElementPropertyChangedEventArgs>
             (AlbumTitleAdjuster));

      /*
      // Alternatively, you can set one handler for
      // all properties of a class.
      // Your handler has to determine which property changed.
      DomainClassInfo classInfo = this.Store.DomainDataDirectory
           .FindDomainClass(typeof(Album));
      this.Store.EventManagerDirectory
          .ElementPropertyChanged.Add(classInfo,
        new EventHandler<ElementPropertyChangedEventArgs>
             (AlbumTitleAdjuster));
       */
      return base.LoadView();
    }

// Undoable adjustment after a property is changed.
// Method can be static since no local access.
private static void AlbumTitleAdjuster(object sender,
         ElementPropertyChangedEventArgs e)
{
  Album album = e.ModelElement as Album;
  Store store = album.Store;

  // We mustn't update the store in an Undo:
  if (store.InUndoRedoOrRollback
      || store.InSerializationTransaction)
      return;

  if (e.DomainProperty.Id == Album.TitleDomainPropertyId)
  {
    string newValue = (string)e.NewValue;
    string lowerCase = newValue.ToLowerInvariant();
    if (!newValue.Equals(lowerCase))
    {
      using (Transaction t = store.TransactionManager
            .BeginTransaction("adjust album title"))
      {
        album.Title = lowerCase;
        t.Commit();
      } // Beware! This could trigger the event again.
    }
  }
  // else other properties of this class.
}
```

如果编写用于更新存储的事件：

- 使用 `store.InUndoRedoOrRollback` 可避免在 Undo 中更改模型元素。 事务管理器会将存储中的所有内容设置回其原始状态。

- 使用 `store.InSerializationTransaction` 可避免在从文件加载模型时进行更改。

- 更改将导致触发更多事件。 请确保避免出现无限循环。

## <a name="store-event-types"></a>存储事件类型

每个事件类型对应于 Store.EventManagerDirectory 中的一个集合。 你可以随时添加或删除事件处理程序，但通常是在加载文档时添加它们。

|`EventManagerDirectory` 属性名称|执行时间|
|-|-|
|ElementAdded|创建域类、域关系、形状、连接器或关系图的实例时。|
|ElementDeleted|模型元素已从存储的元素目录中删除，不再是任何关系的源或目标。 该元素实际上并未从内存中删除，而是保留以备将来执行 Undo 时使用。|
|ElementEventsBegun|在外部事务结束时调用。|
|ElementEventsEnded|在处理完所有其他事件后调用。|
|ElementMoved|模型元素已从一个存储分区移到另一个存储分区。<br /><br /> 这与关系图上形状的位置无关。|
|ElementPropertyChanged|域属性的值已更改。 仅在旧值和新值不相等时，才执行此操作。|
|RolePlayerChanged|关系的两个角色（端点）之一引用了新元素。|
|RolePlayerOrderChanged|在多重大于 1 的角色中，链接序列已更改。|
|TransactionBeginning||
|TransactionCommitted||
|TransactionRolledBack||

## <a name="see-also"></a>另请参阅

- [响应并传播更改](../modeling/responding-to-and-propagating-changes.md)
- [示例代码：线路关系图](https://code.msdn.microsoft.com/Visualization-Modeling-SDK-763778e8)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
