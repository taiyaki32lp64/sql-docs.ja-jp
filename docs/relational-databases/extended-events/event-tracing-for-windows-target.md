---
title: Event Tracing for Windows ターゲット
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- event tracing for windows target
- ETW target
- targets [SQL Server extended events], event tracing for windows target
ms.assetid: ca2bb295-b7f6-49c3-91ed-0ad4c39f89d5
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8923769d3edb35b328c9b0351fd9700ff9168c6c
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75234663"
---
# <a name="event-tracing-for-windows-target"></a>Event Tracing for Windows ターゲット

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Event Tracing for Windows (ETW) をターゲットとして使用する前に、ETW を活用するための知識を身に付けておくことをお勧めします。 ETW トレースは、拡張イベントと組み合わせて使用されるか、拡張イベントのイベント コンシューマーとして使用されます。 ETW の背景情報については、次の外部リンクを参照してください。  
  
-   [Windows イベント](https://go.microsoft.com/fwlink/?LinkId=92380)  
  
-   [ETW によりデバッグおよびパフォーマンス調整を改善する](https://go.microsoft.com/fwlink/?LinkId=92381)  
  
 ETW ターゲットは、多くのセッションに追加できますが、シングルトン ターゲットです。 多くのセッションでイベントが発生した場合、イベントは、イベントの発生ごとに 1 回、ETW ターゲットのみに反映されます。 拡張イベント エンジンは、プロセスあたり 1 つのインスタンスに制限されます。  
  
> [!IMPORTANT]  
>  ETW ターゲットを動作させるには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス開始アカウントが Performance Log Users グループのメンバーであることが必要です。  
  
 ETW セッションに存在するイベントの構成は、拡張イベント エンジンがホストするプロセスによって制御されます。 拡張イベント エンジンは、どのイベントを発生させるか、どのような条件が満たされた場合にイベントを発生させるかを制御します。  
  
 拡張イベント セッションへのバインド後、つまり、プロセスの有効期間中に初めて ETW ターゲットがアタッチされたとき、ETW ターゲットは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロバイダー上で単一の ETW セッションを開きます。 ETW セッションが既に存在していた場合、ETW ターゲットは、既存のセッションへの参照を取得します。 この ETW セッションは、特定のコンピューター上のすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス間で共有されます。 ETW ターゲットが割り当てられているセッションで発生したすべてのイベントは、この ETW セッションが受け取ることになります。  
  
 ETW では、プロバイダーがイベントを利用して、それを ETW に渡すことができるようになっている必要があります。そのため、セッションでは、すべての拡張イベント パッケージが有効化されます。 ETW ターゲットは、発生したイベントを、そのイベントのプロバイダーが有効になっているセッションへ送信します。  
  
 ETW ターゲットは、発生元スレッドでのイベントの同期発行をサポートします。 イベントの非同期発行はサポートしません。  
  
 ETW ターゲットは、外部 ETW コントローラー (たとえば Logman.exe) からのコントロールをサポートしません。 ETW トレースを生成するには、ETW ターゲットを使用してイベント セッションを作成する必要があります。 詳細については、「 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)」を参照してください。  
  
> [!NOTE]  
>  ETW ターゲットを有効にすると、XE_DEFAULT_ETW_SESSION という名前の ETW セッションが作成されます。 XE_DEFAULT_ETW_SESSION という名前のセッションが既に存在する場合は、既存のセッションのプロパティを変更せずに使用されます。 XE_DEFAULT_ETW_SESSION はすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス間で共有されます。 XE_DEFAULT_ETW_SESSION を開始した後に停止する場合は、Logman ツールなどの ETW コントローラーを使用する必要があります。 たとえば、コマンド プロンプトで **logman stop XE_DEFAULT_ETW_SESSION -ets**コマンドを実行できます。  
  
 次の表では、ETW ターゲットの構成に使用できるオプションについて説明します。  
  
|オプション|使用できる値|[説明]|  
|------------|--------------------|-----------------|  
|default_xe_session_name|256 文字までの任意の文字列。 この値は省略可能です。|拡張イベント セッション名。 既定値は、XE_DEFAULT_ETW_SESSION です。|  
|default_etw_session_logfile_path|256 文字までの任意の文字列。 この値は省略可能です。|拡張イベント セッションのログ ファイルへのパス。 既定値は %TEMP%\ XEEtw.etl です。|  
|default_etw_session_logfile_size_mb|任意の符号なし整数。 この値は省略可能です。|拡張イベント セッションのログ ファイル サイズ (MB)。 既定値は 20 MB です。|  
|default_etw_session_buffer_size_kb|任意の符号なし整数。 この値は省略可能です。|拡張イベント セッションのメモリ内バッファーのサイズ (KB)。 既定値は 128 KB です。|  
|retries|任意の符号なし整数。|ETW サブシステムへのイベントのパブリッシュを再試行する回数。この回数を超えるとイベントが破棄されます。 既定値は 0 です。|  
| &nbsp; | &nbsp; | &nbsp; |

 これらの設定は省略できます。 これらの設定については既定値が使用されます。  
  
 ETW ターゲットには、次のような役割があります。  
  
-   既定の ETW セッションを作成する。  
  
-   すべての拡張イベント パッケージを ETW に登録する。 これによって、ETW に登録されたイベントは破棄されなくなります。  
  
-   ETW に対するイベント フローを管理する。 ETW ターゲットは、拡張イベント データを持つ ETW イベントを作成して、それを適切な ETW セッションに送信します。 イベントがバッファー サイズを超えた場合、またはデータを 1 つの ETW イベントに収めることができなかった場合、そのイベントは ETW によって複数のフラグメントに分割されます。  
  
-   拡張イベント パッケージを常時有効に保つ。  
  
 次に ETW で使用される既定のファイル パスを示します。  
  
-   ETW 出力ファイルは %TEMP%\XEEtw.etl に格納されます。  
  
    > [!IMPORTANT]  
    >  最初のセッションの開始後にファイル パスを変更することはできません。  
  
-   マネージド オブジェクト フォーマット (MOF) ファイルは *\<インストール パス&gt;* \Microsoft SQL Server\Shared に格納されます。 詳細については、MSDN の「[マネージド オブジェクト フォーマット](https://go.microsoft.com/fwlink/?LinkId=92851)」を参照してください。

<!-- ?LinkId=92851  ==  https://docs.microsoft.com/windows/desktop/WmiSdk/managed-object-format--mof-
-->

## <a name="adding-the-target-to-a-session"></a>セッションへのターゲットの追加  
 ETW ターゲットを拡張イベント セッションに追加するには、イベント セッションの作成時または変更時に次のステートメントを含める必要があります。  
  
```sql
ADD TARGET package0.etw_classic_sync_target  
```  
  
 データの表示方法を含む、ETW ターゲットの使用法を示す完全な例の詳細については、「 [拡張イベントを使用したシステムの使用状況の監視](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server 拡張イベント ターゲット](targets-for-extended-events-in-sql-server.md)   
 [sys.dm_xe_session_targets &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql.md)   
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)  
  
  
