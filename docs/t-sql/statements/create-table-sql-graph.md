---
title: CREATE TABLE (SQL Graph) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SQL_GRAPH_TSQL
- TABLE
- CREATE_TABLE_TSQL
- NODE
- NODE_TSQL
- AS_NODE
- AS_NODE_TSQL
- EDGE
- EDGE_TSQL
- AS_EDGE
- AS_EDGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- graph
- SQL graph
- CREATE TABLE SQL graph
- NODE
- EDGE
- SQL graph, CREATE TABLE statement
ms.assetid: ''
author: shkale-msft
ms.author: shkale
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 37e374d44fc6013c1cdf6b9594d709ff4282f7aa
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70846722"
---
# <a name="create-table-sql-graph"></a>CREATE TABLE (SQL Graph)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

`NODE` または `EDGE` テーブルで新しい SQL グラフ テーブルを作成します。 
  
> [!NOTE]   
>  標準の Transact-SQL ステートメントについては、「[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)」を参照してください。
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
CREATE TABLE   
    { database_name.schema_name.table_name | schema_name.table_name | table_name }
    ( { <column_definition> } 
       | <computed_column_definition>
       | <column_set_definition>
       | [ <table_constraint> ] [ ,... n ]
       | [ <table_index> ] }
          [ ,...n ]
    )   
    AS [ NODE | EDGE ]
    [ ON { partition_scheme_name ( partition_column_name )
           | filegroup
           | "default" } ]
[ ; ] 

< table_constraint > ::=
[ CONSTRAINT constraint_name ]
{
    { PRIMARY KEY | UNIQUE }
        [ CLUSTERED | NONCLUSTERED ]
        (column [ ASC | DESC ] [ ,...n ] )
        [
            WITH FILLFACTOR = fillfactor
           |WITH ( <index_option> [ , ...n ] )
        ]
        [ ON { partition_scheme_name (partition_column_name)
            | filegroup | "default" } ]
    | FOREIGN KEY
        ( column [ ,...n ] )
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]
        [ NOT FOR REPLICATION ]
    | CONNECTION
        ( { node_table TO node_table } 
          [ , {node_table TO node_table }]
          [ , ...n ]
        )
        [ ON DELETE { NO ACTION | CASCADE } ]
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )
```  
  
  
## <a name="arguments"></a>引数  
このドキュメントでは、SQL グラフに関連する引数のみを一覧表示します。 完全な一覧とサポートされている引数の説明については、「[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)」を参照してください。

 *database_name*    
 テーブルが作成されたデータベースの名前を指定します。 *database_name* には、既存のデータベース名を指定する必要があります。 指定しない場合、*database_name* は現在のデータベースに設定されます。 現在の接続に対するログインには、*database_name* で指定されたデータベース内の既存のユーザー ID を関連付け、そのユーザー ID に CREATE TABLE 権限を許可しておく必要があります。  
  
 *schema_name*    
 新しいテーブルが所属するスキーマの名前です。  
  
 *table_name*      
 ノードまたはエッジ テーブルの名前です。 テーブル名は[識別子](../../relational-databases/databases/database-identifiers.md)の規則に従っている必要があります。 116 文字までしか使用できないローカル一時テーブル名 (名前の先頭に 1 つの番号記号 (#) が付加されます) を除き、*table_name* には、最大 128 文字を使用できます。  
  
 NODE   
 ノード テーブルを作成します。

 EDGE  
 エッジ テーブルを作成します。  
 
 *table_constraint*   
 テーブルに追加される PRIMARY KEY、UNIQUE、FOREIGN KEY、CONNECTION 制約、CHECK 制約、または DEFAULT 定義のプロパティを指定します。
 
 ON { partition_scheme | filegroup | "default" }    
 テーブルが格納されるパーティション構成またはファイル グループを指定します。 partition_scheme を指定すると、テーブルはパーティション テーブルとなり、各パーティションは partition_scheme で指定した 1 つ以上のファイル グループに格納されます。 filegroup を指定すると、テーブルは指定されたファイル グループに格納されます。 ファイル グループがデータベース内に存在している必要があります。 "default" を指定するか、ON をまったく指定しないと、テーブルは既定のファイル グループに格納されます。 CREATE TABLE で指定したテーブルの格納方法を後から変更することはできません。

 ON {partition_scheme | filegroup | "default"}    
 PRIMARY KEY 制約または UNIQUE 制約でも指定できます。 これらの制約はインデックスを作成します。 filegroup を指定すると、インデックスは指定されたファイル グループに格納されます。 "default" を指定するか、ON を指定しなかった場合、インデックスはテーブルと同じファイル グループに格納されます。 PRIMARY KEY または UNIQUE 制約によりクラスター化インデックスが作成される場合、テーブルのデータ ページはインデックスと同じファイル グループに格納されます。 CLUSTERED を指定するか、制約によりクラスター化インデックスを作成し、テーブル定義の partition_scheme または filegroup とは異なる partition_scheme (またはその逆) を指定すると、制約定義だけが優先され、それ以外は無視されます。
  
## <a name="remarks"></a>Remarks  
一時テーブルをノード テーブルまたはエッジ テーブルとして作成することはできません。  

ノード テーブルまたはエッジ テーブルをテンポラル テーブルとして作成することはできません。

ノード テーブルまたはエッジ テーブルではデータベースの拡張はサポートされていません。

ノード テーブルまたはエッジ テーブルは、外部テーブルにすることはできません (グラフ テーブルでは PolyBase はサポートされません)。 

パーティション分割されていないグラフ ノード/エッジ テーブルをパーティション分割されているグラフ ノード/エッジ テーブルに変更することはできません。 
  
 
## <a name="examples"></a>使用例  
  
### <a name="a-create-a-node-table"></a>A. `NODE` テーブルの作成
 次の例では、`NODE` テーブルの作成方法を示しています。

```
 CREATE TABLE Person (
        ID INTEGER PRIMARY KEY, 
        name VARCHAR(100), 
        email VARCHAR(100)
 ) AS NODE;
```

### <a name="b-create-an-edge-table"></a>B. `EDGE` テーブルの作成
次の例では、`EDGE` テーブルの作成方法を示しています。

```
 CREATE TABLE friends (
    id integer PRIMARY KEY,
    start_date date
 ) AS EDGE;

```

```
 -- Create a likes edge table, this table does not have any user defined attributes   
 CREATE TABLE likes AS EDGE;

```


## <a name="see-also"></a>参照 
 [ALTER TABLE table_constraint](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [INSERT (SQL グラフ)](../../t-sql/statements/insert-sql-graph.md)  
 [SQL Server 2017 でのグラフ処理](../../relational-databases/graphs/sql-graph-overview.md)

