---
title: sp_change_log_shipping_secondary_database (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_secondary_database
- sp_change_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_secondary_database
ms.assetid: 3ebcf2f1-980f-4543-a84b-fbaeea54eeac
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d0bd62fe3462441d4eab9d3d89bce20cf1144131
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909553"
---
# <a name="sp_change_log_shipping_secondary_database-transact-sql"></a>sp_change_log_shipping_secondary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  セカンダリデータベースの設定を変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_change_log_shipping_secondary_database  
[ @secondary_database = ] 'secondary_database',  
[, [ @restore_delay = ] 'restore_delay']  
[, [ @restore_all = ] 'restore_all']  
[, [ @restore_mode = ] 'restore_mode']  
[, [ @disconnect_users = ] 'disconnect_users']  
[, [ @block_size = ] 'block_size']  
[, [ @buffer_count = ] 'buffer_count']  
[, [ @max_transfer_size = ] 'max_transfer_size']  
[, [ @restore_threshold = ] 'restore_threshold']   
[, [ @threshold_alert = ] 'threshold_alert']   
[, [ @threshold_alert_enabled = ] 'threshold_alert_enabled']   
[, [ @history_retention_period = ] 'history_retention_period']  
```  
  
## <a name="arguments"></a>引数  
指定されたバックアップファイルを復元する前に、セカンダリサーバーが待機する時間を分単位で `[ @restore_delay = ] 'restore_delay'` します。 *restore_delay*は**int**であり、NULL にすることはできません。 既定値は 0 です。  
  
`[ @restore_all = ] 'restore_all'` が1に設定されている場合、セカンダリサーバーは、復元ジョブの実行時に使用可能なすべてのトランザクションログバックアップを復元します。 それ以外の場合は、1つのファイルが復元された後に停止します。 *restore_all*は**ビット**であり、NULL にすることはできません。  
  
セカンダリデータベースの復元モードを `[ @restore_mode = ] 'restore_mode'` します。  
  
 0 = NORECOVERY でログを復元。  
  
 1 = スタンバイ状態のログを復元します。  
  
 *restore*は**ビット**であり、NULL にすることはできません。  
  
`[ @disconnect_users = ] 'disconnect_users'` 1 に設定すると、復元操作の実行時にユーザーがセカンダリデータベースから切断されます。 既定値は0です。 *disconnect_users*は**ビット**であり、NULL にすることはできません。  
  
バックアップデバイスのブロックサイズとして使用されるサイズ (バイト単位) `[ @block_size = ] 'block_size'` します。 *block_size*は**int**で、既定値は-1 です。  
  
バックアップまたは復元操作で使用されるバッファーの合計数 `[ @buffer_count = ] 'buffer_count'` ます。 *buffer_count*は**int**で、既定値は-1 です。  
  
バックアップデバイスに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって発行された入力要求または出力要求の最大サイズ (バイト単位) を `[ @max_transfer_size = ] 'max_transfer_size'` します。 *max_transfersize*は**int**であり、NULL を指定できます。  
  
復元操作が発生してから警告が生成されるまでの許容時間 (分単位) を `[ @restore_threshold = ] 'restore_threshold'` します。 *restore_threshold*は**int**であり、NULL にすることはできません。  
  
`[ @threshold_alert = ] 'threshold_alert'` は、復元のしきい値を超えたときに発生するアラートです。 *threshold_alert*は**int**,、既定値は14420です。  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'` *restore_threshold*を超過したときにアラートを生成するかどうかを指定します。 1 = 有効。0 = 無効です。 *threshold_alert_enabled*は**ビット**であり、NULL にすることはできません。  
  
`[ @history_retention_period = ] 'history_retention_period'` は、履歴を保持する時間 (分単位) です。 *history_retention_period*は**int**です。値が指定されていない場合は、1440の値が使用されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 [InclusionThresholdSetting]  
  
## <a name="remarks"></a>Remarks  
 **sp_change_log_shipping_secondary_database**は、セカンダリサーバーの**master**データベースから実行する必要があります。 このストアド プロシージャでは次の処理が行われます。  
  
1.  必要に応じて**log_shipping_secondary_database**レコードの設定を変更します。  
  
2.  必要に応じて、指定された引数を使用して、セカンダリサーバー上の**log_shipping_monitor_secondary**のローカル監視レコードを変更します。  

## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="examples"></a>使用例  
 この例では、 **sp_change_log_shipping_secondary_database**を使用してデータベース**LogShipAdventureWorks**のセカンダリデータベースパラメーターを更新する方法を示します。  
  
```  
EXEC master.dbo.sp_change_log_shipping_secondary_database   
 @secondary_database =  'LogShipAdventureWorks'  
,  @restore_delay = 0  
,  @restore_all = 1  
,  @restore_mode = 0  
,  @disconnect_users = 0  
,  @threshold_alert = 14420  
,  @threshold_alert_enabled = 1  
,  @history_retention_period = 14420;  
```  
  
## <a name="see-also"></a>参照  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
