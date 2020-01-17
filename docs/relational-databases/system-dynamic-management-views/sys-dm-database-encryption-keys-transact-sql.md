---
title: sys.dm_database_encryption_keys (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_database_encryption_keys
- sys.dm_database_encryption_keys_TSQL
- dm_database_encryption_keys
- dm_database_encryption_keys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_database_encryption_keys dynamic management view
ms.assetid: 56fee8f3-06eb-4fff-969e-abeaa0c4b8e4
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2c66fbc1cdf98d45a7440d2def9cb3fd1be5635a
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68255754"
---
# <a name="sysdmdatabaseencryptionkeys-transact-sql"></a>sys.dm_database_encryption_keys (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  暗号化キー、データベースとその関連付けられているデータベースの暗号化の状態に関する情報を返します。 データベース暗号化の詳細については、「[Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)」を参照してください。  
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|database_id|**int**|データベースの ID です。|  
|encryption_state|**int**|データベースが暗号化および暗号化されていないかどうかを示します。<br /><br /> 0 = データベース暗号化キーが存在する、暗号化なし<br /><br /> 1 = Unencrypted<br /><br /> 2 = 暗号化中<br /><br /> 3 = 暗号化<br /><br /> 4 = キーの変更中<br /><br /> 5 = 暗号化解除中<br /><br /> 6 = 保護の変更中 (証明書または非対称キーは、データベース暗号化キーの暗号化に変更されています)。|  
|create_date|**datetime**|日付を表示します (UTC) で暗号化キーが作成されました。|  
|regenerate_date|**datetime**|日付を表示します (UTC) で暗号化キーが再生成されました。|  
|modify_date|**datetime**|日付を表示します (UTC) で暗号化キーが変更されました。|  
|set_date|**datetime**|日付を表示します (UTC) で暗号化キーがデータベースに適用されました。|  
|opened_date|**datetime**|データベース キーが最後 (UTC) で開かれたときに表示されます。|  
|key_algorithm|**nvarchar(32)**|キーに使用されるアルゴリズムを表示します。|  
|key_length|**int**|キーの長さを表示します。|  
|encryptor_thumbprint|**varbinary(20)**|暗号化のサムプリントを表示します。|  
|encryptor_type|**nvarchar(32)**|**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] から [現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)。<br /><br /> 暗号化機能をについて説明します。|  
|percent_complete|**real**|データベース暗号化の状態変更の完了率。 状態の変更がない場合は、0 になります。|
|encryption_state_desc|**nvarchar(32)**|**適用対象**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降。<br><br> データベースが暗号化および暗号化されていないかどうかを示す文字列。<br><br>なし<br><br>暗号化されていません。<br><br>暗号化<br><br>DECRYPTION_IN_PROGRESS<br><br>ENCRYPTION_IN_PROGRESS<br><br>KEY_CHANGE_IN_PROGRESS<br><br>PROTECTION_CHANGE_IN_PROGRESS|
|encryption_scan_state|**int**|**適用対象**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降。<br><br>暗号化のスキャンの現在の状態を示します。 <br><br>0 = いいえスキャンが開始されて、TDE が有効になっていません<br><br>1 = スキャンが進行中です。<br><br>2 = スキャンが進行中ですが、中断されている、ユーザーが再開できます。<br><br>3 = スキャンが正常に完了した、TDE が有効になっているし、暗号化が完了します。<br><br>4 = 何らかの理由のスキャンが中止されました、手動による介入が必要です。 詳細については、Microsoft サポートにお問い合わせください。|
|encryption_scan_state_desc|**nvarchar(32)**|**適用対象**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降。<br><br>暗号化のスキャンの現在の状態を示す文字列。<br><br> なし<br><br>RUNNING<br><br>SUSPENDED<br><br>完了<br><br>ABORTED|
|encryption_scan_modify_date|**datetime**|**適用対象**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降。<br><br> 日付を表示します (UTC) で暗号化のスキャン状態が最後に変更します。|
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   

## <a name="see-also"></a>関連項目  

 [セキュリティ関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)   
 [透過的なデータ暗号化 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)   
 [SQL Server の暗号化](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [SQL Server とデータベースの暗号化キー &#40;データベース エンジン&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [ALTER DATABASE SET オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
  
  
