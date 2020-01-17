---
title: sp_cleanup_log_shipping_history (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cleanup_log_shipping_history_TSQL
- sp_cleanup_log_shipping_history
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cleanup_log_shipping_history
ms.assetid: 96d236a9-1d0e-4f83-a4d3-f825b7381e46
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7470baabb9a35a923995d8306b314f9272de0b5c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070370"
---
# <a name="spcleanuplogshippinghistory-transact-sql"></a>sp_cleanup_log_shipping_history (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  このストアド プロシージャは、ローカルおよび保有期間に基づいて、監視サーバー上の履歴をクリーンアップします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_cleanup_log_shipping_history  
[ @agent_id = ] 'agent_id',  
[ @agent_type = ] 'agent_type'  
```  
  
## <a name="arguments"></a>引数  
`[ @agent_id = ] 'agent_id',` バックアップ用のプライマリ ID、またはコピーまたは復元用のセカンダリ ID。 *agent_id*は**uniqueidentifier** NULL にすることはできません。  
  
`[ @agent_type = ] 'agent_type'` ログ配布ジョブの種類。 0 = バックアップ、1 = コピー、2 = 復元です。 *agent_type*は**tinyint** NULL にすることはできません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 [なし] :  
  
## <a name="remarks"></a>コメント  
 **sp_cleanup_log_shipping_history**から実行する必要があります、**マスター**ログ配布サーバー上のデータベース。 このストアド プロシージャのローカルとリモートのコピーをクリーンアップ**log_shipping_monitor_history_detail**と**log_shipping_monitor_error_detail**履歴の保有期間に基づいて。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールは、この手順を実行できます。  
  
## <a name="see-also"></a>関連項目  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
