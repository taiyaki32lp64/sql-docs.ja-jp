---
title: sys.database_event_sessions (Azure SQL データベース) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 02c2cd71-d35e-4d4c-b844-92b240f768f4
author: MightyPen
ms.author: genemi
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 4ef8388e18ee73a0f1217e4e04adc13379892520
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915082"
---
# <a name="sysdatabaseeventsessions-azure-sql-database"></a>sys.database_event_sessions (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  現在のデータベースに存在するすべてのイベント セッション定義を一覧表示[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]します。  
  
> [!NOTE]
>  という名前のようなカタログ ビュー`sys.server_event_sessions`にのみ適用されます[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
||  
|-|  
|**適用対象**: [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]、およびそれ以降のバージョン。|  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|イベント セッションの一意な ID。 NULL 値は許可されません。|  
|NAME|**sysname**|ユーザー定義のイベント セッションを識別する名前。 名前は一意にです。 NULL 値は許可されません。|  
|event_retention_mode|**nchar(1)**|イベントの損失を処理する方法を決定します。 既定値は S です。NULL 値は許可されません。 次のいずれかを指定します。<br /><br /> S. マップ event_retention_mode_desc = ALLOW_SINGLE_EVENT_LOSS。<br /><br /> M. マップ event_retention_mode_desc = ALLOW_MULTIPLE_EVENT_LOSS。<br /><br /> N. マップ event_retention_mode_desc = NO_EVENT_LOSS。|  
|event_retention_mode_desc|**sysname**|イベントの損失を処理する方法について説明します。 既定値は ALLOW_SINGLE_EVENT_LOSS です。 NULL 値は許可されません。 次のいずれかを指定します。<br /><br /> ALLOW_SINGLE_EVENT_LOSS。 イベントは、セッションから削除できます。 1 つのイベントは、すべてのイベント バッファーがいっぱいの場合にのみ削除されます。 イベント バッファーがいっぱいのときに単独のイベントを削除することで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のパフォーマンス特性が許容可能な状態になり、処理後のイベント ストリームでの損失を最小限に抑えることができます。<br /><br /> ALLOW_MULTIPLE_EVENT_LOSS します。 いっぱいイベント バッファーをセッションから削除できます。 削除されるイベントの数は、メモリ、およびバッファー内のイベントのサイズのパーティション分割、セッションに割り当てられたメモリのサイズによって異なります。 このオプションを使用すると、イベント バッファーがすぐにいっぱいになるときにサーバーのパフォーマンスに与える影響を最小限に抑えることができます。 ただし、多数のイベントは、セッションから削除できます。<br /><br /> NO_EVENT_LOSS。 イベントの削除は許可されません。 このオプションにより発生したすべてのイベントが保存されるようになります。 このオプションを使用して、イベント バッファーに空き領域があるまで待機するイベントを発生させるすべてのタスクを強制します。 これは、イベント セッションがアクティブな間、検出可能なパフォーマンスが低下する可能性があります。|  
|max_dispatch_latency|**int**|イベントをセッション ターゲットに渡す前にメモリにバッファリングする時間 (ミリ秒単位)。 有効な値は 1 に 2147483648 および-1 です。 値-1 は、ディスパッチ待機時間が無制限であることを示します。 NULL 値が許可されます。|  
|max_memory|**int**|イベントのバッファリング用にセッションに割り当てられたメモリの量。 既定値は、4 MB です。 NULL 値が許可されます。|  
|max_event_size|**int**|イベント セッション バッファーに収まらないイベント用に確保するメモリの量。 計算されたバッファー サイズを max_event_size が超える場合、サイズが max_event_size のバッファーが追加で 2 つイベント セッションに割り当てられます。 NULL 値が許可されます。|  
|memory_partition_mode|**nchar(1)**|イベント バッファーを作成するメモリ内の場所。 既定のパーティション モードは G です。NULL 値は許可されません。 memory_partition_mode はの 1 つです。<br /><br /> G : NONE<br /><br /> C: PER_CPU<br /><br /> N: PER_NODE|  
|memory_partition_mode_desc|**sysname**|既定では NONE です。 NULL 値は許可されません。 次のいずれかを指定します。<br /><br /> NONE。 1 つのバッファー セットが SQL Server インスタンス内で作成されます。<br /><br /> PER_CPU します。 Cpu ごとのバッファー セットが作成されます。<br /><br /> PER_NODE。 各、non-uniform memory access (NUMA) ノードのバッファー セットが作成されます。|  
|track_causality オプション|**bit**|有効または因果関係の追跡を無効にします。 追跡 1 (ON) に設定されている場合、別のサーバー接続で有効になっていると、関連するイベントを関連付けることができます。 既定値は 0 (OFF) です。 NULL 値は許可されません。|  
|startup_state|**bit**|値は、サーバーの起動時に自動的にセッションが開始するかどうかを決定します。 既定値は 0 です。 NULL 値は許可されません。 いずれかです。<br /><br /> 0 (OFF) です。 セッションは、サーバーの起動時には開始されません。<br /><br /> 1 (ON)。 サーバーの起動時にイベント セッションが開始されます。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
  
