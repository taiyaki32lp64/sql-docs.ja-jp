---
title: 最短パス (SQL グラフ) |Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
f1_keywords:
- SHORTEST PATH
- SHORTEST_PATH
dev_langs:
- TSQL
helpviewer_keywords:
- MATCH statement [SQL Server], SQL graph
- SQL graph, MATCH statement
author: shkale-msft
ms.author: shkale
monikerRange: =azuresqldb-current||>=sql-server-ver15||=sqlallproducts-allversions||=azuresqldb-mi-current
ms.openlocfilehash: 9318a34b4853937983b107491c9210de80e5506c
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056399"
---
# <a name="shortest_path-transact-sql"></a>SHORTEST_PATH (Transact-sql)
[!INCLUDE[tsql-appliesto-ssver2015-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  再帰的または繰り返し検索されるグラフの検索条件を指定します。 SHORTEST_PATH は、SELECT ステートメント内のグラフノードとエッジテーブルとの一致内部で使用できます。 
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="shortest-path"></a>最短パス
SHORTEST_PATH 関数を使用すると、次のことを確認できます。    
* 指定された2つのノードまたはエンティティ間の最短パス
* 単一ソースの最短パス。
* 複数のソースノードから複数のターゲットノードへの最短パス。

任意の長さのパターンを入力として受け取り、2つのノード間に存在する最短のパスを返します。 この関数は、MATCH 内でのみ使用できます。 関数は、指定された2つのノード間の最短パスを1つだけ返します。 ソースノードと宛先ノードのペアの間に、同じ長さの2つ以上の最短パスが存在する場合、関数は、走査中に最初に見つかったパスを1つだけ返します。 任意の長さのパターンを SHORTEST_PATH 関数内でのみ指定できることに注意してください。 

構文については、 [「MATCH (SQL グラフ)](../../t-sql/queries/match-sql-graph.md) 」を参照してください。 

## <a name="for-path"></a>パスの
FOR PATH は、任意の長さのパターンに参加する FROM 句の任意のノードまたはエッジテーブルの名前と共に使用する必要があります。 PATH の場合、ノードまたはエッジテーブルが走査されたパスに沿って見つかったノードまたはエッジのリストを表す順序付けられたコレクションを返すことをエンジンに指示します。 これらのテーブルの属性は、SELECT 句で直接射影することはできません。 これらのテーブルから属性を射影するには、グラフパスの集計関数を使用する必要があります。  

## <a name="arbitrary-length-pattern"></a>任意の長さのパターン
このパターンには、目的のノードに到達するまで、またはパターンで指定された反復処理の最大数が満たされるまで繰り返し走査する必要があるノードとエッジが含まれます。 クエリが実行されるたびに、このパターンを実行した結果は、開始ノードから終了ノードまでのパスに沿って走査されたノードとエッジの順序付けられたコレクションになります。 これは正規表現形式の構文パターンであり、次の2つのパターンの量指定子がサポートされています。

* **' + '** : パターンを1回以上繰り返します。 最短パスが見つかったらすぐに終了します。
* **{1, n}** : パターン1を ' n ' 回繰り返します。 最短のが見つかるとすぐに終了します。

## <a name="last_node"></a>LAST_NODE
LAST_NODE () 関数を使用すると、2つの任意の長さのトラバーサルパターンを連結できます。 次のようなシナリオで使用できます。    
* クエリでは、複数の最短パスパターンが使用され、1つのパターンは前のパターンの最後のノードから始まります。
* 2つの最短パスパターンが同じ LAST_NODE () にマージされます。

## <a name="graph-path-order"></a>グラフのパスの順序
グラフパスの順序とは、出力パス内のデータの順序を指します。 出力パスの順序は、常にパターンの非再帰部分から開始され、再帰部分に出現するノード/エッジが続きます。 クエリの最適化または実行中にグラフがスキャンされる順序は、出力に出力された順序とは関係ありません。 同様に、再帰パターンの矢印の方向も、グラフパスの順序には影響しません。 

## <a name="graph-path-aggregate-functions"></a>グラフパスの集計関数
任意の長さのパターンに関係するノードとエッジによってコレクション (そのパスでスキャンされたノードとエッジ) が返されるため、ユーザーは従来の attributename 構文を使用して直接属性を射影することはできません。 中間ノードまたはエッジテーブルから属性値を射影する必要があるクエリの場合、走査されるパスで、STRING_AGG、LAST_VALUE、SUM、AVG、MIN、MAX、COUNT の各グラフパスの集計関数を使用します。 SELECT 句でこれらの集計関数を使用するための一般的な構文は次のとおりです。

```
<GRAPH_PATH_AGGREGATE_FUNCTION>(<expression> , <separator>)  <order_clause>

    <order_clause> ::=
        { WITHIN GROUP (GRAPH PATH) }

    <GRAPH_PATH_AGGREGATE_FUNCTION> ::=
          STRING_AGG
        | LAST_VALUE
        | SUM
        | COUNT
        | AVG
        | MIN
        | MAX

```

### <a name="string_agg"></a>STRING_AGG
STRING_AGG 関数は、式と区切り記号を入力として受け取り、文字列を返します。 ユーザーは、選択句でこの関数を使用して、走査されたパスの中間ノードまたはエッジから属性を射影することができます。 

### <a name="last_value"></a>LAST_VALUE
走査されたパスの最後のノードから属性を射影するために、LAST_VALUE 集計関数を使用できます。 この関数への入力としてエッジテーブルの別名を指定するとエラーになります。使用できるのは、ノードのテーブル名または別名だけです。

**最後のノード**: 最後のノードは、一致述語の矢印の方向に関係なく、走査されたパスの最後に表示されるノードを参照します。 たとえば、 `MATCH(SHORTEST_PATH(n(-(e)->p)+) )`のようにします。 ここで、パスの最後のノードが最後にアクセスした P ノードになります。 

一方、最後のノードは、このパターンの出力グラフパスの最後の n 番目のノードです。 `MATCH(SHORTEST_PATH((n<-(e)-)+p))`    

### <a name="sum"></a>[SUM]
この関数は、指定されたノード/エッジ属性値またはスキャンされたパスに出現する式の合計を返します。

### <a name="count"></a>[COUNT]
この関数は、パス内の必要なノード/エッジ属性の null 以外の値の数を返します。 COUNT 関数では、ノードまたはエッジテーブルの別名を持つ '\*' 演算子がサポートされています。 ノードまたはエッジテーブルの別名がない場合、\* の使用法があいまいになり、エラーが発生します。

    {  COUNT( <expression> | <node_or_edge_alias>.* )  <order_clause>  }


### <a name="avg"></a>AVG
指定されたノード/エッジ属性値またはスキャンされたパスに出現する式の平均を返します。

### <a name="min"></a>[MIN]
指定されたノード/エッジ属性値またはスキャンパスに出現する式からの最小値を返します。

### <a name="max"></a>[MAX]
指定されたノード/エッジ属性値、またはスキャンされたパスに出現する式から最大値を返します。

## <a name="remarks"></a>Remarks  
shortest_path 関数は、MATCH 内でのみ使用できます。     
LAST_NODE は shortest_path 内でのみサポートされます。     
重み付けされた最短パス、すべてのパス、またはすべての最短パスを検索することはできません。         
場合によっては、ホップ数が多いクエリに対して不適切なプランが生成され、クエリの実行時間が長くなります。 ハッシュ結合ヒントを使用すると役立つ場合があります。    


## <a name="examples"></a>使用例 
ここに示したクエリの例では、 [SQL Graph サンプル](./sql-graph-sample.md)で作成したノードテーブルとエッジテーブルを使用します。

### <a name="a--find-shortest-path-between-2-people"></a>A.  2つのメンバーの間の最短パスを検索する
 次の例では、Jacob と Alice の間の最短のパスを見つけます。 Graph サンプルスクリプトから作成された Person ノードと FriendOf edge が必要になります。 

 ```
SELECT PersonName, Friends
FROM (  
    SELECT
        Person1.name AS PersonName, 
        STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends,
        LAST_VALUE(Person2.name) WITHIN GROUP (GRAPH PATH) AS LastNode
    FROM
        Person AS Person1,
        friendOf FOR PATH AS fo,
        Person FOR PATH  AS Person2
    WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2)+))
    AND Person1.name = 'Jacob'
) AS Q
WHERE Q.LastNode = 'Alice'
 ```

 ### <a name="b--find-shortest-path-from-a-given-node-to-all-other-nodes-in-the-graph"></a>b.  指定されたノードからグラフ内の他のすべてのノードまでの最短パスを検索します。 
 次の例では、グラフ内の Jacob が接続されているすべてのユーザーと、Jacob からすべてのユーザーを対象とする最短パスを検索します。 

 ```
SELECT
    Person1.name AS PersonName, 
    STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends
FROM
    Person AS Person1,
    friendOf FOR PATH AS fo,
    Person FOR PATH  AS Person2
WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2)+))
AND Person1.name = 'Jacob'
 ```

### <a name="c--count-the-number-of-hopslevels-traversed-to-go-from-one-person-to-another-in-the-graph"></a>C.  グラフ内で1人のユーザーから別のユーザーに送られるホップ数またはレベル数をカウントします。
 次の例では、Jacob と Alice の間の最短パスを検索し、Jacob から Alice に移動するために必要なホップ数を出力します。 

 ```
 SELECT PersonName, Friends, levels
FROM (  
    SELECT
        Person1.name AS PersonName, 
        STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends,
        LAST_VALUE(Person2.name) WITHIN GROUP (GRAPH PATH) AS LastNode,
        COUNT(Person2.name) WITHIN GROUP (GRAPH PATH) AS levels
    FROM
        Person AS Person1,
        friendOf FOR PATH AS fo,
        Person FOR PATH  AS Person2
    WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2)+))
    AND Person1.name = 'Jacob'
) AS Q
WHERE Q.LastNode = 'Alice'
 ```

### <a name="d-find-people-1-3-hops-away-from-a-given-person"></a>D. 特定のユーザーからの1-3 のホップを検索する
次の例では、Jacob と、その接続先であるすべての人の間の最短のパスを、グラフ1-3 のホップから離れた場所に検索します。 

```
SELECT
    Person1.name AS PersonName, 
    STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends
FROM
    Person AS Person1,
    friendOf FOR PATH AS fo,
    Person FOR PATH  AS Person2
WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2){1,3}))
AND Person1.name = 'Jacob'
```

### <a name="e-find-people-exactly-2-hops-away-from-a-given-person"></a>E. 特定のユーザーからのホップが2人だけ離れている人を検索する
次の例では、Jacob の間の最短のパスと、そのグラフ内のホップが2人以上離れている人を検索します。 

```
SELECT PersonName, Friends
FROM (
    SELECT
        Person1.name AS PersonName, 
        STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends,
        COUNT(Person2.name) WITHIN GROUP (GRAPH PATH) AS levels
    FROM
        Person AS Person1,
        friendOf FOR PATH AS fo,
        Person FOR PATH  AS Person2
    WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2){1,3}))
    AND Person1.name = 'Jacob'
) Q
WHERE Q.levels = 2
```

## <a name="see-also"></a>参照  
 [MATCH (SQL グラフ)](../../t-sql/queries/match-sql-graph.md)    
 [CREATE TABLE &#40;SQL グラフ&#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [INSERT (SQL グラフ)](../../t-sql/statements/insert-sql-graph.md)  
 [SQL Server 2017 でのグラフ処理](../../relational-databases/graphs/sql-graph-overview.md)     
 
