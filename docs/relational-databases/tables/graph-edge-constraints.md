---
title: グラフのエッジ制約 | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- edge constraints [SQL Server]
- CONNECTION constraints
- edge constraints [Azure SQL Database]
- graph edge constraints
- SQL Graph
author: shkale-msft
ms.author: shkale
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current||=azuresqldb-current'
ms.openlocfilehash: ae08d5baef685a0b338ad574357230f01d3814cf
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70873881"
---
# <a name="edge-constraints"></a>エッジ制約

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

エッジ制約を使用して、データの整合性と特定のセマンティクスを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] グラフ データベース内のエッジ テーブルに適用できます。

## <a name="Connection"></a> エッジ制約

グラフ機能の初回のリリースでは、エッジ テーブルでエッジのエンドポイントに対して強制できることは何もありませんでした。 つまり、グラフ データベース内のエッジは、その種類に関係なく、任意のノードを他の任意のノードに接続することができました。

今回のリリースにはエッジ制約が導入され、ユーザーは、各自のエッジ テーブルに制約を追加することで特定のセマンティクスを適用でき、データの整合性も管理できます。 エッジ制約を持つエッジ テーブルに新しいエッジが追加される場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)] では、エッジが接続を試みるノードが適切なノード テーブルに存在している必要があります。 また、ノードがエッジによって参照されている場合は、ノードを削除することはできません。

### <a name="edge-constraint-clauses"></a>エッジ制約句

各エッジ制約は、1 つまたは複数のエッジ制約句で構成されます。 1 つのエッジ制約句は、特定のエッジが接続する FROM ノードと TO ノードのペアです。

グラフ内に `Product` ノードと `Customer` ノードがあり、`Bought` エッジを使用してこれらのノードを接続することを考えてください。 エッジ制約句には、FROM ノードと TO ノードのペアとエッジの方向が指定されます。 この場合、エッジ制約句は `Customer` TO `Product` になります。 つまり、`Customer` から `Product` 方向への `Bought` の挿入が許可されます。 `Product` から `Customer` 方向へのエッジを挿入する試みは失敗します。

- エッジ制約句には、エッジ制約が適用される FROM ノードと TO ノードのペアが含まれます。
- ユーザーは、エッジ制約ごとに複数のエッジ制約句を指定でき、それらは論理和演算として適用されます。
- 1 つのエッジ テーブルに複数のエッジ制約が作成される場合、エッジはすべての制約を満たす必要があります。

### <a name="indexes-on-edge-constraints"></a>エッジ制約のインデックス

エッジ制約を作成しても、エッジ テーブルの `$from_id` 列と `$to_id` 列の対応するインデックスは自動的に作成されることはありません。 ポイント ルックアップ クエリまたは OLTP ワークロードがある場合は、`$from_id`と `$to_id` のペアに対するインデックスを手動で作成することをお勧めします。

### <a name="on-delete-referential-actions-on-edge-constraints"></a>エッジ制約に対する削除時の参照操作
エッジ制約に対する連鎖操作では、そのエッジが接続されているノードをユーザーが削除したときに、データベース エンジンが実行するアクションをユーザーが定義できます。 以下の参照操作を定義できます。  
*NO ACTION*   
エッジが接続されているノードを削除しようとすると、データベース エンジンでエラーが発生します。  

*CASCADE*   
データベースからノードを削除するときに、接続されているエッジが削除されます。  

## <a name="working-with-edge-constraints"></a>エッジ制約の使用

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、[!INCLUDE[tsql](../../includes/tsql-md.md)] を使用してエッジ制約を作成できます。 エッジ制約は、グラフ エッジ テーブルにのみ定義できます。 エッジ制約を作成、削除、または変更するには、テーブルに対する **ALTER** 権限を持っている必要があります。

### <a name="create-edge-constraints"></a>エッジ制約の作成

新規または既存のテーブルにエッジ制約を作成する方法を、次の例に示します

#### <a name="to-create-an-edge-constraint-on-a-new-edge-table"></a>新しいエッジ テーブルにエッジ制約を作成するには

次の例では、**bought** エッジ テーブルにエッジ制約を作成します。

```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      ,CustomerName VARCHAR(100)
   )
AS NODE;
GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      ,ProductName VARCHAR(100)
   )
AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT
         ,CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product) ON DELETE NO ACTION
   )
   AS EDGE;
   ```

#### <a name="defining-referential-actions-on-a-new-edge-table"></a>新しいエッジ テーブルでの参照操作の定義 

次の例では、**bought** エッジ テーブルにエッジ制約を作成し、ON DELETE CASCADE 参照アクションを定義します。 

```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      ,CustomerName VARCHAR(100)
   )
AS NODE;
GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      ,ProductName VARCHAR(100)
   )
AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT
         ,CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product) ON DELETE CASCADE
   )
   AS EDGE;
   ```

#### <a name="to-add-edge-constraint-to-an-existing-edge-table"></a>既存のエッジ テーブルにエッジ制約を追加するには

次の例では、ALTER TABLE を使用して、**bought** エッジ テーブルにエッジ制約を追加します。

```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY,
      , CustomerName VARCHAR(100)
   )
   AS NODE;
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      , ProductName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT
   )
   AS EDGE;
GO
ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Customer TO Product);
```  

#### <a name="create-a-new-edge-constraint-on-existing-edge-table-with-additional-edge-constraint-clauses"></a>既存のエッジ テーブルに、追加のエッジ制約句を含む新しいエッジ制約を作成する

次の例では、`ALTER TABLE` コマンドを使って、**bought** エッジ テーブルに追加のエッジ制約句を含む新しいエッジ制約を追加します。
  
```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      , CustomerName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Supplier
   (
      ID INTEGER PRIMARY KEY
      , SupplierName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      , ProductName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT
      , CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
   )
   AS EDGE;
-- Drop the existing edge constraint first and then create a new one.
ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT;
GO
-- User ALTER TABLE to create a new edge constraint.
ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Customer TO Product, Supplier TO Product);
```  

前の例では、*EC_BOUGHT1* 制約に 2 つのエッジ制約句があります。**Customer** を **Product** に接続するものと、**Supplier** を **Product** に接続するものです。 両方の句は、論理和演算で適用されます。 つまり、指定されたエッジがエッジ テーブルで許可されるには、これら 2 つの句のいずれかを満たす必要があります。

#### <a name="creating-a-new-edge-constraint-on-existing-edge-table-with-new-edge-constraint-clause"></a>既存のエッジ テーブルに、新しいエッジ制約句を含む新しいエッジ制約を作成する

次の例では、`ALTER TABLE` コマンドを使って、**bought** エッジ テーブルに新しいエッジ制約句を含む新しいエッジ制約を追加します。
  
 ```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      , CustomerName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Supplier
   (
      ID INTEGER PRIMARY KEY
      , SupplierName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      , ProductName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT,
         CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
   )
   AS EDGE;
GO
ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Supplier TO Product);
 ```  

前の例では、**bought** エッジ テーブルに 2 つの別個のエッジ制約 (*EC_BOUGHT* と *EC_BOUGHT1*) を作成しました。 これらのエッジ制約には、どちらにも、異なるエッジ制約句があります。 エッジ テーブルに複数のエッジ制約がある場合、特定のエッジがエッジ テーブルで許可されるには、**すべての**エッジ制約を満たす必要があります。 ここでは、*EC_BOUGHT* と *EC_BOUGHT1* を満たすことができるエッジがないため、**bought** エッジ テーブルは空の状態を維持する必要があります。

エッジ テーブルへの挿入を成功させるには、エッジ制約の 1 つを削除するか両方を削除し、両方のエッジ制約句を含む新しいエッジ制約を作成する必要があります。

```sql
-- Drop the existing edge constraint first and then create a new one.
ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT;
GO
ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT1;
GO
ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT_NEW CONNECTION (Customer TO Product, Supplier TO Product);
GO
```  

指定したエッジが **bought** エッジで許可されるには、それが *EC_BOUGHT_NEW* 制約内のエッジ制約句のいずれかを満たす必要があります。 これで、有効な **Customer** ノードから **Product** ノード、または **Supplier** ノードから **Product** ノードへの接続を試みるすべてのエッジが許可されます。

### <a name="delete-edge-constraints"></a>エッジ制約の削除

次の例では、まずエッジ制約の名前を特定してから制約を削除します。  
  
```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      , CustomerName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      , ProductName VARCHAR(100)
   ) AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT
      , CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
    )
    AS EDGE;
GO
-- Return the name of edge constraint.
SELECT name  
   FROM sys.edge_constraints  
   WHERE type = 'EC' AND parent_object_id = OBJECT_ID('bought');  
GO  
-- Delete the primary key constraint.  
ALTER TABLE bought
DROP CONSTRAINT EC_BOUGHT;
```  

### <a name="modify-edge-constraints"></a>エッジ制約の変更

Transact-SQL を使用してエッジ制約を変更するには、まず既存のエッジ制約を削除してから、新しい定義を使用して再作成する必要があります。


### <a name="view-edge-constraints"></a>エッジ制約の表示

[!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。

この例では、tempdb データベース内のエッジ テーブル `bought` を対象に、すべてのエッジ制約とそのプロパティを取得します。  

```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      , CustomerName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Supplier
   (
      ID INTEGER PRIMARY KEY
      , SupplierName VARCHAR(100)
   )
   AS NODE;
   GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      , ProductName VARCHAR(100)
   )
   AS NODE;

-- CREATE edge table with edge constraints.
CREATE TABLE bought
   (
      PurchaseCount INT
      , CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product, Supplier TO Product)
   )
   AS EDGE;

-- Query sys.edge_constraints and sys.edge_constraint_clauses to view
-- edge constraint properties.
SELECT
   EC.name AS edge_constraint_name
   , OBJECT_NAME(EC.parent_object_id) AS edge_table_name
   , OBJECT_NAME(ECC.from_object_id) AS from_node_table_name
   , OBJECT_NAME(ECC.to_object_id) AS to_node_table_name
   , is_disabled
   , is_not_trusted
FROM sys.edge_constraints EC
   INNER JOIN sys.edge_constraint_clauses ECC
   ON EC.object_id = ECC.object_id
WHERE EC.parent_object_id = object_id('bought');
```  

## <a name="related-tasks"></a>関連タスク

[CREATE TABLE (SQL Graph)](../../t-sql/statements/create-table-sql-graph.md)  
[ALTER TABLE table_constraint](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)  

SQL Server のグラフ テクノロジについて詳しくは、「[SQL Server と Azure SQL Database でのグラフ処理](../graphs/sql-graph-overview.md?view=sql-server-2017)」をご覧ください。

