---
title: RANK を使用して検索結果を制限する方法 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- row ranking [full-text search]
- relevance ranking values [full-text search]
- full-text search [SQL Server], rankings
- index rankings [full-text search]
- ranked results [full-text search]
- rankings [full-text search]
- per-row rank values [full-text search]
ms.assetid: 06a776e6-296c-4ec7-9fa5-0794709ccb17
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7740c95e40b4902e88d1ae5f632b34c7f759f441
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132283"
---
# <a name="limit-search-results-with-rank"></a>RANK を使用して検索結果を制限する方法
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 関数と [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) 関数は、0 ～ 1000 の序数値 (順位値) を含む "RANK" 列を返します。 これらの値を使用すれば、選択基準への適合度合いに応じて、返された行に順位を付けることができます。 この順位値が示しているのは、結果セット内の各行の単なる相対順位であり、値が小さいほど関連性は低くなります。 実際の値は重要ではなく、通常はクエリが実行されるたびに変わります。  
  
> [!NOTE]  
>  CONTAINS 述語と FREETEXT 述語は順位値を返しません。  
  
 検索条件と一致するアイテムの数が膨大になることがよくあります。 CONTAINSTABLE クエリまたは FREETEXTTABLE クエリから多数の一致結果が返されないようにするには、オプションの *top_n_by_rank* パラメーターを使用して、返される行を制限します。 *top_n_by_rank* は整数値です。 *n*は、降順で上位 *n* 個の一致結果のみを返すことを示します。 *top_n_by_rank* を他のパラメーターと組み合わせた場合、クエリから返される行数は、実際にすべての述語に一致する行数より少なくなります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、一致結果を順位で並べ替え、指定された数の行のみを返します。 このオプションを使用すると、パフォーマンスが大幅に向上します。 たとえば、通常ならば 100 万行のテーブルから 10 万行を返すクエリに対して、上位 100 行だけを返すように要求すれば、そのクエリの処理が速くなります。  
  
##  <a name="examples"></a> RANK を使用して検索結果を制限する例  
  
### <a name="example-a-searching-for-only-the-top-three-matches"></a>例 A:上位 3 件の一致結果のみを検索する  
 次の例では、CONTAINSTABLE を使用して上位 3 件の一致結果のみを返します。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT K.RANK, AddressLine1, City  
FROM Person.Address AS A  
  INNER JOIN  
  CONTAINSTABLE(Person.Address, AddressLine1, 'ISABOUT ("des*",  
    Rue WEIGHT(0.5),  
    Bouchers WEIGHT(0.9))',  
    3) AS K  
  ON A.AddressID = K.[KEY]  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
RANK        Address                          City  
----------- -------------------------------- ------------------------------  
172         9005, rue des Bouchers           Paris  
172         5, rue des Bouchers              Orleans  
172         5, rue des Bouchers              Metz  
  
(3 row(s) affected)  
```  
  
  
### <a name="example-b-searching-for-the-top-ten-matches"></a>例 B:上位 10 件の一致結果を検索する  
 次の例では、CONTAINSTABLE を使用して、 `Description` 列内で "light" または "lightweight" という単語の近くに "aluminum" という語句を含んでいる、上位 5 種の製品の説明を返します。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)',  
      5  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
GO  
```  
  
  
##  <a name="how"></a> 検索クエリの結果が順位付けされる方法  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のフルテキスト検索では、フルテキスト クエリが返すデータの関連性を示す省略可能なスコア (順位値) を生成できます。 この順位値は 1 行ごとに計算され、クエリの結果セットを関連性に従って並べ替える順序付け基準として使用できます。 順位値は、単に、結果セット内の各行の相対的な関連順位を示します。 実際の値は重要ではなく、通常はクエリが実行されるたびに変わります。 順位値は、他のクエリでは意味を持ちません。  
  
### <a name="statistics-for-ranking"></a>順位付けの統計  
 順位付けに使用する統計はインデックス作成時に収集されます。 フルテキスト カタログの作成処理で、単一のインデックス構造が直接作成されるわけではありません。 代わりに、データにインデックスが作成されたとき、Full-Text Engine for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって中間インデックスが作成されます。 その後、Full-Text Engine は必要に応じてこれらのインデックスをより大きなインデックスにマージします。 この処理は何度も繰り返される場合があります。 次に、Full-Text Engine は "マスター マージ" と呼ばれる処理を行います。この処理では、すべての中間インデックスが 1 つの巨大なインデックスに結合されます。  
  
 統計は各中間インデックス レベルで収集されます。 インデックスがマージされると、統計もマージされます。 マスターのマージ処理中にのみ生成される統計もあります。  
  
 クエリの結果セットの順位付けを行う際に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では最も大きい中間インデックスの統計が使用されます。 これは、中間インデックスがマージされているかどうかで決まります。 したがって、中間インデックスがマージされていない場合、順位付けの統計の精度にばらつきが生じることがあります。 時間が経つにつれて同じクエリが異なる順位結果を返すことがあるのは、フルテキスト インデックス データの追加、変更、および削除が行われ、小さなインデックスがマージされていくためです。  
  
 インデックスのサイズを最小化し、計算を容易にするために、統計はしばしば丸められます。  
  
 共通に使用される用語と順位の計算に必要な統計値を以下の表に示します。  
  
 プロパティ  
 行の中でフルテキスト インデックスが付けられた列です。  
  
 ドキュメント  
 クエリで返されるエンティティです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では行に相当します。 1 つの行にフルテキスト インデックスが付いた列が複数含まれるのと同様に、1 つのドキュメントには複数のプロパティが含まれる場合があります。  
  
 インデックス  
 1 つまたは複数のドキュメントの単一の逆インデックスです。 インデックスはすべてメモリまたはディスクに格納されています。 クエリ統計の多くは、一致した個々のインデックスと関連しています。  
  
 フルテキスト カタログ  
 クエリで 1 つのエンティティとして扱われる中間インデックスのコレクションです。 カタログは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理者に対して表示される組織の単位です。  
  
 語、トークン、またはアイテム  
 フルテキスト エンジンの一致単位です。 ドキュメントからのテキスト ストリームは、言語固有のワード ブレーカーによって語またはトークンにトークン化されます。  
  
 個数  
 ワード ブレーカーによって決定されるドキュメント プロパティのワード オフセットです。 最初のワードはオカレンス 1、次のワードはオカレンス 2 というように、それ以降順番に番号が付けられます。 語句クエリおよび近接クエリで誤った判断を行わないように、文と段落の末尾にはより大きな間隔値のオカレンスが使用されます。  
  
 TermFrequency  
 行におけるキー値の出現回数です。  
  
 IndexedRowCount  
 インデックスが付けられた合計行数です。 この値は、中間インデックスに保持されている数を基にして計算されます。 この数の精度にはばらつきがあります。  
  
 KeyRowCount  
 指定されたキーを格納するフルテキスト カタログの合計行数です。  
  
 MaxOccurrence  
 行内の指定したプロパティでフルテキスト カタログに保存された最大オカレンスです。  
  
 MaxQueryRank  
 Full-Text Engine が返す最大順位 (1,000) です。  
  
  
### <a name="rank-computation-issues"></a>順位計算に関する問題点  
 順位の計算処理はさまざまな要因に依存します。  ワード ブレーカーの言語が異なると、テキストをトークン化する方法も異なります。 たとえば、あるワード ブレーカーは "dog-house" という文字列を "dog" "house" に分割しますが、別のワード ブレーカーは "dog-house" に分割します。 これは、指定された言語によって一致および順位が異なるということを意味します。単語だけでなく、ドキュメント長も異なるからです。 ドキュメント長の違いは、クエリすべての順位付けに影響します。  
  
 **IndexRowCount** などの統計は大きく異なる場合があります。 たとえば、カタログのマスター インデックスに 20 億の行が格納されている場合、1 つの新規ドキュメントにメモリ内で中間インデックスが作成され、そのメモリ内インデックスのドキュメント数に基づいてドキュメントが順位付けされると、マスター インデックスのドキュメントの順位と整合性のない結果になる可能性があります。 こうした理由から、任意の作成処理により大量の行がインデックス化または再インデックス化された場合は、ALTER FULLTEXT CATALOG ... REORGANIZE [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用してこれらのインデックスをマスター インデックスにマージすることを推奨します。 また、中間インデックスの数やサイズなどのパラメーターを基に、Full-Text Engine によるインデックスのマージも自動的に実行されます。  
  
 **MaxOccurrence** の値は 1 ～ 32 の範囲のいずれかに正規化されます。 これは、たとえば 50 語のドキュメントが 100 語のドキュメントと同様に扱われるということを意味します。 正規化に使用される表を以下に示します。 これらのドキュメント長は以下の表の 32 と 128 の間にあるため、実際には同じドキュメント長 (128) として扱われます (32 < **docLength** <= 128)。  
  
```  
{ 16, 32, 128, 256, 512, 725, 1024, 1450, 2048, 2896, 4096, 5792, 8192, 11585,   
16384, 23170, 28000, 32768, 39554, 46340, 55938, 65536, 92681, 131072, 185363,   
262144, 370727, 524288, 741455, 1048576, 2097152, 4194304 };  
  
```  
  
  
### <a name="ranking-of-containstable"></a>CONTAINSTABLE の順位付け  
 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) の順位付けでは次のアルゴリズムを使用します。  
  
```  
StatisticalWeight = Log2( ( 2 + IndexedRowCount ) / KeyRowCount )  
Rank = min( MaxQueryRank, HitCount * 16 * StatisticalWeight / MaxOccurrence )  
```  
  
 句の一致は個々のキーと同様に順位付けされます。ただし、 **KeyRowCount** (句を含む行数) には予測値が使用され、不正確で実際の値よりも大きくなる可能性があります。  
  
 **NEAR の順位付け**  
  
 CONTAINSTABLE では、NEAR オプションを使用することで、相互に近接する 2 つ以上の検索語句に対するクエリをサポートしています。 返される各行の順位値は、いくつかのパラメーターに基づいています。 順位付けの主な要因の 1 つは、ドキュメントの長さに関連した一致の合計数 ( *ヒット*) です。 したがって、たとえば、100 語のドキュメントと 900 語のドキュメントに同一の一致が含まれている場合は、100 語のドキュメントの方が順位が高くなります。  
  
 行における各ヒットの合計の長さも、そのヒットの最初と最後の検索語句の間の距離に基づいてその行の順位に影響を与えます。 距離が小さいほど、ヒットは行の順位値に大きく影響します フルテキスト クエリで最大距離の整数が指定されていない場合、論理語の間隔が 100 を超えるヒットのみが含まれるドキュメントは、その順位が 0 になります。  
  
 **ISABOUT の順位付け**  
  
 CONTAINSTABLE は、ISABOUT オプションを指定した重み付け語句のクエリをサポートします。 ISABOUT は、従来の情報検索用語で言うところのベクトル空間クエリです。 既定の順位付けアルゴリズムには、Jaccard という一般的に知られている公式が使用されます。 クエリ内の用語ごとに順位付けが計算され、以下に示す方法で各順位付けが結合されます。  
  
```  
ContainsRank = same formula used for CONTAINSTABLE ranking of a single term (above).  
Weight = the weight specified in the query for each term. Default weight is 1.  
WeightedSum = Σ[key=1 to n] ContainsRankKey * WeightKey  
Rank =  ( MaxQueryRank * WeightedSum ) / ( ( Σ[key=1 to n] ContainsRankKey^2 )   
      + ( Σ[key=1 to n] WeightKey^2 ) - ( WeightedSum ) )  
  
```  
  
  
### <a name="ranking-of-freetexttable"></a>FREETEXTTABLE の順位付け  
 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) の順位付けは、OKAPI BM25 という公式を使用して計算されます。 FREETEXTTABLE クエリは屈折生成 (クエリに含まれる元の単語の変化形生成) を行って単語をクエリに追加します。これらの単語は別々の単語として扱われ、生成元の単語とは特に関連を持ちません。 シソーラス機能によって生成されたシノニムは、同等に重み付けされた別々の用語として扱われます。 クエリ内の各単語が順位の要素となります。  
  
```  
Rank = Σ[Terms in Query] w ( ( ( k1 + 1 ) tf ) / ( K + tf ) ) * ( ( k3 + 1 ) qtf / ( k3 + qtf ) ) )  
Where:   
w is the Robertson-Sparck Jones weight.   
In simplified form, w is defined as:   
w = log10 ( ( ( r + 0.5 ) * ( N - R + r + 0.5 ) ) / ( ( R - r + 0.5 ) * ( n - r + 0.5 ) )  
N is the number of indexed rows for the property being queried.   
n is the number of rows containing the word.   
K is ( k1 * ( ( 1 - b ) + ( b * dl / avdl ) ) ).   
dl is the property length, in word occurrences.   
avdl is the average length of the property being queried, in word occurrences.   
k1, b, and k3 are the constants 1.2, 0.75, and 8.0, respectively.   
tf is the frequency of the word in the queried property in a specific row.   
qtf is the frequency of the term in the query.   
```  
  
  
## <a name="see-also"></a>参照  
 [フルテキスト検索でのクエリ](../../relational-databases/search/query-with-full-text-search.md)  
  
  
