---
title: sp_help_log_shipping_monitor (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_monitor_TSQL
- sp_help_log_shipping_monitor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_monitor
ms.assetid: a4e96c45-6dcd-471a-a494-b5c619459855
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d2b8fc2ac96821427aaf0ef2550fb6624a923d7f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68000931"
---
# <a name="sphelplogshippingmonitor-transact-sql"></a>sp_help_log_shipping_monitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  状態と登録済みのプライマリとセカンダリ データベースのプライマリ、セカンダリ、または監視サーバーの他の情報を含む結果セットを返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_log_shipping_monitor  
```  
  
## <a name="arguments"></a>引数  
 [なし] :  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**status**|**bit**|ログ配布データベースのエージェントに関する全般的な状態。<br /><br /> **0** = 正常でないエージェントのエラー。<br /><br /> **1** = それ以外の場合。|  
|**is_primary**|**bit**|この行がプライマリ データベースのものかどうか。<br /><br /> **1** = 行はプライマリ データベースです。<br /><br /> **0** = 行は、セカンダリ データベース。|  
|**server**|**sysname**|このデータベースが存在するプライマリまたはセカンダリ サーバーの名前。|  
|**database_name**|**sysname**|データベース名です。|  
|**time_since_last_backup**|**int**|最後のログ バックアップ以降の分単位の時間の長さ。<br /><br /> NULL = 情報をご利用いただけませんかは関係ありません。|  
|**last_backup_file**|**nvarchar(500)**|前回正常に作成されたログ バックアップ ファイルの名前。<br /><br /> NULL = 情報をご利用いただけませんかは関係ありません。|  
|**backup_threshold**|**int**|前回のバックアップが行われてから、threshold_alert エラーが発生するまでの期間 (分単位)。 **backup_threshold**は**int**、既定値は**60 分**します。<br /><br /> NULL = 情報をご利用いただけませんかは関係ありません。<br /><br /> この値を使用して変更できます[sp_add_log_shipping_primary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)します。|  
|**is_backup_alert_enabled**|**bit**|アラートがあるかどうかを指定する場合に発生します**backup_threshold**を超過します。 いずれかの値 (**1**) で、既定値は、アラートが生成されることを意味します。<br /><br /> NULL = 情報をご利用いただけませんかは関係ありません。<br /><br /> この値を使用して変更できます[sp_add_log_shipping_primary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)します。|  
|**time_since_last_copy**|**int**|前回のログ バックアップがコピーされてから経過した時間 (分単位)。<br /><br /> NULL = 情報をご利用いただけませんかは関係ありません。|  
|**last_copied_file**|**nvarchar(500)**|最後に正常にコピーされたログ バックアップ ファイルの名前。<br /><br /> NULL = 情報をご利用いただけませんかは関係ありません。|  
|**time_since_last_restore**|**int**|最後のログ バックアップが復元されたため、分単位の時間の長さ。<br /><br /> NULL = 情報をご利用いただけませんかは関係ありません。|  
|**last_restored_file**|**nvarchar(500).**|最後に正常に復元されたログ バックアップ ファイルの名前。<br /><br /> NULL = 情報をご利用いただけませんかは関係ありません。|  
|**last_restored_latency**|**int**|時間 (分)、バックアップの復元には、前回のバックアップの作成からの継続時間。<br /><br /> NULL = 情報をご利用いただけませんかは関係ありません。|  
|**restore_threshold**|**int**|許容経過時間を分単位の数は、アラートを生成する前に、操作を復元します。 **restore_threshold** NULL にすることはできません。|  
|**is_restore_alert_enabled**|**bit**|アラートが発生したかどうかを指定します。 ときに**restore_threshold**を超過します。 いずれかの値 (**1**) で、既定では、アラートが発生することを意味します。<br /><br /> NULL = 情報をご利用いただけませんかは関係ありません。<br /><br /> 復元のしきい値を設定する[sp_add_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)します。|  
  
## <a name="remarks"></a>コメント  
 **sp_help_log_shipping_monitor**から実行する必要があります、**マスター**監視サーバー上のデータベース。  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="see-also"></a>関連項目  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
