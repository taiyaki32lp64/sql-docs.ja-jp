---
title: クラスター化インデックスのサイズの見積もり | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- space allocation [SQL Server], index size
- size [SQL Server], tables
- disk space [SQL Server], indexes
- predicting table size [SQL Server]
- table size [SQL Server]
- estimating table size
- space [SQL Server], indexes
- clustered indexes, table size
- nonclustered indexes [SQL Server], table size
- designing databases [SQL Server], estimating size
- calculating table size
ms.assetid: 2b5137f8-98ad-46b5-9aae-4c980259bf8d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fe7b988590de54a3cb02aa540b244e1f56f3ba24
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054130"
---
# <a name="estimate-the-size-of-a-clustered-index"></a>クラスター化インデックスのサイズの見積もり
  クラスター化インデックスにデータを格納するために必要な領域を見積もるには、次の手順を実行します。  
  
1.  クラスター化インデックスのリーフ レベルにデータを格納するために使用する領域を計算します。  
  
2.  クラスター化インデックスのインデックス情報を格納するために使用する領域を計算します。  
  
3.  計算した値を合計します。  
  
## <a name="step-1-calculate-the-space-used-to-store-data-in-the-leaf-level"></a>手順 1. リーフ レベルにデータを格納するために使用する領域を計算する  
  
1.  次のように、テーブル内の行数を指定します。  
  
     ***Num_Rows***  = テーブル内の行数  
  
2.  次のように、固定長列と可変長列の数を指定し、それらの列を格納するために必要な領域を計算します。  
  
     固定長列のグループと可変長列のグループがデータ行内で使用する領域を計算します。 列のサイズは、データ型と長さの指定によって異なります。  
  
     ***Num_Cols***  = 列 (固定長および可変長) の総数  
  
     ***Fixed_Data_Size***  = すべての固定長列の合計バイト サイズ  
  
     ***Num_Variable_Cols***  = 可変長列の数  
  
     ***Max_Var_Size***  = すべての可変長列の最大バイト サイズ  
  
3.  クラスター化インデックスが一意でない場合、次のように *uniqueifier* 列を計上します。  
  
     uniqueifier とは、NULL 値が許容された可変長列です。 一意でないキー値を含む行では、uniqueifier は NULL 値を許容しない 4 バイトの列になります。 この値はインデックス キーの一部で、すべての行に一意のキー値が含まれるようにするために必要です。  
  
     ***Num_Cols***  = ***Num_Cols*** + 1  
  
     ***Num_Variable_Cols***  = ***Num_Variable_Cols*** + 1  
  
     ***Max_Var_Size***  = ***Max_Var_Size*** + 4  
  
     このような変更は、すべての値が一意でなくなることを想定しています。  
  
4.  NULL ビットマップと呼ばれる行の部分は、列の NULL 値の許容を管理するために予約されています。 このサイズは次のように計算します。  
  
     ***Null_Bitmap***  = 2 + ((***Num_Cols*** + 7) / 8)  
  
     上記の式の計算結果の整数部分だけを使用し、小数部分は無視してください。  
  
5.  次の式で、可変長のデータ サイズを計算します。  
  
     テーブル内に可変長列が存在する場合、次の式を使用して、行内でそれらの列を格納するために使用する領域を計算します。  
  
     ***Variable_Data_Size***  = 2 + (***Num_Variable_Cols*** x 2) + ***Max_Var_Size***  
  
     ***Max_Var_Size*** に追加されたバイトは、それぞれの可変長列を追跡するためのものです。 この式は、すべての可変長列がいっぱいになることを前提としています。 可変長列の格納領域の使用率が 100% 以下になることが予想される場合、その使用率に基づいて ***Max_Var_Size*** の値を調整し、テーブルの全体サイズをより正確に見積もることができます。  
  
    > [!NOTE]  
    >  定義済みのテーブルの合計サイズが 8,060 バイトを超える `varchar`、`nvarchar`、`varbinary`、または `sql_variant` 列の連結が可能です。 この場合も、`varchar`、`varbinary`、または `sql_variant` 列の場合は 8,000 バイト、`nvarchar` 列の場合は 4,000 バイトの制限内に、各列のサイズを収める必要があります。 ただし、これらの列を連結したサイズは、テーブルの制限である 8,060 バイトを超過してもかまいません。  
  
     可変長列が存在しない場合は、 ***Variable_Data_Size*** に 0 を設定します。  
  
6.  次の式で行サイズの合計を計算します。  
  
     ***Row_Size***  = ***Fixed_Data_Size*** + ***Variable_Data_Size*** + ***Null_Bitmap*** + 4  
  
     4 という値は、データ行の行ヘッダー オーバーヘッドです。  
  
7.  次の式で、1 ページあたりの行数を計算します (1 ページあたりの空きバイト数は 8,096 です)。  
  
     ***Rows_Per_Page***  = 8096 / (***Row_Size*** + 2)  
  
     行は複数のページにまたがらないので、計算結果の端数は切り捨ててください。 上記の式の 2 という値は、ページのスロット配列内の行のエントリのためのものです。  
  
8.  指定した [FILL FACTOR](../indexes/specify-fill-factor-for-an-index.md) に基づいて、1 ページあたりの予約済みの空き行数を次の式で計算します。  
  
     ***Free_Rows_Per_Page***  = 8096 x ((100 - ***Fill_Factor***) / 100) / (***Row_Size*** + 2)  
  
     計算で使用する FILL FACTOR は、パーセンテージではなく整数値です。 行は複数のページにまたがらないので、計算結果の端数は切り捨ててください。 FILL FACTOR の値が大きくなるほど、各ページに格納できるデータの量が多くなり、ページ数は少なくなります。 上記の式の 2 という値は、ページのスロット配列内の行のエントリのためのものです。  
  
9. 次の式で、すべての行を格納するために必要なページ数を計算します。  
  
     ***Num_Leaf_Pages***  = ***Num_Rows*** / (***Rows_Per_Page*** - ***Free_Rows_Per_Page***)  
  
     算出したページ数の端数は切り上げてください。  
  
10. 次の式で、リーフ レベルにデータを格納するために必要な領域を計算します (1 ページあたりの総バイト数は 8,192 です)。  
  
     ***Leaf_space_used***  = 8192 x ***Num_Leaf_Pages***  
  
## <a name="step-2-calculate-the-space-used-to-store-index-information"></a>手順 2. インデックス情報を格納するために使用する領域を計算する  
 次の手順を実行して、上位レベルのインデックスを格納するために必要な領域を見積もることができます。  
  
1.  次のように、インデックス キーの固定長列と可変長列の数を指定し、それらの列の格納に必要な領域を計算します。  
  
     インデックスのキー列には、固定長列と可変長列を含めることができます。 内部レベルのインデックス行サイズを見積もるには、これらの各列グループによってインデックス行内で占有される領域を計算します。 列のサイズは、データ型と長さの指定によって異なります。  
  
     ***Num_Key_Cols***  = キー列 (固定長および可変長) の総数  
  
     ***Fixed_Key_Size***  = すべての固定長キー列の合計バイト サイズ  
  
     ***Num_Variable_Key_Cols***  = 可変長キー列の数  
  
     ***Max_Var_Key_Size***  = すべての可変長キー列の最大バイト サイズ  
  
2.  インデックスが一意でない場合は、次のように uniqueifier をすべて計上します。  
  
     uniqueifier とは、NULL 値が許容された可変長列です。 一意でないインデックス キー値を含む行では、uniqueifier は NULL 値を許容しない 4 バイトの列になります。 この値はインデックス キーの一部で、すべての行に一意のキー値が含まれるようにするために必要です。  
  
     ***Num_Key_Cols***  = ***Num_Key_Cols*** + 1  
  
     ***Num_Variable_Key_Cols***  = ***Num_Variable_Key_Cols*** + 1  
  
     ***Max_Var_Key_Size***  = ***Max_Var_Key_Size*** + 4  
  
     このような変更は、すべての値が一意でなくなることを想定しています。  
  
3.  次のように、NULL ビットマップのサイズを計算します。  
  
     インデックス キー内に NULL 値を許容する列が存在する場合、インデックス行の部分は NULL ビットマップ用に予約されています。 このサイズは次のように計算します。  
  
     ***Index_Null_Bitmap***  = 2 + ((インデックス行の列数 + 7) / 8)  
  
     上記の式の計算結果は、整数部分だけを使用します。 小数部分は無視してください。  
  
     NULL 値を許容するキー列が存在しない場合は、 ***Index_Null_Bitmap*** を 0 に設定します。  
  
4.  次の式で、可変長のデータ サイズを計算します。  
  
     インデックス内に可変長列が存在する場合は、インデックス行内にそれらの列を格納するために使用する領域を次の式で計算します。  
  
     ***Variable_Key_Size***  = 2 + (***Num_Variable_Key_Cols*** x 2) + ***Max_Var_Key_Size***  
  
     ***Max_Var_Key_Size*** に追加されたバイトは、それぞれの可変長列を追跡するためのものです。 この式は、すべての可変長列がいっぱいになることを前提としています。 可変長列の格納領域の使用率が 100% 以下になることが予想される場合、その使用率に基づいて ***Max_Var_Key_Size*** の値を調整し、テーブルの全体サイズをより正確に見積もることができます。  
  
     可変長列が存在しない場合は、 ***Variable_Key_Size*** に 0 を設定します。  
  
5.  次の式でインデックス行のサイズを計算します。  
  
     ***Index_Row_Size***  = ***Fixed_Key_Size*** + ***Variable_Key_Size*** + ***Index_Null_Bitmap*** + 1 (インデックス行の行ヘッダー オーバーヘッド) + 6 (子ページ ID のポインター)  
  
6.  次の式で、1 ページあたりのインデックス行数を計算します (1 ページあたりの空きバイト数は 8,096 です)。  
  
     ***Index_Rows_Per_Page***  = 8096 / (***Index_Row_Size*** + 2)  
  
     インデックス行は複数のページにまたがらないため、計算結果の端数は切り捨ててください。 上の式の 2 という値は、ページのスロット配列内にある行の入力用です。  
  
7.  次の式で、インデックス内のレベル数を計算します。  
  
     ***Non-leaf_levels*** = 1 + ログ Index_Rows_Per_Page (***Num_Leaf_Pages*** / ***Index_Rows_Per_Page***)  
  
     この値を最も近い整数に切り上げます。 この値には、クラスター化インデックスのリーフ レベルは含まれません。  
  
8.  次の式で、インデックス内の非リーフ ページ数を計算します。  
  
     ***Num_Index_Pages =*** ∑Level ***(Num_Leaf_Pages/(Index_Rows_Per_Page***<sup>レベル</sup>***))***  
  
     ここで、1 <= Level <= ***Non-leaf_Levels***  
  
     それぞれの値を最も近い整数に切り上げます。 簡単な例として、 ***Num_Leaf_Pages*** = 1000、 ***Index_Rows_Per_Page*** = 25 のインデックスを例に取ります。 リーフ レベルより上位の最初のインデックス レベルでは、1000 行のインデックス行が格納されます。リーフ ページあたり 1 行のインデックス行で、1 ページあたり 25 行のインデックス行を納めることができます。 つまり、1,000 行のインデックス行を格納するために 40 ページが必要になります。 次のレベルのインデックスでは、40 行のインデックス行を格納する必要があります。 つまり、2 ページが必要になります。 最上位レベルのインデックスでは、2 行のインデックス行を格納する必要があります。 つまり、1 ページが必要になります。 その結果、非リーフ インデックス ページは 43 ページとなります。 このような数値を前の式で使用すると、次のような結果になります。  
  
     ***Non-leaf_levels*** = 1 + log25 (1000/25) = 3  
  
     ***Num_Index_Pages*** = 1000/(25<sup>3</sup>) + 1000/(25<sup>2</sup>) + 1000/(25<sup>1</sup>) = 1 + 2 + 40 = 43、これは、例で説明したページ数。  
  
9. 次の式で、インデックスのサイズを計算します (1 ページあたりの総バイト数は 8,192 です)。  
  
     ***Index_Space_Used***  = 8192 x ***Num_Index_Pages***  
  
## <a name="step-3-total-the-calculated-values"></a>手順 3. 計算した値を合計します。  
 次の式で、上記の 2 つの手順から取得した値を合計します。  
  
 クラスター化インデックス サイズ (バイト) = ***Leaf_Space_Used*** + ***Index_Space_used***  
  
 この計算では、次のことは考慮されていません。  
  
-   [パーティション分割]  
  
     パーティション分割による領域のオーバーヘッドはわずかですが、計算が複雑になります。 これは、計算に含めるほど重要なことではありません。  
  
-   アロケーション ページ  
  
     ヒープに割り当てられたページの追跡に使用する IAM ページが少なくとも 1 ページありますが、使用される IAM ページ数を正確に計算できるアルゴリズムはなく、領域のオーバーヘッドはわずかです。  
  
-   ラージ オブジェクト (LOB) の値  
  
     LOB データ型の `varchar(max)`、`varbinary(max)`、`nvarchar(max)`、`text`、`ntext`、`xml`、および `image` の値を格納するために使用される領域を正確に特定するのアルゴリズムは複雑です。 LOB データ型の値で使用される領域の計算は、必要な LOB 値の平均サイズを合計し、 ***Num_Rows***で乗算し、クラスター化インデックスの合計サイズに加算するだけで十分です。  
  
-   圧縮  
  
     圧縮されたインデックスのサイズを事前に計算することはできません。  
  
-   スパース列  
  
     スパース列の領域要件については、「 [スパース列の使用](../tables/use-sparse-columns.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [クラスター化インデックスと非クラスター化インデックスの概念](../indexes/clustered-and-nonclustered-indexes-described.md)   
 [テーブル サイズの見積もり](estimate-the-size-of-a-table.md)   
 [クラスター化インデックスの作成](../indexes/create-clustered-indexes.md)   
 [非クラスター化インデックスの作成](../indexes/create-nonclustered-indexes.md)   
 [非クラスター化インデックスのサイズの算出](estimate-the-size-of-a-nonclustered-index.md)   
 [ヒープ サイズの見積もり](estimate-the-size-of-a-heap.md)   
 [データベース サイズの見積もり](estimate-the-size-of-a-database.md)  
  
  
