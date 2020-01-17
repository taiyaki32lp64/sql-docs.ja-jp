---
title: dbo.sysjobs (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysjobs
- sysjobs_TSQL
- dbo.sysjobs
- dbo.sysjobs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobs system table
ms.assetid: e244a6a5-54c2-47a6-8039-dd1852b0ae59
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3ea2b3196e159b19a1baaa032c622a4cf9132402
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097602"
---
# <a name="dbosysjobs-transact-sql"></a>dbo.sysjobs (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによる実行が予定されているジョブに関する情報を格納します。 このテーブルに格納されます、 **msdb**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|ジョブの一意な ID。|  
|**originating_server_id**|**int**|ジョブを実行した元のサーバーの ID。|  
|**name**|**sysname**|ジョブの名前。|  
|**enabled**|**tinyint**|ジョブが実行可能かどうか。|  
|**description**|**nvarchar(512)**|ジョブの説明。|  
|**start_step_id**|**int**|実行を開始するジョブ ステップの ID。|  
|**category_id**|**int**|ジョブ カテゴリの ID。|  
|**owner_sid**|**varbinary(85)**|ジョブ所有者のセキュリティ識別番号 (SID)。|  
|**notify_level_eventlog**|**int**|**ビットマスク**示すどのような場合は、Microsoft Windows アプリケーション ログに、通知イベントが記録する必要があります。<br /><br /> **0** = なし<br /><br /> **1**ジョブ成功時の =<br /><br /> **2** = ジョブが失敗したとき<br /><br /> **3** = (ジョブの結果に関係なく、ジョブが終了したとき|  
|**notify_level_email**|**int**|どのような場合に、ジョブの完了時に通知電子メールを送信するかを示すビットマスク。<br /><br /> **0** = なし<br /><br /> **1**ジョブ成功時の =<br /><br /> **2** = ジョブが失敗したとき<br /><br /> **3** = (ジョブの結果に関係なく、ジョブが終了したとき|  
|**notify_level_netsend**|**int**|ジョブが完了すると、どのような場合、ネットワーク メッセージを示すビットマスクを送信する必要があります。<br /><br /> **0** = なし<br /><br /> **1**ジョブ成功時の =<br /><br /> **2** = ジョブが失敗したとき<br /><br /> **3** = (ジョブの結果に関係なく、ジョブが終了したとき|  
|**notify_level_page**|**int**|どのような場合に、ジョブの完了時にポケットベルのメッセージを送信するのかを示すビットマスク。<br /><br /> **0** = なし<br /><br /> **1**ジョブ成功時の =<br /><br /> **2** = ジョブが失敗したとき<br /><br /> **3** = (ジョブの結果に関係なく、ジョブが終了したとき|  
|**notify_email_operator_id**|**int**|通知先のオペレーターの電子メール名。|  
|**notify_netsend_operator_id**|**int**|コンピューターまたはネットワーク メッセージを送信するときに使用するユーザーの ID。|  
|**notify_page_operator_id**|**int**|コンピューターまたはページを送信するときに使用するユーザーの ID。|  
|**delete_level**|**int**|**ビットマスク**示すジョブの完了時にどのような場合、ジョブを削除する必要があります。<br /><br /> **0** = なし<br /><br /> **1**ジョブ成功時の =<br /><br /> **2** = ジョブが失敗したとき<br /><br /> **3** = (ジョブの結果に関係なく、ジョブが終了したとき|  
|**date_created**|**datetime**|ジョブを作成した日付。|  
|**date_modified**|**datetime**|ジョブを最後に変更した日付。|  
|**version_number**|**int**|ジョブのバージョン。|  
  
  
