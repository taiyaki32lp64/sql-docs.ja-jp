---
title: dbo. sysjobservers (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/26/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysjobservers
- sysjobservers_TSQL
- dbo.sysjobservers
- dbo.sysjobservers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobservers system table
ms.assetid: 9abcc20f-a421-4591-affb-62674d04575e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 03a4457cb5dd087639a439e9e9bb883eaf924366
ms.sourcegitcommit: 8c1c6232a4f592f6bf81910a49375f7488f069c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70026205"
---
# <a name="dbosysjobservers-transact-sql"></a>dbo.sysjobservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

特定のジョブと 1 つ以上のターゲット サーバーとの関連付けまたはリレーションシップを格納します。 このテーブルは、msdb データベースに格納されます。
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|job_id|**uniqueidentifier**|ジョブ識別番号。|  
|server_id|**int**|サーバーの識別番号。|  
|last_run_outcome|**tinyint**|前回のジョブの実行結果。<br /><br /> **0** = 失敗<br /><br /> **1** = 成功<br /><br /> **2** = 再試行<br /><br /> **3** = キャンセル<br /><br /> **4** = 実行中<br /><br /> **5** = 不明 (次の「解説」を参照してください) |  
|last_outcome_ message|**nvarchar(1024)**|last_run_outcome 列に関連付けられているメッセージ (存在する場合)。|  
|last_run_date|**int**|ジョブの前回の実行日付。|  
|last_run_time|**int**|ジョブの前回の実行時刻。|  
|last_run_duration|**int**|ジョブが実行された期間を時間、分、および秒単位で表したもの。 次の式を使用して計算されます: (*時間*\*1万) + (*分*\*100) +*秒*です。|  


## <a name="remarks"></a>コメント

*4*を超える値は、SQL エージェントがそのジョブの状態を認識していないことを意味します。 ジョブを作成すると、 *last_run_outcome*は最初に*5*に設定されます。


## <a name="see-also"></a>関連項目

[SQL Server エージェントテーブル&#40;transact-sql&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
