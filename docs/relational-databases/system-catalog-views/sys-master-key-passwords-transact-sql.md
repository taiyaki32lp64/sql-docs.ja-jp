---
title: sys.master_key_passwords (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.master_key_passwords_TSQL
- master_key_passwords_TSQL
- sys.master_key_passwords
- master_key_passwords
dev_langs:
- TSQL
helpviewer_keywords:
- sys.master_key_passwords catalog view
ms.assetid: b8e18cff-a9e6-4386-98ce-1cd855506e03
author: stevestein
ms.author: sstein
ms.openlocfilehash: 87bb4a97db318330f253d068febb1309e4eda12a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68102402"
---
# <a name="sysmasterkeypasswords-transact-sql"></a>sys.master_key_passwords (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  各データベースのマスター _ キーのパスワードを使用して追加の行を返します、 **sp_control_dbmasterkey_password**ストアド プロシージャ。 マスター _ キーを保護するために使用されるパスワードは、資格情報ストアに格納されます。 資格情報名がこの形式に従います: ##dbmkey_ < database_family_guid > _ < random_password_guid > ## します。 パスワードは、資格情報シークレットとして格納されます。 使用して追加された各パスワード**sp_control_dbmasterkey_password**、内の行がある**sys.credentials**します。  
  
 このビューの各行を示しています、 **credential_id**と**family_guid**のうち、マスター _ キーがその資格情報に関連付けられているパスワードで保護されたデータベース。 参加**sys.credentials**上、 **credential_id**など有用なフィールドを返す、 **create_date**と資格情報の名前。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**credential_id**|**int**|パスワードが属する資格情報の ID。 この ID はサーバー インスタンス内で一意です。|  
|**family_guid**|**uniqueidentifier**|作成時の元のデータベースの一意 ID。 この GUID は、データベースが復元または添付されたり、データベース名が変更されたりしても変わりません。<br /><br /> サービス マスター_キーによる自動暗号化解除が失敗した場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を使用して、 **family_guid**データベース マスター _ キーを保護するために使用するパスワードを含む可能性のある資格情報を識別するためにします。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sp_control_dbmasterkey_password &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
