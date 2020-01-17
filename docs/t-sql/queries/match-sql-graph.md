---
title: MATCH (SQL グラフ) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- MATCH
- MATCH_TSQL
- SHORTEST_PATH
dev_langs:
- TSQL
helpviewer_keywords:
- MATCH statement [SQL Server], SQL graph
- SQL graph, MATCH statement
- Shortest Path, shortest_path
author: shkale-msft
ms.author: shkale
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 40ce8094d651ee9ae1423b9c3feb636c33befca9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901952"
---
# <a name="match-transact-sql"></a>MATCH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

  グラフの検索条件を指定します。 MATCH は、WHERE 句の一部として、SELECT ステートメントでグラフ ノードとエッジのテーブルでのみ使用できます。 
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
MATCH (<graph_search_pattern>)

<graph_search_pattern>::=
  {  
      <simple_match_pattern> 
    | <arbitrary_length_match_pattern>  
    | <arbitrary_length_match_last_node_predicate> 
  }

<simple_match_pattern>::=
  {
      LAST_NODE(<node_alias>) | <node_alias>   { 
          { <-( <edge_alias> )- } 
        | { -( <edge_alias> )-> }
        <node_alias> | LAST(<node_alias>)
        } 
  }
  [ { AND } { ( <simple_match_pattern> ) } ]
  [ ,...n ]

<node_alias> ::=
  node_table_name | node_table_alias 

<edge_alias> ::=
  edge_table_name | edge_table_alias


<arbitrary_length_match_pattern>  ::=
  { 
    SHORTEST_PATH( 
      <arbitrary_length_pattern> 
      [ { AND } { <arbitrary_length_pattern> } ] 
      [ ,…n] 
    )
  } 

<arbitrary_length_match_last_node_predicate> ::=
  {  LAST_NODE( <node_alias> ) = LAST_NODE( <node_alias> ) }


<arbitrary_length_pattern> ::=
    {  LAST_NODE( <node_alias> )   | <node_alias>
     ( <edge_first_al_pattern> [<edge_first_al_pattern>…,n] )
     <al_pattern_quantifier> 
  }
    |  ( {<node_first_al_pattern> [<node_first_al_pattern> …,n] )
        <al_pattern_quantifier> 
        LAST_NODE( <node_alias> ) | <node_alias> 
 }
    
<edge_first_al_pattern> ::=
  { (  
        { -( <edge_alias> )->   } 
      | { <-( <edge_alias> )- } 
      <node_alias>
      ) 
  } 

<node_first_al_pattern> ::=
  { ( 
      <node_alias> 
        { <-( <edge_alias> )- } 
      | { -( <edge_alias> )-> }
      ) 
  } 


<al_pattern_quantifier> ::=
  {
        +
      | { 1 , n }
  }

n -  positive integer only.
 
```

## <a name="arguments"></a>引数  
*graph_search_pattern*  
グラフでの検索パターンまたは走査するパスを指定します。 このパターンは、グラフでパスを走査するために ASCII アート構文を使用します。 このパターンは、提供される矢印の方向でエッジを使用して 1 つのノードから別のノードに移動します。 エッジ名またはエイリアスは、かっこ内に表示されます。 ノード名またはエイリアスは、矢印の 2 つの端に表示されます。 矢印は、パターンのいずれの方向に移動できます。

*node_alias*  
FROM 句で指定されたノード テーブルの名前またはエイリアス。

*edge_alias*  
FROM 句で指定されたエッジ テーブルの名前またはエイリアス。

*SHORTEST_PATH*   
最短パス関数は、グラフ内の特定の 2 つのノード間、またはグラフ内の特定のノードと他のすべてのノード間の、最短パスを探すために使用されます。 入力として任意の長さのパターンを受け取り、グラフ内でそれが繰り返し検索されます。 

*arbitrary_length_match_pattern*  
目的のノードに到達するまで、またはパターンで指定されている繰り返しの最大数が満たされるまで、繰り返しトラバースする必要があるノードとエッジを指定します。 

*al_pattern_quantifier*   
任意の長さのパターンでは、特定の検索パターンの繰り返し回数を指定するため、正規表現スタイルのパターン量指定子を受け取ります。 サポートされている検索パターン量指定子は次のとおりです。   
* **+** :パターンを 1 回以上繰り返します。 最短パスが見つかったらすぐに終了します。    
* **{1,n}** : パターンを 1 から "n" 回繰り返します。 最短パスが見つかったらすぐに終了します。     

## <a name="remarks"></a>Remarks  
MATCH 内のノード名は繰り返すことができます。  つまり、ノードは、同じクエリ内でノードは任意の回数走査できます。  
エッジ名は MATCH 内では繰り返すことはできません。  
エッジは、いずれの方向もポイントできますが、明示的な方向が必要です。  
MATCH パターンでは、OR および NOT 演算子はサポートされていません。 MATCH は、AND と WHERE 句を使用して他の式と組み合わせることができます。 ただし、OR または NOT を使用して他の式と組み合わせることはサポートされていません。 

## <a name="examples"></a>使用例  
### <a name="a--find-a-friend"></a>A.  友達の検索 
 次の例では、Person ノード テーブルと friend エッジ テーブルを作成し、いくつかデータを挿入し、MATCH を使用して、グラフの Alice の友人を検索します。

 ```
 -- Create person node table
 CREATE TABLE dbo.Person (ID integer PRIMARY KEY, name varchar(50)) AS NODE;
 CREATE TABLE dbo.friend (start_date DATE) AS EDGE;

 -- Insert into node table
 INSERT INTO dbo.Person VALUES (1, 'Alice');
 INSERT INTO dbo.Person VALUES (2,'John');
 INSERT INTO dbo.Person VALUES (3, 'Jacob');

-- Insert into edge table
INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'John'), '9/15/2011');

INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'Jacob'), '10/15/2011');

INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'John'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'Jacob'), '10/15/2012');

-- use MATCH in SELECT to find friends of Alice
SELECT Person2.name AS FriendName
FROM Person Person1, friend, Person Person2
WHERE MATCH(Person1-(friend)->Person2)
AND Person1.name = 'Alice';

 ```

 ### <a name="b--find-friend-of-a-friend"></a>B.  友人の友人の検索
 次の例では、Alice の友人の友人の検索を試行します。 

 ```
SELECT Person3.name AS FriendName 
FROM Person Person1, friend, Person Person2, friend friend2, Person Person3
WHERE MATCH(Person1-(friend)->Person2-(friend2)->Person3)
AND Person1.name = 'Alice';

 ```

### <a name="c--more-match-patterns"></a>C.  その他の `MATCH` パターン
 MATCH 内でパターンを指定する他のいくつかの方法を次に示します。

 ```
 -- Find a friend
    SELECT Person2.name AS FriendName
    FROM Person Person1, friend, Person Person2
    WHERE MATCH(Person1-(friend)->Person2);
    
-- The pattern can also be expressed as below

    SELECT Person2.name AS FriendName
    FROM Person Person1, friend, Person Person2 
    WHERE MATCH(Person2<-(friend)-Person1);


-- Find 2 people who are both friends with same person
    SELECT Person1.name AS Friend1, Person2.name AS Friend2
    FROM Person Person1, friend friend1, Person Person2, 
         friend friend2, Person Person0
    WHERE MATCH(Person1-(friend1)->Person0<-(friend2)-Person2);
    
-- this pattern can also be expressed as below

    SELECT Person1.name AS Friend1, Person2.name AS Friend2
    FROM Person Person1, friend friend1, Person Person2, 
         friend friend2, Person Person0
    WHERE MATCH(Person1-(friend1)->Person0 AND Person2-(friend2)->Person0);
 ```
 

## <a name="see-also"></a>参照  
 [CREATE TABLE &#40;SQL グラフ&#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [INSERT (SQL グラフ)](../../t-sql/statements/insert-sql-graph.md)  
 [SQL Server 2017 でのグラフ処理](../../relational-databases/graphs/sql-graph-overview.md)  
