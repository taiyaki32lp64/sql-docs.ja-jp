---
title: 空間データに対するニアレスト ネイバーのクエリ | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 7af4ad5d-484e-45b4-aa16-83c33b358bb6
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 099771b9900d4c39de40b176cde5c92fa0c95462
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014110"
---
# <a name="query-spatial-data-for-nearest-neighbor"></a>空間データに対するニアレスト ネイバーのクエリ
  空間データで使用される一般的なクエリの 1 つに、ニアレスト ネイバー クエリがあります。 ニアレスト ネイバー クエリは、特定の空間オブジェクトに最も近い空間オブジェクトを検索するために使用されます。 たとえば、Web サイトのストア ロケーターは、多くの場合、顧客の場所に最も近い店舗の場所を検索する必要があります。  
  
 ニアレスト ネイバー クエリは、さまざまな有効なクエリ形式で記述できますが、空間インデックスを使用するニアレスト ネイバー クエリでは、次の構文を使用する必要があります。  
  
## <a name="syntax"></a>構文  
  
```vb  
SELECT TOP ( number )  
        [ WITH TIES ]  
        [ * | expression ]   
        [, ...]  
    FROM spatial_table_reference, ...   
        [ WITH   
            (   
                [ INDEX ( index_ref ) ]   
                [ , SPATIAL_WINDOW_MAX_CELLS = <value>]   
                [ ,... ]   
            )   
        ]  
    WHERE   
        column_ref.STDistance ( @spatial_ object )   
            {   
                [ IS NOT NULL ] | [ < const ] | [ > const ]   
                | [ <= const ] | [ >= const ] | [ <> const ] ]   
            }  
            [ AND { other_predicate } ]   
    }  
    ORDER BY column_ref.STDistance ( @spatial_ object ) [ ,...n ]  
[ ; ]  
  
```  
  
## <a name="nearest-neighbor-query-and-spatial-indexes"></a>ニアレスト ネイバー クエリと空間インデックス  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、`TOP` および `ORDER BY` 句は、空間データ列にニアレスト ネイバー クエリを実行するために使用されます。 `ORDER BY` 句には、空間列データ型の `STDistance()` メソッドの呼び出しが含まれます。 `TOP` 句は、クエリで返されるオブジェクトの数を示します。  
  
 ニアレスト ネイバー クエリで空間インデックスを使用するには、次の要件を満たす必要があります。  
  
1.  空間インデックスが空間列の 1 つにあり、`STDistance()` メソッドが `WHERE` および `ORDER BY` 句でその列を使用する必要があります。  
  
2.  `TOP`句は `PERCENT` ステートメントを含むことはできません。  
  
3.  `WHERE` 句は `STDistance()` メソッドを含む必要があります。  
  
4.  `WHERE` 句に複数の述語がある場合、`STDistance()` メソッドを含む述語は、`AND` 結合で他の述語と接続する必要があります。  `STDistance()` メソッドは、`WHERE` 句のオプションの一部にすることはできません。  
  
5.  `ORDER BY` 句の最初の式では `STDistance()` メソッドを使用する必要があります。  
  
6.  `ORDER BY` 句の最初の `STDistance()` 式の並べ替え順序は、`ASC` である必要があります。  
  
7.  `STDistance` が `NULL` を返すすべての行は、フィルターで除外する必要があります。  
  
> [!WARNING]  
>  `geography` または `geometry` データ型を引数として取るメソッドは、SRID がその型と同一でない場合、`NULL` を返します。  
  
 ニアレスト ネイバー クエリで使用されるインデックスでは、新しい空間インデックス テセレーションを使用することをお勧めします。 空間インデックス テセレーションの詳細については、「 [空間データ &#40;SQL Server&#41;](spatial-data-sql-server.md)である必要があります。  
  
## <a name="example"></a>例  
 次のコード例は、空間インデックスを使用できるニアレスト ネイバー クエリを示します。 次の例では、 `Person.Address` データベースにある `AdventureWorks2012` テーブルを使用しています。  
  
```  
USE AdventureWorks2012  
GO  
DECLARE @g geography = 'POINT(-121.626 47.8315)';  
SELECT TOP(7) SpatialLocation.ToString(), City FROM Person.Address  
WHERE SpatialLocation.STDistance(@g) IS NOT NULL  
ORDER BY SpatialLocation.STDistance(@g);  
  
```  
  
 列 SpatialLocation にインデックスを作成して、ニアレスト ネイバー クエリが空間インデックスを使用する方法を確認します。 空間インデックスの作成の詳細については、「 [Create, Modify, and Drop Spatial Indexes](create-modify-and-drop-spatial-indexes.md)」を参照してください。  
  
## <a name="example"></a>例  
 次のコード例は、空間インデックスを使用できないニアレスト ネイバー クエリを示します。  
  
```  
USE AdventureWorks2012  
GO  
DECLARE @g geography = 'POINT(-121.626 47.8315)';  
SELECT TOP(7) SpatialLocation.ToString(), City FROM Person.Address  
ORDER BY SpatialLocation.STDistance(@g);  
  
```  
  
 このクエリは、構文で指定した形式の `STDistance()` を使用する `WHERE` 句がないため、空間インデックスを使用できません。  
  
## <a name="see-also"></a>参照  
 [空間データ &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
