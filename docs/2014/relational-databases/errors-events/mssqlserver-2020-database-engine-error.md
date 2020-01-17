---
title: MSSQLSERVER_2020 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2020 (Database Engine error)
ms.assetid: 4a8bf90f-a083-4c53-84f0-d23c711c8081
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e54a04cc9d787ae4d6d4545bbc5d9661bbba213d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62869383"
---
# <a name="mssqlserver2020"></a>MSSQLSERVER_2020
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|2020|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名||  
|メッセージ テキスト|エンティティ "%.*ls" に対してレポートされた依存関係に、列への参照が含まれていません。 この原因としては、存在しないオブジェクトがエンティティによって参照されていること、またはエンティティの 1 つ以上のステートメントにエラーがあることが挙げられます。  クエリを再実行する前に、エンティティにエラーがないこと、およびエンティティによって参照されているすべてのオブジェクトが存在することを確認してください。|  
  
## <a name="explanation"></a>説明  
 **sys.dm_sql_referenced_entities** システム関数では、スキーマ バインド参照の列レベルの依存関係が報告されます。 たとえば、インデックス付きビューの列レベルの依存関係がすべて報告されます。これは、インデックス付きビューがスキーマ バインドを必要とするためです。 ただし、参照先エンティティがスキーマにバインドされていない場合は、列が参照されているすべてのステートメントをバインドできる場合にのみ、列の依存関係が報告されます。 ステートメントをバインドできるのは、ステートメント解析時にすべてのオブジェクトが存在している場合に限られます。 エンティティに定義されているステートメントを 1 つでもバインドできない場合は、列の依存関係が報告されず、**referenced_minor_id** 列で 0 が返されます。 列の依存関係を解決できない場合は、エラー 2020 が発生します。 このエラーによって、クエリからオブジェクト レベルの依存関係が返されなくなることはありません。  
  
## <a name="user-action"></a>ユーザーの操作  
 エラー 2020 発生前のメッセージで確認されたエラーをすべて修正します。 たとえば次のコード例では、`Production.ApprovedDocuments` テーブルの `Title`、`ChangeNumber`、`Status` の各列で、ビュー `Production.Document` が定義されています。 **sys.dm_sql_referenced_entities** システム関数で、`ApprovedDocuments` ビューが依存するオブジェクトと列がクエリされます。 このビューの作成には WITH SCHEMA_BINDING 句が使用されていないため、ビューで参照されている列が参照先テーブルで変更される可能性があります。 この例では、`ChangeNumber` テーブルの `Production.Document` 列の名前が `TrackingNumber` に変更されています。 カタログ ビューに対して `ApprovedDocuments` ビューに関するクエリが再度実行されますが、ビューに定義されているどの列にもバインドできません。 この問題を示すエラー 207 と 2020 が返されます。 問題を解決するには、列の新しい名前が反映されるようにビューを変更する必要があります。  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 `CREATE VIEW Production.ApprovedDocuments`  
  
 `AS`  
  
 `SELECT Title, ChangeNumber, Status`  
  
 `FROM Production.Document`  
  
 `WHERE Status = 2;`  
  
 `GO`  
  
 `SELECT referenced_schema_name AS schema_name`  
  
 `,referenced_entity_name AS table_name`  
  
 `,referenced_minor_name AS referenced_column`  
  
 `FROM sys.dm_sql_referenced_entities ('Production.ApprovedDocuments', 'OBJECT');`  
  
 `GO`  
  
 `EXEC sp_rename 'Production.Document.ChangeNumber', 'TrackingNumber', 'COLUMN';`  
  
 `GO`  
  
 `SELECT referenced_schema_name AS schema_name`  
  
 `,referenced_entity_name AS table_name`  
  
 `,referenced_minor_name AS referenced_column`  
  
 `FROM sys.dm_sql_referenced_entities ('Production.ApprovedDocuments', 'OBJECT');`  
  
 `GO`  
  
 このクエリでは、次のエラー メッセージが返されます。  
  
 `Msg 207, Level 16, State 1, Procedure ApprovedDocuments, Line 3`  
  
 `Invalid column name 'ChangeNumber'.`  
  
 `Msg 2020, Level 16, State 1, Line 1`  
  
 `The dependencies reported for entity`  
  
 `"Production.ApprovedDocuments" do not include references to`  
  
 `columns. This is either because the entity references an`  
  
 `object that does not exist or because of an error in one or`  
  
 `more statements in the entity. Before rerunning the query,`  
  
 `ensure that there are no errors in the entity and that all`  
  
 `objects referenced by the entity exist.`  
  
 次の例では、ビュー内の列名を修正しています。  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 `ALTER VIEW Production.ApprovedDocuments`  
  
 `AS`  
  
 `SELECT Title,TrackingNumber, Status`  
  
 `FROM Production.Document`  
  
 `WHERE Status = 2;`  
  
 `GO`  
  
## <a name="see-also"></a>参照  
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql)  
  
  
