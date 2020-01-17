---
title: sys.foreign_keys (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- foreign_keys
- sys.foreign_keys
- sys.foreign_keys_TSQL
- foreign_keys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.foreign_keys catalog view
ms.assetid: e960df1a-13fc-43ee-ba91-34c1b719ac2c
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b78466b0c2c20bc3b59fb372870bbad87aef0e74
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133891"
---
# <a name="sysforeignkeys-transact-sql"></a>sys.foreign_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  FOREIGN KEY 制約があるオブジェクトごとに 1 行が含まれています**sys.object.type** F. を =  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<Sys.objects から継承された列 >**||このビューが継承する列の一覧は、次を参照してください。 [sys.objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)します。|  
|**referenced_object_id**|**int**|参照されるオブジェクトの ID。|  
|**key_index_id**|**int**|参照されるオブジェクト内のキー インデックスの ID。|  
|**is_disabled**|**bit**|FOREIGN KEY 制約が無効です。|  
|**is_not_for_replication**|**bit**|FOREIGN KEY 制約は、NOT FOR REPLICATION オプションを使用して作成されました。|  
|**is_not_trusted**|**bit**|FOREIGN KEY 制約がシステムで検証されていません。|  
|**delete_referential_action**|**tinyint**|削除が発生したときに FOREIGN KEY に対して宣言された参照操作。<br /><br /> 0 = 操作なし<br /><br /> 1 = 連鎖<br /><br /> 2 = NULL に設定<br /><br /> 3 = 既定値に設定|  
|**delete_referential_action_desc**|**nvarchar(60)**|削除が発生したときに FOREIGN KEY に対して宣言された参照操作の説明。<br /><br /> NO_ACTION<br /><br /> CASCADE<br /><br /> SET_NULL<br /><br /> SET_DEFAULT|  
|**update_referential_action**|**tinyint**|更新が発生したときに FOREIGN KEY に対して宣言された参照操作。<br /><br /> 0 = 操作なし<br /><br /> 1 = 連鎖<br /><br /> 2 = NULL に設定<br /><br /> 3 = 既定値に設定|  
|**update_referential_action_desc**|**nvarchar(60)**|更新が発生したときに FOREIGN KEY に対して宣言された参照操作の説明。<br /><br /> NO_ACTION<br /><br /> CASCADE<br /><br /> SET_NULL<br /><br /> SET_DEFAULT|  
|**is_system_named**|**bit**|1 = システムによって生成された名前。<br /><br /> 0 = ユーザー指定の名前。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [SQL Server システム カタログに対するクエリに関してよくあるご質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
