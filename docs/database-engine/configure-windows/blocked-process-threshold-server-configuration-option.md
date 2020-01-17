---
title: blocked process threshold サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- thresholds [SQL Server]
- blocked process threshold option
ms.assetid: 3d46d143-bc6a-4220-8b55-6baa37547c25
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 84a94dc6b1d4f2f6f0c921f81746eb64f41d2f07
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68013115"
---
# <a name="blocked-process-threshold-server-configuration-option"></a>blocked process threshold サーバー構成オプション
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  ブロックされたプロセスのレポートを生成するためのしきい値を秒単位で指定するには、 **blocked process threshold** オプションを使用します。 しきい値は 0 ～ 86,400 の範囲で設定できます。 既定では、ブロックされているプロセスのレポートは生成されません。 システム タスクや、検出可能なデッドロックを生成しないリソースで待機しているタスクの場合、このイベントは生成されません。  
  
 このイベントが生成されたときに [警告](../../ssms/agent/alerts.md) が実行されるように定義できます。 たとえば、ブロック状態を処理する適切な操作を行うために、管理者を呼び出すように選択できます。  
  
 blocked process threshold オプションでは、デッドロック監視バックグラウンド スレッドを使用して、設定されたしきい値より長い間待機しているか、またはしきい値の数倍の時間待機しているタスクの一覧を調べます。 イベントは、ブロックされた各タスクの報告間隔ごとに 1 回生成されます。  
  
 ブロックされたプロセスのレポートは、ベスト エフォートの原則で行われます。 リアルタイムまたはリアルタイムに近い報告は保証されていません。  
  
 この設定は、サーバーを停止して再起動しなくてもすぐに有効になります。  
  
## <a name="examples"></a>使用例  
 次の例では、 `blocked process threshold` を `20` 秒に設定して、ブロックされたタスクごとに、ブロックされたプロセスのレポートを生成します。  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
sp_configure 'blocked process threshold', 20 ;  
GO  
RECONFIGURE ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Blocked Process Report イベント クラス](../../relational-databases/event-classes/blocked-process-report-event-class.md)  
  
  
