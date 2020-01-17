---
title: RESTORE LABELONLY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- LABELONLY
- RESTORE_LABELONLY_TSQL
- LABELONLY_TSQL
- RESTORE LABELONLY
dev_langs:
- TSQL
helpviewer_keywords:
- RESTORE LABELONLY statement
- backup media [SQL Server], content information
ms.assetid: 7cf0641e-0d55-4ffb-9500-ecd6ede85ae5
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 4d763ccf2799ea72a1882a576e4b17ef839e3f1e
ms.sourcegitcommit: c5e2aa3e4c3f7fd51140727277243cd05e249f78
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/02/2019
ms.locfileid: "68742950"
---
# <a name="restore-statements---labelonly-transact-sql"></a>RESTORE ステートメント - LABELONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md )]
  指定のバックアップ デバイスによって識別されたバックアップ メディアについての情報が含まれている結果セットを返します。  
  
> [!NOTE]  
>  引数の説明については、「[RESTORE の引数 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
RESTORE LABELONLY   
FROM <backup_device>   
[ WITH   
 {  
--Media Set Options  
   MEDIANAME = { media_name | @media_name_variable }   
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
 RESTORE LABELONLY 引数の説明については、「[RESTORE の引数 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)」を参照してください。  
  
## <a name="result-sets"></a>結果セット  
 RESTORE LABELONLY の結果セットは 1 行のデータで構成され、次の情報が含まれています。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**MediaName**|**nvarchar(128)**|メディアの名前|  
|**MediaSetId**|**uniqueidentifier**|メディア セットの一意な識別番号。|  
|**FamilyCount**|**int**|メディア セット内のメディア ファミリの数。|  
|**FamilySequenceNumber**|**int**|メディア ファミリのシーケンス番号|  
|**MediaFamilyId**|**uniqueidentifier**|メディア ファミリの一意な識別番号。|  
|**MediaSequenceNumber**|**int**|メディア ファミリ内にあるこのメディアのシーケンス番号。|  
|**MediaLabelPresent**|**tinyint**|メディアの説明に含まれる内容<br /><br /> **1** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] Tape Format メディア ラベル<br /><br /> **0** = メディアの説明|  
|**MediaDescription**|**nvarchar (255)**|自由形式のテキストによるメディアの説明、または Tape Format メディアラベル。|  
|**SoftwareName**|**nvarchar(128)**|ラベルを作成したバックアップ ソフトウェアの名前。|  
|**SoftwareVendorId**|**int**|バックアップを作成したソフトウェア ベンダーの一意なベンダー識別番号。|  
|**MediaDate**|**datetime**|ラベルが作成された日時。|  
|**Mirror_Count**|**int**|セットにあるミラーの数 (1 ～ 4)<br /><br /> 注: セット内の各種ミラーに対して作成されたラベルは同一のものです。|  
|**IsCompressed**|**bit**|バックアップが圧縮されているかどうか。<br /><br /> 0 = 非圧縮<br /><br /> 1 = 圧縮|  
  
> [!NOTE]  
>  目的のメディア セットにパスワードが定義されているとき、RESTORE LABELONLY からは、MEDIAPASSWORD オプションに正しいメディア パスワードが指定された場合にのみ情報が返されます。  
  
## <a name="general-remarks"></a>全般的な解説  
 RESTORE LABELONLY を実行すると、バックアップ メディアに含まれている内容をすばやく確認できます。 RESTORE LABELONLY ステートメントはメディア ヘッダーだけを読み取っているので、大容量のテープ デバイスを使用しているときでも処理が短時間で終了します。  
  
## <a name="security"></a>Security  
 バックアップ操作では、メディア セットのパスワードを指定することもできます。 メディア セットにパスワードが設定されている場合は、RESTORE ステートメントで正しいパスワードを指定する必要があります。 パスワードを設定しておくと、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ツールを使って不正に復元操作が行われたり、メディアにバックアップ セットが不正に追加されたりするのを防ぐことができます。 ただし、BACKUP ステートメントで FORMAT オプションが使用された場合、パスワードでメディアの上書きを防ぐことはできません。  
  
> [!IMPORTANT]  
>  パスワードによる保護は強力なものではありません。 権限の有無にかかわらず、ユーザーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ツールを使用して不適切な復元を行わないようにすることを目的としています。 その他の手段によるバックアップ データの読み取りやパスワードの置き換えを防ぐわけではありません。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]バックアップ保護に最適な方法は、バックアップ テープを安全な場所に保管するか、バックアップしたディスク ファイルを適切なアクセス制御リスト (ACL) で保護することです。 ACL は、バックアップを作成するディレクトリのルートに設定する必要があります。  
  
### <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンでは、バックアップ セットやバックアップ デバイスに関する情報の取得には CREATE DATABASE 権限が必要になります。 詳細については、「[GRANT (データベースの権限の許可) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [バックアップの履歴とヘッダーの情報 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
