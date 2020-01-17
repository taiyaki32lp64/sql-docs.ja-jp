---
title: sp_refresh_log_shipping_monitor (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_refresh_log_shipping_monitor
- sp_refresh_log_shipping_monitor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_refresh_log_shipping_monitor
ms.assetid: edefb912-31c5-4d99-9aba-06629afd0171
author: stevestein
ms.author: sstein
ms.openlocfilehash: c19f9b99173ca04e6ce15862e22a25f8a2bf06e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002498"
---
# <a name="sprefreshlogshippingmonitor-transact-sql"></a>sp_refresh_log_shipping_monitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  リモートの監視テーブルを、指定したログ配布エージェントの特定のプライマリまたはセカンダリ サーバーにある最新の情報に更新します。 プロシージャは、プライマリまたはセカンダリ サーバーで呼び出されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_refresh_log_shipping_monitor  
[ @agent_id = ] 'agent_id',  
[ @agent_type = ] 'agent_type'  
[ @database = ] 'database'  
[ @mode ] n  
```  
  
## <a name="arguments"></a>引数  
`[ @agent_id = ] 'agent_id'` バックアップ用のプライマリ ID、またはコピーまたは復元用のセカンダリ ID。 *agent_id*は**uniqueidentifier** NULL にすることはできません。  
  
`[ @agent_type = ] 'agent_type'` ログ配布ジョブの種類。  
  
 0 = バックアップ。  
  
 1 = コピーします。  
  
 2 = 復元です。  
  
 *agent_type*は**tinyint** NULL にすることはできません。  
  
`[ @database = ] 'database'` プライマリまたはセカンダリのデータベースをバックアップや復元エージェントのログ記録で使用します。  
  
`[ @mode ] n` 監視データを更新または削除するかどうかを指定します。 データ型*m* tinyint は、サポートされている値します。  
  
 1 = 更新 (これは、既定値です)。  
  
 2 = delete  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 [なし] :  
  
## <a name="remarks"></a>コメント  
 **sp_refresh_log_shipping_monitor**更新、 **log_shipping_monitor_primary**、 **log_shipping_monitor_secondary**、 **log_shipping_monitor_history_detail**、および**log_shipping_monitor_error_detail**まだ転送されていないすべてのセッション情報とテーブル。 これにより、モニターは、しばらくの間に同期されているときに、プライマリまたはセカンダリ サーバーを監視サーバーを同期できます。 さらに、必要に応じて監視サーバーのモニターの情報をクリーンアップできます。  
  
 **sp_refresh_log_shipping_monitor**から実行する必要があります、**マスター**プライマリまたはセカンダリ サーバー上のデータベース。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールは、この手順を実行できます。  
  
## <a name="see-also"></a>関連項目  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
