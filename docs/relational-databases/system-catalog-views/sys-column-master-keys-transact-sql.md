---
title: column_master_keys (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- column_master_key_definitions_TSQL
- column_master_key_definitions
- sys.column_master_key_definitions_TSQL
- sys.column_master_key_definitions
- column_master_keys_TSQL
- column_master_keys
- sys.column_master_keys_TSQL
- sys.column_master_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_master_key_definitions catalog view
- sys.column_master_keys catalog view
ms.assetid: fbec2efa-5fe9-4121-9b34-60497b0b2aca
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b7c219b2eb56fc299857a5a189ddd9db041f2f47
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594522"
---
# <a name="syscolumn_master_keys-transact-sql"></a>sys.column_master_keys (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [CREATE MASTER key](../../t-sql/statements/create-column-master-key-transact-sql.md)ステートメントを使用して追加されたデータベースマスターキーごとに1行のデータを返します。 各行は1つの列マスターキー (CMK) を表します。  
    
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|CMK の名前。|  
|**column_master_key_id**|**int**|列マスターキーの ID。|  
|**create_date**|**datetime**|列マスターキーが作成された日付。|  
|**modify_date**|**datetime**|列マスターキーが最後に変更された日付。|  
|**key_store_provider_name**|**sysname**|CMK を含む列マスターキーストアのプロバイダーの名前。 使用できる値は、以下のとおりです。<br /><br /> MSSQL_CERTIFICATE_STORE-列マスターキーストアが証明書ストアである場合。<br /><br /> 列マスターキーストアがカスタム型である場合は、ユーザー定義の値。|  
|**key_path**|**nvarchar (4000)**|キーの列マスターキーストア固有のパス。 パスの形式は、列のマスターキーストアの種類によって異なります。 例:<br /><br /> `'CurrentUser/Personal/'<thumbprint>`<br /><br /> カスタム列マスターキーストアの場合、開発者は、カスタム列マスターキーストアのキーパスを定義する必要があります。|  
|**allow_enclave_computations**|**bit**|列マスターキーがエンクレーブに設定されているかどうかを示します (このマスターキーで暗号化された列暗号化キーは、サーバー側の secure enclaves 内の計算に使用できます)。 詳細については、「[セキュア エンクレーブを使用する Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)」を参照してください。|  
|**signature**|**varbinary(max)**|**Key_path**によって参照される列マスターキーを使用して生成された**key_path**および**allow_enclave_computations**のデジタル署名。|


  
## <a name="permissions"></a>アクセス許可  
 **VIEW ANY COLUMN MASTER KEY**権限が必要です。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Always Encrypted のキー管理の概要](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
 [セキュリティで保護されたエンクレーブが設定された Always Encrypted のキーを管理する](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)   
 
  
  
