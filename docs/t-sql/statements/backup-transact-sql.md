---
title: BACKUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/13/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BACKUP_TSQL
- BACKUP
- BACKUP_DATABASE_TSQL
- BACKUP_LOG_TSQL
- BACKUP LOG
- BACKUP DATABASE
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], BACKUP statement
- backing up filegroups [SQL Server]
- backup file formats [SQL Server]
- backups [SQL Server]
- database backups [SQL Server], BACKUP statement
- multifamily media sets [SQL Server]
- mirrored media sets [SQL Server]
- backing up files [SQL Server]
- backup sets [SQL Server], BACKUP statement
- backup compression [SQL Server], BACKUP statement
- BACKUP statement
- backups [SQL Server], BACKUP statement
- backup history tables [SQL Server]
- transaction log backups [SQL Server], BACKUP LOG statement
- READ_WRITE_FILEGROUPS option
- BACKUP DATABASE statement
- concurrency [SQL Server], backups
- backing up databases [SQL Server]
- passwords [SQL Server], backups
- security [SQL Server], backups
- media families [SQL Server]
- BACKUP LOG statement
- backing up transaction logs [SQL Server]
- stripe sets [SQL Server]
- cross-platform backups
ms.assetid: 89a4658a-62f1-4289-8982-f072229720a1
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||>=aps-pdw-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 1c6385fc578bfa1f9d688e9819690e72a3090ce4
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982848"
---
# <a name="backup-transact-sql"></a>BACKUP (Transact-SQL)

SQL Database をバックアップします。

お使いの特定バージョンの SQL の構文、引数、注釈、権限、例を表示するには、以下のいずれかのタブをクリックします。

構文表記規則の詳細については、「[Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)」を参照してください。

## <a name="click-a-product"></a>製品をクリックしてください

次の行から興味がある製品名をクリックしてみてください。 クリックした製品に合わせて、異なるコンテンツが表示されます。

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

||||
|---|---|---|
|**\* _SQL Server \*_** &nbsp;|[SQL Database<br />マネージド インスタンス](backup-transact-sql.md?view=azuresqldb-mi-current)|[Analytics Platform<br />System (PDW)](backup-transact-sql.md?view=aps-pdw-2016)|
||||

&nbsp;

## <a name="sql-server"></a>SQL Server

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース全体をバックアップしてデータベース バックアップを作成するか、データベースの 1 つ以上のファイルまたはファイル グループをバックアップしてファイル バックアップを作成します (BACKUP DATABASE)。 完全復旧モデルまたは一括ログ復旧モデルの場合には、データベースのトランザクション ログをバックアップして、ログ バックアップを作成します (BACKUP LOG)。

## <a name="syntax"></a>構文

```sql
--Backing Up a Whole Database
BACKUP DATABASE { database_name | @database_name_var }
  TO <backup_device> [ ,...n ]
  [ <MIRROR TO clause> ] [ next-mirror-to ]
  [ WITH { DIFFERENTIAL
           | <general_WITH_options> [ ,...n ] } ]
[;]

--Backing Up Specific Files or Filegroups
BACKUP DATABASE { database_name | @database_name_var }
 <file_or_filegroup> [ ,...n ]
  TO <backup_device> [ ,...n ]
  [ <MIRROR TO clause> ] [ next-mirror-to ]
  [ WITH { DIFFERENTIAL | <general_WITH_options> [ ,...n ] } ]
[;]

--Creating a Partial Backup
BACKUP DATABASE { database_name | @database_name_var }
 READ_WRITE_FILEGROUPS [ , <read_only_filegroup> [ ,...n ] ]
  TO <backup_device> [ ,...n ]
  [ <MIRROR TO clause> ] [ next-mirror-to ]
  [ WITH { DIFFERENTIAL | <general_WITH_options> [ ,...n ] } ]
[;]

--Backing Up the Transaction Log (full and bulk-logged recovery models)
BACKUP LOG
  { database_name | @database_name_var }
  TO <backup_device> [ ,...n ]
  [ <MIRROR TO clause> ] [ next-mirror-to ]
  [ WITH { <general_WITH_options> | \<log-specific_optionspec> } [ ,...n ] ]
[;]
  
<backup_device>::=
 {
  { logical_device_name | @logical_device_name_var }
 | {   DISK
     | TAPE
     | URL } =
     { 'physical_device_name' | @physical_device_name_var | 'NUL' }
 }

<MIRROR TO clause>::=
 MIRROR TO <backup_device> [ ,...n ]

<file_or_filegroup>::=
 {
   FILE = { logical_file_name | @logical_file_name_var }
 | FILEGROUP = { logical_filegroup_name | @logical_filegroup_name_var }
 }

<read_only_filegroup>::=
FILEGROUP = { logical_filegroup_name | @logical_filegroup_name_var }

<general_WITH_options> [ ,...n ]::=
--Backup Set Options
   COPY_ONLY
 | { COMPRESSION | NO_COMPRESSION }
 | DESCRIPTION = { 'text' | @text_variable }
 | NAME = { backup_set_name | @backup_set_name_var }
 | CREDENTIAL
 | ENCRYPTION
 | FILE_SNAPSHOT
 | { EXPIREDATE = { 'date' | @date_var }
        | RETAINDAYS = { days | @days_var } }

--Media Set Options
   { NOINIT | INIT }
 | { NOSKIP | SKIP }
 | { NOFORMAT | FORMAT }
 | MEDIADESCRIPTION = { 'text' | @text_variable }
 | MEDIANAME = { media_name | @media_name_variable }
 | BLOCKSIZE = { blocksize | @blocksize_variable }

--Data Transfer Options
   BUFFERCOUNT = { buffercount | @buffercount_variable }
 | MAXTRANSFERSIZE = { maxtransfersize | @maxtransfersize_variable }

--Error Management Options
   { NO_CHECKSUM | CHECKSUM }
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }

--Compatibility Options
   RESTART

--Monitoring Options
   STATS [ = percentage ]

--Tape Options
   { REWIND | NOREWIND }
 | { UNLOAD | NOUNLOAD }

--Log-specific Options
   { NORECOVERY | STANDBY = undo_file_name }
 | NO_TRUNCATE

--Encryption Options
 ENCRYPTION (ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY } , encryptor_options ) <encryptor_options> ::=
   `SERVER CERTIFICATE` = Encryptor_Name | SERVER ASYMMETRIC KEY = Encryptor_Name
```

## <a name="arguments"></a>引数

DATABASE: データベース全体のバックアップを指定します。 ファイルとファイル グループのリストを指定した場合、指定したファイルとファイル グループだけがバックアップされます。 データベース全体のバックアップまたは差分バックアップ中、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、バックアップが復元された場合に一貫性のあるデータベースを生成するのに十分なトランザクション ログをバックアップします。

BACKUP DATABASE (*データ バックアップ*) で作成されたバックアップを復元すると、バックアップ全体が復元されます。 バックアップ内の特定の時点またはトランザクションに復元できるのは、ログ バックアップだけです。

> [!NOTE]
> **master** データベース上では、データベース全体のバックアップのみが可能です。

LOG

トランザクション ログのみのバックアップを指定します。 前回正しく実行されたログ バックアップの位置から、ログの現在の末尾まで、ログのバックアップが行われます。 最初のログ バックアップを作成するには、その前に完全バックアップを作成する必要があります。

[RESTORE LOG](../../t-sql/statements/restore-statements-transact-sql.md) ステートメントで `WITH STOPAT`、`STOPATMARK`、または `STOPBEFOREMARK` を指定して、バックアップ内の特定の時間またはトランザクションにログ バックアップを復元できます。

> [!NOTE]
> `WITH NO_TRUNCATE` または `COPY_ONLY` を指定した場合を除き、一般的なログ バックアップの後、一部のトランザクション ログ レコードが非アクティブになります。 1 つ以上の仮想ログ ファイル内ですべてのレコードがアクティブでなくなった場合、ログは切り捨てられます。 定期的なログ バックアップの後にログが切り捨てられていない場合は、何らかの原因によりログの切り捨てが遅れている可能性があります。 詳細については、「[ログの切り捨てが遅れる原因となる要因](../../relational-databases/logs/the-transaction-log-sql-server.md#FactorsThatDelayTruncation)」を参照してください。

{ _database\_name_ |  **@** _database\_name\_var_ }: トランザクション ログ、データベースの一部、またはデータベース全体のバックアップ元となるデータベースです。 変数 ( **@** _database\_name\_var_) として指定する場合、この名前は、文字列定数 ( **@** _database\_name\_var_ **=** _database name_) として指定するか、**ntext** または**text** データ型以外の文字列データ型の変数として指定します。

> [!NOTE]
> データベース ミラーリング パートナーシップ内のミラー データベースは、バックアップできません。

\<file_or_filegroup> [ **,** ...*n* ]: BACKUP DATABASE のみで使用できます。ファイル バックアップに含めるデータベース ファイルまたはファイル グループを指定するか、部分バックアップに含める読み取り専用ファイルまたはファイル グループを指定します。

FILE **=** { *logical_file_name* | **@** _logical\_file\_name\_var_ }: バックアップに含めるファイルの論理名、またはその論理名と同じ値を保持する変数です。

FILEGROUP **=** { _logical\_filegroup\_name_ |  **@** _logical\_filegroup\_name\_var_ }: バックアップに含めるファイル グループの論理名、またはその論理名と同じ値を保持する変数です。 単純復旧モデルでは、ファイル グループのバックアップは、読み取り専用のファイル グループに対してのみ使用できます。

> [!NOTE]
> データベースのサイズおよびパフォーマンス要件によりデータベース バックアップの実行が難しい場合は、ファイル バックアップの利用を検討してください。 NUL デバイスはバックアップのパフォーマンスをテストするために使用できますが、運用環境では使用できません。

*n*: 複数のファイルおよびファイル グループを、コンマ区切りのリストで指定できることを示すプレースホルダーです。 数の制限はありません。

詳しくは、「[ファイルの完全バックアップ](../../relational-databases/backup-restore/full-file-backups-sql-server.md)」および「[ファイルおよびファイル グループのバックアップ](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)」をご覧ください。

READ_WRITE_FILEGROUPS [ **,** FILEGROUP = { _logical\_filegroup\_name_ |  **@** _logical\_filegroup\_name\_var_ } [ **,** ..._n_ ] ]: 部分バックアップを指定します。 部分バックアップには、データベース内のすべての読み取り/書き込みファイル (プライマリ ファイル グループ、存在する場合は読み取り/書き込みセカンダリ ファイル グループ、および指定の読み取り専用ファイルまたはファイル グループ) が含まれます。

READ_WRITE_FILEGROUPS: 部分バックアップにおいて、すべての読み取り/書き込みファイル グループをバックアップするように指定します。 データベースが読み取り専用の場合、READ_WRITE_FILEGROUPS にはプライマリ ファイル グループのみが含まれます。

> [!IMPORTANT]
> READ_WRITE_FILEGROUPS の代わりに FILEGROUP を使用して、読み取り/書き込みファイル グループのリストを明示的に指定すると、ファイル バックアップが作成されます。

FILEGROUP = { *logical_filegroup_name* |  **@** _logical\_filegroup\_name\_var_ }: 部分バックアップに含める読み取り専用ファイル グループの論理名、またはその論理名と同じ値を保持する変数です。 詳細については、このトピックの前述の "\<file_or_filegroup>" を参照してください。

*n*: 複数の読み取り専用ファイル グループを、コンマ区切りのリストで指定できることを示すプレースホルダーです。

部分バックアップについて詳しくは、「[部分バックアップ](../../relational-databases/backup-restore/partial-backups-sql-server.md)」をご覧ください。

TO \<backup_device> [ **,** ...*n* ] 関連する[バックアップ デバイス](../../relational-databases/backup-restore/backup-devices-sql-server.md)のセットが、ミラー化されていないメディア セット、またはミラー化されたメディア セット内にあるミラーの 1 つ目 (1 つ以上の MIRROR TO 句が宣言されている場合) であることを示します。

\<backup_device>

バックアップ操作に使用する論理または物理バックアップ デバイスを指定します。

{ *logical_device_name* |  **@** _logical\_device\_name\_var_ } **適用対象:** SQL Server: データベースのバックアップが作成されるバックアップ デバイスの論理名です。 論理名は、識別子のルールに従う必要があります。 変数 (@*logical_device_name_var*) として指定する場合、バックアップ デバイス名を文字列定数 (@_logical\_device\_name\_var_ **=** logical backup device name) として指定するか、**ntext** または **text** データ型以外の文字列データ型の変数として指定できます。

{ DISK | TAPE | URL} **=** { **'** _physical\_device\_name_ **'**  |  **@** _physical\_device\_name\_var_ | 'NUL' } **適用対象:** SQL Server に適用する DISK、TAPE、URL。
ディスク ファイルまたはテープ デバイス、あるいは Microsoft Azure BLOB ストレージ サービスを指定します。 URL の形式は、Microsoft Azure ストレージ サービスへのバックアップを作成するために使用されます。 詳細と例については、「[Microsoft Azure BLOB ストレージ サービスを使用した SQL Server のバックアップと復元](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)」を参照してください。 チュートリアルについては、「[チュートリアル: Microsoft Azure BLOB ストレージ サービスへの SQL Server のバックアップと復元](~/relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)」を参照してください。

> [!NOTE]
> NUL ディスク デバイスは送信される情報をすべて破棄し、テストでのみ使用する必要があります。 これは運用環境向けではありません。
> [!IMPORTANT]
> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 から [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] では、URL にバックアップする場合、単一デバイスにのみバックアップできます。 URL へのバックアップ時に複数のデバイスにバックアップするには、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降を使用する必要があります。また、Shared Access Signature (SAS) トークンを使用する必要があります。 Shared Access Signature の作成例については、「[SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)」と「[Simplifying creation of SQL Credentials with Shared Access Signature ( SAS ) tokens on Azure Storage with Powershell](https://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx)」 (Powershell を使用する Azure ストレージにおける Shared Access Signature (SAS) トークンでの SQL 資格情報の作成の簡素化) を参照してください。

**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 以降)。

ディスク デバイスは、BACKUP ステートメント内で指定するときに、まだ存在していなくてもかまいません。 物理デバイスが既に存在し、BACKUP ステートメントに INIT オプションが指定されていない場合、バックアップはデバイスに追加されます。

> [!NOTE]
> NUL デバイスはこのファイルに送信されるすべての入力を破棄しますが、バックアップでは引き続きすべてのページがバックアップ済みとしてマークされます。

詳しくは、「[バックアップ デバイス](../../relational-databases/backup-restore/backup-devices-sql-server.md)」をご覧ください。

> [!NOTE]
> TAPE オプションは将来のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。

*n*: 最大 64 個のバックアップ デバイスを、コンマ区切りのリストで指定できることを示すプレースホルダーです。

MIRROR TO \<backup_device> [ **,** ...*n* ] TO 句で指定したバックアップ デバイスをミラー化する、最大 3 つまでのセカンダリ バックアップ デバイスのセットを指定します。 MIRROR TO 句には、TO 句で指定した同じ種類と数のバックアップ デバイスを指定する必要があります。 MIRROR TO 句の最大数は 3 です。

このオプションは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の Enterprise Edition でのみ使用できます。

> [!NOTE]
> MIRROR TO = DISK の場合、BACKUP では、ディスクのセクター サイズに基づいてデバイス デバイスの適切なブロック サイズが自動的に決まります。 プライマリ バックアップ デバイスとして指定されたディスクとは異なるセクター サイズを使用して MIRROR TO ディスクがフォーマットされた場合、Backup コマンドは失敗します。 セクター サイズが異なるデバイスに対してバックアップをミラー化するには、BLOCKSIZE パラメーターを指定する必要があります。このパラメーターをすべてのターゲット デバイスの中で最も大きなセクター サイズに設定する必要があります。 ブロック サイズの詳細については、このトピックで後述する "BLOCKSIZE" の説明を参照してください。

\<backup_device> このセクションの前述の "\<backup_device>" を参照してください。

*n*: 最大 64 個のバックアップ デバイスを、コンマ区切りのリストで指定できることを示すプレースホルダーです。 MIRROR TO 句内のデバイス数は、TO 句内のデバイス数と同じにする必要があります。

詳細については、このトピックの後述の「[解説](#general-remarks)」の「ミラー化されたメディア セットのメディア ファミリ」を参照してください。

[ *next-mirror-to* ]: 単一の BACKUP ステートメントに、1 つの TO 句と 3 つまでの MIRROR TO 句を含めることができることを示すプレースホルダーです。

### <a name="with-options"></a>WITH オプション

バックアップ操作で使用するオプションを指定します。

CREDENTIAL **適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 以降)。
Microsoft Azure BLOB ストレージ サービスにバックアップを作成する場合にのみ使用します。

FILE_SNAPSHOT **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降)。

すべての SQL Server データベース ファイルが Azure Blob ストレージ サービスを使用して格納される場合は、データベース ファイルの Azure のスナップショットを作成するために使用されます。 詳細については、「[Microsoft Azure 内の SQL Server データ ファイル](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)」を参照してください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スナップショット バックアップでは、データベース ファイル (データとログ ファイル) の Azure スナップショットを一貫性のある状態で取得します。 一貫した Azure のスナップショットのセットは、バックアップを構成し、バックアップ ファイルに記録されます。 `BACKUP DATABASE TO URL WITH FILE_SNAPSHOT` と `BACKUP LOG TO URL WITH FILE_SNAPSHOT` の唯一の違いは、後者ではトランザクション ログの切り捨ても行うのに対して、前者では行わないことです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のスナップショット バックアップでは、バックアップ チェーンを確立するために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で必要な最初の完全バックアップの後、トランザクション ログ バックアップの時点にデータベースを復元する場合、単一のトランザクション ログ バックアップのみが必要になります。 さらに、次の 2 つのトランザクション ログ バックアップ期間の間の特定の時点にデータベースを復元するためには、2 つのトランザクション ログ バックアップのみが必要になります。

DIFFERENTIAL

BACKUP DATABASE のみで使用され、データベースまたはファイルのバックアップが、前回の完全バックアップ以降に変更されたデータベースまたはファイルの部分のみで構成されるように指定します。 通常、差分バックアップは、完全バックアップよりも使用領域が少なくてすみます。 前回の完全バックアップ以降に実行された各ログ バックアップをすべて適用する必要がない場合に、このオプションを使用します。

> [!NOTE]
> 既定では、`BACKUP DATABASE` は完全バックアップを作成します。

詳しくは、「[差分バックアップ](../../relational-databases/backup-restore/differential-backups-sql-server.md)」をご覧ください。

ENCRYPTION: バックアップの暗号化を指定するために使用されます。 バックアップを暗号化するための暗号化アルゴリズムを指定するか、バックアップを暗号化しない場合は `NO_ENCRYPTION` を指定できます。 暗号化は、バックアップ ファイルをセキュリティで保護するために推奨される方法です。 指定できるアルゴリズムの一覧を次に示します。

- `AES_128`
- `AES_192`
- `AES_256`
- `TRIPLE_DES_3KEY`
- `NO_ENCRYPTION`

暗号化することを選択した場合、次の暗号化機能のオプションを使用して、暗号化機能も指定する必要があります。

- `SERVER CERTIFICATE` = Encryptor_Name
- `SERVER ASYMMETRIC KEY` = Encryptor_Name

`SERVER CERTIFICATE` と `SERVER ASYMMETRIC KEY` は、`master` データベースで作成された証明書と非対称キーです。 詳細については、それぞれ [`CREATE CERTIFICATE`](../../t-sql/statements/create-certificate-transact-sql.md) と [`CREATE ASYMMETRIC KEY`](../../t-sql/statements/create-asymmetric-key-transact-sql.md) を参照してください。

> [!WARNING]
> 暗号化が `FILE_SNAPSHOT` 引数と組み合わせて使用されている場合、指定した暗号化アルゴリズムを使用して、メタデータ ファイル自体が暗号化され、システムはデータベースの [Transparent Data Encryption (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) が完了したことを確認します。 データ自体に対しては、追加の暗号化は行われません。 データベースが暗号化されなかったか、バックアップ ステートメントが発行される前に暗号化が完了しなかった場合、バックアップは失敗します。

**バックアップ セット オプション**

以下のオプションは、このバックアップ操作で作成されるバックアップ セットに対して有効なオプションです。

> [!NOTE]
> 復元操作用のバックアップ セットを指定するには、`FILE = <backup_set_file_number>` オプションを使用します。 バックアップ セットを指定する方法について詳しくは、「[RESTORE の引数](../../t-sql/statements/restore-statements-arguments-transact-sql.md)」の「バックアップ セットの指定」をご覧ください。

COPY_ONLY: バックアップが、通常のバックアップの順序には影響しない、*コピーのみのバックアップ*であることを指定します。 コピーのみのバックアップは、定期的に行われる従来のバックアップとは別に作成されます。 コピーのみのバックアップは、データベースの全体的なバックアップと復元の手順に影響しません。

コピーのみのバックアップは、オンラインでファイルを復元する前にログをバックアップするなど、特殊な目的でバックアップを作成する場合にのみ使用してください。 通常、コピーのみのログ バックアップは 1 回だけ使用され、その後は削除されます。

- `BACKUP DATABASE` で使用した場合、`COPY_ONLY` オプションでは、差分ベースとして使用できない完全バックアップが作成されます。 差分ビットマップは更新されず、後に実行する差分バックアップではコピーのみのバックアップは無視され、 従来のバックアップで作成された最新の完全バックアップがベースとして使用されます。

    > [!IMPORTANT]
    > `DIFFERENTIAL` と `COPY_ONLY` が一緒に使用されている場合、`COPY_ONLY` は無視され、差分バックアップが作成されます。

- `BACKUP LOG` で使用した場合、`COPY_ONLY` オプションでは*コピーのみのログ バックアップ*が作成され、トランザクション ログは切り捨てられません。 コピーのみのログ バックアップは、ログ チェーンに影響を及ぼさず、他のログ バックアップはコピーのみのバックアップが存在しない場合と同様に動作します。

詳しくは、「[コピーのみのバックアップ](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)」をご覧ください。

{ COMPRESSION | NO_COMPRESSION }: [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 以降のバージョンのみで、このバックアップに対して[バックアップの圧縮](../../relational-databases/backup-restore/backup-compression-sql-server.md)を実行するかどうかを指定し、サーバー レベルの既定値をオーバーライドします。

インストール時の既定の動作では、バックアップの圧縮は行われません。 ただし、この既定の動作は、[backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) サーバー構成オプションを設定することで変更できます。 このオプションの現在の値の表示については、「[サーバー プロパティの表示または変更](../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md)」をご覧ください。

[透過的なデータ暗号化 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) が有効になっているデータベースでのバックアップの圧縮の使用については、「[解説](#general-remarks)」セクションを参照してください。

COMPRESSION: バックアップの圧縮を明示的に有効にします。

NO_COMPRESSION: バックアップの圧縮を明示的に無効にします。

DESCRIPTION **=** { **'** _text_ **'**  |  **@** _text\_variable_ }: バックアップ セットを記述したテキストを自由な形式で指定します。 文字列の長さは最大 255 文字です。

NAME **=** { *backup_set_name* |  **@** _backup\_set\_var_ }: バックアップ セットの名前を指定します。 名前の長さは最大 128 文字です。 NAME を指定しないと、名前は空白になります。

{ EXPIREDATE **='** _date_ **'** | RETAINDAYS **=** _days_ }: このバックアップのバックアップ セットがいつ上書きできるかを指定します。 これらのオプションを両方とも使用した場合は、RETAINDAYS が EXPIREDATE よりも優先されます。

どちらのオプションも指定されていない場合、失効日は **mediaretention** 構成設定によって決まります。 詳しくは、「[サーバー構成オプション](../../database-engine/configure-windows/server-configuration-options-sql-server.md)」をご覧ください。

> [!IMPORTANT]
> これらのオプションは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でのファイルの上書きを防ぐことのみを目的としています。 テープは、ほかの方法を使用して消去でき、ディスク ファイルはオペレーティング システムから削除できます。 有効期限の確認について詳しくは、このトピックの「SKIP」および「FORMAT」をご覧ください。

EXPIREDATE **=** { **'** _date_ **'**  |  **@** _date\_var_ }: バックアップ セットがいつ期限切れとなり、上書き可能になるかを指定します。 変数 (@_date\_var_) として指定する場合、この日付は構成されたシステムの **datetime** 形式に従い、次のいずれかとして指定する必要があります。

- A string constant (@_date\_var_ **=** date)
- 文字列データ型 (**ntext** または **text** データ型を除く) の変数
- **smalldatetime**
- **datetime** 変数

例:

- `'Dec 31, 2020 11:59 PM'`
- `'1/1/2021'`

**datetime** 値の指定方法については、「[日付と時刻型](../../t-sql/data-types/date-and-time-types.md)」を参照してください。

> [!NOTE]
> 失効日を無視するには、`SKIP` オプションを使用します。

RETAINDAYS **=** { *days* |  **@** _days\_var_ }: このバックアップ メディア セットを上書きできるようになるまでに必要な経過日数を指定します。 変数 ( **@** _days\_var_) として指定する場合は、整数で指定する必要があります。

**メディア セットのオプション**

以下のオプションは、メディア セット全般に適用されます。

{ **NOINIT** | INIT }: バックアップ操作において、バックアップ メディア上の既存のバックアップ セットに追加するか、上書きするかを制御します。 既定では、メディア上の最新のバックアップ セットに追加します (NOINIT)。

> [!NOTE]
> { **NOINIT** | INIT } と { **NOSKIP** | SKIP } の相関関係については、このトピックの後述の「[解説](#general-remarks)」を参照してください。

NOINIT: 既存のバックアップ セットを維持したまま、バックアップ セットが指定のメディア セットに追加されることを示します。 メディア セットのメディア パスワードが定義されている場合は、パスワードを指定する必要があります。 NOINIT が既定値です。

詳しくは、「[メディア セット、メディア ファミリ、およびバックアップ セット](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)」をご覧ください。

INIT: すべてのバックアップ セットが上書きされるように指定します。ただし、メディア ヘッダーは維持されます。 INIT が指定された場合、条件が満たされていれば、そのデバイス上にある既存のすべてのバックアップ セットが上書きされます。 既定では、BACKUP によって次の状況が確認され、いずれかの状況に該当する場合はバックアップ メディアは上書きされません。

- バックアップ セットがまだ期限切れではない。 詳細については、`EXPIREDATE` と `RETAINDAYS` のオプションを参照してください。
- BACKUP ステートメント内に示されたバックアップ セット名 (指定された場合) が、バックアップ メディア上の名前と一致していない。 詳細については、前の NAME オプションを参照してください。

これらのチェックをオーバーライドするには、`SKIP` オプションを使用します。

詳しくは、「[メディア セット、メディア ファミリ、およびバックアップ セット](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)」をご覧ください。

{ **NOSKIP** | SKIP }: バックアップ操作において、上書き前にメディア上のバックアップ セットの失効日時を確認するかどうかを制御します。

> [!NOTE]
> { **NOINIT** | INIT } と { **NOSKIP** | SKIP } の相関関係については、このトピックの後述の「解説」を参照してください。

NOSKIP 上書きを許可する前に、メディア上のすべてのバックアップ セットの有効期限を確認することを BACKUP ステートメントに指示します。 これは既定の動作です。

SKIP: バックアップ セットの有効期限と名前の確認を無効にします。通常は、バックアップ セットの上書きを防止するために BACKUP ステートメントによって行われます。 { INIT | NOINIT } と { NOSKIP | SKIP } の相関関係については、このトピックで後述する「解説」を参照してください。
バックアップ セットの失効日を表示するには、[backupset](../../relational-databases/system-tables/backupset-transact-sql.md) 履歴テーブルの **expiration_date** 列をクエリします。

{ **NOFORMAT** | FORMAT }: このバックアップ操作に使用するボリューム上にメディア ヘッダーを書き込み、既存のメディア ヘッダーとバックアップ セットを上書きするかどうかを指定します。

NOFORMAT: バックアップ操作において、このバックアップ操作に使用するメディア ボリューム上の既存のメディア ヘッダーとバックアップ セットを保持するように指定します。 これは既定の動作です。

FORMAT: 新しいメディア セットを作成するように指定します。 FORMAT が指定されると、バックアップ操作において、バックアップ操作に使用されるすべてのメディア ボリューム上に、新しいメディア ヘッダーを書き込みます。 既存のメディア ヘッダーとバックアップ セットが上書きされるので、そのボリュームの既存のコンテンツは無効になります。

> [!IMPORTANT]
> `FORMAT` は注意して使用してください。 メディア セットに属するボリュームを 1 つでも初期化すると、メディア セット全体が使用できなくなります。 たとえば、既存のストライプ メディア セットに属するテープを 1 つ初期化すると、メディア セット全体が使用できなくなります。

FORMAT を指定することは `SKIP` を実行することを意味します。`SKIP` を明示的に指定する必要はありません。

MEDIADESCRIPTION **=** { *text* | **@** _text\_variable_ }: メディア セットを説明した自由形式のテキストを最大 255 文字で指定します。

MEDIANAME **=** { *media_name* |  **@** _media\_name\_variable_ }: バックアップ メディア セット全体のメディア名を指定します。 メディア名は最長 128 文字まで入力できます。`MEDIANAME` を指定する場合、バックアップ ボリュームに既に存在する、前回指定したメディア名と一致する必要があります。 指定しなかった場合場合、または SKIP オプションを指定した場合、メディア名の照合チェックは行われません。

BLOCKSIZE **=** { *blocksize* |  **@** _blocksize\_variable_ }: 物理的なブロック サイズをバイト単位で指定します。 サポートされるサイズは、512、1024、2048、4096、8192、16384、32768、および 65536 (64 KB) バイトです。 テープ デバイスの場合の既定値は 65536 バイトで、他のデバイスの場合の既定値は 512 バイトです。 通常は、BACKUP によってデバイスに適したブロック サイズが自動的に選択されるので、このオプションは必要ありません。 ブロック サイズを明示的に指定すると、自動選択されたブロック サイズがオーバーライドされます。

バックアップを作成して CD-ROM に格納したり、CD-ROM からバックアップを復元する場合は、BLOCKSIZE=2048 と指定します。

> [!NOTE]
> このオプションがパフォーマンスに影響するのは、通常、テープ デバイスに書き込むときだけです。

**データ転送オプション**

BUFFERCOUNT **=** { *buffercount* |  **@** _buffercount\_variable_ }: バックアップ操作に使用される I/O バッファーの総数を指定します。 任意の正の整数を指定できますが、バッファー数が多いと Sqlservr.exe プロセス内で仮想アドレス空間が不足し、"メモリ不足" エラーが発生する場合があります。

バッファーで使用される領域の合計は、`BUFFERCOUNT * MAXTRANSFERSIZE` で決定されます。

> [!NOTE]
> `BUFFERCOUNT` オプションの使用に関する重要な情報については、ブログ「[Incorrect BufferCount data transfer option can lead to OOM condition](https://blogs.msdn.com/b/sqlserverfaq/archive/2010/05/06/incorrect-buffercount-data-transfer-option-can-lead-to-oom-condition.aspx)」 (不適切な BufferCount データ転送オプションによって OOM の状態になる可能性がある) を参照してください。

MAXTRANSFERSIZE **=** { *maxtransfersize* |  _**@** maxtransfersize\_variable_ } Specifies the largest unit of transfer in bytes to be used between [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] and the backup media. 有効値は 65536 バイト (64 KB) の倍数で、最大有効値は 4194304 バイト (4 MB) です。

> [!NOTE]
> SQL ライター サービスを使用してバックアップを作成する際に、データベースに [FILESTREAM](../../relational-databases/blob/filestream-sql-server.md) が構成されているか、[メモリ最適化ファイル グループ](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)が含まれている場合、復元時の `MAXTRANSFERSIZE` はバックアップの作成時に使用された `MAXTRANSFERSIZE` 以上である必要があります。

> [!NOTE]
> 単一のデータ ファイルを含む、[透過的なデータ暗号化 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) が有効になっているデータベースの場合、既定の `MAXTRANSFERSIZE` は 65536 (64 KB) です。 TDE で暗号化されていないデータベースでは、ディスクへのバックアップを使用する場合は既定の `MAXTRANSFERSIZE` が 1048576 (1 MB) となり、VDI または TAPE を使用する場合は 65536 (64 KB) となります。
> TDE で暗号化されたデータベースでのバックアップの圧縮の使用の詳細については、「[解説](#general-remarks)」セクションを参照してください。

**エラー管理オプション**

以下のオプションでは、バックアップ操作に対してバックアップのチェックサムを有効にするかどうかと、エラー発生時に操作を停止するかどうかを判別できます。

{ **NO_CHECKSUM** | CHECKSUM }: バックアップのチェックサムを有効にするかどうかを制御します。

NO_CHECKSUM: バックアップ チェックサムの生成 (およびページ チェックサムの検証) を明示的に無効にします。 これは既定の動作です。

CHECKSUM: 有効かつ使用可能であれば、バックアップ操作において各ページのチェックサムおよび破損ページを検証し、バックアップ全体のチェックサムを生成するように指定します。

バックアップ チェックサムを使用すると、ワークロードとバックアップのスループットに影響する場合があります。

詳しくは、「[バックアップ中および復元中に発生する可能性があるメディア エラー](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)」をご覧ください。

{ **STOP_ON_ERROR** | CONTINUE_AFTER_ERROR }: ページ チェックサム エラーの発生後に、バックアップ操作を停止するか続行するかを制御します。

STOP_ON_ERROR: ページ チェックサムが正しくない場合、BACKUP が失敗になるように指示します。 これは既定の動作です。

CONTINUE_AFTER_ERROR: 無効なチェックサムやページの破損などのエラーが発生しても、BACKUP を続行するように指示します。

データベースが破損したときに、NO_TRUNCATE オプションを使用してもログの末尾をバックアップできない場合は、NO_TRUNCATE の代わりに CONTINUE_AFTER_ERROR を指定して[ログ末尾のバックアップ](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)を試すことができます。

詳しくは、「[バックアップ中および復元中に発生する可能性があるメディア エラー](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)」をご覧ください。

**互換性オプション**

RESTART [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降では無効です。 このオプションは、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] との互換性を維持するために使用できます。

**監視オプション**

STATS [ **=** _percentage_ ]: 各 *percentage* の完了ごとにメッセージを表示します。進行状況を判断するために使用されます。 *percentage* を省略した場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では 10% 完了するごとにメッセージが表示されます。

STATS オプションでは、次のパーセンテージ間隔を報告するしきい値に達した時点までに、完了したパーセンテージを報告します。 これは、ほぼ指定したパーセンテージになります。たとえば、STATS=10 とすると、40% が完了した場合に、オプションでは 43% と表示されることがあります。 大規模なバックアップ セットの場合は、完了した I/O 呼び出し間での完了パーセンテージの変化が非常に遅くなるため、これは重要な問題にはなりません。

**テープ オプション**

このオプションはテープ デバイスにのみ適用されます。 テープ以外のデバイスが使用される場合、このオプションは無視されます。

{ **REWIND** | NOREWIND } REWIND

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でテープを解放して巻き戻すように指定します。 既定値は REWIND です。

NOREWIND

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でバックアップ操作後にテープを開いたままにしておくことを指定します。 このオプションを使用すると、1 つのテープに対して複数のバックアップ操作を実行する場合のパフォーマンスを向上させることが可能です。

NOREWIND は暗黙的に NOUNLOAD も意味しており、これらのオプションを 1 つの BACKUP ステートメント内で同時に使用することはできません。

> [!NOTE]
> `NOREWIND` を使用する場合、テープ ドライブの所有権は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスによって保持されます。同じプロセス内で実行される BACKUP または RESTORE ステートメントで `REWIND` または `UNLOAD` オプションが使用されるか、サーバー インスタンスがシャットダウンすると、所有権は解放されます。 テープを開いたままにすると、他のプロセスではそのテープにアクセスできません。 開いているテープの一覧を表示する方法、および開いているテープを閉じる方法については、「[バックアップ デバイス](../../relational-databases/backup-restore/backup-devices-sql-server.md)」をご覧ください。

{ **UNLOAD** | NOUNLOAD }

> [!NOTE]
> `UNLOAD` および `NOUNLOAD` はセッションの設定であり、セッションが終了するまで、または代わりとなるオプションの指定によりリセットされるまで有効です。

UNLOAD

バックアップ完了後、テープの巻き戻しおよびアンロードを自動的に行います。 UNLOAD は、セッション開始時の既定値です。

NOUNLOAD

BACKUP 操作の後、テープ ドライブにテープを読み込んだままにすることを指定します。

> [!NOTE]
> テープ バックアップ デバイスへのバックアップの場合、`BLOCKSIZE` オプションはバックアップ操作のパフォーマンスに影響します。 このオプションがパフォーマンスに影響するのは、通常、テープ デバイスに書き込むときだけです。

**ログ関係のオプション**

以下のオプションは、`BACKUP LOG` でのみ使用します。

> [!NOTE]
> ログ バックアップを取得しない場合は、単純復旧モデルを使用します。 詳しくは、「[復旧モデル](../../relational-databases/backup-restore/recovery-models-sql-server.md)」をご覧ください。

{ NORECOVERY | STANDBY **=** _undo_file_name_ }

NORECOVERY

ログの末尾をバックアップし、データベースを RESTORING の状態のままにします。 NORECOVERY は、セカンダリ データベースにフェールオーバーする場合、または RESTORE 操作の前にログの末尾を保存する場合に便利です。

ログの切り捨てをスキップするベストエフォートのログ バックアップを実行して、データベースを自動的に RESTORING 状態にするには、`NO_TRUNCATE` および `NORECOVERY` オプションを同時に使用します。

STANDBY **=** _standby_file_name_

ログの末尾をバックアップし、データベースを読み取り専用かつ STANDBY の状態のままにします。 STANDBY 句では、スタンバイ データが書き込まれます。ロールバックが実行されますが、追加の復元を行うこともできます。 STANDBY オプションの使用は、BACKUP LOG WITH NORECOVERY の後に RESTORE WITH STANDBY を使用する場合と同じ効果があります。

スタンバイ モードの使用にはスタンバイ ファイルが必要で、これは *standby_file_name* で指定します。その位置はデータベースのログに格納されます。 指定したファイルが既に存在する場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)]によってファイルが上書きされます。ファイルが存在しない場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)]によってファイルが作成されます。 スタンバイ ファイルは、データベースの一部になります。

このファイルでは、ロールバックされた変更内容を保持しており、RESTORE LOG 操作が後から適用される場合は、変更内容の順序を逆にする必要があります。 コミットされていないトランザクションのロールバックによって変更されたデータベース内の個々のページすべてをスタンバイ ファイルに保存できるように、ファイルの増大に備えて十分なディスク容量が必要になります。

NO_TRUNCATE

ログが切り捨てられないように指定し、データベースの状態に関係なく、[!INCLUDE[ssDE](../../includes/ssde-md.md)]によってバックアップが試行されるようにします。 その結果、`NO_TRUNCATE` で実行されるバックアップに不完全なメタデータが含まれる場合があります。 このオプションを使用すると、データベースが破損している場合でもログをバックアップできます。

BACKUP LOG の NO_TRUNCATE オプションを指定すると、COPY_ONLY と CONTINUE_AFTER_ERROR の両方を指定する場合と同じ結果が得られます。

`NO_TRUNCATE` オプションを使用しない場合は、データベースが ONLINE 状態である必要があります。 データベースが SUSPENDED 状態の場合は、`NO_TRUNCATE` を指定することによってバックアップを作成できる可能性があります。 ただし、データベースが OFFLINE または EMERGENCY 状態の場合、`NO_TRUNCATE` を使用しても BACKUP は使用できません。 データベースの状態については、「[データベースの状態](../../relational-databases/databases/database-states.md)」を参照してください。

## <a name="about-working-with-sql-server-backups"></a>SQL Server バックアップの操作について

このセクションでは、次の基本的なバックアップの概念について説明します。

[バックアップの種類](#Backup_Types)
[トランザクション ログの切り捨て](#Tlog_Truncation)
[バックアップ メディアのフォーマット](#Formatting_Media)
[バックアップ デバイスとメディア セットの操作](#Backup_Devices_and_Media_Sets)
[SQL Server バックアップの復元](#Restoring_Backups)

> [!NOTE]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でのバックアップの概要については、「[バックアップの概要](../../relational-databases/backup-restore/backup-overview-sql-server.md)」をご覧ください。

### <a name="Backup_Types"></a> バックアップの種類

サポートされるバックアップの種類は、次のようにデータベースの復旧モデルに依存します。

- データの完全バックアップと差分バックアップはすべての復旧モデルで実行できます。

    |バックアップの範囲|バックアップの種類|
    |---------------------|------------------|
    |データベース全体|[データベース バックアップ](../../relational-databases/backup-restore/full-database-backups-sql-server.md)では、データベース全体が対象となります。<br /><br /> 必要に応じて、各データベース バックアップは、1 つ以上の[データベースの差分バックアップ](../../relational-databases/backup-restore/differential-backups-sql-server.md)のベースとして使用することもできます。|
    |データベースの部分バックアップ|[部分バックアップ](../../relational-databases/backup-restore/partial-backups-sql-server.md)では、読み取り/書き込みファイル グループ、および必要な場合は 1 つ以上の読み取り専用ファイルまたはファイル グループが対象となります。<br /><br /> 必要に応じて、各部分バックアップは、1 つ以上の[部分的な差分バックアップ](../../relational-databases/backup-restore/differential-backups-sql-server.md)のベースとして使用することもできます。|
    |ファイルまたはファイル グループ|[ファイル バックアップ](../../relational-databases/backup-restore/full-file-backups-sql-server.md)では、1 つ以上のファイルまたはファイル グループが対象となります。このバックアップは、複数のファイル グループを含むデータベースにのみ関連します。 単純復旧モデルでは、ファイル バックアップは基本的に、読み取り専用のセカンダリ ファイル グループに限定されます。<br /> 必要に応じて、各ファイル バックアップは、1 つ以上の[ファイルの差分バックアップ](../../relational-databases/backup-restore/differential-backups-sql-server.md)のベースとして使用することもできます。|

- 完全復旧モデルまたは一括ログ復旧モデルでは、従来のバックアップの必須作業として、シーケンシャル *トランザクション ログ バックアップ* (または*ログ バックアップ*) も含まれます。 各ログ バックアップでは、トランザクション ログのうち、バックアップが作成された時点でアクティブだった部分と、前回のログ バックアップにおいてバックアップされなかったすべてのログ レコードが対象となります。

    作業損失の可能性を最小に抑えるには、管理のオーバーヘッドが発生しても、ログ バックアップを頻繁に行うようにスケジュールする必要があります。 完全バックアップの合間に差分バックアップを行うようにスケジュールすると、データを復元した後で復元する必要のあるログ バックアップの数が減るので、復元時間を短縮することができます。

     ログ バックアップは、データベースのバックアップとは別のボリュームに配置することをお勧めします。

    > [!NOTE]
    > 最初のログ バックアップを作成するには、その前に完全バックアップを作成する必要があります。

- *コピーのみのバックアップ*は、従来のバックアップで行われる一連の作業とは別に、特別な目的で行われる完全バックアップまたはログ バックアップです。 コピーのみのバックアップを作成するには、BACKUP ステートメント内で COPY_ONLY オプションを指定します。 詳しくは、「[コピーのみのバックアップ](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)」をご覧ください。

### <a name="Tlog_Truncation"></a> トランザクション ログの切り捨て

データベースのトランザクション ログがいっぱいにならないように、トランザクション ログを定期的にバックアップする必要があります。 ログの切り捨ては、単純復旧モデルではデータベースのバックアップ後に、完全復旧モデルではトランザクション ログのバックアップ後に、自動的に行われます。 ただし、切り捨ての処理が遅れる場合もあります。 ログの切り捨てが遅れる要因については、「[トランザクション ログ](../../relational-databases/logs/the-transaction-log-sql-server.md)」をご覧ください。

> [!NOTE]
> `BACKUP LOG WITH NO_LOG` および `WITH TRUNCATE_ONLY` オプションは廃止されました。 完全復旧モデルまたは一括ログ復旧モデルの復旧を使用している場合に、ログ バックアップ チェーンをデータベースから削除するには、単純復旧モデルに切り替える必要があります。 詳しくは、「[データベースの復旧モデルの表示または変更](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)」をご覧ください。

### <a name="Formatting_Media"></a> バックアップ メディアのフォーマット

次の条件のいずれか 1 つでも該当する場合は、BACKUP ステートメントでバックアップ メディアがフォーマットされます。

- `FORMAT` オプションが指定されている。
- メディアが空である。
- 操作が、連続するテープの書き込みになっている。

### <a name="Backup_Devices_and_Media_Sets"></a> バックアップ デバイスとメディア セットの操作

#### <a name="backup-devices-in-a-striped-media-set-a-stripe-set"></a>ストライプ メディア セット (ストライプ セット) 内のバックアップ デバイス
*ストライプ セット* とは、データがブロックに分割され、一定の順序で分散される、一連のディスク ファイルです。 ストライプ セットで使用されるバックアップ デバイスの数は、(`FORMAT` でメディアを最初期化する場合を除いて) 常に同じである必要があります。

次の例では、[!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] データベースのバックアップを、3 つのディスク ファイルを使用する新しいストライプ メディア セットに書き込みます。

```sql
BACKUP DATABASE AdventureWorks2012
TO DISK='X:\SQLServerBackups\AdventureWorks1.bak',
DISK='Y:\SQLServerBackups\AdventureWorks2.bak',
DISK='Z:\SQLServerBackups\AdventureWorks3.bak'
WITH FORMAT,
  MEDIANAME = 'AdventureWorksStripedSet0',
  MEDIADESCRIPTION = 'Striped media set for AdventureWorks2012 database';
GO
```

バックアップ デバイスをストライプ セットの一部として定義すると、以降は FORMAT を指定しない限り、単一デバイスのバックアップに使用することはできません。 同様に、非ストライプ バックアップを含むバックアップ デバイスは、FORMAT を指定しない限り、ストライプ セットでは使用できません。 ストライプ バックアップ セットを分割するには、FORMAT を使用します。

メディア ヘッダーを書き込むときに MEDIANAME と MEDIADESCRIPTION のいずれも指定しない場合、空白項目に該当するメディアのヘッダー フィールドは空になります。

#### <a name="working-with-a-mirrored-media-set"></a>ミラー化されたメディア セットの操作

通常、バックアップはミラー化されず、BACKUP ステートメントには単純に TO 句のみを指定します。 ただし、メディア セットごとに全部で 4 つまで、ミラーを指定することが可能です。 ミラー化メディア セットの場合、バックアップ操作では、バックアップ デバイスの複数のグループに書き込みが行われます。 バックアップ デバイスの各グループは、ミラー化メディア セット内の 1 つのミラーから構成されます。 それぞれのミラーでは同じ容量および種類の物理バックアップ デバイスを使用する必要があり、プロパティがすべて同じである必要があります。

ミラー化メディア セットにバックアップするには、すべてのミラーが存在している必要があります。 ミラー化されたメディア セットにバックアップするには、`TO` 句に 1 つ目のミラーを指定し、`MIRROR TO` 句にその他のミラーをそれぞれ指定します。

ミラー化されたメディア セットの場合、各 `MIRROR TO` 句では、TO 句と同じ数および種類のデバイスのリストを指定する必要があります。 次の例では、ミラー化メディア セットに書き込みを行います。このメディア セットには 2 つのミラーが含まれ、各ミラーに 3 つのデバイスが使用されています。

```sql
BACKUP DATABASE AdventureWorks2012
TO DISK='X:\SQLServerBackups\AdventureWorks1a.bak',
  DISK='Y:\SQLServerBackups\AdventureWorks2a.bak',
  DISK='Z:\SQLServerBackups\AdventureWorks3a.bak'
MIRROR TO DISK='X:\SQLServerBackups\AdventureWorks1b.bak',
  DISK='Y:\SQLServerBackups\AdventureWorks2b.bak',
  DISK='Z:\SQLServerBackups\AdventureWorks3b.bak';
GO
```

> [!IMPORTANT]
> この例は、ローカル システム上でテストできるように設計されています。 実際には同じドライブ上にある複数のデバイスにバックアップすると、パフォーマンスが低下するおそれがあり、ミラー化されたメディア セットの設計目的でもある冗長性が損なわれる可能性があります。

##### <a name="media-families-in-mirrored-media-sets"></a>ミラー化されたメディア セットのメディア ファミリ

BACKUP ステートメントの `TO` 句で指定する各バックアップ デバイスは、メディア ファミリに対応します。 たとえば、`TO` 句で 3 つのデバイスのリストを指定する場合、BACKUP では 3 つのメディア ファミリにデータが書き込まれます。 ミラー化メディア セットでは、どのミラーにもすべてのメディア ファミリのコピーが含まれている必要があります。 このため、各ミラーでデバイス数が一致する必要があります。

各ミラーに対し複数のデバイスのリストを指定する順番によって、どのメディア ファミリがどのデバイスに書き込まれるかが決まります。 たとえば、各デバイスのリストで、2 番目のデバイスは 2 番目のメディア ファミリに対応します。 先に示した例のデバイスでは、デバイスとメディア ファミリの対応は次の表のようになります。

|ミラー|メディア ファミリ 1|メディア ファミリ 2|メディア ファミリ 3|
|---------|---------|---------|---------|
|0|`Z:\AdventureWorks1a.bak`|`Z:\AdventureWorks2a.bak`|`Z:\AdventureWorks3a.bak`|
|1|`Z:\AdventureWorks1b.bak`|`Z:\AdventureWorks2b.bak`|`Z:\AdventureWorks3b.bak`|

 1 つのメディア ファミリは常に、特定のミラー内の同じデバイス上にバックアップされる必要があります。 したがって、既存のメディア セットを使用するときは毎回、メディア セットを作成したときに指定した同じ順序で各ミラーのデバイスを列挙してください。

ミラー化メディア セットについて詳しくは、「[ミラー化バックアップ メディア セット](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)」をご覧ください。 メディア セットとメディア ファミリの概要について詳しくは、「[メディア セット、メディア ファミリ、およびバックアップ セット](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)」をご覧ください。

### <a name="Restoring_Backups"></a> SQL Server バックアップの復元

データベースを復元し、必要に応じて、そのデータベースを復旧してオンラインにする、またはファイルやファイル グループを復元するには、[!INCLUDE[tsql](../../includes/tsql-md.md)] の [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) ステートメントを使用するか、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の**復元**タスクを使用します。 詳しくは、「[復元と復旧の概要](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)」をご覧ください。

## <a name="Additional_Considerations"></a> BACKUP のオプションに関するその他の注意点

### <a name="Interactions_SKIP_etc"></a> SKIP、NOSKIP、INIT、および NOINIT の相関関係

次の表に、{ **NOINIT** | INIT } と { **NOSKIP** | SKIP } オプションの相関関係を示します。

> [!NOTE]
> テープ メディアが空の場合、またはディスクのバックアップ ファイルが存在しない場合は、これらすべての相関関係によってメディア ヘッダーが記述され、続行されます。 ただし、メディアが空でなく、有効なメディア ヘッダーがない場合、これらの操作によって、有効な MTF メディアでないことを示すフィードバックが返され、バックアップ操作が中断されます。

||NOINIT|INIT|
|------|------------|----------|
|NOSKIP|ボリュームに有効なメディア ヘッダーが含まれる場合は、`MEDIANAME` が指定されていれば、その値とメディア名が一致していることを確認します。 メディア名が一致した場合は、すべての既存のバックアップ セットはそのままにして、バックアップ セットを追加します。<br /> ボリュームに有効なメディア ヘッダーが含まれない場合は、エラーが発生します。|ボリュームに有効なメディア ヘッダーが含まれている場合は、次のチェックを実行します。<br /><ul><li>`MEDIANAME` を指定した場合は、指定されているメディア名がメディア ヘッダーのメディア名と一致していることを確認します。<sup>1</sup></li><li>メディア上に失効前のバックアップ セットが既に存在していないことを確認します。 存在している場合は、バックアップを中断します。</li></ul><br />上のチェックにパスした場合は、メディア ヘッダーだけをそのままにして、メディア上のすべてのバックアップ セットを上書きします。<br /> ボリュームに有効なメディア ヘッダーが含まれない場合は、`MEDIANAME` および `MEDIADESCRIPTION` が指定されていれば、これらのオプションを使用してメディア ヘッダーを生成します。|
|SKIP|ボリュームに有効なメディア ヘッダーが含まれる場合は、すべての既存のバックアップ セットをそのまま保持して、バックアップ セットを追加します。|ボリュームに有効な<sup>2</sup> メディア ヘッダーが含まれる場合は、メディア ヘッダーだけをそのままにして、メディア上のすべてのバックアップ セットを上書きします。<br /> メディアが空の場合は、`MEDIANAME` および `MEDIADESCRIPTION` が指定されていれば、これらのオプションを使用してメディア ヘッダーを生成します。|

<sup>1</sup> ユーザーは、バックアップ操作を実行する適切な固定データベースまたはサーバー ロールに属している必要があります。

<sup>2</sup> 有効性には、MTF のバージョン番号およびその他のヘッダー情報が含まれます。 指定されたバージョンがサポートされていないか、予期しない値の場合、エラーが発生します。

## <a name="compatibility"></a>互換性

> [!CAUTION]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって作成されたバックアップは、それより前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では復元できません。

以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] との下位互換性を提供するため、BACKUP では `RESTART` オプションがサポートされます。 ただし、RESTART は無効です。

## <a name="general-remarks"></a>全般的な解説

データベースやログのバックアップは、任意のディスクまたはテープ デバイスに追加できます。これによって、データベースとそのトランザクション ログすべてを物理的な 1 つの場所の中に格納できます。

BACKUP ステートメントは、明示的または暗黙的なトランザクションでは使用できません。

オペレーティング システムがデータベースの照合順序をサポートしている限り、プロセッサの種類が違っていても、プラットフォーム間にわたるバックアップ操作を実行できます。

単一のデータ ファイルを含む、[透過的なデータ暗号化 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) が有効になっているデータベースでバックアップの圧縮を使用する場合は、**65536 (64 KB) より大きい** `MAXTRANSFERSIZE` 設定を使用することをお勧めします。
[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降では、これにより、最初にページを暗号化解除し、圧縮してから再度暗号化する、TDE で暗号化されたデータベースの最適化された圧縮アルゴリズムが有効になります。 `MAXTRANSFERSIZE = 65536` (64 KB) を使用する場合、TDE で暗号化されたデータベースでのバックアップの圧縮では暗号化されたページが直接圧縮され、適切な圧縮比率が得られない可能性があります。 詳細については、「[Backup Compression for TDE-enabled Databases](https://blogs.msdn.microsoft.com/sqlcat/2016/06/20/sqlsweet16-episode-1-backup-compression-for-tde-enabled-databases/)」 (TDE が有効になっているデータベースのバックアップの圧縮) を参照してください。

> [!NOTE]
> 次のように、既定の `MAXTRANSFERSIZE` が 64 K より大きくなる場合もあります。
>
> - データベースに複数のデータ ファイルが作成されている場合、64 K より大きい `MAXTRANSFERSIZE` が使用されます。
> - URL へのバックアップを実行する場合、既定値は `MAXTRANSFERSIZE = 1048576` (1 MB) になります。
>
> これらの条件のいずれかが当てはまる場合は、バックアップ コマンドで明示的に 64 K より大きい `MAXTRANSFERSIZE` を設定して、新しいバックアップ圧縮アルゴリズムを取得する必要があります。

既定では、バックアップ操作が成功するたびに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログおよびシステム イベント ログにエントリが 1 つ追加されます。 ログを頻繁にバックアップすると、これらの成功メッセージがすぐに蓄積され、他のメッセージを探すのが困難になるほどエラー ログが大きくなることがあります。 そのような場合、これらのエントリに依存するスクリプトがなければ、トレース フラグ 3226 を使用することによってこれらのログ エントリを除外できます。 詳しくは、「[トレース フラグ](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)」をご覧ください。

## <a name="interoperability"></a>相互運用性

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、オンライン バックアップを使用して、使用中のデータベースをバックアップできます。 バックアップ中はほとんどの操作が可能です。たとえば、INSERT、UPDATE、または DELETE ステートメントはバックアップ操作中でも使用できます。

データベース バックアップやトランザクション ログ バックアップ中に実行できない操作には、次のものがあります。

- `ADD FILE` または `REMOVE FILE` オプションを指定した `ALTER DATABASE` ステートメントなどのファイル管理操作。

- データベースまたはファイルの圧縮操作。 これには自動圧縮操作も含まれます。

バックアップ操作がファイル管理または圧縮操作と重複すると、競合が発生します。 どの競合操作が最初に始まったかに関係なく、最初の操作によって設定されたロックがタイムアウトになるまで、2 番目の操作は待機します (タイムアウト時間は、セッション タイムアウト設定によって制御されます)。 ロックがタイムアウト期間内に解放されると、2 番目の操作が開始されます。 ロックがタイムアウトになると、2 番目の操作は実行されません。

## <a name="metadata"></a>メタデータ

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には次のようなバックアップ履歴テーブルがあり、これによってバックアップ処理が追跡されます。

- [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md)
- [backupfilegroup](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)
- [backupmediafamily](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)
- [backupmediaset](../../relational-databases/system-tables/backupmediaset-transact-sql.md)
- [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)

復元を実行するときに、バックアップ セットが **msdb** データベースにまだ記録されていないと、バックアップ履歴テーブルが変更される可能性があります。

## <a name="security"></a>Security

[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降では、バックアップの作成での `PASSWORD` と `MEDIAPASSWORD` オプションが廃止されました。 パスワード付きで作成されたバックアップを復元することは、引き続き可能です。

### <a name="permissions"></a>アクセス許可

BACKUP DATABASE 権限と BACKUP LOG 権限は、既定では、 **sysadmin** 固定サーバー ロール、 **db_owner** 固定データベース ロール、および **db_backupoperator** 固定データベース ロールのメンバーに与えられています。

バックアップ デバイスの物理ファイルに対する所有と許可の問題によって、バックアップ操作が妨げられることがあります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、デバイスに対して読み書きを実行できる必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスが実行されているアカウントには書き込み権限が必要です。 ただし、システム テーブルにバックアップ デバイスのエントリを追加する [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)では、ファイル アクセスの権限は確認されません。 バックアップ デバイスの物理ファイルに関するこのような問題は、バックアップや復元が試行され、物理リソースがアクセスされるまで、表面化しない可能性があります。

## <a name="examples"></a> 使用例

ここでは、次の例について説明します。

- A. [データベース全体をバックアップする](#backing_up_db)
- B. [データベースおよびログをバックアップする](#backing_up_db_and_log)
- C. [セカンダリ ファイル グループの完全ファイル バックアップを作成する](#full_file_backup)
- D. [セカンダリ ファイル グループの差分ファイル バックアップを作成する](#differential_file_backup)
- E. [単一ファミリ ミラー化メディア セットを作成し、そこにバックアップを作成する](#create_single_family_mirrored_media_set)
- F. [マルチファミリ ミラー化メディア セットを作成し、そこにバックアップを作成する](#create_multifamily_mirrored_media_set)
- G. [既存のミラー化メディア セットにバックアップする](#existing_mirrored_media_set)
- H. [新しいメディア セットに圧縮されたバックアップを作成する](#creating_compressed_backup_new_media_set)
- I. [Microsoft Azure BLOB ストレージ サービスへのバックアップ](#url)
- J. [バックアップ ステートメントの進行状況を追跡する](#backup_progress)

> [!NOTE]
> バックアップ方法に関するトピックには、他にも例が記載されています。 詳しくは、「[バックアップの概要](../../relational-databases/backup-restore/backup-overview-sql-server.md)」をご覧ください。

### <a name="backing_up_db"></a> A. データベース全体をバックアップする

次の例では、[!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] データベースをディスク ファイルにバックアップします。

```sql
BACKUP DATABASE AdventureWorks2012
 TO DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'
    WITH FORMAT;
GO
```

### <a name="backing_up_db_and_log"></a> B. データベースおよびログをバックアップする

次の例では、既定により単純復旧モデルを使用する [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースをバックアップします。 ここではまず、ログをバックアップするため、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースを修正して完全復旧モデルを使用するようにします。

次に [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md) を使用して、データのバックアップ用に論理[バックアップ デバイス](../../relational-databases/backup-restore/backup-devices-sql-server.md) `AdvWorksData` を作成し、ログのバックアップ用に別の論理バックアップ デバイス `AdvWorksLog` を作成します。

その後、`AdvWorksData` にデータベースの完全バックアップを作成し、更新操作の期間後、ログを `AdvWorksLog` にバックアップします。

```sql
-- To permit log backups, before the full database backup, modify the database
-- to use the full recovery model.
USE master;
GO
ALTER DATABASE AdventureWorks2012
    SET RECOVERY FULL;
GO
-- Create AdvWorksData and AdvWorksLog logical backup devices.
USE master
GO
EXEC sp_addumpdevice 'disk', 'AdvWorksData',
'Z:\SQLServerBackups\AdvWorksData.bak';
GO
EXEC sp_addumpdevice 'disk', 'AdvWorksLog',
'X:\SQLServerBackups\AdvWorksLog.bak';
GO

-- Back up the full AdventureWorks2012 database.
BACKUP DATABASE AdventureWorks2012 TO AdvWorksData;
GO
-- Back up the AdventureWorks2012 log.
BACKUP LOG AdventureWorks2012
    TO AdvWorksLog;
GO
```

> [!NOTE]
> 運用データベースでは、ログを定期的にバックアップしてください。 ログのバックアップは、データ損失から万全に保護できるように頻繁に行ってください。

### <a name="full_file_backup"></a> C. セカンダリ ファイル グループの完全ファイル バックアップを作成する

次の例では、両方のセカンダリ ファイル グループ内のすべてのファイルについて、完全ファイル バックアップを作成します。

```sql
--Back up the files in SalesGroup1:
BACKUP DATABASE Sales
    FILEGROUP = 'SalesGroup1',
    FILEGROUP = 'SalesGroup2'
    TO DISK = 'Z:\SQLServerBackups\SalesFiles.bck';
GO
```

### <a name="differential_file_backup"></a> D. セカンダリ ファイル グループの差分ファイル バックアップを作成する

次の例では、両方のセカンダリ ファイル グループ内のすべてのファイルについて、差分ファイル バックアップを作成します。

```sql
--Back up the files in SalesGroup1:
BACKUP DATABASE Sales
    FILEGROUP = 'SalesGroup1',
    FILEGROUP = 'SalesGroup2'
    TO DISK = 'Z:\SQLServerBackups\SalesFiles.bck'
    WITH
      DIFFERENTIAL;
GO
```

### <a name="create_single_family_mirrored_media_set"></a> E. 単一ファミリ ミラー化メディア セットを作成し、そこにバックアップを作成する

次の例では、単一メディア ファミリと 4 つのミラーを含むミラー化メディア セットを作成し、そこに [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] データベースのバックアップを作成します。

```sql
BACKUP DATABASE AdventureWorks2012
TO TAPE = '\\.\tape0'
MIRROR TO TAPE = '\\.\tape1'
MIRROR TO TAPE = '\\.\tape2'
MIRROR TO TAPE = '\\.\tape3'
WITH
    FORMAT,
    MEDIANAME = 'AdventureWorksSet0';
```

### <a name="create_multifamily_mirrored_media_set"></a> F. マルチファミリ ミラー化メディア セットを作成して、そこにバックアップする

次の例では、各ミラーが 2 つのメディア ファミリで構成されているミラー化メディア セットを作成します。 その後、両方のミラーに [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] データベースのバックアップが作成されます。

```sql
BACKUP DATABASE AdventureWorks2012
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'
WITH
    FORMAT,
    MEDIANAME = 'AdventureWorksSet1';
```

### <a name="existing_mirrored_media_set"></a> G. 既存のミラー化メディア セットにバックアップする

次の例では、前の例で作成されたメディア セットにバックアップ セットを追加します。

```sql
BACKUP LOG AdventureWorks2012
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'
WITH
    NOINIT,
    MEDIANAME = 'AdventureWorksSet1';
```

> [!NOTE]
> NOINIT は既定値ですが、ここではわかりやすくするために記載しています。

### <a name="creating_compressed_backup_new_media_set"></a> H. 新しいメディア セットに圧縮されたバックアップを作成する

次の例では、メディアをフォーマットして新しいメディア セットを作成し、[!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] データベースの圧縮された完全バックアップを実行します。

```sql
BACKUP DATABASE AdventureWorks2012 TO DISK='Z:\SQLServerBackups\AdvWorksData.bak'
WITH
    FORMAT,
    COMPRESSION;
```

### <a name="url"></a> I. Microsoft Azure BLOB ストレージ サービスへのバックアップ

この例では、Microsoft Azure BLOB ストレージ サービスへの `Sales` のデータベースの完全バックアップを実行します。 ストレージ アカウント名は `mystorageaccount`です。 コンテナーは `myfirstcontainer`と呼ばれます。 保存されたアクセス ポリシーは読み取り、書き込み、削除および一覧表示権で作成されています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資格情報 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` は、保存されたアクセス ポリシーに関連付けられている Shared Access Signature を使用して作成されています。 Microsoft Azure BLOB ストレージ サービスへの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバックアップについては、「[Microsoft Azure BLOB ストレージ サービスを使用した SQL Server のバックアップと復元](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)」および「[SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)」を参照してください。

```sql
BACKUP DATABASE Sales
TO URL = 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_20160726.bak'
WITH STATS = 5;
```

### <a name="backup_progress"></a> J. バックアップ ステートメントの進行状況を追跡する

次のクエリでは、現在実行中のバックアップ ステートメントに関する情報が返されます。
```sql
SELECT query = a.text, start_time, percent_complete,
    eta = dateadd(second,estimated_completion_time/1000, getdate())
FROM sys.dm_exec_requests r
    CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) a
WHERE r.command LIKE 'BACKUP%'
```

## <a name="see-also"></a>参照

- [バックアップ デバイス](../../relational-databases/backup-restore/backup-devices-sql-server.md)
- [メディア セット、メディア ファミリ、およびバックアップ セット](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)
- [ログ末尾のバックアップ](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)
- [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)
- [DBCC SQLPERF](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)
- [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)
- [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)
- [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)
- [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)
- [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)
- [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)
- [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [sp_helpfile](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)
- [sp_helpfilegroup](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)
- [サーバー構成オプション](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
- [メモリ最適化テーブルを持つデータベースの段階的な部分復元](../../relational-databases/in-memory-oltp/piecemeal-restore-of-databases-with-memory-optimized-tables.md)

::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

> ||||
> |---|---|---|
> |[SQL Server](backup-transact-sql.md?view=sql-server-2016)|**_\* SQL Database<br />マネージド インスタンス \*_** &nbsp;|[分析プラットフォーム <br />システム (PDW)](backup-transact-sql.md?view=aps-pdw-2016)|

&nbsp;

## <a name="azure-sql-database-managed-instance"></a>Azure SQL Database マネージド インスタンス

Azure SQL Database Managed Instance に配置/ホストされている SQL Database をバックアップします。 SQL Database [マネージド インスタンス](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)には自動バックアップがあり、ユーザーは完全なデータベース `COPY_ONLY` バックアップを作成できます。 差分、ログ、およびファイル スナップショットのバックアップはサポートされていません。

## <a name="syntax"></a>構文

```sql
BACKUP DATABASE { database_name | @database_name_var }
  TO URL = { 'physical_device_name' | @physical_device_name_var }[ ,...n ]
  WITH COPY_ONLY [, { <general_WITH_options> } ]
[;]

<general_WITH_options> [ ,...n ]::=

--Media Set Options
   MEDIADESCRIPTION = { 'text' | @text_variable }
 | MEDIANAME = { media_name | @media_name_variable }
 | BLOCKSIZE = { blocksize | @blocksize_variable }

--Data Transfer Options
   BUFFERCOUNT = { buffercount | @buffercount_variable }
 | MAXTRANSFERSIZE = { maxtransfersize | @maxtransfersize_variable }

--Error Management Options
   { NO_CHECKSUM | CHECKSUM }
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }

--Compatibility Options
   RESTART

--Monitoring Options
   STATS [ = percentage ]

--Encryption Options
 ENCRYPTION (ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY } , encryptor_options ) <encryptor_options> ::=
   SERVER CERTIFICATE = Encryptor_Name | SERVER ASYMMETRIC KEY = Encryptor_Name
```

## <a name="arguments"></a>引数

DATABASE: データベース全体のバックアップを指定します。 データベースのバックアップ時、Managed Instance では、バックアップが復元された場合に一貫性のあるデータベースを生成するのに十分なトランザクション ログをバックアップします。

> [!IMPORTANT]
> マネージド インスタンスで作成されたデータベース バックアップは、別の マネージド インスタンス上にのみ復元できます。 (SQL Server 2016 データベースのバックアップを SQL Server 2012 インスタンスに復元できないことと同様に) SQL Server のオンプレミス インスタンスに復元することはできません。

BACKUP DATABASE (*データ バックアップ*) で作成されたバックアップを復元すると、バックアップ全体が復元されます。 Azure SQL Database マネージド インスタンスの自動バックアップから復元する方法については、「[データベースをマネージド インスタンスに復元する](/azure/sql-database/sql-database-managed-instance-get-started-restore)」を参照してください。

{ *database_name* |  **@** _database\_name\_var_ }: データベース全体のバックアップ元となるデータベースです。 変数 ( **@** _database\_name\_var_) として指定する場合、この名前は、文字列定数 ( **@** _database\_name\_var_ **=** _database name_) として指定するか、**ntext** または**text** データ型以外の文字列データ型の変数として指定します。

詳しくは、「[ファイルの完全バックアップ](../../relational-databases/backup-restore/full-file-backups-sql-server.md)」および「[ファイルおよびファイル グループのバックアップ](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)」をご覧ください。

TO URL

バックアップ操作に使用する URL を指定します。 URL の形式は、Microsoft Azure ストレージ サービスへのバックアップを作成するために使用されます。

> [!IMPORTANT]
> URL へのバックアップ時に複数のデバイスにバックアップするには、Shared Access Signature (SAS) トークンを使用する必要があります。 Shared Access Signature の作成例については、「[SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)」と「[Simplifying creation of SQL Credentials with Shared Access Signature ( SAS ) tokens on Azure Storage with Powershell](https://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx)」 (Powershell を使用する Azure ストレージにおける Shared Access Signature (SAS) トークンでの SQL 資格情報の作成の簡素化) を参照してください。

*n*: 最大 64 個のバックアップ デバイスを、コンマ区切りのリストで指定できることを示すプレースホルダーです。

### <a name="with-optionsspecifies-options-to-be-used-with-a-backup-operation"></a>WITH オプション: バックアップ操作で使用するオプションを指定します。

CREDENTIAL: Microsoft Azure BLOB ストレージ サービスにバックアップを作成する場合にのみ、使用されます。

ENCRYPTION: バックアップの暗号化を指定するために使用されます。 バックアップを暗号化するための暗号化アルゴリズムを指定するか、バックアップを暗号化しない場合は `NO_ENCRYPTION` を指定できます。 暗号化は、バックアップ ファイルをセキュリティで保護するために推奨される方法です。 指定できるアルゴリズムの一覧を次に示します。

- `AES_128`
- `AES_192`
- `AES_256`
- `TRIPLE_DES_3KEY`
- `NO_ENCRYPTION`

暗号化することを選択した場合、次の暗号化機能のオプションを使用して、暗号化機能も指定する必要があります。

- `SERVER CERTIFICATE = <Encryptor_Name>`
- `SERVER ASYMMETRIC KEY = <Encryptor_Name>`

**バックアップ セット オプション**

COPY_ONLY: バックアップが、通常のバックアップの順序には影響しない、*コピーのみのバックアップ*であることを指定します。 コピーのみのバックアップは、Azure SQL Database の自動バックアップとは関係なく作成されます。 詳しくは、「[コピーのみのバックアップ](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)」をご覧ください。

{ COMPRESSION | NO_COMPRESSION }: このバックアップに[バックアップの圧縮](../../relational-databases/backup-restore/backup-compression-sql-server.md)を実行するかどうかを指定し、サーバー レベルの既定値をオーバーライドします。

既定の動作では、バックアップの圧縮は行われません。 ただし、この既定の動作は、[backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) サーバー構成オプションを設定することで変更できます。 このオプションの現在の値の表示については、「[サーバー プロパティの表示または変更](../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md)」をご覧ください。

COMPRESSION: バックアップの圧縮を明示的に有効にします。

NO_COMPRESSION: バックアップの圧縮を明示的に無効にします。

DESCRIPTION **=** { **'** _text_ **'**  |  **@** _text\_variable_ }: バックアップ セットを記述したテキストを自由な形式で指定します。 文字列の長さは最大 255 文字です。

NAME **=** { *backup_set_name* |  **@** _backup\_set\_var_ }: バックアップ セットの名前を指定します。 名前の長さは最大 128 文字です。 NAME を指定しないと、名前は空白になります。

MEDIADESCRIPTION **=** { *text* | **@** _text\_variable_ }: メディア セットを説明した自由形式のテキストを最大 255 文字で指定します。

MEDIANAME **=** { *media_name* |  **@** _media\_name\_variable_ }: バックアップ メディア セット全体のメディア名を指定します。 メディア名は最長 128 文字まで入力できます。`MEDIANAME` を指定する場合、バックアップ ボリュームに既に存在する、前回指定したメディア名と一致する必要があります。 指定しなかった場合場合、または SKIP オプションを指定した場合、メディア名の照合チェックは行われません。

BLOCKSIZE **=** { *blocksize* |  **@** _blocksize\_variable_ }: 物理的なブロック サイズをバイト単位で指定します。 サポートされるサイズは、512、1024、2048、4096、8192、16384、32768、および 65536 (64 KB) バイトです。 テープ デバイスの場合の既定値は 65536 バイトで、他のデバイスの場合の既定値は 512 バイトです。 通常は、BACKUP によってデバイスに適したブロック サイズが自動的に選択されるので、このオプションは必要ありません。 ブロック サイズを明示的に指定すると、自動選択されたブロック サイズがオーバーライドされます。

**データ転送オプション**

BUFFERCOUNT **=** { *buffercount* |  **@** _buffercount\_variable_ }: バックアップ操作に使用される I/O バッファーの総数を指定します。 任意の正の整数を指定できますが、バッファー数が多いと Sqlservr.exe プロセス内で仮想アドレス空間が不足し、"メモリ不足" エラーが発生する場合があります。

バッファーで使用される領域の合計は、`BUFFERCOUNT * MAXTRANSFERSIZE` で決定されます。

> [!NOTE]
> `BUFFERCOUNT` オプションの使用に関する重要な情報については、ブログ「[Incorrect BufferCount data transfer option can lead to OOM condition](https://blogs.msdn.com/b/sqlserverfaq/archive/2010/05/06/incorrect-buffercount-data-transfer-option-can-lead-to-oom-condition.aspx)」 (不適切な BufferCount データ転送オプションによって OOM の状態になる可能性がある) を参照してください。

MAXTRANSFERSIZE **=** { *maxtransfersize* |  _**@** maxtransfersize\_variable_ } Specifies the largest unit of transfer in bytes to be used between [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] and the backup media. 有効値は 65536 バイト (64 KB) の倍数で、最大有効値は 4194304 バイト (4 MB) です。

> [!NOTE]
> 単一のデータ ファイルを含む、[透過的なデータ暗号化 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) が有効になっているデータベースの場合、既定の `MAXTRANSFERSIZE` は 65536 (64 KB) です。 TDE で暗号化されていないデータベースでは、ディスクへのバックアップを使用する場合は既定の `MAXTRANSFERSIZE` が 1048576 (1 MB) となり、VDI または TAPE を使用する場合は 65536 (64 KB) となります。

**エラー管理オプション**

以下のオプションでは、バックアップ操作に対してバックアップのチェックサムを有効にするかどうかと、エラー発生時に操作を停止するかどうかを判別できます。

{ **NO_CHECKSUM** | CHECKSUM }: バックアップのチェックサムを有効にするかどうかを制御します。

NO_CHECKSUM: バックアップ チェックサムの生成 (およびページ チェックサムの検証) を明示的に無効にします。 これは既定の動作です。

CHECKSUM: 有効かつ使用可能であれば、バックアップ操作において各ページのチェックサムおよび破損ページを検証し、バックアップ全体のチェックサムを生成するように指定します。

バックアップ チェックサムを使用すると、ワークロードとバックアップのスループットに影響する場合があります。

詳しくは、「[バックアップ中および復元中に発生する可能性があるメディア エラー](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)」をご覧ください。

{ **STOP_ON_ERROR** | CONTINUE_AFTER_ERROR }: ページ チェックサム エラーの発生後に、バックアップ操作を停止するか続行するかを制御します。

STOP_ON_ERROR: ページ チェックサムが正しくない場合、BACKUP が失敗になるように指示します。 これは既定の動作です。

CONTINUE_AFTER_ERROR: 無効なチェックサムやページの破損などのエラーが発生しても、BACKUP を続行するように指示します。

データベースが破損したときに、NO_TRUNCATE オプションを使用してもログの末尾をバックアップできない場合は、NO_TRUNCATE の代わりに CONTINUE_AFTER_ERROR を指定して[ログ末尾のバックアップ](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)を試すことができます。

詳しくは、「[バックアップ中および復元中に発生する可能性があるメディア エラー](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)」をご覧ください。

**互換性オプション**

RESTART は無効です。 このオプションは、以前のバージョンの SQL Server との互換性を維持するために使用できます。

**監視オプション**

STATS [ **=** _percentage_ ]: 各 *percentage* の完了ごとにメッセージを表示します。進行状況を判断するために使用されます。 *percentage* を省略した場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では 10% 完了するごとにメッセージが表示されます。

STATS オプションでは、次のパーセンテージ間隔を報告するしきい値に達した時点までに、完了したパーセンテージを報告します。 これは、ほぼ指定したパーセンテージになります。たとえば、STATS=10 とすると、40% が完了した場合に、オプションでは 43% と表示されることがあります。 大規模なバックアップ セットの場合は、完了した I/O 呼び出し間での完了パーセンテージの変化が非常に遅くなるため、これは重要な問題にはなりません。

## <a name="limitations-for-sql-database-managed-instance"></a>SQL Database マネージド インスタンスの制限事項

バックアップの最大ストライプ サイズは 195 GB (最大 BLOB サイズ) です。 バックアップ コマンドでストライプ サイズを増やして、個々のストライプ サイズを減らし、この制限内に収まるようにします。

## <a name="security"></a>Security

### <a name="permissions"></a>アクセス許可

BACKUP DATABASE アクセス許可は、既定では、**sysadmin** 固定サーバー ロール、**db_owner** 固定データベース ロール、および **db_backupoperator** 固定データベース ロールのメンバーに与えられています。

URL に対する所有とアクセス許可の問題によって、バックアップ操作が妨げられることがあります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、デバイスに対して読み書きを実行できる必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスが実行されているアカウントには書き込み権限が必要です。

## <a name="examples"></a> 使用例

この例では、Microsoft Azure BLOB ストレージ サービスへの `Sales` のデータベースの COPY_ONLY バックアップを実行します。 ストレージ アカウント名は `mystorageaccount`です。 コンテナーは `myfirstcontainer`と呼ばれます。 保存されたアクセス ポリシーは読み取り、書き込み、削除および一覧表示権で作成されています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資格情報 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` は、保存されたアクセス ポリシーに関連付けられている Shared Access Signature を使用して作成されています。 Microsoft Azure BLOB ストレージ サービスへの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバックアップについては、「[Microsoft Azure BLOB ストレージ サービスを使用した SQL Server のバックアップと復元](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)」および「[SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)」を参照してください。

```sql
BACKUP DATABASE Sales
TO URL = 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_20160726.bak'
WITH STATS = 5, COPY_ONLY;
```

## <a name="see-also"></a>参照

[データベースの復元](restore-statements-transact-sql.md)

::: moniker-end
::: moniker range=">=aps-pdw-2016||=sqlallproducts-allversions"

> ||||
> |---|---|---|
> |[SQL Server](backup-transact-sql.md?view=sql-server-2016)|[SQL Database<br />マネージド インスタンス](backup-transact-sql.md?view=azuresqldb-mi-current)|**_\*分析<br />プラットフォーム システム (PDW) \*_** &nbsp;|

&nbsp;

## <a name="analytics-platform-system"></a>分析プラットフォーム システム

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] データベースのバックアップを作成し、アプライアンスから離れた、ユーザーが指定したネットワーク上の場所に保存します。 ディザスター リカバリーのため、または1 つのアプライアンスから別のアプライアンスへデータベースをコピーするために、[RESTORE DATABASE - Analytics Platform System](../../t-sql/statements/restore-statements-transact-sql.md) と共にこのステートメントを使用します。

**開始する前に**、[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] の「Acquire and Configure a Backup Server」 (バックアップ サーバーを入手し、構成する) をご覧ください。

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] には、2 種類のバックアップがあります。 *データベースの完全バックアップ*では、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] データベース全体をバックアップします。 *差分バックアップ*では、最後の完全バックアップ以降の変更のみをバックアップします。 ユーザー データベースのバックアップには、データベース ユーザーとデータベース ロールが含まれます。 master データベースのバックアップにはログインが含まれます。

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] データベース バックアップの詳細については、[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] の 「バックアップと復元」に関するセクションをご覧ください。

## <a name="syntax"></a>構文

```sql
--Create a full backup of a user database or the master database.
BACKUP DATABASE database_name
    TO DISK = '\\UNC_path\backup_directory'
    [ WITH [ ( ]<with_options> [ ,...n ][ ) ] ]
[;]

--Create a differential backup of a user database.
BACKUP DATABASE database_name
    TO DISK = '\\UNC_path\backup_directory'
    WITH [ ( ] DIFFERENTIAL
    [ , <with_options> [ ,...n ] [ ) ]
[;]

<with_options> ::=
    DESCRIPTION = 'text'
    | NAME = 'backup_name'
```

## <a name="arguments"></a>引数

*database_name*: バックアップを作成するデータベースの名前。 データベースには、master データベースかユーザー データベースを指定できます。

TO DISK = '\\\\*UNC_path*\\*backup_directory*': [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] によってバックアップ ファイルが書き込まれるネットワーク パスとディレクトリ。 たとえば、'\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup' です。

- バックアップ ディレクトリ名のパスが既に存在し、完全修飾 UNC (汎用名前付け規則) パスとして指定されている必要があります。
- バックアップ ディレクトリ *backup_directory* は、バックアップ コマンドの実行前に存在することはできません。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] によってバックアップ ディレクトリが作成されます。
- バックアップ ディレクトリのパスにはローカル パスを指定できません。[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] アプライアンス ノード上の場所にすることもできません。
- UNC パスとバックアップ ディレクトリ名の最大長は 200 文字です。
- サーバーまたはホストは IP アドレスとして指定する必要があります。 これはホストまたはサーバー名として指定できません。

DESCRIPTION = **'** _text_ **'** : バックアップの説明テキストを指定します。 テキストの最大長は 255 文字です。

説明はメタデータに格納されます。バックアップ ヘッダーが RESTORE HEADERONLY で復元されるときに表示されます。

NAME = **'** _backup \_name_ **'** : バックアップの名前を指定します。 バックアップ名には、データベース名とは異なる名前を指定できます。

- 名前の長さは最大 128 文字です。
- パスを含めることはできません。
- 先頭の文字はアルファベット、数字、アンダースコア (_) のいずれかにする必要があります。 特殊文字としてはアンダースコア (\_)、ハイフン (-)、スペース ( ) が許可されます。 バックアップ名の最後の文字をスペースにすることはできません。
- 指定の場所に *backup_name* が既に存在する場合、ステートメントは失敗します。

この名前はメタデータに格納されます。バックアップ ヘッダーが RESTORE HEADERONLY で復元されるときに表示されます。

DIFFERENTIAL: ユーザー データベースの差分バックアップを実行するように指定します。 省略した場合、データベースの完全バックアップが選択されます。 差分バックアップの名前は、完全バックアップの名前に一致する必要がありません。 差分バックアップとそれに対応する完全バックアップを追跡記録するために、同じ名前に 'full' または 'diff' を付けることを検討してください。

例:

`BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerFull';`

`BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerDiff' WITH DIFFERENTIAL;`

## <a name="permissions"></a>アクセス許可

**BACKUP DATABASE** 許可または **db_backupoperator** 固定データベース ロールのメンバーシップが必要です。 master データベースは、**db_backupoperator** 固定データベース ロールに追加された標準ユーザーではバックアップできません。 master データベースをバックアップできるのは、**sa**、ファブリック管理者、または **sysadmin** 固定サーバー ロールのメンバーに限られます。

バックアップ ディレクトリにアクセスし、作成や書き込みを行うことが許可された Windows アカウントが必要です。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] に Windows アカウント名とパスワードを保存する必要もあります。 これらのネットワーク資格情報を [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] に追加するには、[sp_pdw_add_network_credentials - SQL Data Warehous](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) ストアド プロシージャを使用します。

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] の資格情報を管理する方法については、「[セキュリティ](#Security)」セクションをご覧ください。

## <a name="error-handling"></a>エラー処理

次の条件下での BACKUP DATABASE エラー:

- バックアップの実行に必要なアクセス許可がユーザーにありません。
- [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] には、バックアップが保存されるネットワーク上の場所にアクセスする権限がありません。
- データベースが存在しません。
- ターゲット ディレクトリがネットワーク共有に既に存在します。
- ターゲット ネットワーク共有が利用できません。
- ターゲット ネットワーク共有には、バックアップのための領域が十分にありません。 BACKUP DATABASE コマンドは、バックアップの開始前に十分なディスク領域があることを確認しません。BACKUP DATABASE の実行中、ディスク容量不足エラーが生成されます。 ディスク容量不足が発生すると、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] は BACKUP DATABASE コマンドをロールバックします。 データベースのサイズを減らすには、[DBCC SHRINKLOG (Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) を実行します。
- トランザクション内でバックアップを開始しようとします。

::: moniker-end
::: moniker range=">=aps-pdw-2016||>=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"
## <a name="general-remarks"></a>全般的な解説

データベース バックアップを実行する前に、[DBCC SHRINKLOG (Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) を使用し、データベースのサイズを減らします。

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] バックアップは、同じディレクトリ内で複数のファイルのセットとして保存されます。

通常、差分バックアップは完全バックアップよりも短時間で完了します。完全バックアップよりも頻繁に実行できます。 複数の差分バックアップが同じ完全バックアップに基づくとき、各差分バックアップには、前の差分バックアップのすべての変更が含まれます。

BACKUP コマンドをキャンセルした場合、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] はターゲット ディレクトリとバックアップのために作成されたあらゆるファイルを削除します。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] で共有へのネットワーク接続が失われると、ロールバックを完了できません。

完全バックアップと差分バックアップは別々のディレクトリに保存されます。 完全バックアップと差分バックアップが同じバックアップに属することを指定するために名前付け規則が強制されることはありません。 独自の名前付け規則で追跡できます。 あるいは、WITH DESCRIPTION オプションで説明を追加し、RESTORE HEADERONLY ステートメントで説明を取得するという方法でも追跡できます。

::: moniker-end
::: moniker range=">=aps-pdw-2016||=sqlallproducts-allversions"
## <a name="limitations-and-restrictions"></a>制限事項と制約事項

master データベースは差分バックアップできません。 master データベースでは、完全バックアップのみ可能です。

バックアップ ファイルは、[RESTORE DATABASE - Analytics Platform System](../../t-sql/statements/restore-statements-transact-sql.md) ステートメントを利用して、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] アプライアンスにバックアップを復元するのに適した形式でのみ保存されます。

データやユーザー情報を SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに移動するために、バックアップと BACKUP DATABASE ステートメントを使用することはできません。 この機能については、リモート テーブル コピー機能を使用できます。 詳細については、[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] の "Remote Table Copy" (リモート テーブル コピー) をご覧ください。

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップ技術を利用し、データベースをバックアップし、復元します。 バックアップ圧縮を使用するために、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップ オプションが事前構成されています。 圧縮、チェックサム、ブロック サイズ、バッファー カウントなど、バックアップ オプションを設定することはできません。

アプライアンスで一度に実行できるデータベース バックアップまたは復元は 1 つに限られます。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] は、現在のバックアップまたは復元コマンドが完了するまで、バックアップまたは復元コマンドを待ち行列に入れます。

バックアップを復元するためのターゲット アプライアンスには、ソース アプライアンスと同じ数の計算ノードが含まれている必要があります。 ターゲット アプライアンスにはソース アプライアンスより多くの計算ノードが含まれていても構いませんが、少ないことは許可されません。

バックアップはアプライアンスから離れた場所に保存されるため、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] はバックアップの場所や名前を追跡しません。

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] はデータベース バックアップの成功または失敗を追跡します。

差分バックアップは、前回の完全バックアップが正常に完了した場合にのみ許可されます。 たとえば、月曜日に Sales データベースの完全バックアップを作成し、バックアップが正常に完了したとします。 火曜日にも Sales データベースの完全バックアップを作成するが失敗します。 この失敗の後、月曜日の完全バックアップに基づいて差分バックアップを作成することはできません。 差分バックアップを作成するには、最初に完全バックアップを正常に作成する必要があります。

## <a name="metadata"></a>メタデータ

これらの動的管理ビューには、すべてのバックアップ操作、復元操作、読み込み操作に関する情報が含まれています。 情報は、システムの再起動の間で永続化します。

- [sys.pdw_loader_backup_runs](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)
- [sys.pdw_loader_backup_run_details](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)
- [sys.pdw_loader_run_stages](../../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)

## <a name="performance"></a>パフォーマンス

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] では、バックアップを実行するために、最初にメタデータをバックアップし、それから計算ノードに保存されているデータベース データの並列バックアップを実行します。 データは各計算ノードから直接、バックアップ ディレクトリにコピーされます。 計算ノードからバックアップ ディレクトリにデータを最も効率的に移動するために、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] では、同時にデータをコピーする計算ノードの数が制御されます。

## <a name="locking"></a>ロック

DATABASE オブジェクトに ExclusiveUpdate ロックを実行します。

## <a name="Security"></a> セキュリティ

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] バックアップはアプライアンスに格納されません。 そのため、IT チームは、バックアップ セキュリティのあらゆる面の管理を担当します。 これには、バックアップ データのセキュリティ、バックアップの保存に使用されるサーバーのセキュリティ、バックアップ サーバーを [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] アプライアンスに接続するネットワーク インフラストラクチャのセキュリティなどの管理が含まれます。

**ネットワーク資格情報の管理**

バックアップ ディレクトリへのネットワーク アクセスは、標準 Windows ファイル共有セキュリティに基づきます。 バックアップを実行する前に、バックアップ ディレクトリに [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] の信頼性を証明するための Windows アカウントを作成または指定する必要があります。 この Windows アカウントには、バックアップ ディレクトリにアクセスし、作成や書き込みを行うための許可を与える必要があります。

> [!IMPORTANT]
> データのセキュリティ リスクを緩和するために、バックアップ操作と復元操作を実行する目的のためだけに Windows アカウントを 1 つ用意することをお勧めします。 そのアカウントのアクセス許可をバックアップの場所に限定します。

[sp_pdw_add_network_credentials - SQL Data Warehouse](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) ストアド プロシージャを実行し、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] にユーザー名とパスワードを保存する必要があります。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] では Windows Credential Manager を利用し、計算ノードにユーザー名とパスワードを保存し、復号します。 資格情報は BACKUP DATABASE コマンドでバックアップされません。

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] からネットワーク資格情報を削除する方法については、「[sp_pdw_remove_network_credentials - SQL Data Warehouse](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)」をご覧ください。

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] に保存されているネットワーク資格情報を一覧表示するには、[sys.dm_pdw_network_credentials](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md) 動的管理ビューを使用してください。

## <a name="examples"></a>使用例

### <a name="a-add-network-credentials-for-the-backup-location"></a>A. バックアップ場所のネットワーク資格情報を追加する

バックアップを作成するには、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] にバックアップ ディレクトリの読み取り/書き込み許可を与える必要があります。 次の例は、ユーザーの資格情報を追加する方法です。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] では、これらの資格情報を格納し、バックアップ操作と復元操作に利用します。

> [!IMPORTANT]
> セキュリティ上の理由から、バックアップ専用のドメイン アカウントを 1 つ作成することをお勧めします。

```sql
EXEC sp_pdw_add_network_credentials 'xxx.xxx.xxx.xxx', 'domain1\backupuser', '*****';
```

### <a name="b-remove-network-credentials-for-the-backup-location"></a>B. バックアップ場所のネットワーク資格情報を削除する

次の例は、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] からドメイン ユーザーの資格情報を削除する方法です。

```sql
EXEC sp_pdw_remove_network_credentials 'xxx.xxx.xxx.xxx';
```

### <a name="c-create-a-full-backup-of-a-user-database"></a>C. ユーザー データベースの完全バックアップを作成する

次の例では、Invoices ユーザー データベースの完全バックアップを作成します。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] は Invoices2013 ディレクトリを作成し、バックアップ ファイルを \\\10.192.63.147\backups\yearly\Invoices2013Full ディレクトリに保存します。

```sql
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';
```

### <a name="d-create-a-differential-backup-of-a-user-database"></a>D. ユーザー データベースの差分バックアップを作成する

次の例では、差分バックアップを作成します。Invoices データベースの前回の完全バックアップ以降に行われたすべての変更が含まれます。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] は \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff ディレクトリを作成し、それにファイルが保存されます。 'Invoices 2013 differential backup' というバックアップの説明がヘッダー情報と共に格納されます。

差分バックアップは、Invoices の前回の完全バックアップが正常に完了した場合にのみ正常に実行されます。

```sql
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'
    WITH DIFFERENTIAL,
    DESCRIPTION = 'Invoices 2013 differential backup';
```

### <a name="e-create-a-full-backup-of-the-master-database"></a>E. master データベースの完全バックアップを作成する

次の例では、master データベースの完全バックアップを作成し、ディレクトリ '\\\10.192.63.147\backups\2013\daily\20130722\master' にそれを格納します。

```sql
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master';
```

### <a name="f-create-a-backup-of-appliance-login-information"></a>F. アプライアンス ログイン情報のバックアップを作成する

master データベースにはアプライアンス ログイン情報が保存されます。 アプライアンス ログイン情報をバックアップするには、master をバックアップする必要があります。

次の例では、master データベースの完全バックアップを作成します。

```sql
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master'
WITH (
    DESCRIPTION = 'Master Backup 20130722',
    NAME = 'login-backup'
)
;
```

## <a name="see-also"></a>参照

[RESTORE DATABASE - Parallel Data Warehous](../../t-sql/statements/restore-statements-transact-sql.md)

::: moniker-end
