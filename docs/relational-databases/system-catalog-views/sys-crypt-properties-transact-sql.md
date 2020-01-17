---
title: sys.crypt_properties (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- crypt_properties
- crypt_properties_TSQL
- sys.crypt_properties_TSQL
- sys.crypt_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.crypt_properties catalog view
ms.assetid: d5684f5a-30b1-418e-ae4d-ab040db9257e
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9655866d4fd2d6f98b38532f77f94bc12f16f9b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109482"
---
# <a name="syscrypt_properties-transact-sql"></a>sys.crypt_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  関連付けられたセキュリティ保護可能な暗号化プロパティごとに 1 行を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**class**|**tinyint**|プロパティが存在するリソースのクラスの識別子。<br /><br /> 1 = オブジェクトまたは列<br /> 5 = アセンブリ|  
|**class_desc**|**nvarchar(60)**|プロパティが存在するリソースのクラスの説明です。<br /><br /> OBJECT_OR_COLUMN<br /> ASSEMBLY|  
|**major_id**|**int**|クラスに基づいて解釈されます、プロパティが存在するリソースの ID。|  
|**thumbprint**|**varbinary(32)**|証明書または非対称キーの使用の sha-1 ハッシュ。|  
|**crypt_type**|**char(4)**|暗号化の種類。<br /><br /> SPVC 証明書の秘密キーによって署名を =<br /><br /> SPVA = 非対称秘密キー署名済み<br /><br /> CPVC = 証明書の秘密キーによって副署されます。<br /><br /> CPVA = 非対称キーによって副署されます。|  
|**crypt_type_desc**|**nvarchar(60)**|暗号化の種類の説明です。<br /><br /> SIGNATURE BY CERTIFICATE<br /><br /> SIGNATURE BY ASYMMETRIC KEY<br /><br /> 証明書で副署<br /><br /> 非対称キーによって副署|  
|**crypt_property**|**varbinary(max)**|署名された、または暗号化されたビット。 署名付きモジュールこれらには、モジュールの署名のビットです。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
