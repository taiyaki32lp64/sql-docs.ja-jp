---
title: system_health セッションの使用 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], system health session
- extended events [SQL Server], system_health session
- system_health session [SQL Server extended events]
- system health session [SQL Server extended events]
ms.assetid: 1e1fad43-d747-4775-ac0d-c50648e56d78
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 6ea2e46b38919ae72ea70440523d75517e6efa92
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62512554"
---
# <a name="use-the-systemhealth-session"></a>system_health セッションの使用
  system_health セッションは、既定で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に含まれている拡張イベント セッションです。 このセッションは、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] の起動時に自動的に開始されます。実行中にパフォーマンスに大きな影響が及ぶことはありません。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のパフォーマンスの問題をトラブルシューティングするのに役立つシステム データを収集します。 そのため、このセッションを停止または削除しないことをお勧めします。  
  
 このセッションでは、次の情報を収集します。  
  
-   重大度が 20 以上のエラーが発生したすべてのセッションの sql_text と session_id。  
  
-   メモリ関連のエラーが発生したすべてのセッションの sql_text とsession_id。 エラーには、17803、701、802、8645、8651、8657、8902 などがあります。  
  
-   応答していないスケジューラの問題の記録 (これらはエラー 17883 として [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログに書き込まれます)。  
  
-   検出されたすべてのデッドロック。  
  
-   ラッチ (またはその他の注目する必要があるリソース) での待機時間が 15 秒を超えるすべてのセッションの callstack、sql_text、および session_id。  
  
-   ロックでの待機時間が 30 秒を超えるすべてのセッションの callstack、sql_text、および session_id。  
  
-   プリエンプティブ待機のために長時間待機しているすべてのセッションの callstack、sql_text、および session_id。 待機時間は、待機の種類によって異なります。 プリエンプティブ待機とは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が外部の API 呼び出しを待機している状態です。  
  
-   CLR の割り当てと仮想の割り当ての失敗に対する呼び出し履歴と session_id。  
  
-   メモリ ブローカー、スケジューラ モニター、メモリ ノード OOM、セキュリティ、接続性に関する ring_buffer イベント。  
  
-   sp_server_diagnostics からのシステム コンポーネントの結果。  
  
-   scheduler_monitor_system_health_ring_buffer_recorded によって収集されたインスタンスの正常性。  
  
-   CLR 割り当ての失敗。  
  
-   connectivity_ring_buffer_recorded を使用する接続のエラー。  
  
-   security_error_ring_buffer_recorded を使用するセキュリティのエラー。  
  
## <a name="viewing-the-session-data"></a>セッション データの表示  
 このセッションでは、リング バッファー ターゲットを使用して、データを格納します。 セッション データを表示するには、次のクエリを使用します。  
  
```  
SELECT CAST(xet.target_data as xml) FROM sys.dm_xe_session_targets xet  
JOIN sys.dm_xe_sessions xe  
ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'system_health'  
```  
  
 イベント ファイルからセッション データを表示するには、Management Studio の拡張イベント ユーザー インターフェイスを使用します。 参照してください[イベント セッション データの表示](../../database-engine/view-event-session-data.md)詳細についてはします。  
  
## <a name="restoring-the-systemhealth-session"></a>system_health セッションの復元  
 system_health セッションを削除した場合、クエリ エディターで **u_tables.sql** ファイルを実行することでそのセッションを復元できます。 このファイルは次のフォルダーにあります (C: は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プログラム ファイルのインストール先ドライブを表しています)。  
  
 C:\Program Files\Microsoft SQL Server\MSSQL12.\<*instanceid*>\MSSQL\Install  
  
 セッションを復元したら、ALTER EVENT SESSION ステートメントを使用するか、オブジェクト エクスプローラーで **[拡張イベント]** ノードを使用して、セッションを開始する必要があります。 ただし、そのようにして開始しない場合でも、次に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを再起動したときにセッションは自動的に開始されます。  
  
## <a name="see-also"></a>参照  
 [拡張イベントのツール](extended-events-tools.md)  
  
  
