---
title: GUID と uniqueidentifier 値の比較
description: SQL Server と .NET で GUID と uniqueidentifier の値を操作する方法について説明します。
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: aababd75-2335-43e3-ace8-4b7ae84191a8
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 8a4c5fcc63c2d2ddb8414227ea049e78db1cba10
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452283"
---
# <a name="comparing-guid-and-uniqueidentifier-values"></a>GUID と uniqueidentifier 値の比較

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server のグローバル一意識別子 (GUID) データ型は、16バイトのバイナリ値を格納する `uniqueidentifier` データ型によって表されます。 GUID は2進数で、多くのサイトに多数のコンピューターが存在するネットワーク内で一意である必要がある識別子として使用されます。 Guid は、Transact-sql NEWID 関数を呼び出すことによって生成でき、世界中で一意であることが保証されています。 詳細については、「 [uniqueidentifier (transact-sql)](../../../t-sql/data-types/uniqueidentifier-transact-sql.md)」を参照してください。  
  
## <a name="working-with-sqlguid-values"></a>SqlGuid 値の操作  
Guid 値は長すぎて見えないため、ユーザーにとって意味がありません。 ランダムに生成された Guid をキー値に使用し、大量の行を挿入すると、ランダム i/o がインデックスに反映されるため、パフォーマンスが低下する可能性があります。 Guid も、他のデータ型と比較すると比較的大きくなります。 一般に、他のデータ型が適していない非常に狭いシナリオでのみ、Guid を使用することをお勧めします。  
  
### <a name="comparing-guid-values"></a>GUID 値の比較  
`uniqueidentifier` 型の値には比較演算子が使用できます。 しかし、2 つの値のビット パターンを比較することによって、順序付けは実装されません。 `uniqueidentifier` 値に対して実行可能な唯一の操作は、比較 (=、<>、\<、>、\<=、>=) と NULL の確認 (IS NULL および IS NOT NULL) です。 他の算術演算子は使用できません。  
  
<xref:System.Guid> と <xref:System.Data.SqlTypes.SqlGuid> のどちらにも、異なる GUID 値を比較するための `CompareTo` メソッドがあります。 ただし、`System.Guid.CompareTo` と `SqlTypes.SqlGuid.CompareTo` の実装方法が異なります。 <xref:System.Data.SqlTypes.SqlGuid> は SQL Server の動作を使用して `CompareTo` を実装します。これは、値の最後の6バイトで最も重要です。 <xref:System.Guid> は、16バイトすべてを評価します。 次の例は、この動作の違いを示しています。 コードの最初のセクションには、並べ替えられていない <xref:System.Guid> 値が表示され、コードの2番目のセクションには並べ替えられた <xref:System.Guid> 値が表示されます。 3番目のセクションには、並べ替えられた <xref:System.Data.SqlTypes.SqlGuid> 値が表示されます。 コードリストの下に出力が表示されます。  
  
[!code-csharp[DataWorks SqlGuid#1](~/../sqlclient/doc/samples/SqlGuid.cs#1)]
  
この例の結果は、次のようになります。  
  
```console
Unsorted Guids:  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
  
Sorted Guids:  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
  
Sorted SqlGuids:  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
```  
  
## <a name="next-steps"></a>次の手順
- [SQL Server のデータ型と ADO.NET](sql-server-data-types.md)
