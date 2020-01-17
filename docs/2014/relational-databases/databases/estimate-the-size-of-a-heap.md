---
title: ヒープ サイズの見積もり | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- disk space [SQL Server], indexes
- estimating heap size
- size [SQL Server], heap
- space [SQL Server], indexes
- heaps
ms.assetid: 81fd5ec9-ce0f-4c2c-8ba0-6c483cea6c75
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 80ba5505204f592ef04c939b3e84b6f3ca3c7c89
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62916746"
---
# <a name="estimate-the-size-of-a-heap"></a>ヒープ サイズの見積もり
  ヒープにデータを格納するために必要な領域は、次の手順で見積もることができます。  
  
1.  次のように、テーブル内の行数を指定します。  
  
     ***Num_Rows***  = テーブル内の行数  
  
2.  次のように、固定長列と可変長列の数を指定し、それらの列を格納するために必要な領域を計算します。  
  
     固定長列のグループと可変長列のグループがデータ行内で使用する領域を計算します。 列のサイズは、データ型と長さの指定によって異なります。  
  
     ***Num_Cols***  = 列 (固定長および可変長) の総数  
  
     ***Fixed_Data_Size***  = すべての固定長列の合計バイト サイズ  
  
     ***Num_Variable_Cols***  = 可変長列の数  
  
     ***Max_Var_Size***  = すべての可変長列の最大合計バイト サイズ  
  
3.  NULL ビットマップと呼ばれる行の部分は、列の NULL 値の許容を管理するために予約されています。 このサイズは次のように計算します。  
  
     ***Null_Bitmap***  = 2 + ((***Num_Cols*** + 7) / 8)  
  
     この式の計算結果は、整数部分だけを使用します。 小数部分は無視してください。  
  
4.  次の式で、可変長のデータ サイズを計算します。  
  
     テーブル内に可変長列が存在する場合、次の式を使用して、行内でそれらの列を格納するために使用する領域を計算します。  
  
     ***Variable_Data_Size***  = 2 + (***Num_Variable_Cols*** x 2) + ***Max_Var_Size***  
  
     ***Max_Var_Size*** に追加されたバイトは、それぞれの可変長列を追跡するためのものです。 この式は、すべての可変長列がいっぱいになることを前提としています。 可変長列の格納領域の使用率が 100% 以下になることが予想される場合、その使用率に基づいて ***Max_Var_Size*** の値を調整し、テーブルの全体サイズをより正確に見積もることができます。  
  
    > [!NOTE]  
    >  定義済みのテーブルの合計サイズが 8,060 バイトを超える `varchar`、`nvarchar`、`varbinary`、または `sql_variant` 列の連結が可能です。 これらの列のそれぞれの長さ 8,000 バイトの制限内に収まる必要があります、 `varchar`、 `nvarchar,``varbinary`、または`sql_variant`列。 ただし、これらの列を連結したサイズは、テーブルの制限である 8,060 バイトを超過してもかまいません。  
  
     可変長列が存在しない場合は、 ***Variable_Data_Size*** に 0 を設定します。  
  
5.  次の式で行サイズの合計を計算します。  
  
     ***Row_Size***  = ***Fixed_Data_Size*** + ***Variable_Data_Size*** + ***Null_Bitmap*** + 4  
  
     上記の式の 4 という値は、データ行の行ヘッダー オーバーヘッドです。  
  
6.  次の式で、1 ページあたりの行数を計算します (1 ページあたりの空きバイト数は 8,096 です)。  
  
     ***Rows_Per_Page***  = 8096 / (***Row_Size*** + 2)  
  
     行は複数のページにまたがらないので、計算結果の端数は切り捨ててください。 上記の式の 2 という値は、ページのスロット配列内の行のエントリのためのものです。  
  
7.  次の式で、すべての行を格納するために必要なページ数を計算します。  
  
     ***Num_Pages***  = ***Num_Rows*** / ***Rows_Per_Page***  
  
     算出したページ数の端数は切り上げてください。  
  
8.  次の式で、ヒープにデータを格納するために必要な領域を計算します (1 ページあたりの総バイト数は 8,192 です)。  
  
     ヒープのサイズ (バイト) = 8192 x ***Num_Pages***  
  
 この計算では、次のことは考慮されていません。  
  
-   [パーティション分割]  
  
     パーティション分割による領域のオーバーヘッドはわずかですが、計算が複雑になります。 これは、計算に含めるほど重要なことではありません。  
  
-   アロケーション ページ  
  
     ヒープに割り当てられたページの追跡に使用する IAM ページが少なくとも 1 ページありますが、使用される IAM ページ数を正確に計算できるアルゴリズムはなく、領域のオーバーヘッドはわずかです。  
  
-   ラージ オブジェクト (LOB) の値  
  
     LOB データ型を格納する領域の量を使用する正確に特定するアルゴリズム`varchar(max)`、 `varbinary(max)`、 `nvarchar(max)`、 `text`、 **ntextxml**、および`image`値は複雑です。 LOB データ型の値で使用される領域の計算は、予想される LOB 値の平均サイズを合計し、ヒープの合計サイズに加算するだけで十分です。  
  
-   圧縮  
  
     圧縮されたヒープのサイズを事前に計算することはできません。  
  
-   スパース列  
  
     スパース列の領域要件については、「 [スパース列の使用](../tables/use-sparse-columns.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [ヒープ &#40;クラスター化インデックスなしのテーブル&#41;](../indexes/heaps-tables-without-clustered-indexes.md)   
 [クラスター化インデックスと非クラスター化インデックスの概念](../indexes/clustered-and-nonclustered-indexes-described.md)   
 [クラスター化インデックスの作成](../indexes/create-clustered-indexes.md)   
 [非クラスター化インデックスの作成](../indexes/create-nonclustered-indexes.md)   
 [テーブル サイズの見積もり](estimate-the-size-of-a-table.md)   
 [クラスター化インデックスのサイズの見積もり](estimate-the-size-of-a-clustered-index.md)   
 [非クラスター化インデックスのサイズの算出](estimate-the-size-of-a-nonclustered-index.md)   
 [データベース サイズの見積もり](estimate-the-size-of-a-database.md)  
  
  
