---
title: 一括コピー バッチ サイズの管理 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- ODBC, bulk copy operations
- batches [ODBC]
- bulk copy [ODBC], batch sizes
ms.assetid: 4b24139f-788b-45a6-86dc-ae835435d737
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 07f87bf0f231419e4f1345369211ba6ceebf1d12
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199174"
---
# <a name="managing-bulk-copy-batch-sizes"></a>一括コピー バッチ サイズの管理
  一括コピー操作でバッチを使用する主な目的は、トランザクションのスコープを定義することです。 一括コピー関数では、バッチ サイズが設定されていないと、一括コピー全体を 1 つのトランザクションと見なします。 バッチ サイズが設定されている場合、各バッチはそのバッチの終了時にコミットされるトランザクションで構成されます。  
  
 バッチ サイズを指定せずに一括コピーを実行し、エラーが発生した場合は、一括コピー全体がロールバックされます。 実行時間が長い一括コピーの復旧には時間がかかることがあります。 バッチ サイズを設定すると、各バッチが 1 つのトランザクションと見なされ、各バッチがコミットされます。 エラーが発生した場合は、最後の未解決のバッチだけがロールバックされます。  
  
 バッチ サイズは、ロックのオーバーヘッドにも影響を与えることがあります。 に対して一括コピーを実行するときに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を使用して TABLOCK ヒントを指定できます[bcp_control](../native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)行ロックではなくテーブル ロックを取得します。 1 つのテーブル ロックを設定すると、一括コピー操作全体のオーバーヘッドを最小限に抑えることができます。 TABLOCK を指定しないと各行がロックされるので、一括コピーの実行中にすべてのロックを保持するオーバーヘッドにより、パフォーマンスが低下することがあります。 トランザクションの長さだけロックが保持されるので、バッチ サイズを指定すると、定期的にコミットが発生して、その時点で保持されているロックが解放されるため、この問題を解決できます。  
  
 大量の行を一括コピーする場合、1 つのバッチを構成する行数がパフォーマンスに大きな影響を与えることがあります。 推奨バッチ サイズは、実行する一括コピーの種類によって異なります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への一括コピーを行う場合は、TABLOCK 一括コピー ヒントを指定し、大きなバッチ サイズを設定します。  
  
-   TABLOCK を指定しない場合は、バッチ サイズを 1,000 行未満に制限します。  
  
 バッチ サイズが呼び出すことによって指定された一括コピー データ ファイルから、 **bcp_control**を呼び出す前に BCPBATCH オプション[bcp_exec](../native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)します。 一括を使用してプログラム変数からコピーする場合[bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)と[bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)、バッチ サイズが呼び出すことによって制御される[bcp_batch](../native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md)呼び出した後[bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) *x*回*x*はバッチ内の行の数です。  
  
 バッチはトランザクションのサイズを指定するだけでなく、ネットワーク経由でサーバーに行を送信するときにも影響を与えます。 一括コピー関数は通常の行をキャッシュ**bcp_sendrow**まで、ネットワーク パケットが入力し、サーバーに完全なパケットを送信します。 アプリケーションを呼び出すと**bcp_batch**、ただし、現在のパケットがいっぱいになったかどうかに関係なく、サーバーに送信します。 バッチ サイズを非常に小さくすると、いっぱいになっていないパケットが大量にサーバーに送信されるので、パフォーマンスが低下することがあります。 たとえば、呼び出し**bcp_batch**後すべて**bcp_sendrow**により各の行を個別にパケットで送信され、行が非常に大きい場合を除き、各パケット内の領域を浪費します。 アプリケーションが呼び出すことによって、サイズを変更できますが、SQL Server のネットワーク パケットの既定のサイズは 4 KB、 [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md)から SQL_ATTR_PACKET_SIZE 属性を指定します。  
  
 バッチのもう 1 つの副作用がある各バッチでは、未解決の結果セットが完了するとまでは考慮**bcp_batch**します。 バッチが未解決、中に、接続ハンドルで他の操作が試行した場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、エラーを発行 sqlstate ="HY000"のエラー メッセージ文字列。  
  
```  
"[Microsoft][SQL Server Native Client] Connection is busy with  
results for another hstmt."  
```  
  
## <a name="see-also"></a>参照  
 [一括コピー操作を実行する&#40;ODBC&#41;](performing-bulk-copy-operations-odbc.md)   
 [データの一括インポートと一括エクスポート &#40;SQL Server&#41;](../import-export/bulk-import-and-export-of-data-sql-server.md)  
  
  
