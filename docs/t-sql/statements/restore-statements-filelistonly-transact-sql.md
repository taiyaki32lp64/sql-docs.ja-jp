---
title: RESTORE FILELISTONLY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RESTORE FILELISTONLY
- RESTORE_FILELISTONLY_TSQL
- FILELISTONLY
- FILELISTONLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backups [SQL Server], file lists
- RESTORE FILELISTONLY statement
- listing backed up files
ms.assetid: 0b4b4d11-eb9d-4f3e-9629-6c79cec7a81a
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 892b18ac9780054cafe90d62569afb63f8261b3e
ms.sourcegitcommit: c5e2aa3e4c3f7fd51140727277243cd05e249f78
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/02/2019
ms.locfileid: "68742979"
---
# <a name="restore-statements---filelistonly-transact-sql"></a>RESTORE ステートメント - FILELISTONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md )]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバックアップ セットに保存されているデータベースとログ ファイルのリストを含んだ結果セットを返します。  

> [!NOTE]  
>  引数の説明については、「[RESTORE の引数 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
RESTORE FILELISTONLY   
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
 RESTORE FILELISTONLY 引数の説明については、「[RESTORE の引数 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)」を参照してください。  
  
## <a name="result-sets"></a>結果セット  
 クライアントでは、RESTORE FILELISTONLY を使用して、バックアップ セットに含まれるファイルの一覧を取得できます。 この情報は、ファイル 1 件あたり 1 行のデータで構成される結果セットとして返されます。  
  
|列名|データ型|[説明]|  
|-|-|-|  
|LogicalName|**nvarchar(128)**|ファイルの論理名です。|  
|PhysicalName|**nvarchar(260)**|ファイルの物理名またはオペレーティング システム名です。|  
|型|**char(1)**|ファイルの種類。次のいずれかになります。<br /><br /> **L** = Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログ ファイル<br /><br /> **D** = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ ファイル<br /><br /> **F** = フルテキスト カタログ<br /><br /> **S** = FileStream、FileTable、または [!INCLUDE[hek_2](../../includes/hek-2-md.md)] コンテナー|  
|FileGroupName|**nvarchar(128)** NULL|このファイルを含むファイル グループの名前。|  
|サイズ|**numeric(20,0)**|現在のサイズ (バイト単位)。|  
|MaxSize|**numeric(20,0)**|最大許容サイズ (バイト単位)。|  
|FileID|**bigint**|データベース内で一意なファイル識別子。|  
|CreateLSN|**numeric(25,0)**|ファイルが作成されたときのログ シーケンス番号。|  
|DropLSN|**numeric(25,0)** NULL|ファイルが削除されたときのログ シーケンス番号。 ファイルが削除されていない場合、この値は NULL です。|  
|UniqueID|**uniqueidentifier**|ファイルのグローバル一意識別子。|  
|ReadOnlyLSN|**numeric(25,0) NULL**|このファイルを含むファイル グループが、前回読み書き可能から読み取り専用に変更されたときのログ シーケンス番号。|  
|ReadWriteLSN|**numeric(25,0)** NULL|このファイルを含むファイル グループが、前回読み取り専用から読み書き可能に変更されたときのログ シーケンス番号。|  
|BackupSizeInBytes|**bigint**|このファイルのバックアップ サイズ (バイト単位)。|  
|SourceBlockSize|**int**|ファイルが格納されている物理デバイス (バックアップ デバイス以外) のバイト単位のブロック サイズ。|  
|FileGroupID|**int**|ファイル グループの ID。|  
|LogGroupGUID|**uniqueidentifier** NULL|NULL。|  
|DifferentialBaseLSN|**numeric(25,0)** NULL|差分バックアップの場合、**DifferentialBaseLSN** 以上のログ シーケンス番号を持つ変更が差分に含まれます。<br /><br /> その他の種類のバックアップの場合、この値は NULL です。|  
|DifferentialBaseGUID|**uniqueidentifier** NULL|差分ベースの一意識別子 (差分バックアップの場合)。<br /><br /> その他の種類のバックアップの場合、この値は NULL です。|  
|IsReadOnly|**bit**|**1** = ファイルは読み取り専用。|  
|IsPresent|**bit**|**1** = ファイルはバックアップ済み。|  
|TDEThumbprint|**varbinary(32)** NULL|データベース暗号化キーの拇印を表示します。 暗号化の拇印とは、キーの暗号化で使用された証明書の SHA-1 ハッシュです。 データベース暗号化の詳細については、「[Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)」を参照してください。|  
|SnapshotURL|**nvarchar(360)** NULL|FILE_SNAPSHOT バックアップに含まれているデータベース ファイルの Azure のスナップショットの URL。 FILE_SNAPSHOT バックアップがない場合は、NULL を返します。|  
  
## <a name="security"></a>Security  
 バックアップ操作では、オプションで、メディア セットとバックアップ セットにそれぞれパスワードを設定できます。 メディア セットまたはバックアップ セットにパスワードが設定されている場合は、RESTORE ステートメントで正しいパスワードを指定する必要があります。 これらのパスワードを設定しておくと、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ツールを使用して不正に復元操作が行われたり、メディアにバックアップ セットが不正に追加されたりするのを防ぐことができます。 ただし、BACKUP ステートメントで FORMAT オプションが使用された場合、パスワードでメディアの上書きを防ぐことはできません。  
  
> [!IMPORTANT]  
>  パスワードによる保護は強力なものではありません。 権限の有無にかかわらず、ユーザーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ツールを使用して不適切な復元を行わないようにすることを目的としています。 その他の手段によるバックアップ データの読み取りやパスワードの置き換えを防ぐわけではありません。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] バックアップ保護に最適な方法は、バックアップ テープを安全な場所に保管するか、バックアップしたディスク ファイルを適切なアクセス制御リスト (ACL) で保護することです。 ACL は、バックアップを作成するディレクトリのルートに設定する必要があります。  
  
### <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンでは、バックアップ セットやバックアップ デバイスに関する情報の取得には CREATE DATABASE 権限が必要になります。 詳細については、「[GRANT (データベースの権限の許可) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
 次の例は、`AdventureWorksBackups` というバックアップ デバイスから情報を返します。 この例では `FILE` オプションを使用して、デバイスで 2 番目のバックアップ セットを指定しています。  
  
```  
RESTORE FILELISTONLY FROM AdventureWorksBackups   
   WITH FILE=2;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [バックアップの履歴とヘッダーの情報 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
