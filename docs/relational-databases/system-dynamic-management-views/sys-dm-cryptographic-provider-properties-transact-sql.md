---
title: sys.dm_cryptographic_provider_properties (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_cryptographic_provider_properties_TSQL
- sys.dm_cryptographic_provider_properties
- sys.dm_cryptographic_provider_properties_TSQL
- dm_cryptographic_provider_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cryptographic_provider_properties dynamic management view
ms.assetid: 024b0095-6766-4189-a39a-d316c5ec2874
author: stevestein
ms.author: sstein
ms.openlocfilehash: cc1e0915fb48b42429bb2821476f98154ac39451
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005104"
---
# <a name="sysdmcryptographicproviderproperties-transact-sql"></a>sys.dm_cryptographic_provider_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  登録されている暗号化サービス プロバイダーに関する情報を返します。  
  
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|provider_id|**int**|暗号プロバイダーの id 番号。|  
|guid|**uniqueidentifier**|固有のプロバイダーの GUID です。|  
|provider_version|**nvarchar (256)**|形式でプロバイダーのバージョン '*aa.bb.cccc.dd*' です。|  
|sqlcrypt_version|**nvarchar (256)**|メジャー バージョン、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]形式で Cryptographic API '*aa.bb.cccc.dd*'。|  
|friendly_name|**nvarchar(2048)**|プロバイダーによって提供される名前です。|  
|authentication_type|**nvarchar (256)**|WINDOWS、BASIC、またはその他。|  
|symmetric_key_support|**tinyint**|0 (サポートされていません)<br /><br /> 1 (サポートされています)|  
|symmetric_key_export|**tinyint**|0 (サポートされていません)<br /><br /> 1 (サポートされています)|  
|symmetric_key_import|**tinyint**|0 (サポートされていません)<br /><br /> 1 (サポートされています)|  
|symmetric_key_persistance|**tinyint**|0 (サポートされていません)<br /><br /> 1 (サポートされています)|  
|asymmetric_key_support|**tinyint**|0 (サポートされていません)<br /><br /> 1 (サポートされています)|  
|asymmetric_key_export|**tinyint**|0 (サポートされていません)<br /><br /> 1 (サポートされています)|  
|symmetric_key_import|**tinyint**|0 (サポートされていません)<br /><br /> 1 (サポートされています)|  
|symmetric_key_persistance|**tinyint**|0 (サポートされていません)<br /><br /> 1 (サポートされています)|  
  
## <a name="remarks"></a>コメント  
 sys.dm_cryptographic_provider_properties ビューはパブリックに表示できます。  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [拡張キー管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [セキュリティ関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
