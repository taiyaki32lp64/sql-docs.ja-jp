---
title: dbo.sysalerts (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysalerts
- sysalerts_TSQL
- dbo.sysalerts_TSQL
- sysalerts
dev_langs:
- TSQL
helpviewer_keywords:
- sysalerts system table
ms.assetid: a2c2f50d-61f3-4951-996a-add5ad092cc2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4645b586c07635a405b2e678b84c4846762f7582
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084685"
---
# <a name="dbosysalerts-transact-sql"></a>dbo.sysalerts (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  警告 1 件につき 1 行のデータを格納します。 アラートは、イベントに応答して送信されるメッセージです。 警告メッセージは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境の外に転送でき、電子メールやポケットベルのメッセージとして送信することもできます。 また、警告でタスクを生成することもできます。  このテーブルに格納されます、 **msdb**データベース。
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|警告 ID。|  
|**name**|**sysname**|アラートの名前。|  
|**event_source**|**nvarchar(100)**|イベントのソース ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])。|  
|**event_category_id**|**int**|将来使用するために予約されています。|  
|**event_id**|**int**|将来使用するために予約されています。|  
|**message_id**|**int**|ユーザー定義メッセージの ID またはへの参照を**sysmessages**このアラートをトリガーするメッセージ。|  
|**severity**|**int**|このアラートをトリガーする重大度。|  
|**enabled**|**tinyint**|アラートの状態:<br /><br /> **0** = 無効になっています。<br /><br /> **1** = 有効にします。|  
|**delay_between_responses**|**int**|このアラートを通知する間隔 (秒) には、期間、待機します。|  
|**last_occurrence_date**|**int**|アラートの最後に見つかった (日付)。|  
|**last_occurrence_time**|**int**|前回の警告発生時刻。|  
|**last_response_date**|**int**|前回の警告通知日。|  
|**last_response_time**|**int**|前回のアラートの通知 (1 日の時刻)。|  
|**notification_message**|**nvarchar(512)**|追加情報が、アラートを送信します。|  
|**include_event_description**|**tinyint**|イベントの説明は、電子メール、ポケットベル、または Net send によって送信されるかどうかを表すビットマスク。 値の下のグラフを参照してください。|  
|**database_name**|**nvarchar(512)**|データベースがこの警告がこのアラートが発生する必要があります。|  
|**event_description_keyword**|**nvarchar(100)**|エラーのパターンは、アラートをトリガーするために一致する必要があります。|  
|**occurrence_count**|**int**|警告の発生回数。|  
|**count_reset_date**|**int**|Day (日) のカウントをリセットする**0**します。|  
|**count_reset_time**|**int**|指定された日数の時間にリセットする**0**します。|  
|**job_id**|**uniqueidentifier**|警告が発生したときに実行するタスクの ID。|  
|**has_notification**|**int**|アラート発生時に電子メール通知を受信するオペレーターの数。|  
|**flags**|**int**|予約済み。|  
|**performance_condition**|**nvarchar(512)**|予約済み。|  
|**category_id**|**int**|予約済み。|  
  
 ## <a name="remarks"></a>コメント

次の表では、include_event_description ビットマスクの値を示します。 Dbo.sysalerts 10 進数の値が返されます。 

|Decimal | バイナリ | 意味 |
|------|------|------|
|0 |0000 |メッセージはありません。 |
|1 |0001 |電子メール |
|2 |0010 |ポケットベル (pager) |
|3 |0011 |ポケットベルとメール |
|4 |0100 |[Net Send] |
|5 |0101 |Net send および電子メール |
|6 |0110 |Net send およびポケットベル |
|7 |0111 |Net send、ポケットベル、および電子メール |
  
