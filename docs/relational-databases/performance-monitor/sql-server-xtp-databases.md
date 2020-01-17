---
title: SQL Server XTP Databases | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQL Server 2016 XTP Databases
ms.assetid: 488ff55e-173f-43f6-9bdb-67b35e7cebfe
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 01336bc87411fec167a3f78dfd3bf397a93b6d2c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947797"
---
# <a name="sql-server-xtp-databases"></a>SQL Server XTP Databases
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**SQL Server XTP Databases** パフォーマンス オブジェクトは、インメモリ OLTP データベース固有のカウンターを提供します。

> [!NOTE]
>  現在、SQL Server XTP Databases カウンターは、sys.dm_os_performance_counters からは表示できません。  [システム モニター](../../relational-databases/performance/start-system-monitor-windows.md)で表示することはできます。

次の表では、 **SQL Server XTP Databases** カウンターについて説明します。

|カウンター|[説明]| 
|-------------|-----------------|  
|**Avg Transaction Segment Large Data Size**|トランザクション セグメントの大きいデータ ペイロードの平均サイズ。 これは非常に低レベルのカウンターであり、お客様による使用は想定されていません。|
|**Avg Transaction Segment Size**|トランザクション セグメントのペイロードの平均サイズ。 この値がゼロになると、バックエンド アロケーターからより多くのページが割り当てられます。 これは非常に低レベルのカウンターであり、お客様による使用は想定されていません。|
|**Flush Thread 256K Queue Depth**|256 K I/O 要求のフラッシュ スレッド キューの深さ。|
|**Flush Thread 4K Queue Depth**|4 K I/O 要求のフラッシュ スレッド キューの深さ。|
|**Flush Thread 64K Queue Depth**|64 K I/O 要求のフラッシュ スレッド キューの深さ。|
|**Flush Thread Frozen IOs/sec (256K)**|ページのフラッシュ処理の間に発生した 256 K IO 要求のうち、フリーズしきい値より大きいので発行できないものの数。|
|**Flush Thread Frozen IOs/sec (4K)**|ページのフラッシュ処理の間に発生した 4 K IO 要求のうち、フリーズしきい値より大きいので発行できないものの数。|
|**Flush Thread Frozen IOs/sec (64K)**|ページのフラッシュ処理の間に発生した 64 K IO 要求のうち、フリーズしきい値より大きいので発行できないものの数。|
|**IoPagePool256K Free List Count**|256 K IO ページ プール空きリスト内のページの数。 この値がゼロになると、バックエンド アロケーターからより多くのページが割り当てられます。 これは非常に低レベルのカウンターであり、お客様による使用は想定されていません。|
|**IoPagePool256K Total Allocated**|バックエンド アロケーターから割り当てられて 256 K IO ページ プールによって保持されているページの合計数。 これは非常に低レベルのカウンターであり、お客様による使用は想定されていません。|
|**IoPagePool4K Free List Count**|4 K IO ページ プール空きリスト内のページの数。 この値がゼロになると、バックエンド アロケーターからより多くのページが割り当てられます。 これは非常に低レベルのカウンターであり、お客様による使用は想定されていません。|
|**IoPagePool4K Total Allocated**|バックエンド アロケーターから割り当てられて 4 K IO ページ プールによって保持されているページの合計数。 これは非常に低レベルのカウンターであり、お客様による使用は想定されていません。|
|**IoPagePool64K Free List Count**|64 K IO ページ プール空きリスト内のページの数。 この値がゼロになると、バックエンド アロケーターからより多くのページが割り当てられます。 これは非常に低レベルのカウンターであり、お客様による使用は想定されていません。|
|**IoPagePool64K Total Allocated**|バックエンド アロケーターから割り当てられて 64 K IO ページ プールによって保持されているページの合計数。 これは非常に低レベルのカウンターであり、お客様による使用は想定されていません。|
|**MtLog 256K Expand Count**|256 K MtLog が拡張された回数。 これは非常に低レベルのカウンターであり、お客様による使用は想定されていません。|
|**MtLog 256K IOs Outstanding**|MtLog から発行された未解決の 256 K IO 要求の数。|
|**MtLog 256K Page Fill %/Page Flushed**|フラッシュされた各 256 K MtLog ページの平均の使用済み割合。 これは非常に低レベルのカウンターであり、お客様による使用は想定されていません。|
|**MtLog 256K Write Bytes/sec**|256 K MtLog オブジェクトでの 1 秒あたりの書き込みバイト数。 これは非常に低レベルのカウンターであり、お客様による使用は想定されていません。|
|**MtLog 4K Expand Count**|4 K MtLog が拡張された回数。 これは非常に低レベルのカウンターであり、お客様による使用は想定されていません。|
|**MtLog 4K IOs Outstanding**|MtLog から発行された未解決の 4 K IO 要求の数。|
|**MtLog 4K Page Fill %/Page Flushed**|フラッシュされた各 4 K MtLog ページの平均の使用済み割合。 これは非常に低レベルのカウンターであり、お客様による使用は想定されていません。|
|**MtLog 4K Write Bytes/sec**|4 K MtLog オブジェクトでの 1 秒あたりの書き込みバイト数。 これは非常に低レベルのカウンターであり、お客様による使用は想定されていません。|
|**MtLog 64K Expand Count**|64 K MtLog が拡張された回数。 これは非常に低レベルのカウンターであり、お客様による使用は想定されていません。|
|**MtLog 64K IOs Outstanding**|MtLog から発行された未解決の 64 K IO 要求の数。|
|**MtLog 64K Page Fill %/Page Flushed**|フラッシュされた各 64 K MtLog ページの平均の使用済み割合。 これは非常に低レベルのカウンターであり、お客様による使用は想定されていません。|
|**MtLog 64K Write Bytes/sec**|64 K MtLog オブジェクトでの 1 秒あたりの書き込みバイト数。 これは非常に低レベルのカウンターであり、お客様による使用は想定されていません。|
|**Num Merges**|処理中のマージの数。|
|**Num Merges/sec**|1 秒間に作成されたマージの数 (平均)。|
|**Num Serializations**|処理中のシリアル化の数。|
|**Num Serializations/sec**|1 秒間に作成されたシリアル化の数 (平均)。|
|**Tail Cache Page Count**|テール キャッシュに割り当てられたページの数。 これは非常に低レベルのカウンターであり、お客様による使用は想定されていません。|
|**Tail Cache Page Count Peak**|テール キャッシュに割り当てられたページの最大数。 これは非常に低レベルのカウンターであり、お客様による使用は想定されていません。|


## <a name="see-also"></a>参照  
[SQL Server XTP &#40;インメモリ OLTP&#41; パフォーマンス カウンター](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)
