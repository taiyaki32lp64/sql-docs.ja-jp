---
title: sys.asymmetric_keys (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- asymmetric_keys
- sys.asymmetric_keys_TSQL
- asymmetric_keys_TSQL
- sys.asymmetric_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.asymmetric_keys catalog view
ms.assetid: bbca796a-9bb5-4a62-9ca8-1d255984553d
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c05aa2d1543cfc3ebd1cbab6c199cd2992febfe2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070473"
---
# <a name="sysasymmetric_keys-transact-sql"></a>sys.asymmetric_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  非対称キーごとに行を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|キーの名前。 データベース内で一意です。|  
|**principal_id**|**int**|キーを所有するデータベース プリンシパルの ID。|  
|**asymmetric_key_id**|**int**|キーの ID。 データベース内で一意です。|  
|**pvt_key_encryption_type**|**char(2)**|キーの暗号化方法。<br /><br /> NA = 暗号化されていません。<br /><br /> MK = キーはマスター キーにより暗号化されています。<br /><br /> PW = キーはユーザー定義パスワードにより暗号化<br /><br /> SK = キーはサービス マスター キーにより暗号化されています。|  
|**pvt_key_encryption_type_desc**|**nvarchar(60)**|秘密キーを暗号化する方法の説明です。<br /><br /> NO_PRIVATE_KEY<br /><br /> ENCRYPTED_BY_MASTER_KEY<br /><br /> ENCRYPTED_BY_PASSWORD<br /><br /> ENCRYPTED_BY_SERVICE_MASTER_KEY|  
|**thumbprint**|**varbinary(32)**|キーの sha-1 ハッシュ。 ハッシュはグローバルに一意です。|  
|**algorithm**|**char(2)**|キーと一緒に使用されるアルゴリズム。<br /><br /> 1R = 512 ビット RSA<br /><br /> 2R = 1024 ビット RSA<br /><br /> 3R = 2048 ビット RSA|  
|**algorithm_desc**|**nvarchar(60)**|キーで使用されるアルゴリズムの説明です。<br /><br /> RSA_512<br /><br /> RSA_1024<br /><br /> RSA_2048|  
|**key_length**|**int**|キーのビット長。|  
|**sid**|**varbinary(85)**|このキーに対するログイン SID。 拡張キー管理キーには、この値を NULL となります。|  
|**string_sid**|**nvarchar(128)**|キーのログイン SID の文字列形式。 拡張キー管理キーには、この値を NULL となります。|  
|**public_key**|**varbinary(max)**|公開キー。|  
|**attested_by**|**nvarchar(260)**|システムでのみ使用します。|  
|**provider_type**|**nvarchar(120)**|暗号化サービス プロバイダーの種類:<br /><br /> CRYPTOGRAPHIC PROVIDER = 拡張キー管理キー<br /><br /> NULL = 非拡張キー管理キー|  
|**cryptographic_provider_guid**|**uniqueidentifier**|暗号化サービス プロバイダーの GUID です。 非拡張キー管理キーは、この値を NULL となります。|  
|**cryptographic_provider_algid**|**sql_variant**|暗号化サービス プロバイダーのアルゴリズム ID。 非拡張キー管理キーは、この値を NULL となります。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [拡張キー管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
  
  
