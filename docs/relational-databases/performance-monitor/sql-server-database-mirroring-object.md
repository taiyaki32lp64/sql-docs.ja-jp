---
title: SQL Server:Database Mirroring オブジェクト | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Database Mirroring
- database mirroring [SQL Server], performance counters
- performance counters [SQL Server], database mirroring
- Database Mirroring object
ms.assetid: a27b51ee-7637-4525-9424-bcc16947dc13
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 639d661dd9a7196119bbb34f11f0ed5a9161a978
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986677"
---
# <a name="sql-server-database-mirroring-object"></a>SQL Server:Database Mirroring オブジェクト
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **SQLServer:Database Mirroring** パフォーマンス オブジェクトには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータベース ミラーリングに関する情報を報告するパフォーマンス カウンターが含まれています。 次の表は、このオブジェクトに含まれているカウンターを示します。  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|**Bytes Received/sec**|1 秒間に受信されたバイト数。|  
|**Bytes Sent/sec**|1 秒間に送信されたバイト数。|  
|**受信ログ バイト数/秒**|1 秒間に受信されたログのバイト数。|  
|**Log Bytes Redone from Cache/sec**|最後の 1 秒間にミラーリング ログ キャッシュから取得された再実行ログ バイト数。<br /><br /> このカウンターは、ミラー サーバーのみで使用されます。 プリンシパル サーバーでは、値は常に 0 です。|  
|**Log Bytes Sent from Cache/sec**|最後の 1 秒間にミラーリング ログ キャッシュから取得された送信ログ バイト数。<br /><br /> このカウンターは、プリンシパル サーバーのみで使用されます。 ミラー サーバーでは、値は常に 0 です。|  
|**Log Bytes Sent/sec**|1 秒間に送信されたログのバイト数。|  
|**Log Compressed Bytes Rcvd/sec**|最後の 1 秒間に受信したログの圧縮バイト数。|  
|**Log Compressed Bytes Sent/sec**|最後の 1 秒間に送信したログの圧縮バイト数。|  
|**Log Harden Time (ms)**|最後の 1 秒間にディスクへのログ ブロックの書き込みを待機したミリ秒数。|  
|**Log Remaining for Undo KB**|フェールオーバー後に新しいミラー サーバーによって引き続きスキャンされるログの合計 KB 数。<br /><br /> このカウンターは、元に戻すフェーズの間、ミラー サーバーのみで使用されます。 元に戻すフェーズが完了すると、カウンターは 0 にリセットされます。 プリンシパル サーバーでは、値は常に 0 です。|  
|**Log Scanned for Undo KB**|フェールオーバー以降に新しいミラー サーバーによってスキャンされたログの合計 KB 数。<br /><br /> このカウンターは、元に戻すフェーズの間、ミラー サーバーのみで使用されます。 元に戻すフェーズが完了すると、カウンターは 0 にリセットされます。 プリンシパル サーバーでは、値は常に 0 です。|  
|**Log Send Flow Control Time (ms)**|最後の 1 秒間にログ ストリーム メッセージが送信フロー制御を待機したミリ秒数。<br /><br /> ミラーリング パートナーへのログ データとメタデータの送信は、データベース ミラーリングにおける最もデータが集中する操作で、データベース ミラーリングおよび Service Broker の送信バッファーを占有する可能性があります。 このカウンターを使用すると、データベース ミラーリング セッションによる送信バッファーの使用を監視できます。|  
|**Log Send Queue KB**|ミラー サーバーにまだ送信されていないログの合計 KB 数。|  
|**Mirrored Write Transactions/sec**|最後の 1 秒間に、ミラー化されたデータベースに書き込んだトランザクションのうち、コミットするためにログがミラーに送信されるのを待機したトランザクションの数。<br /><br /> このカウンターは、プリンシパル サーバーがミラー サーバーにログ レコードをアクティブに送信しているときだけ増加します。|  
|**Pages Sent/sec**|1 秒間に送信されたページ数。|  
|**Receives/sec**|1 秒間に受信されたミラーリング メッセージの数。|  
|**Redo Bytes/sec**|ミラー データベースで 1 秒間にロールフォワードされたログのバイト数。|  
|**Redo Queue KB**|再実行用として書き込まれたログのうち、ロールフォワードするためにまだミラー データベースに適用されていないログの合計 KB 数。 このログは、ミラー サーバーからプリンシパル サーバーに送信されます。|  
|**Send/Receive Ack Time**|最後の 1 秒間にメッセージがパートナーからの受信確認を待機したミリ秒数。<br /><br /> このカウンターは、不明なフェールオーバー、多数の送信キュー、トランザクションの長い遅延など、ネットワークのボトルネックによって発生する可能性のある問題のトラブルシューティングに役立ちます。 そのような場合、このカウンターの値を分析することで、問題の原因となっているのがネットワークかどうかを判断できます。|  
|**Sends/sec**|1 秒間に送信されたミラーリング メッセージの数。|  
|**Transaction Delay**|終了していないコミットの確認を待機中に生じた遅延。|  
  
> [!NOTE]  
>  各パートナーでは、一部のカウンターの値が 0 を示します。値が 0 になるカウンターは、パートナーが現在担っている役割によって異なります。  
  
## <a name="remarks"></a>Remarks  
 パフォーマンス カウンターを使用して、データベース ミラーリングのパフォーマンスを監視できます。 たとえば、データベース ミラーリングがプリンシパル サーバーのパフォーマンスに影響を及ぼしているかどうかを確認するには、 **Transaction Delay** カウンターを調べることができます。また、ミラー データベースとプリンシパル データベース間の遅延時間がいかに少ないかを確認するには、 **Redo Queue** カウンターと **Log Send Queue** カウンターを調べることができます。 1 秒間に送信されたログの量を監視する場合は、 **Log Bytes Sent/sec** カウンターを調べることができます。  
  
## <a name="see-also"></a>参照  
 [リソースの利用状況の監視 &#40;システム モニター&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
