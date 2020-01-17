---
title: sp_trace_create (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_create_TSQL
- sp_trace_create
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_create
ms.assetid: f3a43597-4c5a-4520-bcab-becdbbf81d2e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7d698932bb7ef7e0fd37a0ced8ab536eeb0d5d68
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096031"
---
# <a name="sptracecreate-transact-sql"></a>sp_trace_create (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  トレース定義を作成します。 新しいトレースは停止状態になります。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに拡張イベントを使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_trace_create [ @traceid = ] trace_id OUTPUT   
          , [ @options = ] option_value   
          , [ @tracefile = ] 'trace_file'   
     [ , [ @maxfilesize = ] max_file_size ]  
     [ , [ @stoptime = ] 'stop_time' ]  
     [ , [ @filecount = ] 'max_rollover_files' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @traceid = ] trace_id` によって割り当てられた番号[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]新しいトレースにします。 任意のユーザーの入力は無視されます。 *trace_id*は**int**、既定値は NULL です。 ユーザーが採用して、 *trace_id*識別、変更、およびこのストアド プロシージャが定義されているトレースを制御する値。  
  
`[ @options = ] option_value` トレースの設定オプションを指定します。 *option_value*は**int**、既定値はありません。 ユーザーは複数のオプションの組み合わせを選択することもできます。これにはオプションの合計値を指定します。 たとえば、TRACE_FILE_ROLLOVER と SHUTDOWN_ON_ERROR の両方のオプションをオンにする次のように指定します。 **6**の*option_value*します。  
  
 次の表は、オプション、説明、およびその値を示します。  
  
|オプション名|オプション値|説明|  
|-----------------|------------------|-----------------|  
|TRACE_FILE_ROLLOVER|**2**|指定する場合、 *max_file_size*に達すると、現在のトレース ファイルが閉じられるし、新しいファイルが作成されます。 新しいファイルには、すべての新しいレコードが書き込まれます。 新しいファイルは以前のファイルと同じ名前を持つが、そのシーケンスを示す整数が追加されます。 たとえば、元のトレース ファイルの名前が filename.trc の場合、次のトレース ファイルの名前は順に filename_1.trc、filename_2.trc となります。<br /><br /> 多くのロール オーバー トレース ファイルが作成ファイル名の増大に順番に追加する整数値。<br /><br /> SQL Server の既定値を使用して*max_file_size* (5 MB) の値を指定せずにこのオプションが指定されている場合*max_file_size*します。|  
|SHUTDOWN_ON_ERROR|**4**|なんらかの理由によりトレースをファイルに書き込めない場合、SQL Server はシャットダウンします。 このオプションは、セキュリティ監査トレースを実行するときに役立ちます。|  
|TRACE_PRODUCE_BLACKBOX|**8**|最後のレコード 5 mb 以上のサーバーによって生成されたトレース情報が保存されることによって、サーバーを指定します。 TRACE_PRODUCE_BLACKBOX は、その他のすべてのオプションと互換性がありません。|  
  
`[ @tracefile = ] 'trace_file'` トレースを書き込むファイルの名前と場所を指定します。 *trace_file*は**nvarchar (245)** 既定値はありません。 *trace_file* (N 'C:\MSSQL\Trace\trace.trc') などのローカル ディレクトリまたは UNC 共有またはパスのいずれかにすることができます (N'\\\\*Servername*\\*Sharename*\\*ディレクトリ*\trace.trc')。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 追加、 **.trc**すべてのトレース ファイル名に拡張します。 場合、TRACE_FILE_ROLLOVER オプションと*max_file_size*指定すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元のトレース ファイルが最大サイズに拡張する場合は、新しいトレース ファイルを作成します。 新しいファイルに同じ名前が、元のファイル、_*n*以降では、そのシーケンスを示すために追加される**1**します。 たとえば、最初のトレース ファイルの名前は**filename.trc**、2 つ目のトレース ファイルの名前は**filename_1.trc**します。  
  
 TRACE_FILE_ROLLOVER オプションを使用する場合、元のトレース ファイル名にアンダースコア文字を使用しないことをお勧めします。 アンダー スコアを使用する場合は、次の動作が発生します。  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 自動的に負荷をしませんまたは (これらのファイルのロール オーバー オプションのいずれかが構成されている) 場合は、ロール オーバー ファイルを読み込むことを確認します。  
  
-   Fn_trace_gettable 関数はロール オーバー ファイルを読み込めません (を使用して指定すると、 *number_files*引数) 元のファイル名がアンダー スコアと数値が終了します。 ただし、この状況は、ファイルがロールオーバーされるときに自動的に追加されたアンダースコアおよび数値については該当しません。  
  
> [!NOTE]  
>  このような動作に対処するには、元のファイル名のアンダースコアを削除してトレース ファイルの名前を変更します。 たとえば、元のファイルの名前は**my_trace.trc**、ロール オーバー ファイルの名前は**my_trace_1.trc**、ファイルの名前を変更することができます**mytrace.trc**と**mytrace_1.trc**内のファイルを開く前に[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]します。  
  
 *trace_file* TRACE_PRODUCE_BLACKBOX オプションを使用する場合は指定できません。  
  
`[ @maxfilesize = ] max_file_size` メガバイト (MB) のトレース ファイルの最大サイズを指定します。 *max_file_size*は**bigint**の既定値を持つ**5**します。  
  
 使用されるディスク領域がで指定された容量を超えると、トレースがファイルへの記録を停止場合、このパラメーターを指定して、TRACE_FILE_ROLLOVER オプションを指定せず、 *max_file_size*します。  
  
`[ @stoptime = ] 'stop_time'` 日付と、トレースを停止する時刻を指定します。 *stop_time*は**datetime**、既定値は NULL です。 この値を NULL にすると、トレースを手動で停止するか、サーバーがシャットダウンするまで、トレースは実行されます。  
  
 両方*stop_time*と*max_file_size*指定すると、TRACE_FILE_ROLLOVER でないと指定すると、トレースが上限指定した停止時刻、またはファイルの最大サイズに達するとします。 場合*stop_time*、 *max_file_size*、し、TRACE_FILE_ROLLOVER を指定すると、ドライブをトレースがいっぱいにならないと仮定すると、指定された停止時に、トレースを停止します。  
  
`[ @filecount = ] 'max_rollover_files'` 同じ基本ファイル名で保持する最大数、またはトレース ファイルを指定します。 *max_rollover_files*は**int**、1 より大きい。 このパラメーターは、TRACE_FILE_ROLLOVER オプションを指定した場合のみ有効です。 ときに*max_rollover_files*が指定されている[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に保以上*max_rollover_files*新しいトレース ファイルを開く前に、最も古いトレース ファイルを削除することによってトレース ファイル。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 基本ファイル名に番号を追加して、トレース ファイルの世代を追跡します。  
  
 たとえば、 *trace_file* "c:\mytrace_123.trc"名前を持つファイルは"c:\mytrace_124.trc"名前のファイルよりも古い"c:\mytrace"とパラメーターを指定します。 場合*max_rollover_files*は 2 に設定し、SQL Server は、"c:\mytrace_123.trc"というファイルを削除します。"c:\mytrace_125.trc"トレース ファイルを作成する前にします。  
  
 注意[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各を削除するだけの試行が 1 回、ファイルし、別のプロセスによって使用されているファイルを削除することはできません。 このため、トレースの実行中に別のアプリケーションによってトレース ファイルが使用されている場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではそれらのトレース ファイルがファイル システムに残されることがあります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 次の表は、このストアド プロシージャの完了時に返されるコード値を示しています。  
  
|リターン コード|説明|  
|-----------------|-----------------|  
|0|エラーなし。|  
|1|不明なエラー。|  
|10|無効なオプションです。 指定したオプションが一致しない場合に返されます。|  
|12|ファイルが作成されていない。|  
|13|メモリ不足。 指定したアクションを実行するための十分なメモリがない場合に返されます。|  
|14|無効な終了時刻。 指定した停止時刻が既に過ぎている場合に返されます。|  
|15|パラメーターが無効。 ユーザーには、互換性のないパラメーターが指定した場合に返されます。|  
  
## <a name="remarks"></a>コメント  
 **sp_trace_create**は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ストアド プロシージャで実行される操作の多くを**xp_trace _\*** 拡張ストアド プロシージャの SQL Server の以前のバージョンで使用できます。 使用**sp_trace_create**の代わりにします。  
  
-   **xp_trace_addnewqueue**  
  
-   **xp_trace_setqueuecreateinfo**  
  
-   **xp_trace_setqueuedestination**  
  
 **sp_trace_create**のみのトレース定義を作成します。 このストアド プロシージャを使用してトレースを開始したり変更することはできません。  
  
 パラメーターのすべての SQL トレース ストアド プロシージャ (**sp_trace_xx**) は厳密に型指定されます。 これらのパラメーターを、引数の説明で指定されている正しいデータ型で指定しないと、このストアド プロシージャではエラーが返されます。  
  
 **Sp_trace_create**、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サービス アカウントでは、トレース ファイル フォルダーに対する書き込み権限が必要です。 場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サービス アカウントが管理者でないトレース ファイルが配置されているコンピューターでは、書き込みアクセス許可を明示的に付与する必要があります、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サービス アカウント。  
  
> [!NOTE]  
>  作成されたトレース ファイルを自動的に読み込むことができます**sp_trace_create**を使用してテーブルに、 **fn_trace_gettable**システム関数。 このシステム関数を使用する方法については、次を参照してください。 [sys.fn_trace_gettable &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md)します。  
  
 トレース ストアド プロシージャを使用した例については、「[トレースの作成 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)」を参照してください。  
  
 **TRACE_PRODUCE_BLACKBOX**は次の特性があります。  
  
-   これは、ロール オーバー トレースです。 既定の*file_count*は 2 ですが、ユーザーを使用してオーバーライドできます*filecount*オプション。  
  
-   既定の*file_size*他のトレースは 5 MB と変更できます。  
  
-   ファイル名を指定しません。 ファイルは に保存されます。**N'%SQLDIR%\MSSQL\DATA\blackbox.trc'**  
  
-   次のイベントのみとその列がトレースに含まれています。  
  
    -   **RPC の開始**  
  
    -   **バッチの開始**  
  
    -   **例外**  
  
    -   **注意**  
  
-   イベントまたは列を追加またはこのトレースから削除することはできません。  
  
-   このトレースのフィルターを指定することはできません。  
  
## <a name="permissions"></a>アクセス許可  
 ALTER TRACE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [sp_trace_generateevent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [SQL トレース (SQL Trace)](../../relational-databases/sql-trace/sql-trace.md)  
  
  
