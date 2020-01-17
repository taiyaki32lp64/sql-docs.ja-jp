---
title: sys.dm_os_buffer_pool_extension_configuration (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/09/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_buffer_pool_extension_configuration
- sys.dm_os_buffer_pool_extension_configuration_TSQL
- dm_os_buffer_pool_extension_configuration_TSQL
- sys.dm_os_buffer_pool_extension_configuration
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_buffer_pool_extension_configuration dynamic management view
ms.assetid: d52cc481-4d29-4f33-b63d-231ec35d092f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 38e4e1ad85a5e968d4b0bb33a3a72a829942585b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900218"
---
# <a name="sysdmosbufferpoolextensionconfiguration-transact-sql"></a>sys.dm_os_buffer_pool_extension_configuration (TRANSACT-SQL)

[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  バッファー プール拡張に関する構成情報を返します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 各バッファー プール拡張ファイルの 1 つの行を返します。  
  

  
| 列名 | データ型 | 説明 |
| :---------- | :-------- | :---------- |
|path|**nvarchar**(256)|バッファー プール拡張キャッシュのパスとファイル名。 Null 値を許容します。|  
|file_id|**int**|バッファー プール拡張ファイルの ID。 NULL 値は許可されません。|  
|state|**int**|バッファー プール拡張機能の状態。 NULL 値は許可されません。<br /><br /> 0 - バッファー プール拡張機能が無効<br /><br /> 1 - バッファー プール拡張機能の無効化<br /><br /> 2 - 将来使用するため予約されています<br /><br /> 3 - バッファー プール拡張機能の有効化<br /><br /> 4 - 将来使用するため予約されています<br /><br /> 5 - バッファー プール拡張機能が有効|  
|state_description|**nvarchar**(60)|バッファー プール拡張機能の状態を説明します。 NULL 値が許可されます。<br /><br /> 0 = バッファー プール拡張機能が無効<br /><br /> 5 = バッファー プール拡張機能が有効になっています。|
|current_size_in_kb|**bigint**|現在、バッファー プール拡張ファイルのサイズ。 NULL 値は許可されません。|
| &nbsp; | &nbsp; | &nbsp; |

## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-configuration-buffer-pool-extension-information"></a>A. バッファー プール拡張の構成情報を返す  
 次の例は、sys.dm_os_buffer_pool_extension_configruation DMV のすべての列を返します。  
  
```sql  
SELECT path, file_id, state, state_description, current_size_in_kb  
FROM sys.dm_os_buffer_pool_extension_configuration;  
```  
  
### <a name="b-returning-the-number-of-cached-pages-in-the-buffer-pool-extension-file"></a>B. バッファー プール拡張ファイル内のキャッシュされたページ数を返す  
 次の例は、各バッファー プール拡張ファイル内のキャッシュされたページ数を返します。  
  
```sql  
SELECT COUNT(*) AS cached_pages_count  
FROM sys.dm_os_buffer_descriptors  
WHERE is_in_bpool_extension <> 0  
;  
```  
  
## <a name="see-also"></a>関連項目  
 [バッファー プール拡張機能](../../database-engine/configure-windows/buffer-pool-extension.md)   
 [sys.dm_os_buffer_descriptors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-descriptors-transact-sql.md)  
  
  
