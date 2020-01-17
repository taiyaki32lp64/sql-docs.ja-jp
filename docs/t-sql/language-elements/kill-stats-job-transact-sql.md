---
title: KILL STATS JOB (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- KILL STATS JOB
- KILL_STATS_JOB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ending statistics update jobs [SQL Server]
- stopping statistics update jobs
- terminating statistics update jobs
- asynchronous statistics updates [SQL Server]
- KILL STATS JOB statement
- statistics update jobs [SQL Server]
ms.assetid: 55a8f9f1-3259-45c0-8ab9-60b9c088b4b4
author: rothja
ms.author: jroth
ms.openlocfilehash: b0dd587240a56dcdfab4d618255ee838491054af
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122285"
---
# <a name="kill-stats-job-transact-sql"></a>KILL STATS JOB (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で統計の非同期更新ジョブを終了します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
KILL STATS JOB job_id   
```  
  
## <a name="arguments"></a>引数  
 *job_id*  
 ジョブの sys.dm_exec_background_job_queue 動的管理ビューによって返された job_id フィールドです。  
  
## <a name="remarks"></a>Remarks  
 job_id は、他の形式の KILL ステートメントで使用されている session_id または作業単位とは無関係です。  
  
## <a name="permissions"></a>アクセス許可  
 sys.dm_exec_background_job_queue 動的管理ビューからの情報にアクセスするには VIEW SERVER STATE 権限が必要です。  
  
 KILL STATS JOB 権限は、特に指定のない限り固定データベース ロール sysadmin および processadmin のメンバーに与えられ、これを譲渡することはできません。  
  
## <a name="examples"></a>使用例  
 次の例は、*job_id* = `53` のジョブに関連付けられた統計情報の更新を終了する方法を示しています。  
  
```  
KILL STATS JOB 53;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [KILL &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-transact-sql.md)   
 [KILL QUERY NOTIFICATION SUBSCRIPTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-query-notification-subscription-transact-sql.md)   
 [sys.dm_exec_background_job_queue &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-background-job-queue-transact-sql.md)   
 [統計](../../relational-databases/statistics/statistics.md)  
  
  
