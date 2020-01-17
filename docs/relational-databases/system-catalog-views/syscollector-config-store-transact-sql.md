---
title: syscollector_config_store (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_config_store_TSQL
- syscollector_config_store
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_config_store view
ms.assetid: f15f6b05-6808-4b76-b6a8-48dec844cf63
author: stevestein
ms.author: sstein
ms.openlocfilehash: 174fa1af651c2e713bdb91ba217e896b833467b2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060371"
---
# <a name="syscollectorconfigstore-transact-sql"></a>syscollector_config_store (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  コレクションではなく、すべてのデータ コレクターに適用されるプロパティを返しますでは、インスタンスを設定します。 このビューの各行は、管理データ ウェアハウスの名前や、管理データ ウェアハウスが置かれているインスタンスの名前など、データ コレクターの特定のプロパティを表します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|parameter_name|**nvarchar(128)**|プロパティの名前。 NULL 値は許可されません。|  
|parameter_value|**sql_variant**|プロパティの実際の値。 NULL 値が許可されます。|  
  
## <a name="permissions"></a>アクセス許可  
 ビューの SELECT 権限、または dc_operator、dc_proxy、dc_admin のいずれかの固定データベース ロールのメンバーシップが必要です。  
  
## <a name="remarks"></a>コメント  
 使用可能なプロパティの一覧が固定され、適切なストアド プロシージャを使用してその値を変更することができますのみ。 次の表で、このビューを介して公開されるプロパティについて説明します。  
  
|プロパティ名|説明|  
|-------------------|-----------------|  
|CacheDirectory|コレクター型のパッケージが一時的な情報を格納するファイル システム内のディレクトリの名前です。<br /><br /> NULL = 既定の一時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ディレクトリが使用されます。|  
|CacheWindow|失敗したデータのアップロード用のキャッシュ ディレクトリのデータ保有ポリシーを示します。<br /><br /> -1 = アップロード エラーが発生した場合は常にデータを保持します。<br /><br /> 0 = アップロード エラーが発生した場合にデータを保持しません。<br /><br /> *n*からデータの保持を = *n*以前のアップロード エラー、 *n* > = 1。<br /><br /> この値を変更するには、sp_syscollector_set_cache_window ストアド プロシージャを使用します。|  
|CollectorEnabled|データ コレクターの状態を示します。<br /><br /> 0 = 無効になっています<br /><br /> 1 = 有効になっています。<br /><br /> この値を変更するには、sp_syscollector_enable_collector ストアド プロシージャまたは sp_syscollector_disable_collector ストアド プロシージャを使用します。|  
|MDWDatabase|管理データ ウェアハウスの名前。 この値を変更するには、sp_syscollector_set_warehouse_database_name ストアド プロシージャを使用します。|  
|なっています|管理データ ウェアハウスが存在する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前です。 この値を変更するには、sp_syscollector_set_warehouse_instance_name ストアド プロシージャを使用します。|  
  
## <a name="examples"></a>使用例  
 次の例では、syscollector_config_store ビューのクエリを実行します。  
  
```sql  
SELECT parameter_name, parameter_value  
FROM msdb.dbo.syscollector_config_store;  
```  
  
## <a name="see-also"></a>関連項目  
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [データ コレクターのビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)   
 [sp_syscollector_enable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)   
 [sp_syscollector_disable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)   
 [sp_syscollector_set_warehouse_database_name &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-database-name-transact-sql.md)   
 [sp_syscollector_set_warehouse_instance_name &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-instance-name-transact-sql.md)   
 [sp_syscollector_set_cache_window &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)  
  
  
