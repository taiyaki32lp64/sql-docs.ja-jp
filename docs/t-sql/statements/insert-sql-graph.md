---
title: INSERT (SQL グラフ) | Microsoft Docs
description: SQL のグラフ ノードまたはエッジ テーブルの INSERT 構文
ms.date: 05/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.custom: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- INSERT statement [SQL Server], SQL graph
- SQL graph, INSERT statement
ms.assetid: ''
author: shkale-msft
ms.author: shkale
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8c4cfba19dc16e043ba6325fb6c9acb1665a597f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071169"
---
# <a name="insert-sql-graph"></a>INSERT (SQL グラフ)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、1 つまたは複数の行を`node`や`edge`に追加します。 

> [!NOTE]   
>  標準の Transact-SQL ステートメントについては、「[INSERT TABLE (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)」を参照してください。
  
![記事のリンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "記事のリンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="insert-into-node-table-syntax"></a>ノード テーブルへの INSERT 構文 
ノード テーブルに挿入するための構文は、通常のテーブルの場合と同じです。 

```sql
[ WITH <common_table_expression> [ ,...n ] ]  
INSERT   
{  
        [ TOP ( expression ) [ PERCENT ] ]   
        [ INTO ]   
        { <object> | rowset_function_limited   
          [ WITH ( <Table_Hint_Limited> [ ...n ] ) ]  
        }  
    {  
        [ (column_list) ] | [(<edge_table_column_list>)]  
        [ <OUTPUT Clause> ]  
        { VALUES ( { DEFAULT | NULL | expression } [ ,...n ] ) [ ,...n     ]   
        | derived_table   
        | execute_statement  
        | <dml_table_source>  
        | DEFAULT VALUES   
        }  
    }  
}  
[;]  
  
<object> ::=  
{   
    [ server_name . database_name . schema_name .   
      | database_name .[ schema_name ] .   
      | schema_name .   
    ]  
    node_table_name  | edge_table_name
}  
  
<dml_table_source> ::=  
    SELECT <select_list>  
    FROM ( <dml_statement_with_output_clause> )   
      [AS] table_alias [ ( column_alias [ ,...n ] ) ]  
    [ WHERE <on_or_where_search_condition> ]  
        [ OPTION ( <query_hint> [ ,...n ] ) ]  

<on_or_where_search_condition> ::=
    {  <search_condition_with_match> | <search_condition> }

<search_condition_with_match> ::=
    { <graph_predicate> | [ NOT ] <predicate> | ( <search_condition> ) }
    [ AND { <graph_predicate> | [ NOT ] <predicate> | ( <search_condition> ) } ]
    [ ,...n ]

<search_condition> ::=
    { [ NOT ] <predicate> | ( <search_condition> ) }
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition> ) } ]
    [ ,...n ]

<graph_predicate> ::=
    MATCH( <graph_search_pattern> [ AND <graph_search_pattern> ] [ , ...n] )

<graph_search_pattern>::=
    <node_alias> { { <-( <edge_alias> )- | -( <edge_alias> )-> } <node_alias> }

<edge_table_column_list> ::=
    ($from_id, $to_id, [column_list])

```  
  
 
## <a name="arguments"></a>引数  
このドキュメントでは、SQL グラフに関連する引数について説明します。 INSERT ステートメントの完全な一覧とサポートされている引数の説明については、「[INSERT TABLE (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)」を参照してください。

INTO  
`INSERT` と対象のテーブルとの間で使用できるキーワードで、省略可能です。  
  
*search_condition_with_match*   
`MATCH` 句は、ノードまたはエッジ テーブルへの挿入中に、サブクエリで使用できます。 `MATCH` ステートメントの構文については、「[GRAPH MATCH (Transact-SQL)](../../t-sql/queries/match-sql-graph.md)」を参照してください。

*graph_search_pattern*   
グラフ述語の一部として `MATCH` 句に指定された検索パターン。

*edge_table_column_list*   
ユーザーが、エッジを挿入するときに `$from_id` と `$to_id` の値を指定する必要があります。 値が指定されていないか、null がこれらの列に挿入された場合、エラーが返されます。 
  

## <a name="remarks"></a>Remarks  
ノードへの挿入は、すべてのリレーショナル テーブルへの挿入と同じです。 $Node_id 列の値が自動的に生成されます。

ユーザーが、エッジを挿入するときに `$from_id` と `$to_id` の値を指定する必要があります。   

ノード テーブルの一括挿入は、リレーショナル テーブルの一括挿入と同じです。

エッジ テーブルに一括挿入する前に、ノード テーブルをインポートする必要があります。 `$from_id` と `$to_id` の値をノード テーブルの `$node_id` 列から抽出し、エッジとして挿入できます。 

  
### <a name="permissions"></a>アクセス許可  
対象のテーブルに対する INSERT 権限が必要です。  
  
INSERT 権限は、既定では **sysadmin** 固定サーバー ロール、**db_owner** 固定データベース ロール、および **db_datawriter** 固定データベース ロールのメンバーと、テーブル所有者に与えられています。 **sysadmin**、**db_owner**、および **db_securityadmin** ロールのメンバー、およびテーブル所有者は、他のユーザーに権限を譲渡できます。  
  
OPENROWSET 関数の BULK オプションで INSERT を実行するには、**sysadmin** 固定サーバー ロールまたは **bulkadmin** 固定サーバー ロールのメンバーであることが必要です。  
  

## <a name="examples"></a>使用例  
  
#### <a name="a--insert-into-node-table"></a>A.  ノード テーブルへの挿入  
次の例では、Person のノードを作成し、2 つの行をテーブルに挿入します。

```sql
-- Create person node table
CREATE TABLE dbo.Person (ID integer PRIMARY KEY, name varchar(50)) AS NODE;
 
-- Insert records for Alice and John
INSERT INTO dbo.Person VALUES (1, 'Alice');
INSERT INTO dbo.Person VALUES (2,'John');
```
  
#### <a name="b--insert-into-edge-table"></a>B.  エッジ テーブルへの挿入  
次の例では、friend エッジ テーブルを作成し、エッジをテーブルに挿入します。

```sql
-- Create friend edge table
CREATE TABLE dbo.friend (start_date DATE) AS EDGE;

-- Create a friend edge, that connect Alice and John
INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'John'), '9/15/2011');
```

  
## <a name="see-also"></a>参照  
[INSERT TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
[SQL Server 2017 でのグラフ処理](../../relational-databases/graphs/sql-graph-overview.md)  


