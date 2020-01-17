---
title: 拡張イベント ログの診断情報へのアクセス | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a79e9468-2257-4536-91f1-73b008c376c3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1f4dfb22027ca448848d7027232e41359ff1664d
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028492"
---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>拡張イベント ログの診断情報へのアクセス
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] では、トレース ([ドライバー操作のトレース](../../connect/jdbc/tracing-driver-operation.md)) が更新されました。サーバーの接続リング バッファーおよび拡張イベント ログ内のアプリケーション パフォーマンス情報から、接続エラーなどの診断情報にクライアント イベントを関連付けやすくなっています。 拡張イベント ログを表示する方法については、「[イベント セッション データの表示](https://msdn.microsoft.com/library/hh710068(SQL.110).aspx)」を参照してください。  
  
## <a name="details"></a>詳細  
 接続操作では、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] によってクライアント接続 ID が送信されます。 接続に失敗した場合は、接続リング バッファー ([接続リング バッファーによる SQL Server 2008 での接続トラブルシューティング](https://go.microsoft.com/fwlink/?LinkId=207752)) にアクセスし、**ClientConnectionID** フィールドを見つけて、接続エラーに関する診断情報を取得することができます。 クライアント接続 ID は、エラーが発生した場合にのみリング バッファーに記録されます (ログイン前のパケットを送信する前に接続に失敗した場合、クライアント接続 ID は生成されません)。クライアント接続 ID は 16 バイトの GUID です。 また、**client_connection_id** 操作を拡張イベント セッションのイベントに追加すると、拡張イベントのターゲット出力でクライアント接続 ID を検索することもできます。 クライアント ドライバーの詳しい診断サポートが必要な場合は、トレースを有効にして、接続コマンドを再実行し、トレース内の **ClientConnectionID** フィールドを調べます。  
  
 [ISQLServerConnection インターフェイス](../../connect/jdbc/reference/isqlserverconnection-interface.md)を使用して、プログラムでクライアント接続 ID を取得できます。 接続 ID は接続関連の例外にも含まれます。  
  
 接続エラーが発生する場合、サーバーの Built In Diagnostics (BID) トレース情報および接続リング バッファーに含まれるクライアント接続 ID を使用すると、クライアント接続をサーバー上の接続に関連付けることができます。 サーバー上の BID トレースの詳細については、「[SQL Server 2008 でのデータ アクセスのトレース](https://go.microsoft.com/fwlink/?LinkId=125805)」を参照してください。 データ アクセスのトレースに関する記事には、データ アクセスのトレースに関する情報も含まれていますが、これは [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] には当てはまりません。[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] を使用してデータ アクセスのトレースを実行する方法については、「[ドライバー操作のトレース](../../connect/jdbc/tracing-driver-operation.md)」を参照してください。  
  
 JDBC Driver からは、スレッド固有のアクティビティ ID も送信されます。 アクティビティ ID は、TRACK_CAUSAILITY オプションを有効にしてセッションを開始した場合、拡張イベント セッションでキャプチャされます。 アクティブな接続に関するパフォーマンスの問題については、クライアントのトレース (ActivityID フィールド) からアクティビティ ID を取得し、このアクティビティ ID を拡張イベント出力で探すことができます。 拡張イベント内のアクティビティ ID とは、16 バイトの GUID (クライアント接続 ID の GUID とは異なる) の後に 4 バイトのシーケンス番号が付いたものです。 このシーケンス番号は、スレッド内の要求順序を表しています。 ActivityId は、SQL バッチ ステートメントおよび RPC 要求用に送信されます。 ActivityId をサーバーに送信できるようにするには、まず Logging.Properties ファイル内で次のキー/値ペアを指定する必要があります。  
  
```
com.microsoft.sqlserver.jdbc.traceactivity = on  
```  
  
 `on` (大文字小文字を区別) 以外の値の場合には、ActivityId の送信は無効になります。  
  
 詳細については、「[ドライバー操作のトレース](../../connect/jdbc/tracing-driver-operation.md)」を参照してください。 このトレース フラグは、JDBC Driver で ActivityId をトレースおよび送信するかどうかを決定するために、対応する JDBC オブジェクト ロガーと共に使用されます。 Logging.Properties ファイルの更新に加えて、ロガー com.microsoft.sqlserver.jdbc を FINER 以上で有効にする必要があります。 特定のクラスによる要求に対してサーバーに ActivityId を送信する場合は、対応するクラス ロガーを FINER または FINEST で有効にする必要があります。 たとえば、クラスが SQLServerStatement であれば、ロガー com.microsoft.sqlserver.jdbc.SQLServerStatement を有効にします。  
  
 次のサンプルでは、[!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、拡張イベント セッションを開始しています。この拡張イベント セッションはリング バッファーに格納され、RPC 操作およびバッチ操作でクライアントから送信されたアクティビティ ID を記録します。  
  
```sql
create event session MySession on server  
add event connectivity_ring_buffer_recorded,  
add event sql_statement_starting (action (client_connection_id)),  
add event sql_statement_completed (action (client_connection_id)),  
add event rpc_starting (action (client_connection_id)),  
add event rpc_completed (action (client_connection_id))  
add target ring_buffer with (track_causality=on)  
```  
  
## <a name="see-also"></a>参照  
 [JDBC ドライバーに関する問題の診断](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
