---
title: dbo.sysoperators (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysoperators
- dbo.sysoperators
- dbo.sysoperators_TSQL
- sysoperators_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysoperators system table
ms.assetid: c2afa20c-b15f-46ca-ae74-2eb65909409e
author: stevestein
ms.author: sstein
ms.openlocfilehash: e4336fdeeb0867018e9a2a630f2212cc06259482
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67984909"
---
# <a name="dbosysoperators-transact-sql"></a>dbo.sysoperators (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのオペレーターごとに 1 行のデータを格納します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|オペレーターの ID。|  
|**name**|**sysname**|オペレーターの名前。|  
|**enabled**|**tinyint**|アラート通知 (ブール値) の状態です。 場合**1**アラートが発生した場合、このオペレーターが通知を受信できます。|  
|**email_address**|**nvarchar(100)**|オペレーターの電子メール アドレス。|  
|**last_email_date**|**int**|この演算子は、電子メールによる警告通知を前回受信した日付。|  
|**last_email_time**|**int**|この演算子は、電子メールによる警告通知を前回受信した時刻。|  
|**pager_address**|**nvarchar(100)**|オペレーターのポケットベル アドレス。|  
|**last_pager_date**|**int**|このオペレーターが前回ポケットベルによる警告通知を受信した日付。|  
|**last_pager_time**|**int**|このオペレーターが前回ポケットベルによる警告通知を受信した時刻。|  
|**weekday_pager_start_time**|**int**|このオペレーターがポケットベルによる警告通知を受信可能になる曜日 (月曜から金曜) での時刻。|  
|**weekday_pager_end_time**|**int**|平日 (月曜から金曜まで)、オペレーターのポケットベルによる警告通知が受信不能になる時刻。|  
|**saturday_pager_start_time**|**int**|土曜日にこのオペレーターがポケットベルによる警告通知を受信可能になる時刻。|  
|**saturday_pager_end_time**|**int**|その後この演算子は、ポケットベルによる警告通知の受信に使用できる土曜日の時間です。|  
|**sunday_pager_start_time**|**int**|日曜日、このオペレーターがポケットベルによる警告通知を受信可能になる時刻。|  
|**sunday_pager_end_time**|**int**|その後この演算子は、ポケットベルによる警告通知の受信に使用できる日曜日の時間です。|  
|**pager_days**|**tinyint**|このオペレーターのポケットベルによる警告通知の受信に使用できる期間の曜日を表すビットマスク。|  
|**netsend_address**|**nvarchar(100)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**last_netsend_date**|**int**|指定したオペレーター ID に最新のネットワーク メッセージが送信された前回の日付|  
|**last_netsend_time**|**int**|指定したオペレーター ID に最新のネットワーク メッセージが送信された前回の時間|  
|**category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="see-also"></a>関連項目  
 [SQL Server エージェント テーブル&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
