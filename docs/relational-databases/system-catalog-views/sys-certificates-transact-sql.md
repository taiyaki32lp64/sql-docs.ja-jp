---
title: sys. 証明書 (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- certificates
- certificates_TSQL
- sys.certificates_TSQL
- sys.certificates
dev_langs:
- TSQL
helpviewer_keywords:
- sys.certificates catalog view
ms.assetid: e5046102-a65c-401e-b80d-05636884dec9
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 08193bd8f9b6dfd3aace80315c75bbb88e076f3a
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75255841"
---
# <a name="syscertificates-transact-sql"></a>sys. 証明書 (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  データベース内の証明書ごとに1行のデータを返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**指定**|**sysname**|証明書の名前。 データベース内で一意です。|  
|**certificate_id**|**通り**|証明書の ID。 データベース内で一意です。|  
|**principal_id**|**通り**|この証明書を所有するデータベースプリンシパルの ID。|  
|**pvt_key_encryption_type**|**char (2)**|秘密キーの暗号化方法。<br /><br /> NA = 証明書に秘密キーはありません。<br /><br /> MK = 秘密キーはマスターキーによって暗号化されています<br /><br /> PW = 秘密キーは、ユーザー定義のパスワードによって暗号化されます。<br /><br /> SK = 秘密キーは、サービスマスターキーによって暗号化されます。|  
|**pvt_key_encryption_type_desc**|**nvarchar (60)**|秘密キーの暗号化方法の説明。<br /><br /> NO_PRIVATE_KEY<br /><br /> ENCRYPTED_BY_MASTER_KEY<br /><br /> ENCRYPTED_BY_PASSWORD<br /><br /> ENCRYPTED_BY_SERVICE_MASTER_KEY|  
|**is_active_for_begin_dialog**|**bit**|1の場合、この証明書は暗号化されたサービスダイアログを開始するために使用されます。|  
|**issuer_name**|**nvarchar (442)**|証明書の発行者の名前。|  
|**cert_serial_number**|**nvarchar (64)**|証明書のシリアル番号。|  
|**sid**|**varbinary (85)**|この証明書のログイン SID。|  
|**string_sid**|**nvarchar(128)**|この証明書のログイン SID の文字列表現|  
|**subject**|**nvarchar(4000)**|証明書のサブジェクト。|  
|**expiry_date**|**/**|証明書の有効期限が切れた場合。|  
|**start_date**|**/**|証明書が有効になったとき。|  
|**拇印**|**varbinary (32)**|証明書の SHA-1 ハッシュ。 SHA-1 ハッシュはグローバルに一意です。|  
|**attested_by**|**nvarchar (260)**|システムでのみ使用されます。|  
|**pvt_key_last_backup_date**|**/**|証明書の秘密キーが最後にエクスポートされた日付と時刻。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]詳細については、「[メタデータ表示の構成](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [セキュリティカタログビュー &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;カタログビュー](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Transact-sql&#41;&#40;証明書の作成](../../t-sql/statements/create-certificate-transact-sql.md)  
  
  
