---
title: sys.dm_cryptographic_provider_algorithms (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_cryptographic_provider_algorithms_TSQL
- sys.dm_cryptographic_provider_algorithms
- sys.dm_cryptographic_provider_algorithms_TSQL
- dm_cryptographic_provider_algorithms
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cryptographic_provider_algorithms dynamic management function
ms.assetid: 8bcccb37-5cfb-4e1e-a0bb-7ff4c279fe8e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cb48a9f0f7e30e6df4fa09485b9e0ea0c9fc8a56
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2018
ms.locfileid: "47699210"
---
# <a name="sysdmcryptographicprovideralgorithms-transact-sql"></a>sys.dm_cryptographic_provider_algorithms (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  拡張キー管理 (EKM) プロバイダーによってサポートされているアルゴリズムを返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.dm_cryptographic_provider_algorithms ( provider_id )  
```  
  
## <a name="arguments"></a>引数  
 *provider_id*  
 EKM プロバイダーの識別番号。既定値はありません。  
  
## <a name="tables-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|algorithm_id|**int**|アルゴリズムの識別番号を指定します。|  
|algorithm_tag|**nvarchar(60)**|アルゴリズムの識別タグを指定します。|  
|key_type|**nvarchar(128)**|キーの種類を示します。 ASYMMETRIC KEY または SYMMETRIC KEY を返します。|  
|key_length|**int**|キーの長さをビット単位で示します。|  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーは、public データベース ロールのメンバーである必要があります。  
  
## <a name="examples"></a>使用例  
 次の例では、識別番号が `1234567` であるプロバイダーのプロバイダー オプションを表示しています。  
  
```  
SELECT * FROM sys.dm_cryptographic_provider_algorithms(1234567);  
GO  
```  
  
## <a name="see-also"></a>参照  
 [拡張キー管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [セキュリティ関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
