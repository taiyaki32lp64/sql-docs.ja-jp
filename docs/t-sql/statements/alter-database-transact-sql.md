---
title: ALTER DATABASE (Transact-SQL)| Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_DATABASE_TSQL
- ALTER DATABASE
dev_langs:
- TSQL
helpviewer_keywords:
- databases [SQL Server], modifying
- ALTER DATABASE statement
- databases [SQL Server], renaming
- renaming databases
- database modifications [SQL Server]
- ALTER DATABASE statement, syntax described
- database names [SQL Server], ALTER DATABASE
- modifying databases
- collations [SQL Server], modifying
- database mirroring [SQL Server], Transact-SQL
ms.assetid: 15f8affd-8f39-4021-b092-0379fc6983da
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-current||=azuresqldb-mi-current||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 3627e62bafefaa33eee4b238e1e33cd1ea127137
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982157"
---
# <a name="alter-database-transact-sql"></a>ALTER DATABASE (Transact-SQL)

データベースの特定の構成オプションを変更します。

この記事では、選択した SQL 製品について、構文、引数、注釈、アクセス許可、例を紹介します。

構文表記規則の詳細については、「[Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)」を参照してください。

## <a name="click-a-product"></a>製品をクリックしてください

次の行から興味がある製品名をクリックしてみてください。 この Web ページでは、クリックした製品に合わせて、異なるコンテンツが表示されます。

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

||||||
|---|---|---|---|---|
|**\* _SQL Server \*_** &nbsp;|[SQL Database<br />単一データベース/エラスティック プール](alter-database-transact-sql.md?view=azuresqldb-current)|[SQL Database<br />マネージド インスタンス](alter-database-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](alter-database-transact-sql.md?view=azure-sqldw-latest)|[Analytics Platform<br />System (PDW)](alter-database-transact-sql.md?view=aps-pdw-2016-au7)|
||||||

&nbsp;

## <a name="overview-sql-server"></a>概要:SQL Server

SQL Server では、このステートメントはデータベース、またはそのデータベースに関連付けられているファイルおよびファイル グループを変更します。 データベースに対するファイルやファイル グループの追加と削除、データベースおよびデータベースのファイルやファイル グループの属性の変更、データベースの照合順序の変更、データベース オプションの設定を行えます。 データベース スナップショットを変更することはできません。 レプリケーションに関連するデータベース オプションを変更するには、[sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) を使用してください。

解説が長くなるため、ALTER DATABASE の構文は複数の記事に分けて説明します。

ALTER DATABASE: この記事では、データベースの名前と照合順序を変更するための構文および関連情報について説明します。

「[ALTER DATABASE の File および Filegroup オプション](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)」では、データベースのファイルおよびファイル グループを追加したり削除したりするための構文と関連情報のほか、ファイルおよびファイル グループの属性を変更するための構文について説明します。

「[ALTER DATABASE の SET オプション](../../t-sql/statements/alter-database-transact-sql-set-options.md)」では、ALTER DATABASE の SET オプションを使ってデータベースの属性を変更するための構文と関連情報について説明します。

[ALTER DATABASE のデータベース ミラーリング](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md) ALTER DATABASE のデータベース ミラーリングに関連した SET オプションの構文と関連情報について説明します。

[ALTER DATABASE の SET HADR](../../t-sql/statements/alter-database-transact-sql-set-hadr.md) Always On 可用性グループのセカンダリ レプリカ上のセカンダリ データベースを構成するための、ALTER DATABASE の [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] オプションの構文と関連情報について説明します。

「[ALTER DATABASE 互換性レベル](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)」では、ALTER DATABASE のデータベース互換レベルに関連した SET オプションの構文と関連情報について説明します。

[ALTER DATABASE SCOPED CONFIGURATION](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 関連する動作のクエリの最適化とクエリの実行など、個別のデータベース レベルの設定に使用するため、データベース スコープ構成に関連する構文について説明します。

## <a name="syntax"></a>構文

```
-- SQL Server Syntax
ALTER DATABASE { database_name | CURRENT }
{
    MODIFY NAME = new_database_name
  | COLLATE collation_name
  | <file_and_filegroup_options>
  | SET <option_spec> [ ,...n ] [ WITH <termination> ]
}
[;]

<file_and_filegroup_options>::=
  <add_or_modify_files>::=
  <filespec>::=
  <add_or_modify_filegroups>::=
  <filegroup_updatability_option>::=

<option_spec>::=
{
  | <auto_option>
  | <change_tracking_option>
  | <cursor_option>
  | <database_mirroring_option>
  | <date_correlation_optimization_option>
  | <db_encryption_option>
  | <db_state_option>
  | <db_update_option>
  | <db_user_access_option><delayed_durability_option>
  | <external_access_option>
  | <FILESTREAM_options>
  | <HADR_options>
  | <parameterization_option>
  | <query_store_options>
  | <recovery_option>
  | <service_broker_option>
  | <snapshot_option>
  | <sql_option>
  | <termination>
  | <temporal_history_retention>
  | <compatibility_level>
      { 150 | 140 | 130 | 120 | 110 | 100 | 90 }
}
```

## <a name="arguments"></a>引数

*database_name*: 変更するデータベースの名前です。

> [!NOTE]
> このオプションは、包含データベースでは使用できません。

現在の**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。

使用中の現在のデータベースを変更することを指定します。

MODIFY NAME **=** _new_database_name_: データベースの名前を、*new_database_name* で指定した名前に変更します。

COLLATE *collation_name*: データベースの照合順序を指定します。 *collation_name* には、Windows 照合順序名または SQL 照合順序名を指定できます。 指定しない場合は、データベースに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの照合順序が割り当てられます。

> [!NOTE]
> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] でデータベースが作成された後は、照合順序を変更することはできません。

既定の照合順序以外でデータベースを作成する場合、データベース内のデータは常に、指定された照合順序を優先します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、包含データベースを作成する場合、内部カタログの情報は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定の照合順序、**Latin1_General_100_CI_AS_WS_KS_SC** を使用して維持されます。

Windows 照合順序名および SQL 照合順序名について詳しくは、「[COLLATE](~/t-sql/statements/collations.md)」をご覧ください。

**\<delayed_durability_option> ::=** 
**適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降。

詳しくは、「[ALTER DATABASE の SET オプション](../../t-sql/statements/alter-database-transact-sql-set-options.md)」および「[トランザクションの持続性の制御](../../relational-databases/logs/control-transaction-durability.md)」をご覧ください。

**\<file_and_filegroup_options>::=** 詳細については、[ALTER DATABASE の File および Filegroup オプション](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)に関するページを参照してください。

## <a name="remarks"></a>Remarks
データベースを削除するには、[DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md) を使用します。

データベースのサイズを縮小するには、[DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md) を使用します。

`ALTER DATABASE` ステートメントは自動コミット モード (既定のトランザクション管理モード) で実行する必要があり、明示的または暗黙的なトランザクションでは許可されません。

データベース ファイルの状態 (オンラインかオフラインかなど) は、データベースの状態とは別に保持されます。 詳しくは、「[ファイルの状態](../../relational-databases/databases/file-states.md)」をご覧ください。 ファイル グループ内のファイルの状態は、ファイル グループ全体の可用性を決定します。 ファイル グループを使用可能にするには、ファイル グループ内のすべてのファイルがオンラインである必要があります。 ファイル グループがオフラインの場合、SQL ステートメントでそのファイル グループにアクセスを試行するとエラーが発生します。 SELECT ステートメントのクエリ プランを作成する場合、クエリ オプティマイザーは、オフラインのファイル グループにある非クラスター化インデックスやインデックス付きビューを回避します。 これにより、これらのステートメントは正常に実行できます。 ただし、オフラインのファイル グループに、対象テーブルのヒープやクラスター化インデックスが含まれている場合には、SELECT ステートメントは失敗します。 また、オフラインのファイル グループ内にあるインデックス付きのテーブルを変更する `INSERT`、`UPDATE`、または `DELETE` ステートメントは失敗します。

データベースが RESTORING 状態にある場合、ほとんどの `ALTER DATABASE` ステートメントは失敗します。 ただし、データベース ミラーリング オプションの設定は例外です。 データベースが RESTORING 状態になるのは、アクティブな復元操作中や、バックアップ ファイルの破損によりデータベースまたはログ ファイルの復元操作が失敗した場合などです。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのプラン キャッシュは、次のいずれかのオプションを設定することにより消去されます。

|||
|-|-|
|OFFLINE|READ_WRITE|
|ONLINE|MODIFY FILEGROUP DEFAULT|
|MODIFY_NAME|MODIFY FILEGROUP READ_WRITE|
|COLLATE|MODIFY FILEGROUP READ_ONLY|
|READ_ONLY|PAGE_VERIFY|

プラン キャッシュが消去されると、後続のすべての実行プランが再コンパイルされ、場合によっては、クエリ パフォーマンスが一時的に急激に低下します。 プラン キャッシュ内のキャッシュストアが消去されるたびに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログに、以下の通知メッセージが記録されます。`SQL Server has encountered %d occurrence(s) of cachestore flush for the '%s' cachestore (part of plan cache) due to some database maintenance or reconfigure operations` このメッセージは、5 分以内にキャッシュがフラッシュされる限り、5 分間隔でログに記録されます。

プラン キャッシュは、次のシナリオでもフラッシュされます。

- `AUTO_CLOSE` データベース オプションが ON に設定されている。 データベースを参照 (または使用) するユーザー接続が 1 つも存在しない場合、バックグラウンド タスクがデータベースを自動的に閉じてシャットダウンすることを試みます。
- 既定のオプションが設定されているデータベースに対して複数のクエリを実行した。 データベースはその後削除されます。
- ソース データベースのデータベース スナップショットが削除された。
- データベースのトランザクション ログを正常に再構築した。
- データベースのバックアップを復元した。
- データベースをデタッチした。

## <a name="changing-the-database-collation"></a>データベースの照合順序の変更

データベースに別の照合順序を適用する前に、次の条件が満たされているかどうかを確認してください。

- 現在データベースを使用しているのは、1 人だけである。
- データベースの照合順序に依存するスキーマ バインド オブジェクトがない。

データベースの照合順序に依存する次のオブジェクトがデータベース内に存在する場合、ALTER DATABASE*database_name*COLLATE ステートメントは失敗します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、`ALTER` アクションをブロックしているオブジェクトごとにエラー メッセージを返します。

- SCHEMABINDING を指定して作成されたユーザー定義関数およびビュー
- 計算列
- CHECK 制約
- 既定のデータベース照合順序から継承した照合順序を持つ文字型列がテーブルにある場合に、そのテーブルを返すテーブル値関数
  
非スキーマ バインド エンティティの依存関係情報は、データベースの照合順序が変更されると自動的に更新されます。

データベースの照合順序を変更しても、データベース オブジェクトのシステム名に重複は発生しません。 照合順序の変更によって名前が重複する場合、次の名前空間が原因でデータベースの照合順序の変更が失敗することがあります。

- プロシージャ、テーブル、トリガー、ビューなどのオブジェクト名
- スキーマ名
- グループ、ロール、ユーザーなどのプリンシパル
- システム型、ユーザー定義型などのスカラー型の名前
- フルテキスト カタログ名
- オブジェクト内の列名またはパラメーター名
- テーブル内のインデックス名

新しい照合順序によって名前が重複すると、変更操作が失敗し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は重複が見つかった名前空間を示すエラー メッセージを返します。

## <a name="viewing-database-information"></a>データベース情報の表示

カタログ ビュー、システム関数、およびシステム ストアド プロシージャを使用して、データベース、ファイルおよびファイル グループについての情報を返すことができます。

## <a name="permissions"></a>アクセス許可

データベースに対する `ALTER` 権限が必要です。

## <a name="examples"></a>使用例

### <a name="a-changing-the-name-of-a-database"></a>A. データベースの名前を変更する

次の例では、`AdventureWorks2012` データベースの名前を `Northwind` に変更します。

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
Modify Name = Northwind ;
GO
```

### <a name="b-changing-the-collation-of-a-database"></a>B. データベースの照合順序を変更する

次の例では、`testdb`S 照合順序で `SQL_Latin1_General_CP1_CI_A` という名前のデータベースを作成した後、`testdb` データベースの照合順序を `COLLATE French_CI_AI` に変更します。

**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。

```sql
USE master;
GO

CREATE DATABASE testdb
COLLATE SQL_Latin1_General_CP1_CI_AS ;
GO

ALTER DATABASE testDB
COLLATE French_CI_AI ;
GO
```

## <a name="see-also"></a>参照

- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)
- [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)
- [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)
- [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)
- [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)
- [システム データベース](../../relational-databases/databases/system-databases.md)

::: moniker-end
::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"

||||||
|---|---|---|---|---|
|[SQL Server](alter-database-transact-sql.md?view=sql-server-2017)|**_\* SQL Database<br />単一データベース/エラスティック プール\*_** &nbsp;|[SQL Database<br />マネージド インスタンス](alter-database-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](alter-database-transact-sql.md?view=azure-sqldw-latest)|[Analytics Platform<br />System (PDW)](alter-database-transact-sql.md?view=aps-pdw-2016-au7)|
||||||

&nbsp;

## <a name="overview-azure-sql-database-single-databaseelastic-pool"></a>概要:Azure SQL Database 単一データベース/エラスティック プール

Azure SQL Database では、このステートメントを使って単一データベース/エラスティック プール上のデータベースを変更します。 データベースの名前の変更、データベースのエディションとサービス目標の変更、エラスティック プールへのデータベースの参加またはエラスティック プールからのデータベースの削除、データベース オプションの設定、geo レプリケーション リレーションシップでのセカンダリ としてのデータベースの追加または削除、データベースの互換性レベルの設定を行うには、このステートメントを使います。

解説が長くなるため、ALTER DATABASE の構文は複数の記事に分けて説明します。

ALTER DATABASE: この記事では、データベースの名前と照合順序を変更するための構文および関連情報について説明します。

「[ALTER DATABASE の SET オプション](../../t-sql/statements/alter-database-transact-sql-set-options.md?view=azuresqldb-currentls)」では、ALTER DATABASE の SET オプションを使ってデータベースの属性を変更するための構文と関連情報について説明します。

「[ALTER DATABASE 互換性レベル](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md?view=azuresqldb-currentls)」では、ALTER DATABASE のデータベース互換レベルに関連した SET オプションの構文と関連情報について説明します。

## <a name="syntax"></a>構文

```
-- Azure SQL Database Syntax
ALTER DATABASE { database_name | CURRENT }
{
    MODIFY NAME = new_database_name
  | MODIFY ( <edition_options> [, ... n] )
  | SET { <option_spec> [ ,... n ] WITH <termination>}
  | ADD SECONDARY ON SERVER <partner_server_name>
    [WITH ( <add-secondary-option>::=[, ... n] ) ]
  | REMOVE SECONDARY ON SERVER <partner_server_name>
  | FAILOVER
  | FORCE_FAILOVER_ALLOW_DATA_LOSS
}
[;]

<edition_options> ::=
{

  MAXSIZE = { 100 MB | 250 MB | 500 MB | 1 ... 1024 ... 4096 GB }
  | EDITION = { 'basic' | 'standard' | 'premium' | 'GeneralPurpose' | 'BusinessCritical' | 'Hyperscale'}
  | SERVICE_OBJECTIVE =
       { <service-objective>
       | { ELASTIC_POOL (name = <elastic_pool_name>) }
       }
}

<add-secondary-option> ::=
   {
      ALLOW_CONNECTIONS = { ALL | NO }
     | SERVICE_OBJECTIVE =
       { <service-objective>
       | { ELASTIC_POOL ( name = <elastic_pool_name>) }
       }
   }

<service-objective> ::={ 'basic' |'S0' | 'S1' | 'S2' | 'S3'| 'S4'| 'S6'| 'S7'| 'S9'| 'S12'
       | 'P1' | 'P2' | 'P4'| 'P6' | 'P11' | 'P15'
      | 'GP_Gen4_1' | 'GP_Gen4_2' | 'GP_Gen4_3' | 'GP_Gen4_4' | 'GP_Gen4_5' | 'GP_Gen4_6'
      | 'GP_Gen4_7' | 'GP_Gen4_8' | 'GP_Gen4_9' | 'GP_Gen4_10' | 'GP_Gen4_16' | 'GP_Gen4_24'
      | 'GP_Gen5_2' | 'GP_Gen5_4' | 'GP_Gen5_6' | 'GP_Gen5_8' | 'GP_Gen5_10' | 'GP_Gen5_12' | 'GP_Gen5_14'
      | 'GP_Gen5_16' | 'GP_Gen5_18' | 'GP_Gen5_20' | 'GP_Gen5_24' | 'GP_Gen5_32' | 'GP_Gen5_40' | 'GP_Gen5_80'
      | 'GP_Fsv2_72'
      | 'GP_S_Gen5_1' | 'GP_S_Gen5_2' | 'GP_S_Gen5_4' | 'GP_S_Gen5_6' | 'GP_S_Gen5_8'
      | 'GP_S_Gen5_10' | 'GP_S_Gen5_12' | 'GP_S_Gen5_14' | 'GP_S_Gen5_16'
      | 'BC_Gen4_1' | 'BC_Gen4_2' | 'BC_Gen4_3' | 'BC_Gen4_4' | 'BC_Gen4_5' | 'BC_Gen4_6'
      | 'BC_Gen4_7' | 'BC_Gen4_8' | 'BC_Gen4_9' | 'BC_Gen4_10' | 'BC_Gen4_16' | 'BC_Gen4_24'
      | 'BC_Gen5_2' | 'BC_Gen5_4' | 'BC_Gen5_6' | 'BC_Gen5_8' | 'BC_Gen5_10' | 'BC_Gen5_12' | 'BC_Gen5_14'
      | 'BC_Gen5_16' | 'BC_Gen5_18' | 'BC_Gen5_20' | 'BC_Gen5_24' | 'BC_Gen5_32' | 'BC_Gen5_40' | 'BC_Gen5_80'
      | 'BC_M_128'
      | 'HS_GEN4_1' | 'HS_GEN4_2' | 'HS_GEN4_4' | 'HS_GEN4_8' | 'HS_GEN4_16' | 'HS_GEN4_24'
      | 'HS_GEN5_2' | 'HS_GEN5_4' | 'HS_GEN5_8' | 'HS_GEN5_16' | 'HS_GEN5_24' | 'HS_GEN5_32' | 'HS_GEN5_48' | 'HS_GEN5_80'
      | { ELASTIC_POOL(name = <elastic_pool_name>) }
      }

<option_spec> ::=
{
    <auto_option>
  | <change_tracking_option>
  | <cursor_option>
  | <db_encryption_option>
  | <db_update_option>
  | <db_user_access_option>
  | <delayed_durability_option>
  | <parameterization_option>
  | <query_store_options>
  | <snapshot_option>
  | <sql_option>
  | <target_recovery_time_option>
  | <termination>
  | <temporal_history_retention>
  | <compatibility_level>
    { 150 | 140 | 130 | 120 | 110 | 100 | 90 }

}
```

## <a name="arguments"></a>引数

*database_name*: 変更するデータベースの名前です。

CURRENT: 使用中の現在のデータベースを変更する必要があることを指定します。

MODIFY NAME **=** _new_database_name_: データベースの名前を、*new_database_name* で指定した名前に変更します。 次の例では、`db1` データベースの名前を `db2` に変更します。

```sql
ALTER DATABASE db1
    MODIFY Name = db2 ;
```

MODIFY (EDITION **=** ['basic' | 'standard' | 'premium' |'GeneralPurpose' | 'BusinessCritical' | 'Hyperscale']): データベースのサービス レベルを変更します。

次の例では、エディションを `premium` に変更します。

```sql
ALTER DATABASE current
    MODIFY (EDITION = 'premium');
```

> [!IMPORTANT]
> データベースの MAXSIZE プロパティがそのエディションでサポートされる有効な範囲内の値に設定されていない場合、EDITION の変更は失敗します。

MODIFY (MAXSIZE **=** [100 MB | 500 MB | 1 | 1024...4096] GB): データベースの最大サイズを指定します。 最大サイズは、データベースの EDITION プロパティの有効な値セットに準拠している必要があります。 データベースの最大サイズを変更すると、データベースの EDITION も変更される場合があります。

> [!NOTE]
> **MAXSIZE** 引数は、ハイパースケール サービス層の単一データベースには適用されません。 ハイパースケール サービス層のデータベースは、必要に応じて 100 TB まで拡張できます。 SQL Database サービスによってストレージが自動的に追加されます。最大サイズを設定する必要はありません。

**DTU モデル**

|**MAXSIZE**|**基本**|**S0-S2**|**S3-S12**|**P1-P6**|**P11-P15**|
|-----------------|---------------|------------------|-----------------|-----------------|-----------------|-----------------|
|100 MB|√|√|√|√|√|
|250 MB|√|√|√|√|√|
|500 MB|√|√|√|√|√|
|1 GB|√|√|√|√|√|
|2 GB|√ (D)|√|√|√|√|
|5 GB|なし|√|√|√|√|
|10 GB|なし|√|√|√|√|
|20 GB|なし|√|√|√|√|
|30 GB|なし|√|√|√|√|
|40 GB|なし|√|√|√|√|
|50 GB|なし|√|√|√|√|
|100 GB|なし|√|√|√|√|
|150 GB|なし|√|√|√|√|
|200 GB|なし|√|√|√|√|
|250 GB|なし|√ (D)|√ (D)|√|√|
|300 GB|なし|√|√|√|√|
|400 GB|なし|√|√|√|√|
|500 GB|なし|√|√|√ (D)|√|
|750 GB|なし|√|√|√|√|
|1024 GB|なし|√|√|√|√ (D)|
|1024 GB から 4096 GB (256 GB ずつ増分)*|なし|なし|なし|なし|√|

\* P11 と P15 では 1024 GB を既定のサイズとして MAXSIZE が 4 TB まで許可されます。 P11 と P15 では、追加料金なしで付属のストレージを 4 TB まで使用できます。 次の地域の Premium レベルでは、現在 1 TB を超える MAXSIZE を使用できます: 米国東部 2、米国西部、米国政府バージニア、西ヨーロッパ、ドイツ中部、東南アジア、東日本、オーストラリア東部、カナダ中部、カナダ東部。 DTU モデルのリソースの制限事項に関する詳細については、[DTU リソースの制限](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)に関する記事を参照してください。

DTU モデルの MAXSIZE 値。指定される場合は、上記の表に示すように指定されたサービス レベルで有効な値である必要があります。

**仮想コア モデル**

**General Purpose - プロビジョニング済みコンピューティング - Gen4 (パート 1)**

|MAXSIZE|GP_Gen4_1|GP_Gen4_2|GP_Gen4_3|GP_Gen4_4|GP_Gen4_5|GP_Gen4_6|
|:----- | ------: |-------: |-------: |-------: |-------: |--------:|
|データの最大サイズ (GB)|1024|1024|1024|1536|1536|1536|

**General Purpose - プロビジョニング済みコンピューティング - Gen4 (パート 2)**

|MAXSIZE|GP_Gen4_7|GP_Gen4_8|GP_Gen4_9|GP_Gen4_10|GP_Gen4_16|GP_Gen4_24
|:----- | ------: |-------: |-------: |-------: |-------: |--------:|
|データの最大サイズ (GB)|1536|3072|3072|3072|4096|4096|

**General Purpose - プロビジョニング済みコンピューティング - Gen5 (パート 1)**

|MAXSIZE|GP_Gen5_2|GP_Gen5_4|GP_Gen5_6|GP_Gen5_8|GP_Gen5_10|GP_Gen5_12|GP_Gen5_14|
|:----- | ------: |-------: |-------: |-------: |--------: |---------:|--------: |
|データの最大サイズ (GB)|1024|1024|1024|1536|1536|1536|1536|

**General Purpose - プロビジョニング済みコンピューティング - Gen5 (パート 2)**

|MAXSIZE|GP_Gen5_16|GP_Gen5_18|GP_Gen5_20|GP_Gen5_24|GP_Gen5_32|GP_Gen5_40|GP_Gen5_80|
|:----- | ------: |-------: |-------: |-------: |--------: |---------:|--------: |
|データの最大サイズ (GB)|3072|3072|3072|4096|4096|4096|4096|

**General Purpose - プロビジョニング済みコンピューティング - Fsv2 シリーズ (プレビュー)**

|MAXSIZE|GP_Fsv2_72|
|:----- | ------: |
|データの最大サイズ (GB)|4096|

**General Purpose - サーバーレス コンピューティング - Gen5 (パート 1)**

|MAXSIZE|GP_S_Gen5_1|GP_S_Gen5_2|GP_S_Gen5_4|GP_S_Gen5_6|GP_S_Gen5_8|
|:----- | ------: |-------: |-------: |-------: |--------: |
|最大仮想コア数|1|2|4|6|8|

**General Purpose - サーバーレス コンピューティング - Gen5 (パート 2)**

|MAXSIZE|GP_S_Gen5_10|GP_S_Gen5_12|GP_S_Gen5_14|GP_S_Gen5_16|
|:----- | ------: |-------: |-------: |-------: |
|最大仮想コア数|10|12|14|16|

**Business Critical - プロビジョニング済みコンピューティング - Gen4 (パート 1)**

|パフォーマンス レベル|BC_Gen4_1|BC_Gen4_2|BC_Gen4_3|BC_Gen4_4|BC_Gen4_5|BC_Gen4_6|
|:--------------- | ------: |-------: |-------: |-------: |-------: |-------: |
|データの最大サイズ (GB)|1024|1024|1024|1024|1024|1024|

**Business Critical - プロビジョニング済みコンピューティング - Gen4 (パート 2)**

|パフォーマンス レベル|BC_Gen4_7|BC_Gen4_8|BC_Gen4_9|BC_Gen4_10|BC_Gen4_16|BC_Gen4_24|
|:--------------- | ------: |-------: |-------: |--------: |--------: |--------: |
|データの最大サイズ (GB)|1024|1024|1024|1024|1024|1024|

**Business Critical - プロビジョニング済みコンピューティング - Gen5 (パート 1)**

|MAXSIZE|BC_Gen5_2|BC_Gen5_4|BC_Gen5_6|BC_Gen5_8|BC_Gen5_10|BC_Gen5_12|BC_Gen5_14|
|:----- | ------: |-------: |-------: |-------: |---------: |--------:|--------: |
|データの最大サイズ (GB)|1024|1024|1024|1536|1536|1536|1536|

**Business Critical - プロビジョニング済みコンピューティング - Gen5 (パート 2)**

|MAXSIZE|BC_Gen5_16|BC_Gen5_18|BC_Gen5_20|BC_Gen5_24|BC_Gen5_32|BC_Gen5_40|BC_Gen5_80|
|:----- | -------: |--------: |--------: |--------: |--------: |---------:|--------: |
|データの最大サイズ (GB)|3072|3072|3072|4096|4096|4096|4096|

**Business Critical - プロビジョニング済みコンピューティング - M シリーズ (プレビュー)**

|MAXSIZE|BC_M_128|
|:----- | -------: |
|データの最大サイズ (GB)|4096|


vCore モデルを使用する場合に `MAXSIZE` 値が設定されていない場合、既定値は 32 GB です。 仮想コア モデルのリソースの制限事項の詳細については、[仮想コア リソースの制限](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)に関するページを参照してください。

引数 MAXSIZE および EDITION には、以下の規則が適用されます。

- EDITION が指定され、MAXSIZE が指定されていない場合は、エディションの既定値が使用されます。 たとえば、EDITION が Standard に設定されていて、MAXSIZE が指定されていない場合、MAXSIZE は自動的に 250 MB に設定されます。
- MAXSIZE も EDITION も指定されていない場合、EDITION は General Purpose に設定され、MAXSIZE は 32 GB に設定されます。

MODIFY (SERVICE_OBJECTIVE = \<service-objective>): パフォーマンス レベルを指定します。 次の例では、Premium データベースのサービスの目標を `P6` に変更します。

```sql
ALTER DATABASE current
    MODIFY (SERVICE_OBJECTIVE = 'P6');
```

SERVICE_OBJECTIVE

- **単一のデータベースおよびプールされたデータベースの場合**

  - パフォーマンス レベルを指定します。 サービスの目標に使用できる値は、`S0`、`S1`、`S2`、`S3`、`S4`、`S6`、`S7`、`S9`、`S12`、`P1`、`P2`、`P4`、`P6`、`P11`、`P15`、`GP_GEN4_1`、`GP_GEN4_2`、`GP_GEN4_3`、`GP_GEN4_4`、`GP_GEN4_5`、`GP_GEN4_6`、`GP_GEN4_7`、`GP_GEN4_8`、`GP_GEN4_7`、`GP_GEN4_8`、`GP_GEN4_9`、`GP_GEN4_10`、`GP_GEN4_16`、`GP_GEN4_24`、`BC_GEN4_1`、`BC_GEN4_2`、`BC_GEN4_3`、`BC_GEN4_4`、`BC_GEN4_5`、`BC_GEN4_6`、`BC_GEN4_7`、`BC_GEN4_8`、`BC_GEN4_9`、`BC_GEN4_10`、`BC_GEN4_16`、`BC_GEN4_24`、`GP_Gen5_2`、`GP_Gen5_4`、`GP_Gen5_6`、`GP_Gen5_8`、`GP_Gen5_10`、`GP_Gen5_12`、`GP_Gen5_14`、`GP_Gen5_16`、`GP_Gen5_18`、`GP_Gen5_20`、`GP_Gen5_24`、`GP_Gen5_32`、`GP_Gen5_40`、`GP_Gen5_80`、`GP_Fsv2_72`、`BC_Gen5_2`、`BC_Gen5_4`、`BC_Gen5_6`、`BC_Gen5_8`、`BC_Gen5_10`、`BC_Gen5_12`、`BC_Gen5_14`、`BC_Gen5_16`、`BC_Gen5_18`、`BC_Gen5_20`、`BC_Gen5_24`、`BC_Gen5_32`、`BC_Gen5_40`、`BC_Gen5_80`、`BC_M_128` です。


- **サーバーレス データベースの場合**

  - パフォーマンス レベルを指定します。 サービスの目標に使用できる値は、`GP_S_Gen5_1`、`GP_S_Gen5_2`、`GP_S_Gen5_4`、`GP_S_Gen5_6`、`GP_S_Gen5_8`、`GP_S_Gen5_10`、`GP_S_Gen5_12`、`GP_S_Gen5_14`、`GP_S_Gen5_16` です。


- **ハイパースケール サービス層の単一データベースの場合**

  - パフォーマンス レベルを指定します。 サービスの目標に使用できる値は、`HS_GEN4_1` `HS_GEN4_2` `HS_GEN4_4` `HS_GEN4_8` `HS_GEN4_16`、`HS_GEN4_24`、`HS_Gen5_2`、`HS_Gen5_4`、`HS_Gen5_8`、`HS_Gen5_16`、`HS_Gen5_24`、`HS_Gen5_32`、`HS_Gen5_48`、`HS_Gen5_80` です。

サービス目標に関する説明およびサイズ、エディション、サービス目標の組み合わせの詳細については、[Azure SQL Database サービス レベルとパフォーマンス レベル](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)、[DTU リソースの制限](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)、[仮想コア リソースの制限](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)に関する記事を参照してください。 PRS サービスの目標のサポートはなくなりました。 質問については、電子メール エイリアス premium-rs@microsoft.com を使用してください。

MODIFY (SERVICE_OBJECTIVE = ELASTIC\_POOL (name = \<elastic_pool_name>): エラスティック プールに既存のデータベースを追加するには、データベースの SERVICE_OBJECTIVE を ELASTIC_POOL に設定し、エラスティック プールの名前を指定します。 このオプションを使用して、データベースを同じサーバー内の別のエラスティック プールに変更することもできます。 詳しくは、[SQL Database エラスティック プールの作成と管理](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)に関するページをご覧ください。 エラスティック プールからデータベースを削除するには、ALTER DATABASE を使用して、SERVICE_OBJECTIVE を 1 つのデータベースのパフォーマンス レベルに設定します。

> [!NOTE]
> ハイパースケール サービス層のデータベースをエラスティック プールに追加することはできません。

ADD SECONDARY ON SERVER \<partner_server_name>

パートナー サーバー上に同じ名前の geo レプリケーションのセカンダリ データベースを作成し、ローカル データベースを geo レプリケーションのプライマリにして、プライマリから新しいセカンダリに非同期でデータのレプリケーションを開始します。 セカンダリ上に同じ名前のデータベースが既に存在する場合、コマンドは失敗します。 コマンドは、プライマリとなるローカル データベースをホストしているサーバーの master データベースで実行されます。

> [!IMPORTANT]
> ハイパースケール サービス層では、geo レプリケーションは現在サポートされていません。

WITH ALLOW_CONNECTIONS { **ALL** | NO }: ALLOW_CONNECTIONS が指定されていない場合は、これは既定で ALL に設定されます。 ALL に設定されている場合は、適切なアクセス許可を持つすべてのログインに接続を許可する読み取り専用データベースになります。

WITH SERVICE_OBJECTIVE { `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `GP_GEN4_1`, `GP_GEN4_2`, `GP_GEN4_3`, `GP_GEN4_4`, `GP_GEN4_5`, `GP_GEN4_6`, `GP_GEN4_7`, `GP_GEN4_8`, `GP_GEN4_7`, `GP_GEN4_8`, `GP_GEN4_9`, `GP_GEN4_10`, `GP_GEN4_16`, `GP_GEN4_24`, `BC_GEN4_1`, `BC_GEN4_2`, `BC_GEN4_3`, `BC_GEN4_4`, `BC_GEN4_5`, `BC_GEN4_6`, `BC_GEN4_7`, `BC_GEN4_8`, `BC_GEN4_9`, `BC_GEN4_10`, `BC_GEN4_16`, `BC_GEN4_24`, `GP_Gen5_2`, `GP_Gen5_4`, `GP_Gen5_6`, `GP_Gen5_8`, `GP_Gen5_10`, `GP_Gen5_12`, `GP_Gen5_14`, `GP_Gen5_16`, `GP_Gen5_18`, `GP_Gen5_20`, `GP_Gen5_24`, `GP_Gen5_32`, `GP_Gen5_40`, `GP_Gen5_80`, `GP_Fsv2_72`, `GP_S_Gen5_1`, `GP_S_Gen5_2`, `GP_S_Gen5_4`, `GP_S_Gen5_6`, `GP_S_Gen5_8`, `GP_S_Gen5_10`, `GP_S_Gen5_12`, `GP_S_Gen5_14`, `GP_S_Gen5_16`, `BC_Gen5_2`, `BC_Gen5_4`, `BC_Gen5_6`, `BC_Gen5_8`, `BC_Gen5_10`, `BC_Gen5_12`, `BC_Gen5_14`, `BC_Gen5_16`, `BC_Gen5_18`, `BC_Gen5_20`, `BC_Gen5_24`, `BC_Gen5_32`,`BC_Gen5_40`, `BC_Gen5_80`, `BC_M_128` }

SERVICE_OBJECTIVE が指定されていない場合、セカンダリ データベースがプライマリ データベースと同じサービス レベルで作成します。 SERVICE_OBJECTIVE を指定した場合は、指定したレベルでセカンダリ データベースが作成されます。 このオプションでは、サービス レベルのコストが比較的低い geo レプリケートされたセカンダリの作成がサポートされます。 指定する SERVICE_OBJECTIVE は、ソースと同じエディション内でなければなりません。 たとえば、エディションが Premium の場合、S0 を指定することはできません。

ELASTIC_POOL (name = \<elastic_pool_name>): ELASTIC_POOL が指定されていない場合、セカンダリ データベースはエラスティック プールに作成されません。 ELASTIC_POOL が指定されている場合、セカンダリ データベースが指定されたプールに作成されます。

> [!IMPORTANT]
> ADD SECONDARY コマンドを実行するユーザーは、プライマリ サーバー上で DBManager であること、ローカル データベース内で db_owner メンバーシップを持っていること、およびセカンダリ サーバー上で DBManager であることが必要です。

REMOVE SECONDARY ON SERVER \<partner_server_name>: 指定されたサーバー上にある、指定された geo レプリケートされたセカンダリ データベースを削除します。 このコマンドは、プライマリ データベースをホストしているサーバー上の master データベース上で実行されます。

> [!IMPORTANT]
> REMOVE SECONDARY コマンドを実行するユーザーは、プライマリ サーバー上で DBManager でなければなりません。

FAILOVER: コマンドを実行する geo レプリケーション パートナーシップ内のセカンダリ データベースのレベルを上げてプライマリにし、現在のプライマリのレベルを下げて新しいセカンダリにします。 このプロセスの一環として、geo レプリケーション モードは、非同期モードから同期モードへと一時的に切り替わります。 フェールオーバー プロセス時:

1. プライマリでは、新しいトランザクションが処理が停止されます。
2. すべての未処理のトランザクションは、セカンダリにフラッシュされます。
3. セカンダリがプライマリになり、古いプライマリと新しいセカンダリを使用して、非同期の geo レプリケーションが開始されます。

このシーケンスは、データの損失が発生しないことを保証します。 両方のデータベースが使用できない期間は、ロールを切り替えている間の 0 から 25 秒程度です。 操作全体を約 1 分以内に実行する必要があります。 このコマンドが実行されたときにプライマリ データベースが使用できない場合、プライマリ データベースが使用できないことを示すエラー メッセージで、コマンドは失敗します。 フェールオーバー プロセスが完了せず、スタックしているように見える場合は、まず、強制フェールオーバー コマンドを使用して、データの消失を許容します。次に、消失したデータを復旧する必要がある場合は、DevOps (CSS) に連絡して、消失したデータの復旧を依頼します。

> [!IMPORTANT]
> FAILOVER コマンドを実行するユーザーは、プライマリ サーバーとセカンダリ サーバーの両方で DBManager になる必要があります。

FORCE_FAILOVER_ALLOW_DATA_LOSS: コマンドを実行する geo レプリケーション パートナーシップ内のセカンダリ データベースのレベルを上げてプライマリにし、現在のプライマリのレベルを下げて新しいセカンダリにします。 現在のプライマリが使用できない場合にのみ、このコマンドを使用します。 これは、可用性の復元が不可欠で、一部のデータ消失が許容される場合のディザスター リカバリー専用に設計されています。

強制フェールオーバー中:

1. 指定したセカンダリ データベースはすぐに、プライマリ データベースになり、新しいトランザクションの受け入れを開始します。
2. 元のプライマリが新しいプライマリに再接続できると、元のプライマリ上で増分バックアップが実行され、元のプライマリは新しいセカンダリになります。
3. 古いプライマリのこの増分バックアップからデータを復旧するには、ユーザーは devops/CSS である必要があります。
4. その他のセカンダリがある場合は、自動的に再構成されて新しいプライマリのセカンダリになります。 このプロセスは非同期で、このプロセスが完了するまで、遅延が発生することがあります。 再構成が完了するまで、セカンダリは古いプライマリのセカンダリであり続けます。

> [!IMPORTANT]
> `FORCE_FAILOVER_ALLOW_DATA_LOSS` コマンドを実行するユーザーは、プライマリ サーバーとセカンダリ サーバーの両方で `dbmanager` ロールに属する必要があります。

## <a name="remarks"></a>Remarks

データベースを削除するには、[DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md) を使用します。
データベースのサイズを縮小するには、[DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md) を使用します。

`ALTER DATABASE` ステートメントは自動コミット モード (既定のトランザクション管理モード) で実行する必要があり、明示的または暗黙的なトランザクションでは許可されません。

プラン キャッシュが消去されると、後続のすべての実行プランが再コンパイルされ、場合によっては、クエリ パフォーマンスが一時的に急激に低下します。 プラン キャッシュ内のキャッシュストアが消去されるたびに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログに、以下の通知メッセージが記録されます。`SQL Server has encountered %d occurrence(s) of cachestore flush for the '%s' cachestore (part of plan cache) due to some database maintenance or reconfigure operations` このメッセージは、5 分以内にキャッシュがフラッシュされる限り、5 分間隔でログに記録されます。

プロシージャ キャッシュは、次のシナリオでもフラッシュされます。既定のオプションが設定されているデータベースに対して複数のクエリを実行した。 データベースはその後削除されます。

## <a name="viewing-database-information"></a>データベース情報の表示

カタログ ビュー、システム関数、およびシステム ストアド プロシージャを使用して、データベース、ファイルおよびファイル グループについての情報を返すことができます。

## <a name="permissions"></a>アクセス許可

データベースを変更するには、ログインがサーバーレベル プリンシパル ログイン (プロビジョニング プロセスで作成)、マスターの `dbmanager` データベース ロールのメンバー、現在のデータベースの `db_owner` データベース ロールのメンバー、またはデータベースの `dbo` のいずれかである必要があります。

## <a name="examples"></a>使用例

### <a name="a-check-the-edition-options-and-change-them"></a>A. エディション オプションを確認して変更します。

データベース db1 のエディションと最大サイズを設定します。

```sql
SELECT Edition = DATABASEPROPERTYEX('db1', 'EDITION'),
        ServiceObjective = DATABASEPROPERTYEX('db1', 'ServiceObjective'),
        MaxSizeInBytes =  DATABASEPROPERTYEX('db1', 'MaxSizeInBytes');

ALTER DATABASE [db1] MODIFY (EDITION = 'Premium', MAXSIZE = 1024 GB, SERVICE_OBJECTIVE = 'P15');
```

### <a name="b-moving-a-database-to-a-different-elastic-pool"></a>B. データベースを別のエラスティック プールに移動します。

pool1 という名前のプールに既存のデータベースを移動します。

```sql
ALTER DATABASE db1
MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = pool1 ) ) ;
```

### <a name="c-add-a-geo-replication-secondary"></a>C. geo レプリケーションのセカンダリを追加します。

ローカル サーバー上の db1 のサーバー `secondaryserver` に読み取り可能なセカンダリ データベース db1 を作成します。

```sql
ALTER DATABASE db1
ADD SECONDARY ON SERVER secondaryserver
WITH ( ALLOW_CONNECTIONS = ALL )
```

### <a name="d-remove-a-geo-replication-secondary"></a>D. geo レプリケーションのセカンダリを削除します。

サーバー `secondaryserver` 上のセカンダリ データベース db1 を削除します。

```sql
ALTER DATABASE db1
REMOVE SECONDARY ON SERVER testsecondaryserver
```

### <a name="e-failover-to-a-geo-replication-secondary"></a>E. geo レプリケーションのセカンダリにフェールオーバーします。

サーバー `secondaryserver` で実行されると、サーバー `secondaryserver` 上のセカンダリ データベース db1 を昇格させて新しいプライマリ データベースにします。

```sql
ALTER DATABASE db1 FAILOVER
```

### <a name="e-force-failover-to-a-geo-replication-secondary-with-data-loss"></a>E. geo レプリケーションのセカンダリへのフェールオーバーを強制します (この場合、データが失われることがあります)。

プライマリ データベースが使用不可能になった場合、サーバー `secondaryserver` で実行されると、サーバー `secondaryserver` 上のセカンダリ データベース db1 が新しいプライマリ データベースとして強制されます。 このオプションでは、データが失われる可能性があります。

```sql
ALTER DATABASE db1 FORCE_FAILOVER_ALLOW_DATA_LOSS
```

### <a name="g-update-a-single-database-to-service-tier-s0-standard-edition-performance-level-0"></a>G. 単一データベースをサービス層 S0 (標準エディション、パフォーマンス レベル 0) に更新します。

単一データベースをパフォーマンス レベルが S0、最大サイズが 250 GB の標準エディション (サービス層) に更新します。

```sql
ALTER DATABASE [db1] MODIFY (EDITION = 'Standard', MAXSIZE = 250 GB, SERVICE_OBJECTIVE = 'S0');
```

## <a name="see-also"></a>参照

- [CREATE DATABASE - Azure SQL Database](../../t-sql/statements/create-database-transact-sql.md?view=azuresqldb-currentls)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)
- [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)
- [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)
- [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)
- [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)
- [システム データベース](../../relational-databases/databases/system-databases.md)

::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

||||||
|---|---|---|---|---|
|[SQL Server](alter-database-transact-sql.md?view=sql-server-2017)|[SQL Database<br />単一データベース/エラスティック プール](alter-database-transact-sql.md?view=azuresqldb-current)|**_\* SQL Database<br />マネージド インスタンス \*_** &nbsp;|[SQL Data<br />Warehouse](alter-database-transact-sql.md?view=azure-sqldw-latest)|[Analytics Platform<br />System (PDW)](alter-database-transact-sql.md?view=aps-pdw-2016-au7)|
||||||

&nbsp;

## <a name="overview-azure-sql-database-managed-instance"></a>概要:Azure SQL Database マネージド インスタンス

Azure SQL Database マネージド インスタンスでは、このステートメントを使ってデータベース オプションを設定します。

解説が長くなるため、ALTER DATABASE の構文は複数の記事に分けて説明します。

ALTER DATABASE: この記事では、ファイルとファイル グループのオプションの設定、データベース オプションの設定、およびデータベースの互換性レベルの設定のための構文と関連情報を説明します。  
  
「[ALTER DATABASE の File および Filegroup オプション](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md?&tabs=sqldbmi)」では、データベースのファイルおよびファイル グループを追加したり削除したりするための構文と関連情報のほか、ファイルおよびファイル グループの属性を変更するための構文について説明します。  
  
「[ALTER DATABASE の SET オプション](../../t-sql/statements/alter-database-transact-sql-set-options.md?&tabs=sqldbmi)」では、ALTER DATABASE の SET オプションを使ってデータベースの属性を変更するための構文と関連情報について説明します。  
  
「[ALTER DATABASE 互換性レベル](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md?&tabs=sqldbmi)」では、ALTER DATABASE のデータベース互換レベルに関連した SET オプションの構文と関連情報について説明します。  

## <a name="syntax"></a>構文

```
-- Azure SQL Database Syntax  
ALTER DATABASE { database_name | CURRENT }  
{
    MODIFY NAME = new_database_name
  | COLLATE collation_name
  | <file_and_filegroup_options>  
  | SET <option_spec> [ ,...n ]  
}  
[;]

<file_and_filegroup_options>::=  
  <add_or_modify_files>::=  
  <filespec>::=
  <add_or_modify_filegroups>::=  
  <filegroup_updatability_option>::=  

<option_spec> ::=
{
    <auto_option>
  | <change_tracking_option>
  | <cursor_option>
  | <db_encryption_option>  
  | <db_update_option>
  | <db_user_access_option>
  | <delayed_durability_option>
  | <parameterization_option>
  | <query_store_options>
  | <snapshot_option>
  | <sql_option>
  | <target_recovery_time_option>
  | <temporal_history_retention>
  | <compatibility_level>
      { 150 | 140 | 130 | 120 | 110 | 100 | 90 }

}  

```

## <a name="arguments"></a>引数

*database_name*: 変更するデータベースの名前です。

CURRENT: 使用中の現在のデータベースを変更する必要があることを指定します。

## <a name="remarks"></a>Remarks

データベースを削除するには、[DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md) を使用します。
データベースのサイズを縮小するには、[DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md) を使用します。

`ALTER DATABASE` ステートメントは自動コミット モード (既定のトランザクション管理モード) で実行する必要があり、明示的または暗黙的なトランザクションでは許可されません。

プラン キャッシュが消去されると、後続のすべての実行プランが再コンパイルされ、場合によっては、クエリ パフォーマンスが一時的に急激に低下します。 プラン キャッシュ内のキャッシュストアが消去されるたびに、"[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、一部のデータベース メンテナンス操作または再構成操作により、'%s' キャッシュストア (プラン キャッシュの一部) のキャッシュストア フラッシュを %d 個検出しました" という情報メッセージが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログに含まれます。 このメッセージは、5 分以内にキャッシュがフラッシュされる限り、5 分間隔でログに記録されます。

既定オプションのデータベースに対して複数のクエリが実行されても、プラン キャッシュはフラッシュされます。 データベースはその後削除されます。

## <a name="viewing-database-information"></a>データベース情報の表示

カタログ ビュー、システム関数、およびシステム ストアド プロシージャを使用して、データベース、ファイルおよびファイル グループについての情報を返すことができます。

## <a name="permissions"></a>アクセス許可

データベースを変更できるのは、(準備プロセスによって作成される) サーバーレベルのプリンシパルのログイン、または `dbcreator` データベース ロールのメンバーだけです。

> [!IMPORTANT]
> データベースの所有者であっても `dbcreator` ロールのメンバーでない場合は、データベースを変更できません。

## <a name="examples"></a>使用例

自動チューニングを設定する方法と、マネージド インスタンスにファイルを追加する方法の例を次に示します。

```sql
ALTER DATABASE WideWorldImporters
  SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON)

ALTER DATABASE WideWorldImporters
  ADD FILE (NAME = 'data_17')
```

## <a name="see-also"></a>参照

- [CREATE DATABASE - Azure SQL Database](../../t-sql/statements/create-database-transact-sql.md?view=azuresqldb-mi-current)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)
- [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)[sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)
- [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)
- [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)
- [システム データベース](../../relational-databases/databases/system-databases.md)

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

||||||
|---|---|---|---|---|
|[SQL Server](alter-database-transact-sql.md?view=sql-server-2017)|[SQL Database<br />単一データベース/エラスティック プール](alter-database-transact-sql.md?view=azuresqldb-current)|[SQL Database<br />マネージド インスタンス](alter-database-transact-sql.md?view=azuresqldb-mi-current)|**_\* SQL Data<br />Warehouse \*_** &nbsp;|[Analytics Platform<br />System (PDW)](alter-database-transact-sql.md?view=aps-pdw-2016-au7)|
||||||

&nbsp;

## <a name="overview-azure-sql-data-warehouse"></a>概要:Azure SQL Data Warehouse

Azure SQL Data Warehouse では、'ALTER DATABASE' によりデータベースの名前、最大サイズ、またはサービス目標が変更されます。

解説が長くなるため、ALTER DATABASE の構文は複数の記事に分けて説明します。

「[ALTER DATABASE の SET オプション](../../t-sql/statements/alter-database-transact-sql-set-options.md)」では、ALTER DATABASE の SET オプションを使ってデータベースの属性を変更するための構文と関連情報について説明します。

## <a name="syntax"></a>構文

```console
ALTER DATABASE { database_name | CURRENT }
{
  MODIFY NAME = new_database_name
| MODIFY ( <edition_option> [, ... n] )
| SET <option_spec> [ ,...n ] [ WITH <termination> ]
}
[;]

<edition_option> ::=
      MAXSIZE = {
            250 | 500 | 750 | 1024 | 5120 | 10240 | 20480
          | 30720 | 40960 | 51200 | 61440 | 71680 | 81920
          | 92160 | 102400 | 153600 | 204800 | 245760
      } GB
      | SERVICE_OBJECTIVE = {
            'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500'
          | 'DW600' | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000'
          | 'DW3000' | 'DW6000' | 'DW500c' | 'DW1000c' | 'DW1500c'
          | 'DW2000c' | 'DW2500c' | 'DW3000c' | 'DW5000c' | 'DW6000c'
          | 'DW7500c' | 'DW10000c' | 'DW15000c' | 'DW30000c'
      }
```

## <a name="arguments"></a>引数

*database_name*: 変更するデータベースの名前を指定します。

MODIFY NAME = *new_database_name*: データベースの名前を、*new_database_name* で指定した名前に変更します。

MAXSIZE 既定値は 245,760 GB (240 TB) です。

**適用対象:** Gen1 コンピューティングに最適化

データベースの最大許容サイズ。 データベースは MAXSIZE を超えることはできません。

**適用対象:** Gen2 コンピューティングに最適化

データベースの行ストア データの最大許容サイズ。 行ストア テーブル、列ストア インデックスのデルタストア、またはクラスター化列ストア インデックスの非クラスター化インデックスに格納されているデータは MAXSIZE を超えることはできません。 列ストア形式に圧縮されたデータにはサイズ制限はなく、MAXSIZE に制約されません。

SERVICE_OBJECTIVE: パフォーマンス レベルを指定します。 SQL Data Warehouse のサービス目標の詳細については、「[Data Warehouse ユニット (DWU)](https://docs.microsoft.com/azure/sql-data-warehouse/what-is-a-data-warehouse-unit-dwu-cdwu)」を参照してください。

## <a name="permissions"></a>アクセス許可

以下のアクセス許可が必要です。

- サーバー レベル プリンシパル ログイン (プロビジョニング処理で作成されたもの) または
- `dbmanager` データベース ロールのメンバー。

所有者が `dbmanager` ロールのメンバーである場合を除き、データベースの所有者はデータベースを変更することはできません。

## <a name="general-remarks"></a>全般的な解説

現在のデータベースは、変更対象とは異なるデータベースである必要があります。したがって、**ALTER は master データベースに接続されている間に実行する必要があります**。

SQL Data Warehouse は COMPATIBILITY_LEVEL 130 に設定されており、変更することはできません。 詳細については、「[ALTER DATABASE (TRANSACT-SQL) の互換性レベル](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/)」を参照してください。

## <a name="limitations-and-restrictions"></a>制限事項と制約事項

`ALTER DATABASE` を実行するには、データベースをオンラインにする必要があり、一時停止状態にすることはできません。

`ALTER DATABASE` ステートメントは、既定のトランザクション管理モードである自動コミット モードで実行する必要があります。 これは、接続の設定で設定されます。

`ALTER DATABASE` ステートメントをユーザー定義のトランザクションに含めることはできません。

データベースの照合順序を変更することはできません。

## <a name="examples"></a>使用例

これらの例を実行する前に、変更対象のデータベースが現在のデータベースでないことを確認します。 現在のデータベースは、変更対象とは異なるデータベースである必要があります。したがって、**ALTER は master データベースに接続されている間に実行する必要があります**。

### <a name="a-change-the-name-of-the-database"></a>A. データベースの名前を変更します。

```sql
ALTER DATABASE AdventureWorks2012
MODIFY NAME = Northwind;
```

### <a name="b-change-max-size-for-the-database"></a>B. データベースの最大サイズを変更します。

```sql
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB );
```

### <a name="c-change-the-performance-level"></a>C. パフォーマンス レベルを変更します。

```sql
ALTER DATABASE dw1 MODIFY ( SERVICE_OBJECTIVE= 'DW1200' );
```

### <a name="d-change-the-max-size-and-the-performance-level"></a>D. 最大サイズとパフォーマンス レベルを変更します。

```sql
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB, SERVICE_OBJECTIVE= 'DW1200' );
```

## <a name="see-also"></a>参照

- [CREATE DATABASE (Azure SQL Data Warehouse)](../../t-sql/statements/create-database-transact-sql.md?view=aps-pdw-2016-au7)
- [参照記事の SQL Data Warehouse の一覧](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-overview-reference/)

::: moniker-end
::: moniker range=">=aps-pdw-2016||=sqlallproducts-allversions"

||||||
|---|---|---|---|---|
|[SQL Server](alter-database-transact-sql.md?view=sql-server-2017)|[SQL Database<br />単一データベース/エラスティック プール](alter-database-transact-sql.md?view=azuresqldb-current)|[SQL Database<br />マネージド インスタンス](alter-database-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](alter-database-transact-sql.md?view=azure-sqldw-latest)|**_\* Analytics<br />Platform System (PDW) \*_** &nbsp;|
||||||

&nbsp;

## <a name="overview-analytics-platform-system"></a>概要:分析プラットフォーム システム

PDW の複製テーブル、分散テーブル、およびトランザクション ログの最大データベース サイズ オプションを変更します。 このステートメントを使用すると、サイズの増加または減少に合わせてデータベースのディスク領域割り当てを管理できます。 また、この記事では PDW のデータベース オプションの設定に関連する構文についても説明します。

## <a name="syntax"></a>構文

```
-- Analytics Platform System
ALTER DATABASE database_name
    SET ( <set_database_options> | <db_encryption_option> )
[;]

<set_database_options> ::=
{
    AUTOGROW = { ON | OFF }
    | REPLICATED_SIZE = size [GB]
    | DISTRIBUTED_SIZE = size [GB]
    | LOG_SIZE = size [GB]
    | SET AUTO_CREATE_STATISTICS { ON | OFF }
    | SET AUTO_UPDATE_STATISTICS { ON | OFF }
    | SET AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }
}

<db_encryption_option> ::=
    ENCRYPTION { ON | OFF }
```

## <a name="arguments"></a>引数

*database_name*: 変更するデータベースの名前です。 アプライアンス上でデータベースの一覧を表示するには、[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) を使用します。

AUTOGROW = { ON | OFF }: AUTOGROW オプションを更新します。 AUTOGROW が ON のとき、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] は、複製テーブル、分散テーブル、トランザクション ログの割り当て領域を必要に応じて自動的に増やし、記憶域要件の増加に対応します。 AUTOGROW が OFF のとき、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] は、複製テーブル、分散テーブル、トランザクション ログが最大サイズ設定を超過したときにエラーを返します。

REPLICATED_SIZE = *size* [GB]: 変更されているデータベースのすべての複製テーブルを格納するための新しい最大 GB を計算ノードごとに指定します。 アプライアンスの記憶域を計画している場合、アプライアンスの計算ノード数に REPLICATED_SIZE を掛ける必要があります。

DISTRIBUTED_SIZE = *size* [GB]: 変更されているデータベースのすべての分散テーブルを格納するための新しい最大 GB をデータベースごとに指定します。 このサイズは、アプライアンスの計算ノード全体で分散されます。

LOG_SIZE = *size* [GB]: 変更されているデータベースのすべてのトランザクション ログを格納するための新しい最大 GB をデータベースごとに指定します。 このサイズは、アプライアンスの計算ノード全体で分散されます。

ENCRYPTION { ON | OFF }: データベースを暗号化する (ON) か、暗号化しない (OFF) かを設定します。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] の暗号化は、[sp_pdw_database_encryption](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md) が **1** に設定されているときにのみ構成できます。 Transparent Data Encryption を構成するには、先にデータベース暗号化キーを作成する必要があります。 データベース暗号化の詳細については、「[Transparent Data Encryption (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md)」を参照してください。

SET AUTO_CREATE_STATISTICS { ON | OFF } 統計の自動作成オプション AUTO_CREATE_STATISTICS がオンの場合、クエリ プランのカーディナリティの推定を向上させるために、クエリ オプティマイザーによってクエリ述語内の個々の列に関する統計が必要に応じて作成されます。 これらの 1 列ずつの統計は、既存の統計オブジェクトにまだヒストグラムがない列について作成されます。

AU7 へのアップグレード後に作成された新しいデータベースの場合、既定値は ON です。 アップグレードの前に作成されたデータベースの場合、既定値は OFF です。

統計の詳細については、「[統計](../../relational-databases/statistics/statistics.md)」を参照してください。

SET AUTO_UPDATE_STATISTICS { ON | OFF } 統計の自動更新オプション AUTO_UPDATE_STATISTICS がオンの場合、古くなっている可能性がある統計がクエリ オプティマイザーによって判断され、それらがクエリで使用されると更新されます。 挿入、更新、削除、またはマージの各操作によってテーブルまたはインデックス付きビューのデータの分布が変わると、統計は古くなったと判断されます。 クエリ オプティマイザーでは、統計が前回更新されてから発生したデータ変更の数をカウントし、その変更の数をしきい値と比較することで、統計が古くなっている可能性がないかを判断します。 このしきい値は、テーブルまたはインデックス付きビューの行数に基づいて決められます。

AU7 へのアップグレード後に作成された新しいデータベースの場合、既定値は ON です。 アップグレードの前に作成されたデータベースの場合、既定値は OFF です。

統計の詳細については、「[統計](../../relational-databases/statistics/statistics.md)」を参照してください。

SET AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF } 統計の非同期更新オプション AUTO_UPDATE_STATISTICS_ASYNC によって、クエリ オプティマイザーで統計の同期更新と非同期更新のどちらを使用するかが決まります。 AUTO_UPDATE_STATISTICS_ASYNC オプションは、インデックスに対して作成された統計オブジェクト、クエリ述語内の列に対して 1 列ずつ作成された統計オブジェクト、および CREATE STATISTICS ステートメントを使用して作成された統計に適用されます。

AU7 へのアップグレード後に作成された新しいデータベースの場合、既定値は ON です。 アップグレードの前に作成されたデータベースの場合、既定値は OFF です。

統計の詳細については、「[統計](/sql/relational-databases/statistics/statistics)」を参照してください。

## <a name="permissions"></a>アクセス許可

データベースに対する `ALTER` 権限が必要です。

## <a name="error-messages"></a>エラー メッセージ

自動統計が無効になっている場合に、統計の設定を変更しようとすると、`This option is not supported in PDW` というエラーが PDW から出力されます。 システム管理者は、機能スイッチ [AutoStatsEnabled](../../analytics-platform-system/appliance-feature-switch.md) を有効にすることにより、自動統計を有効にすることができます。

## <a name="general-remarks"></a>全般的な解説

`REPLICATED_SIZE`、`DISTRIBUTED_SIZE`、`LOG_SIZE` は、データベースの現在の値と同じ値か、それより大きい値か、それより小さい値に設定できます。

## <a name="limitations-and-restrictions"></a>制限事項と制約事項

増加と縮小はおおよそで行われます。 結果的に与えられる実際のサイズはサイズ パラメーターとは異なる場合があります。

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] は ALTER DATABASE ステートメントを不可分操作として実行しません。 実行中、ステートメントが中止された場合、既に発生している変更はそのまま残ります。

統計の設定は、管理者によって自動統計が有効にされた場合にのみ機能します。管理者である場合は、機能スイッチ [AutoStatsEnabled](../../analytics-platform-system/appliance-feature-switch.md) を使用して自動統計を有効または無効にします。

## <a name="locking-behavior"></a>ロック動作

DATABASE オブジェクトを共有ロックします。 別のユーザーが読み取りまたは書き込みをしているデータベースを変更することはできません。 データベースで [USE](../language-elements/use-transact-sql.md) ステートメントを発行しているセッションもこれに該当します。

## <a name="performance"></a>パフォーマンス

データベース内の実際のデータ サイズとディスクの断片化の量によっては、データベースの縮小に多大な時間とシステム リソースが必要となります。 たとえば、データベースの縮小に数時間かかることがあります。

## <a name="determining-encryption-progress"></a>暗号化の進捗状況を見る

次のクエリを使用すると、データベースの Transparent Data Encryption の進捗状況を割合で見ることができます。

```sql
WITH
database_dek AS (
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id,
        dek.encryption_state, dek.percent_complete,
        dek.key_algorithm, dek.key_length, dek.encryptor_thumbprint,
        type
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek
    INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map
        ON dek.database_id = node_db_map.database_id
        AND dek.pdw_node_id = node_db_map.pdw_node_id
    LEFT JOIN sys.pdw_database_mappings AS db_map
        ON node_db_map .physical_name = db_map.physical_name
    INNER JOIN sys.dm_pdw_nodes nodes
        ON nodes.pdw_node_id = dek.pdw_node_id
    WHERE dek.encryptor_thumbprint <> 0x
),
dek_percent_complete AS (
    SELECT database_dek.database_id, AVG(database_dek.percent_complete) AS percent_complete
    FROM database_dek
    WHERE type = 'COMPUTE'
    GROUP BY database_dek.database_id
)
SELECT DB_NAME( database_dek.database_id ) AS name,
    database_dek.database_id,
    ISNULL(
       (SELECT TOP 1 dek_encryption_state.encryption_state
        FROM database_dek AS dek_encryption_state
        WHERE dek_encryption_state.database_id = database_dek.database_id
        ORDER BY (CASE encryption_state
            WHEN 3 THEN -1
            ELSE encryption_state
            END) DESC), 0)
        AS encryption_state,
dek_percent_complete.percent_complete,
database_dek.key_algorithm, database_dek.key_length, database_dek.encryptor_thumbprint
FROM database_dek
INNER JOIN dek_percent_complete
    ON dek_percent_complete.database_id = database_dek.database_id
WHERE type = 'CONTROL';
```

TDE 実装の全手順を包括的な例で見るには、「[Transparent Data Encryption (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md)」を参照してください。

## <a name="examples-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

### <a name="a-altering-the-autogrow-setting"></a>A. AUTOGROW 設定を変更する

データベース `CustomerSales` の AUTOGROW を ON に設定します。

```sql
ALTER DATABASE CustomerSales
    SET ( AUTOGROW = ON );
```

### <a name="b-altering-the-maximum-storage-for-replicated-tables"></a>B. 複製テーブルの最大記憶域を変更する

次の例では、データベース `CustomerSales` の複製テーブルの記憶域上限を 1 GB に設定します。 これは計算ノードごとの記憶域上限になります。

```sql
ALTER DATABASE CustomerSales
    SET ( REPLICATED_SIZE = 1 GB );
```

### <a name="c-altering-the-maximum-storage-for-distributed-tables"></a>C. 分散テーブルの最大記憶域を変更する

 次の例では、データベース `CustomerSales` の分散テーブルの記憶域上限を 1000 GB (1 テラバイト) に設定します。 これは、計算ノードごとの記憶域上限ではなく、アプライアンス全体の全計算ノードの記憶域上限を 1 つにしたものになります。

```sql
ALTER DATABASE CustomerSales
    SET ( DISTRIBUTED_SIZE = 1000 GB );
```

### <a name="d-altering-the-maximum-storage-for-the-transaction-log"></a>D. トランザクション ログの最大記憶域を変更する

 次の例では、データベース `CustomerSales` を更新し、アプライアンスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] トランザクション ログの最大サイズを 10 GB にします。

```sql
ALTER DATABASE CustomerSales
    SET ( LOG_SIZE = 10 GB );
```

### <a name="e-check-for-current-statistics-values"></a>E. 現在の統計値を確認する

次のクエリを実行すると、すべてのデータベースについて現在の統計値が返されます。 値が 1 の場合は機能がオンであることを意味し、値が 0 の場合は機能がオフであることを意味します。

```sql
SELECT NAME,
    is_auto_create_stats_on,
    is_auto_update_stats_on,
    is_auto_update_stats_async_on
FROM sys.databases;
```

### <a name="f-enable-auto-create-and-auto-update-stats-for-a-database"></a>F. データベースに対して統計の自動作成および自動更新を有効にする

次のステートメントを使用して、データベース CustomerSales について自動的かつ非同期的に統計を作成および更新する機能を有効にします。 これにより、高品質のクエリ プランを作成するために必要に応じて統計が作成および更新されます。

```sql
ALTER DATABASE CustomerSales
    SET AUTO_CREATE_STATISTICS ON;
ALTER DATABASE CustomerSales
    SET AUTO_UPDATE_STATISTICS ON;
ALTER DATABASE
    SET AUTO_UPDATE_STATISTICS_ASYNC ON;
```

## <a name="see-also"></a>参照

- [CREATE DATABASE - Analytics Platform System](../../t-sql/statements/create-database-transact-sql.md?view=aps-pdw-2016-au7)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)

::: moniker-end
