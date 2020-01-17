---
title: DBCC CLONEDATABASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/23/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CLONEDATABASE
- CLONE DATABASE
- DBCC_CLONEDATABASE_TSQL
- DBCC CLONEDATABASE
- DBCC CLONE DATABASE
- CLONEDATABASE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database cloning [SQL Server]
- cloning databases
- clone databases
- cloning database
- clone database
- copying databases
- copy databases
- copying database
- copy database
- NO_STATISTICS option
- NO_QUERYSTORE option
- VERIFY_CLONEDB option
- BACKUP_CLONEDB option
- database copying [SQL Server]
- database cloning [SQL Server]
- DBCC CLONEDATABASE statement
ms.assetid: ''
author: bluefooted
ms.author: pamela
manager: amitban
ms.openlocfilehash: cd1fc9d36200a571a3dfd0e5367d4e3e01278466
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262322"
---
# <a name="dbcc-clonedatabase-transact-sql"></a>DBCC CLONEDATABASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

クエリ オプティマイザー関連のパフォーマンス問題を調査する目的で DBCC CLONEDATABASE を使用し、データベースをスキーマのみで複製します。

![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```
DBCC CLONEDATABASE   
(  
    source_database_name
    ,  target_database_name
)
    [ WITH { [ NO_STATISTICS ] [ , NO_QUERYSTORE ] [ , VERIFY_CLONEDB | SERVICEBROKER ] [ , BACKUP_CLONEDB ] } ]     
```  
  
## <a name="arguments"></a>引数  
*source_database_name*  
複製するデータベースの名前です。 
  
*target_database_name*  
複製元データベースの複製先となるデータベースの名前です。 このデータベースは DBCC CLONEDATABASE により作成されます。まだ作成されていないことが条件となります。 
  
NO_STATISTICS  
テーブル/インデックス統計をクローンから除外する必要があるかどうかを指定します。 このオプションが指定されていない場合、テーブル/インデックス統計は自動的に含まれます。 このオプションは、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 CU3 と [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以降で使用できます。

NO_QUERYSTORE<br>
クエリ ストア データをクローンから除外する必要があるかどうかを指定します。 このオプションが指定されていない場合、クエリ ストアが複製元データベースで有効になっていれば、クエリ ストア データがクローンに複製されます。 このオプションは、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以降で使用できます。

VERIFY_CLONEDB  
新しいデータベースの一貫性を確認します。  このオプションは、実稼働で使用する目的でデータベースが複製される場合に必要です。  また、VERIFY_CLONEDB を有効にすると、統計とクエリ ストア コレクションが無効になります。そのため、WITH VERIFY_CLONEDB、NO_STATISTICS、NO_QUERYSTORE の実行と等しくなります。  このオプションは、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP3、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2、[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU8 以降で使用できます。

> [!NOTE]  
> 次のコマンドは、複製されたデータベースが実稼働対応であることを確認する目的で使用できます。 <br/>`SELECT DATABASEPROPERTYEX('clone_database_name', 'IsVerifiedClone')`


SERVICEBROKER<br>
Service Broker の関連システム カタログを複製に含めるかどうかを指定します。  SERVICEBROKER オプションは、VERIFY_CLONEDB と組み合わせて使用することはできません。  このオプションは、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP3、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2、[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU8 以降で使用できます。

BACKUP_CLONEDB  
クローン データベースのバックアップを作成し、検証します。  VERIFY_CLONEDB と組み合わせて使用した場合、バックアップが作成される前にクローン データベースが検証されます。  このオプションは、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP3、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2、[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU8 以降で使用できます。
  
## <a name="remarks"></a>Remarks
次の検証は、DBCC CLONEDATABASE によって実行されます。 いずれかの検証に失敗すると、コマンドは失敗となります。
- 複製元データベースはユーザー データベースにする必要があります。 システム データベース (master、model、msdb、tempdb、ディストリビューション データベースなど) は複製できません。
- 複製元データベースはオンラインにするか、読み取り可能になっている必要があります。
- クローン データベースと同じ名前を使用するデータベースがまだ作成されていないことが条件となります。
- コマンドはユーザー トランザクションで行われません。

すべての検証に成功した場合、次の操作によって複製元データベースが複製されます。
- 複製元と同じファイル レイアウトを使用する新しいデータベースを model データベースの既定のファイル サイズで複製します。
- 複製元データベースの内部スナップショットを作成します。
- 複製元から複製先のデータベースにシステム メタデータが複製されます。
- 複製元から複製先のデータベースに全オブジェクトの全スキーマが複製されます。
- 複製元から複製先のデータベースに全インデックスの統計が複製されます。

> [!NOTE]  
> DBCC CLONEDATABASE から生成された新しいデータベースは、主にトラブルシューティングと診断を目的とします。  複製したデータベースを運用データベースとして使用するには、VERIFY_CLONEDB オプションを使用する必要があります。

複製先データベースの全ファイルが model データベースからサイズと増加設定を継承します。 複製先データベースのファイル名は、source_file_name _underscore_random number という規則に従います。 生成されたファイル名が複製先のフォルダーに既に存在する場合、DBCC CLONEDATABASE は失敗します。

DBCC CLONEDATABASE では、model データベースでユーザー オブジェクト (テーブル、インデックス、スキーマ、ロールなど) が作成されている場合、クローンを作成できません。 ユーザー オブジェクトが model データベースに存在する場合、データベースは複製に失敗し、次のエラー メッセージが表示されます。

```
Msg 2601, Level 14, State 1, Line 1
Cannot insert duplicate key row in object <system table> with unique index 'index name'. The duplicate key value is <key value>   
```

> [!IMPORTANT]
> 列ストア インデックスがある場合、[クローン データベースの列ストア インデックスでクエリを調整するときの考慮事項](https://techcommunity.microsoft.com/t5/SQL-Server/Considerations-when-tuning-your-queries-with-columnstore-indexes/ba-p/385294)に関するブログ投稿を参照し、**DBCC CLONEDATABASE** コマンドを実行する前に列ストア インデックス統計を更新してください。  SQL Server 2019 以降では、**DBCC CLONEDATABASE** コマンドで自動的にこの情報が収集されるので、上記の記事に記載されている手動手順は必要なくなります。

<a name="ctp23"></a>

## <a name="stats-blob-for-columnstore-indexes"></a>列ストア インデックスの統計 BLOB

[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] の `DBCC CLONEDATABASE` では、列ストア インデックスの統計 BLOB が自動的にキャプチャされるので、手動で行う必要ありません。`DBCC CLONEDATABASE` では、データをコピーすることなくクエリのパフォーマンスに関する問題をトラブルシューティングするのに必要なすべての要素を含む、スキーマのみのデータベースのコピーが作成されます。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のコマンドでは、列ストア インデックスのクエリのトラブルシューティングを正確に行うために必要な統計情報がコピーされず、手作業でこの情報をキャプチャする必要がありました。

複製されたデータベースのデータ セキュリティ関連の詳細については、[複製されたデータベースのデータ セキュリティの概要](https://techcommunity.microsoft.com/t5/SQL-Server/Understanding-data-security-in-cloned-databases-created-using/ba-p/385287)ブログを参照してください。

## <a name="internal-database-snapshot"></a>内部データベース スナップショット
DBCC CLONEDATABASE では、複製に必要なトランザクション整合性のためにソース データベースの内部データベース スナップショットを使用します。 このスナップショットを使用することで、コマンド実行時のブロックやコンカレンシーの問題を回避できます。 スナップショットを作成できない場合、DBCC CLONEDATABASE は失敗します。 

複製プロセスの次の手順の間、データベース レベルのロックが維持されます。
- 複製元データベースを検証する
- 複製元データベースの S ロックを取得する
- 複製元データベースのスナップショットを作成する
- クローン データベース (model データベースから継承された空のデータベース) を作成する
- クローン データベースの X ロックを取得する
- クローン データベースにメタデータを複製する
- すべての DB ロックを解除する

コマンドが実行を終えると、内部スナップショットが削除されます。 複製されたデータベースでは、TRUSTWORTHY オプションと DB_CHAINING オプションがオフになります。 

## <a name="supported-objects"></a>サポート対象のオブジェクト
次のオブジェクトのみ、複製先のデータベースで複製できます。 暗号化されたオブジェクトは複製されますが、クローン データベースでは使用できません。 次のセクションに記載されていないオブジェクトはクローンでサポートされていません。 
- APPLICATION ROLE
- AVAILABILITY GROUP
- COLUMNSTORE INDEX
- CDB
- CDC
- CLR ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 CU3、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以降のバージョンで)
- DATABASE PROPERTIES
- DEFAULT
- FILES AND FILEGROUPS
- フルテキスト ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU2 以降で)
- FUNCTION
- INDEX
- Login
- PARTITION FUNCTION
- PARTITION SCHEME
- PROCEDURE   
> [!NOTE]   
> [!INCLUDE[tsql](../../includes/tsql-md.md)] プロシージャは [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 以降のすべてのリリースでサポートされています。 CLR プロシージャは [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 CU3 以降でサポートされています。 ネイティブ コンパイルされたプロシージャは [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以降でサポートされています。  

- QUERY STORE ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以降)   
> [!NOTE]   
> クエリ ストア データは、複製先データベースで有効になっている場合にのみ複製されます。 クエリ ストアの一部として最新のランタイム統計を複製するには、DBCC CLONEDATABASE を実行する前に sp_query_store_flush_db を実行し、ランタイム統計をクエリ ストアにフラッシュして (書き出して) ください。  

- ROLE
- RULE
- SCHEMA
- SEQUENCE
- SPATIAL INDEX
- STATISTICS
- SYNONYM
- TABLE
- MEMORY OPTIMIZED TABLES ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以降のバージョンでのみ)
- FILESTREAM AND FILETABLE OBJECTS ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 CU3、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以降のバージョンで) 
- TRIGGER
- TYPE
- UPGRADED DB
- User
- VIEW
- XML INDEX
- XML SCHEMA COLLECTION  

## <a name="permissions"></a>アクセス許可  
**sysadmin** 固定サーバー ロールのメンバーシップが必要です。

## <a name="error-log-messages"></a>エラー ログ メッセージ
次のメッセージは、複製プロセス中にエラー ログに記録されるメッセージの一例です。

```
2018-03-26 15:33:56.05 spid53 Database cloning for 'sourcedb' has started with target as 'sourcedb_clone'.

2018-03-26 15:33:56.46 spid53 Starting up database 'sourcedb_clone'.

2018-03-26 15:33:57.80 spid53 Setting database option TRUSTWORTHY to OFF for database 'sourcedb_clone'.

2018-03-26 15:33:57.80 spid53 Setting database option DB_CHAINING to OFF for database 'sourcedb_clone'.

2018-03-26 15:33:57.88 spid53 Starting up database 'sourcedb_clone'.

2018-03-26 15:33:57.91 spid53 Database 'sourcedb_clone' is a cloned database. A cloned database should be used for diagnostic purposes only and is not supported for use in a production environment.

2018-03-26 15:33:57.92 spid53 Database cloning for 'sourcedb' has finished. Cloned database is 'sourcedb_clone'.
```

## <a name="database-properties"></a>データベース プロパティ
`DATABASEPROPERTYEX('dbname', 'IsClone')` は、データベースが DBCC CLONEDATABASE を利用して生成された場合に 1 を返します。

`DATABASEPROPERTYEX('dbname', 'IsVerifiedClone')` は、データベースが WITH VERIFY_CLONEDB を利用して正常に検証された場合に 1 を返します。

## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-clone-of-a-database-that-includes-schema-statistics-and-query-store"></a>A. スキーマ、統計、クエリ ストアを含むデータベースを複製する 
次の例では、スキーマ、統計、クエリ ストア データを含む AdventureWorks データベースが複製されます ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以降のバージョン)

```sql  
DBCC CLONEDATABASE (AdventureWorks, AdventureWorks_Clone);    
GO 
```  
  
### <a name="b-creating-a-schema-only-clone-of-a-database-without-statistics"></a>B. データベースを統計なし、スキーマのみで複製する 
次の例では、統計を含めずに AdventureWorks データベースが複製されます ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 CU3 以降のバージョン)

```sql  
DBCC CLONEDATABASE (AdventureWorks, AdventureWorks_Clone) WITH NO_STATISTICS;    
GO 
```  

### <a name="c-creating-a-schema-only-clone-of-a-database-without-statistics-and-query-store"></a>C. データベースを統計とクエリ ストアなし、スキーマのみで複製する 
次の例では、統計とクエリ ストア データを含めずに AdventureWorks データベースが複製されます ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以降のバージョン)。

```sql  
DBCC CLONEDATABASE (AdventureWorks, AdventureWorks_Clone) WITH NO_STATISTICS, NO_QUERYSTORE;    
GO 
```  

### <a name="d-creating-a-clone-of-a-database-that-is-verified-for-production-use"></a>D. データベースを複製し、運用環境向けであることを確認する
次の例では、AdventureWorks データベースを統計とクエリ ストア データなし、スキーマのみで複製し、運用環境向けであることが確認されます ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 以降のバージョン)。

```sql  
DBCC CLONEDATABASE (AdventureWorks, AdventureWorks_Clone) WITH VERIFY_CLONEDB;    
GO 
```  
  
### <a name="e-creating-a-clone-of-a-database-that-is-verified-for-production-use-that-includes-a-backup-of-the-cloned-database"></a>E. データベースを複製し、運用環境向けであることを確認し、複製したデータベースのバックアップを作成する
次の例では、統計とクエリ ストア データなしで AdventureWorks データベースのスキーマのみが複製され、運用環境向けであることが確認されます。  複製したデータベースのバックアップも検証の上、作成されます ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 以降のバージョン)。

```sql  
DBCC CLONEDATABASE (AdventureWorks, AdventureWorks_Clone) WITH VERIFY_CLONEDB, BACKUP_CLONEDB;    
GO 
```

## <a name="see-also"></a>参照
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)    
[SQL Server で統計のみのデータベースを作成するために必要なデータベース メタデータのスクリプトを生成する方法](https://support.microsoft.com/help/914288)   

