---
title: sys.dm_column_encryption_enclave (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: system-objects
ms.topic: language-reference
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: d10bef0df04501c177086b6c89b3f67dec3bab10
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73599245"
---
# <a name="sysdm_column_encryption_enclave-transact-sql"></a>sys.dm_column_encryption_enclave (Transact-sql)
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

Always Encrypted の secure エンクレーブのパフォーマンスカウンターを返します。 詳細については、「[セキュア エンクレーブを使用する Always Encrypted](../security/encryption/always-encrypted-enclaves.md)」を参照してください。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の最後の再起動後にエンクレーブが構成され、正しく初期化されている場合、ビューには1つの行だけが含まれます。 エンクレーブが構成されていないか、正しく初期化されていない場合、ビューは行を返しません。 

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|current_enclave_session_count|**int**|エンクレーブを使用しているクライアントセッションの現在の数。|  
|current_column_encryption_key_count|**int**|エンクレーブで現在保持されている列の暗号化キーの数。|  
|current_memory_size_kb|**bigint**|エンクレーブのメモリサイズ (KB 単位)|  
|total_evicted_session_count|**bigint**|前回のサーバーの再起動以降に削除されたエンクレーブセッションの合計数。|   
  
## <a name="permissions"></a>アクセス許可  
`VIEW SERVER STATE` 権限が必要です。   
  
## <a name="examples"></a>使用例  
 
```sql  
SELECT * FROM sys.dm_column_encryption_enclave;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Always Encrypted サーバー構成オプションのエンクレーブ type の構成](../../database-engine/configure-windows/configure-column-encryption-enclave-type.md)
  
  
