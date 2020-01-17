---
title: RESTORE VERIFYONLY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- VERIFYONLY
- RESTORE VERIFYONLY
- VERIFYONLY_TSQL
- RESTORE_VERIFYONLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RESTORE VERIFYONLY statement
- backups [SQL Server], verifying
- verifying backups
- checking backups
ms.assetid: cba3b6a0-b48e-4c94-812b-5b3cbb408bd6
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 1fec8542ec7575013f8dd101c1e50e3a7b6a13a6
ms.sourcegitcommit: c5e2aa3e4c3f7fd51140727277243cd05e249f78
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/02/2019
ms.locfileid: "68742995"
---
# <a name="restore-statements---verifyonly-transact-sql"></a>RESTORE ステートメント - VERIFYONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md )]

  復元せずにバックアップを確認して、バックアップ セットが完全なものであること、およびバックアップのすべてが読み取り可能であることを確認します。 ただし、RESTORE VERIFYONLY ステートメントが、バックアップ ボリュームに含まれているデータの構造を確認することはありません。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、データに対して追加のチェックを行い、エラーの検出率を高めることができるように RESTORE VERIFYONLY が強化されています。 この機能の目的は、実際の復元操作にできるだけ近い状況を実現することです。 詳細については、「解説」を参照してください。  

 バックアップが有効な場合は、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] は正常に終了したことを知らせるメッセージを返します。  
  
> [!NOTE]  
>  引数の説明については、「[RESTORE の引数 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
RESTORE VERIFYONLY  
FROM <backup_device> [ ,...n ]  
[ WITH    
 {  
   LOADHISTORY   
  
--Restore Operation Option  
 | MOVE 'logical_file_name_in_backup' TO 'operating_system_file_name'   
          [ ,...n ]   
  
--Backup Set Options  
 | FILE = { backup_set_file_number | @backup_set_file_number }   
 | PASSWORD = { password | @password_variable }   
  
--Media Set Options  
 | MEDIANAME = { media_name | @media_name_variable }   
 | MEDIAPASSWORD = { mediapassword | @mediapassword_variable }  
  
--Error Management Options  
 | { CHECKSUM | NO_CHECKSUM }   
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }  
  
--Monitoring Options  
 | STATS [ = percentage ]   
  
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
 RESTORE VERIFYONLY 引数の説明については、「[RESTORE の引数 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)」を参照してください。  
  
## <a name="general-remarks"></a>全般的な解説  
 メディア セットまたはバックアップ セットには、Microsoft Tape Format として解釈できるように最小限の正しい情報が含まれている必要があります。 含まれていない場合は、RESTORE VERIFYONLY が停止し、バックアップの形式が無効であることが示されます。  
  
 RESTORE VERIFYONLY で実行される確認項目には、次のようなものがあります。  
  
-   バックアップ セットが完全で、すべてのボリュームが読み取り可能であること。  
  
-   ページ ID など、データベース ページのヘッダー フィールドの情報 (データ書き込みを想定した確認)。  
  
-   チェックサム (メディアに存在する場合)。  
  
-   バックアップ先デバイスに十分な容量があるかどうか。  
  
> [!NOTE]  
>  RESTORE VERIFYONLY は、データベース スナップショットでは動作しません。 元に戻す操作を行う前にデータベース スナップショットを確認するには、DBCC CHECKDB を実行してください。  
  
> [!NOTE]  
>  スナップショットのバックアップでは、バックアップ ファイルで指定された場所にスナップショットが存在することが RESTORE VERIFYONLY によって確認されます。 スナップショット バックアップは、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] の新機能です。 スナップショット バックアップの詳細については、「[Azure でのデータベース ファイルのスナップショット バックアップ](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)」を参照してください。  
  
## <a name="security"></a>Security  
 バックアップ操作では、オプションで、メディア セットとバックアップ セットにそれぞれパスワードを設定できます。 メディア セットまたはバックアップ セットにパスワードが設定されている場合は、RESTORE ステートメントで正しいパスワードを指定する必要があります。 これらのパスワードを設定しておくと、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ツールを使って不正に復元操作が行われたり、メディアにバックアップ セットが不正に追加されたりするのを防ぐことができます。 ただし、BACKUP ステートメントで FORMAT オプションが使用された場合、パスワードでメディアの上書きを防ぐことはできません。  
  
> [!IMPORTANT]  
>  パスワードによる保護は強力なものではありません。 権限の有無にかかわらず、ユーザーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ツールを使用して不適切な復元を行わないようにすることを目的としています。 その他の手段によるバックアップ データの読み取りやパスワードの置き換えを防ぐわけではありません。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]バックアップ保護に最適な方法は、バックアップ テープを安全な場所に保管するか、バックアップしたディスク ファイルを適切なアクセス制御リスト (ACL) で保護することです。 ACL は、バックアップを作成するディレクトリのルートに設定する必要があります。  
  
### <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンでは、バックアップ セットやバックアップ デバイスに関する情報の取得には CREATE DATABASE 権限が必要になります。 詳細については、「[GRANT (データベースの権限の許可) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)」を参照してください。  
 
## <a name="examples"></a>使用例  
 次の例ではディスクからのバックアップを検証します。
  
```  
RESTORE VERIFYONLY FROM DISK = 'D:\AdventureWorks.bak';
GO
```  
  
## <a name="see-also"></a>参照  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [バックアップの履歴とヘッダーの情報 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
