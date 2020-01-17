---
title: グラフの処理
titleSuffix: SQL Server and Azure SQL Database
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, overview
ms.assetid: ''
author: shkale-msft
ms.author: shkale
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3ca26af4738de25937b71e0c97c6272414a0957a
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096085"
---
# <a name="graph-processing-with-sql-server-and-azure-sql-database"></a>SQL Server と Azure SQL Database を使用したグラフの処理
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、多対多リレーションシップをモデル化するためのグラフデータベース機能が用意されています。 グラフのリレーションシップは [!INCLUDE[tsql-md](../../includes/tsql-md.md)] に統合されており、基盤となるデータベース管理システムとして [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用する利点があります。


## <a name="what-is-a-graph-database"></a>グラフデータベースとは  
グラフ データベースは、ノード (または頂点) とエッジ (またはリレーションシップ) のコレクションです。 ノードはエンティティ (たとえば人や組織) を表し、エッジはそれが接続する 2 つのノードのリレーションシップ (たとえば好感や友人) を表します。 ノードとエッジの両方に、プロパティが関連付けられている場合があります。 グラフデータベースを一意にするための機能を次に示します。  
-   エッジまたはリレーションシップは、グラフデータベース内の最初のクラスエンティティであり、属性またはプロパティを関連付けることができます。 
-   1つのエッジを使用すると、グラフデータベース内の複数のノードを柔軟に接続できます。
-   パターンマッチングとマルチホップのナビゲーションクエリを簡単に表現できます。
-   推移的なクロージャとポリモーフィックなクエリを簡単に表現できます。

## <a name="when-to-use-a-graph-database"></a>グラフデータベースを使用する場合

グラフデータベースは実現できません。これは、リレーショナルデータベースを使用しては実現できません。 ただし、グラフデータベースを使用すると、特定の種類のクエリを簡単に表現できるようになります。 また、特定の最適化を使用すると、特定のクエリのパフォーマンスが向上する場合があります。 どちらか一方を選択するかどうかは、次の要因に基づいて決めることができます。  
-   アプリケーションに階層データがある。 HierarchyID データ型は階層の実装に使用できますが、いくつかの制限があります。 たとえば、1つのノードに複数の親を格納することはできません。
-   アプリケーションに複雑な多対多リレーションシップがある。アプリケーションの進化に伴って、新しいリレーションシップが追加されます。
-   相互接続されたデータとリレーションシップを分析する必要があります。

## <a name="graph-features-introduced-in-includesssqlv14includessssqlv14-mdmd"></a>[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] で導入されたグラフ機能 
グラフのデータの格納とクエリを容易にするために、SQL Server にグラフ拡張機能を追加し始めます。 次の機能は、最初のリリースで導入されました。 


### <a name="create-graph-objects"></a>グラフオブジェクトの作成
[!INCLUDE[tsql-md](../../includes/tsql-md.md)] 拡張機能を使用すると、ユーザーはノードテーブルまたはエッジテーブルを作成できます。 ノードとエッジの両方にプロパティを関連付けることができます。 ノードとエッジはテーブルとして格納されるため、リレーショナルテーブルでサポートされているすべての操作は、ノードまたはエッジテーブルでサポートされています。 以下に例を示します。  

```   
CREATE TABLE Person (ID INTEGER PRIMARY KEY, Name VARCHAR(100), Age INT) AS NODE;
CREATE TABLE friends (StartDate date) AS EDGE;
```   

![個人-友人-テーブル](../../relational-databases/graphs/media/person-friends-tables.png "Person ノードと友人のエッジテーブル")  
ノードとエッジはテーブルとして格納されます。  

### <a name="query-language-extensions"></a>クエリ言語の拡張機能  
新しい `MATCH` 句は、グラフを使用したパターンマッチングとマルチホップのナビゲーションをサポートするために導入されました。 `MATCH` 関数では、パターンマッチングに ASCII アートスタイル構文を使用します。 例 :  

```   
-- Find friends of John
SELECT Person2.Name 
FROM Person Person1, Friends, Person Person2
WHERE MATCH(Person1-(Friends)->Person2)
AND Person1.Name = 'John';
```   
 
### <a name="fully-integrated-in-includessnoversionincludesssnoversion-mdmd-engine"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エンジンに完全に統合されている 
グラフ拡張機能は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エンジンに完全に統合されています。 同じストレージエンジン、メタデータ、クエリプロセッサなどを使用して、グラフデータを格納し、クエリを実行します。 1つのクエリで、グラフとリレーショナルデータにまたがるクエリを実行します。 グラフ機能と他の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テクノロジ (列ストア、HA、R services など) との組み合わせSQL graph データベースでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で使用できるすべてのセキュリティ機能とコンプライアンス機能もサポートされています。
 
### <a name="tooling-and-ecosystem"></a>ツールとエコシステム

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に用意されている既存のツールとエコシステムを活用できます。 バックアップと復元、インポート、エクスポートなどのツールは、すぐに使用できます。 SSIS、SSRS、Power BI などの他のツールやサービスは、リレーショナルテーブルを操作するのと同じように、グラフテーブルで使用できます。

## <a name="edge-constraints"></a>エッジ制約
エッジ制約は、グラフエッジテーブルで定義され、特定のエッジタイプが接続できるノードテーブルのペアです。 これにより、ユーザーはグラフスキーマをより適切に制御できるようになります。 エッジ制約を使用すると、特定のエッジが接続を許可されているノードの種類を制限できます。 

エッジの制約を作成して使用する方法の詳細については、「[エッジの制約](../../relational-databases/tables/graph-edge-constraints.md)」を参照してください。

## <a name="merge-dml"></a>DML のマージ 
[MERGE](../../t-sql/statements/merge-transact-sql.md)ステートメントは、ソーステーブルとの結合の結果に基づいて、対象テーブルに対して挿入、更新、または削除の操作を実行します。 たとえば、ターゲットテーブルとソーステーブルの違いに基づいて、対象テーブルの行を挿入、更新、または削除することによって、2つのテーブルを同期できます。 MERGE ステートメントでの MATCH 述語の使用は、Azure SQL Database と SQL Server vNext でサポートされるようになりました。 つまり、INSERT/UPDATE/DELETE ステートメントを個別に指定する代わりに、MATCH 述語を使用して、現在のグラフデータ (ノードテーブルまたはエッジテーブル) を新しいデータとマージできるようになりました。

Merge DML で match を使用する方法の詳細については、 [Merge ステートメント](../../t-sql/statements/merge-transact-sql.md)に関するページを参照してください。

## <a name="shortest-path"></a>最短パス
[SHORTEST_PATH](./sql-graph-shortest-path.md)関数は、グラフ内の2つのノード間、または特定のノードからグラフ内の他のすべてのノードまでの最短パスを検索します。 最短パスを使用して、グラフ内で推移的なクロージャまたは任意の長さのトラバーサルを見つけることもできます。 

 ## <a name="next-steps"></a>次の手順  
[SQL グラフデータベース-アーキテクチャ](./sql-graph-architecture.md)の読み取り
   

