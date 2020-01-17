---
title: RESTORE HEADERONLY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- HEADERONLY
- RESTORE HEADERONLY
- RESTORE_HEADERONLY_TSQL
- HEADERONLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup sets [SQL Server], header information
- headers [SQL Server]
- RESTORE HEADERONLY statement
- backup header information [SQL Server]
ms.assetid: 4b88e98c-49c4-4388-ab0e-476cc956977c
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 4ff8da4a1076d8ade4d54e5d44c51d3263480c1c
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983030"
---
# <a name="restore-statements---headeronly-transact-sql"></a>RESTORE Statements - HEADERONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md )]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で特定のバックアップ デバイス上にあるすべてのバックアップ セットについて、すべてのバックアップ ヘッダー情報を含む結果セットを返します。 
 
> [!NOTE]  
>  引数の説明については、「[RESTORE の引数 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
RESTORE HEADERONLY   
FROM <backup_device>   
[ WITH   
 {  
--Backup Set Options  
   FILE = { backup_set_file_number | @backup_set_file_number }   
 | PASSWORD = { password | @password_variable }   
  
--Media Set Options  
 | MEDIANAME = { media_name | @media_name_variable }   
 | MEDIAPASSWORD = { mediapassword | @mediapassword_variable }  
  
--Error Management Options  
 | { CHECKSUM | NO_CHECKSUM }   
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }  
  
--Tape Options  
 | { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }    
 } [ ,...n ]  
]  
[;]  
  
<backup_device> ::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
   | { DISK | TAPE | URL } = { 'physical_backup_device_name' |  
       @physical_backup_device_name_var }   
}  
  
```  
> [!NOTE] 
> URL は、Microsoft Azure Blob Storage の場所とファイル名を指定するために使用される形式であり、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 以降でサポートされています。 Microsoft Azure ストレージはサービスですが、実装はディスクやテープと似ており、3 つのデバイスすべてで一貫したシームレスな復元エクスペリエンスを実現できます。

## <a name="arguments"></a>引数  
 RESTORE HEADERONLY の引数の説明については、「[RESTORE の引数 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)」を参照してください。  
  
## <a name="result-sets"></a>結果セット  
 指定されたデバイス上にあるバックアップごとに、サーバーからヘッダー情報の行が送信されます。下に説明する列が含まれています。  
  
> [!NOTE]
>  RESTORE HEADERONLY では、メディア上のすべてのバックアップ セットが確認されます。 そのため、大容量のテープ ドライブを使用している場合は結果セットの生成に時間がかかることがあります。 バックアップ セットごとの情報を取得せずにメディアの内容をすばやく確認するには、RESTORE LABELONLY を使用するか、FILE **=** _backup_set_file_number_ を指定します。  
> 
> [!NOTE]
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Tape Format の特性により、他のソフトウェア プログラムから作成されたバックアップ セットと [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバックアップ セットが同じメディア上に記録されている場合があります。 RESTORE HEADERONLY によって返される結果セットには、その他のバックアップ セットの情報も 1 件につき 1 行ずつ含まれます。  
  
|列名|データ型|SQL Server バックアップ セットの場合の説明|  
|-----------------|---------------|--------------------------------------------|  
|**BackupName**|**nvarchar(128)**|バックアップ セット名。|  
|**BackupDescription**|**nvarchar (255)**|バックアップ セットの説明。|  
|**BackupType**|**smallint**|バックアップの種類:<br /><br /> **1** = データベース<br /><br /> **2** = トランザクション ログ<br /><br /> **4** = ファイル<br /><br /> **5** = データベースの差分<br /><br /> **6** = ファイルの差分<br /><br /> **7** = 部分的<br /><br /> **8** = 部分的な差分|  
|**ExpirationDate**|**datetime**|バックアップ セットの失効日。|  
|**Compressed**|**BYTE(1)**|ソフトウェア ベースの圧縮によりバックアップ セットが圧縮されているかどうか:<br /><br /> **0** = いいえ<br /><br /> **1** = はい|  
|**Position**|**smallint**|ボリューム内でのバックアップ セットの位置 (FILE = のオプションで使用)。|  
|**DeviceType**|**tinyint**|バックアップ操作で使用するデバイスに対応する値。<br /><br /> ディスク:<br /><br /> **2** = 論理<br /><br /> **102** = 物理<br /><br /> テープ:<br /><br /> **5** = 論理<br /><br /> **105** = 物理<br /><br /> 仮想デバイス:<br /><br /> **7** = 論理<br /><br /> **107** = 物理<br /><br /> 論理デバイス名とデバイス番号は **sys.backup_devices** です。詳細については、「[sys.backup_devices &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)」を参照してください。|  
|**UserName**|**nvarchar(128)**|バックアップ操作を実行したユーザーの名前。|  
|**ServerName**|**nvarchar(128)**|バックアップ セットを作成したサーバーの名前。|  
|**DatabaseName**|**nvarchar(128)**|バックアップの作成元であるデータベースの名前。|  
|**DatabaseVersion**|**int**|バックアップの作成元であるデータベースのバージョン。|  
|**DatabaseCreationDate**|**datetime**|データベースが作成された日時。|  
|**BackupSize**|**numeric(20,0)**|バックアップのサイズ (バイト単位)。|  
|**FirstLSN**|**numeric(25,0)**|バックアップ セット内にある先頭のログ レコードのログ シーケンス番号。|  
|**LastLSN**|**numeric(25,0)**|バックアップ セットの次のログ レコードのログ シーケンス番号。|  
|**CheckpointLSN**|**numeric(25,0)**|バックアップが作成された時点における最新チェックポイントのログ シーケンス番号。|  
|**DatabaseBackupLSN**|**numeric(25,0)**|データベース全体の最新バックアップのログ シーケンス番号。<br /><br /> **DatabaseBackupLSN** は、バックアップの開始時にトリガーされる "チェックポイントの先頭" です。 データベースがアイドル状態で、レプリケーションが構成されていないときにバックアップが実行された場合、この LSN は **FirstLSN** と同じになります。|  
|**BackupStartDate**|**datetime**|バックアップ操作が開始した日時。|  
|**BackupFinishDate**|**datetime**|バックアップ操作が終了した日時。|  
|**SortOrder**|**smallint**|サーバーの並べ替え順。 この列はデータベース バックアップのみで有効です。 これは旧バージョンとの互換性のために用意されています。|  
|**CodePage**|**smallint**|サーバーが使用するサーバー コード ページまたは文字セット。|  
|**UnicodeLocaleId**|**int**|Unicode 文字データの並べ替えに使用する、サーバー Unicode ロケール ID 構成オプション。 これは旧バージョンとの互換性のために用意されています。|  
|**UnicodeComparisonStyle**|**int**|Unicode データの並べ替えに詳細な設定を追加できる、サーバー Unicode 比較スタイル構成オプション。 これは旧バージョンとの互換性のために用意されています。|  
|**CompatibilityLevel**|**tinyint**|バックアップの作成元であるデータベースの互換性レベル設定。|  
|**SoftwareVendorId**|**int**|ソフトウェア ベンダーの識別番号。 SQL Server の場合、この値は **4608** (16 進数では **0x1200**) です。|  
|**SoftwareVersionMajor**|**int**|バックアップ セットを作成したサーバーのメジャー バージョン番号。|  
|**SoftwareVersionMinor**|**int**|バックアップ セットを作成したサーバーのマイナー バージョン番号。|  
|**SoftwareVersionBuild**|**int**|バックアップ セットを作成したサーバーのビルド番号。|  
|**MachineName**|**nvarchar(128)**|バックアップ操作を実行したコンピューターの名前。|  
|**Flags**|**int**|**1** に設定されている場合の個々のフラグ ビットの意味は次のとおりです。<br /><br /> **1** = ログ バックアップに一括ログ操作が含まれている。<br /><br /> **2** = スナップショット バックアップ。<br /><br /> **4** = データベースがバックアップ時に読み取り専用だった。<br /><br /> **8** = データベースがバックアップ時にシングル ユーザー モードだった。<br /><br /> **16** = バックアップにバックアップ チェックサムが含まれている。<br /><br /> **32** = データベースがバックアップ時に損傷したが、エラーに関係なくバックアップ操作の続行が要求された。<br /><br /> **64** = ログ末尾のバックアップ。<br /><br /> **128** = 不完全なメタデータでのログ末尾のバックアップ。<br /><br /> **256** = NORECOVERY でのログ末尾のバックアップ。<br /><br /> **重要:** **Flags** ではなく、下に示す **HasBulkLoggedData** から **IsCopyOnly** までのブール値をとる各列の使用をお勧めします。|  
|**BindingID**|**uniqueidentifier**|データベースに割り当てられたバインド ID。 これは、**sys.database_recovery_status database_guid** に対応します。 データベースが復元されると、新しい値が割り当てられます。 **FamilyGUID** (下記) も参照してください。|  
|**RecoveryForkID**|**uniqueidentifier**|最後の復旧分岐の ID。 この列は、[backupset](../../relational-databases/system-tables/backupset-transact-sql.md) テーブル内の **last_recovery_fork_guid** に対応します。<br /><br /> データのバックアップでは、**RecoveryForkID** は **FirstRecoveryForkID** と同じです。|  
|**Collation**|**nvarchar(128)**|データベースで使用されている照合順序。|  
|**FamilyGUID**|**uniqueidentifier**|元のデータベースに関する作成時の ID。 この値は、データベースが復元されても変わりません。|  
|**HasBulkLoggedData**|**bit**|**1** = 一括ログ記録操作を含むログ バッグアップ。|  
|**IsSnapshot**|**bit**|**1** = スナップショット バックアップ。|  
|**IsReadOnly**|**bit**|**1** = データベースがバックアップ時に読み取り専用だった。|  
|**IsSingleUser**|**bit**|**1** = データベースがバックアップ時にシングル ユーザーだった。|  
|**HasBackupChecksums**|**bit**|**1** = バックアップ チェックサムを含むバックアップ。|  
|**IsDamaged**|**bit**|**1** = データベースがバックアップ時に損傷したが、エラーに関係なくバックアップ操作の続行が要求された。|  
|**BeginsLogChain**|**bit**|**1** =1 連鎖的なログ バックアップの先頭。 データベースが作成された後、または単純復旧モデルが完全復旧モデルや一括ログ復旧モデルに切り替わったときに、最初に行われるログ バックアップを先頭にして、ログ チェーンが形成されます。|  
|**HasIncompleteMetaData**|**bit**|**1** = 不完全なメタデータでのログ末尾のバックアップ。<br /><br /> 不完全なバックアップ メタデータでのログ末尾のバックアップについては、「[ログ末尾のバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)」を参照してください。|  
|**IsForceOffline**|**bit**|**1** = NORECOVERY で行われたバックアップ。データベースがバックアップによってオフラインになった。|  
|**IsCopyOnly**|**bit**|**1** = コピーのみのバックアップ。<br /><br /> コピーのみのバックアップを行っても、データベースの全体的なバックアップと復元の手順に影響はありません。 詳細については、「[コピーのみのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)」を参照してください。|  
|**FirstRecoveryForkID**|**uniqueidentifier**|最初の復旧分岐の ID。 この列は、[backupset](../../relational-databases/system-tables/backupset-transact-sql.md) テーブルの **first_recovery_fork_guid** に対応します。<br /><br /> データのバックアップでは、**FirstRecoveryForkID** は **RecoveryForkID** と同じです。|  
|**ForkPointLSN**|**numeric(25,0)** NULL|**FirstRecoveryForkID** が **RecoveryForkID** と同じでない場合、これは分岐ポイントのログ シーケンス番号になります。 これらが同じである場合、この値は NULL になります。|  
|**RecoveryModel**|**nvarchar(60)**|データベースの復旧モデル。次のいずれかになります。<br /><br /> FULL<br /><br /> BULK-LOGGED<br /><br /> SIMPLE|  
|**DifferentialBaseLSN**|**numeric(25,0)** NULL|シングル ベースの差分バックアップの場合、値は差分ベースの **FirstLSN** と同じになります。**DifferentialBaseLSN** 以上の LSN の変更は差分に含まれます。<br /><br /> マルチ ベースの差分バックアップの場合、この値は NULL です。ベース LSN はファイル レベルで決定される必要があります。 詳細については、[RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md) を参照してください。<br /><br /> 差分バックアップ以外の種類のバックアップの場合は常に NULL。<br /><br /> 詳細については、「 [差分バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)」を参照してください。|  
|**DifferentialBaseGUID**|**uniqueidentifier**|シングル ベースの差分バックアップの場合は、差分ベースの一意識別子。<br /><br /> マルチ ベースの差分バックアップの場合は、NULL。差分のベースはファイルごとに決定する必要があります。<br /><br /> 差分バックアップ以外の種類の場合、値は NULL です。|  
|**BackupTypeDescription**|**nvarchar(60)**|バックアップの種類を表す文字列。次のいずれかになります。<br /><br /> DATABASE<br /><br /> TRANSACTION LOG<br /><br /> FILE OR FILEGROUP<br /><br /> DATABASE DIFFERENTIAL<br /><br /> FILE DIFFERENTIAL PARTIAL<br /><br /> PARTIAL DIFFERENTIAL|  
|**BackupSetGUID**|**uniqueidentifier** NULL|メディア上のバックアップ セットを識別する、バックアップ セットの一意識別番号。|  
|**CompressedBackupSize**|**bigint**|バックアップ セットのバイト数。 圧縮されていないバックアップの場合、この値は **BackupSize** と同じです。<br /><br /> 圧縮比率を計算するには、**CompressedBackupSize** と **BackupSize** を使用します。<br /><br /> この値は、**msdb** のアップグレード中に、**BackupSize** 列の値と一致するように設定されます。|  
|**containment**|**tinyint** not NULL|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> データベースの包含状態を示します。<br /><br /> 0 = データベースの包含がオフ<br /><br /> 1 = データベースは部分的な包含|  
|**KeyAlgorithm**|**nvarchar(32)**|**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (CU1) から現在のバージョンまで)。<br /><br /> バックアップの暗号化に使用される暗号化アルゴリズム。 NO_Encryption では、バックアップが暗号化されていないことを示します。 システムに正しい値を特定できない場合、値は NULL になります。|  
|**EncryptorThumbprint**|**varbinary(20)**|**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (CU1) から現在のバージョンまで)。<br /><br /> データベースに保存されている証明書や非対称キーを検索するために使用される暗号化機能の拇印。 バックアップが暗号化されていない場合、この値は NULL となります。|  
|**EncryptorType**|**nvarchar(32)**|**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (CU1) から現在のバージョンまで)。<br /><br /> 使用される暗号化の種類:証明書キーまたは非対称キー。 バックアップが暗号化されていない場合、この値は NULL となります。|  
  
> [!NOTE]  
>  バックアップ セットにパスワードが定義されている場合、RESTORE HEADERONLY によって完全な情報が返されるのは、コマンドの PASSWORD オプションと同じパスワードが指定されているバックアップ セットに対してのみです。 また保護されていないバックアップ セットについても、RESTORE HEADERONLY では完全な情報が返されます。 メディア上にある、他のパスワードで保護されているバックアップ セットについては、**BackupName** 列が ' **_Password Protected_** ' に設定され、他の列は NULL になります。  
  
## <a name="general-remarks"></a>全般的な解説  
 クライアントは RESTORE HEADERONLY を使用して、特定のバックアップ デバイス上のすべてのバックアップについて、バックアップ ヘッダーに関するすべての情報を取得できます。 バックアップ デバイス上にあるバックアップごとに、ヘッダー情報が 1 行のデータとしてサーバーから送信されます。  
  
## <a name="security"></a>Security  
 バックアップ操作では、オプションで、メディア セットとバックアップ セットにそれぞれパスワードを設定できます。 メディア セットまたはバックアップ セットにパスワードが設定されている場合は、RESTORE ステートメントで正しいパスワードを指定する必要があります。 これらのパスワードを設定しておくと、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ツールを使用して不正に復元操作が行われたり、メディアにバックアップ セットが不正に追加されたりするのを防ぐことができます。 ただし、BACKUP ステートメントで FORMAT オプションが使用された場合、パスワードでメディアの上書きを防ぐことはできません。  
  
> [!IMPORTANT]  
>  パスワードによる保護は強力なものではありません。 権限の有無にかかわらず、ユーザーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ツールを使用して不適切な復元を行わないようにすることを目的としています。 その他の手段によるバックアップ データの読み取りやパスワードの置き換えを防ぐわけではありません。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]バックアップ保護に最適な方法は、バックアップ テープを安全な場所に保管するか、バックアップしたディスク ファイルを適切なアクセス制御リスト (ACL) で保護することです。 ACL は、バックアップを作成するディレクトリのルートに設定する必要があります。  
  
### <a name="permissions"></a>アクセス許可  
 バックアップ セットやバックアップ デバイスに関する情報の取得には CREATE DATABASE 権限が必要になります。 詳細については、「[GRANT (データベースの権限の許可) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
 次の例では、ディスク ファイル `C:\AdventureWorks-FullBackup.bak` のヘッダー情報を返します。  
  
```  
RESTORE HEADERONLY   
FROM DISK = N'C:\AdventureWorks-FullBackup.bak'   
WITH NOUNLOAD;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [バックアップの履歴とヘッダーの情報 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)   
 [バックアップ中または復元中にバックアップ チェックサムを有効または無効にする &#40;SQL Server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)   
 [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [復旧モデル &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
  
