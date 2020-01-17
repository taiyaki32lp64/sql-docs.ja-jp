---
title: ALTER EVENT SESSION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/07/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER EVENT SESSION
- ALTER_EVENT_SESSION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- event sessions [SQL Server]
- extended events [SQL Server], Transact-SQL
- ALTER EVENT SESSION statement
ms.assetid: da006ac9-f914-4995-a2fb-25b5d971cd90
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 795ef4c95981636eec2e95bc6f85c24d7da27eb9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065659"
---
# <a name="alter-event-session-transact-sql"></a>ALTER EVENT SESSION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  イベント セッションの開始および停止、またはイベント セッションの構成変更を行います。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
ALTER EVENT SESSION event_session_name  
ON SERVER  
{  
    [ [ {  <add_drop_event> [ ,...n] }     
       | { <add_drop_event_target> [ ,...n ] } ]   
    [ WITH ( <event_session_options> [ ,...n ] ) ]  
    ]  
    | [ STATE = { START | STOP } ]  
}  
  
<add_drop_event>::=  
{  
    [ ADD EVENT <event_specifier>   
         [ ( {   
                 [ SET { event_customizable_attribute = <value> [ ,...n ] } ]  
                 [ ACTION ( { [event_module_guid].event_package_name.action_name [ ,...n ] } ) ]  
                 [ WHERE <predicate_expression> ]  
        } ) ]  
   ]   
   | DROP EVENT <event_specifier> }  
  
<event_specifier> ::=  
{  
[event_module_guid].event_package_name.event_name  
}  
  
<predicate_expression> ::=   
{  
    [ NOT ] <predicate_factor> | {( <predicate_expression> ) }   
    [ { AND | OR } [ NOT ] { <predicate_factor> | ( <predicate_expression> ) } ]   
    [ ,...n ]  
}  
  
<predicate_factor>::=   
{  
    <predicate_leaf> | ( <predicate_expression> )  
}  
  
<predicate_leaf>::=  
{  
      <predicate_source_declaration> { = | < > | ! = | > | > = | < | < = } <value>   
    | [event_module_guid].event_package_name.predicate_compare_name ( <predicate_source_declaration>, <value> )   
}  
  
<predicate_source_declaration>::=   
{  
    event_field_name | ( [event_module_guid].event_package_name.predicate_source_name )  
}  
  
<value>::=   
{  
    number | 'string'  
}  
  
<add_drop_event_target>::=  
{  
    ADD TARGET <event_target_specifier>  
        [ ( SET { target_parameter_name = <value> [ ,...n] } ) ]  
    | DROP TARGET <event_target_specifier>  
}  
  
<event_target_specifier>::=  
{  
    [event_module_guid].event_package_name.target_name  
}  
  
<event_session_options>::=  
{  
    [    MAX_MEMORY = size [ KB | MB] ]  
    [ [,] EVENT_RETENTION_MODE = { ALLOW_SINGLE_EVENT_LOSS | ALLOW_MULTIPLE_EVENT_LOSS | NO_EVENT_LOSS } ]  
    [ [,] MAX_DISPATCH_LATENCY = { seconds SECONDS | INFINITE } ]  
    [ [,] MAX_EVENT_SIZE = size [ KB | MB ] ]  
    [ [,] MEMORY_PARTITION_MODE = { NONE | PER_NODE | PER_CPU } ]  
    [ [,] TRACK_CAUSALITY = { ON | OFF } ]  
    [ [,] STARTUP_STATE = { ON | OFF } ]  
}  
```  
  
## <a name="arguments"></a>引数  
  
|||  
|-|-|  
|項目|定義|  
|*event_session_name*|既存のイベント セッションの名前です。|  
|STATE = START &#124; STOP|イベント セッションを開始または停止します。 この引数は、ALTER EVENT SESSION がイベント セッション オブジェクトに適用される場合にのみ有効です。|  
|ADD EVENT \<event_specifier>|\<event_specifier> で識別されるイベントをイベント セッションに関連付けます。|
|[*event_module_guid*] *.event_package_name.event_name*|以下の場合、イベント パッケージ内のイベントです。<br /><br /> -   *event_module_guid* は、イベントを含むモジュールの GUID です。<br />-   *event_package_name* は、アクション オブジェクトを含むパッケージです。<br />-   *event_name* は、イベント オブジェクトです。<br /><br /> イベントは、object_type 'event' として sys.dm_xe_objects ビューに表示されます。|  
|SET { *event_customizable_attribute*= \<value> [ ,...*n*] }|カスタマイズ可能なイベントの属性を指定します。 カスタマイズ可能な属性は、column_type 'customizable' および object_name = *event_name* として sys.dm_xe_object_columns ビューに表示されます。|  
|ACTION ( { [*event_module_guid*] *.event_package_name.action_name* [ **,** ...*n*] } )|以下の場合、イベント セッションに関連付けるアクションです。<br /><br /> -   *event_module_guid* は、イベントを含むモジュールの GUID です。<br />-   *event_package_name* は、アクション オブジェクトを含むパッケージです。<br />-   *action_name* は、アクション オブジェクトです。<br /><br /> アクションは、object_type 'action' として sys.dm_xe_objects ビューに表示されます。|  
|WHERE \<predicate_expression>|イベントを処理する必要があるかどうかを判定するために使用する述語式を指定します。 \<predicate_expression> が true の場合、イベントは、セッションのアクションおよびターゲットによって処理されます。 \<predicate_expression> が false の場合、イベントは、セッションのアクションおよびターゲットによって処理される前にセッションによって削除されます。 述語式は 3,000 文字に制限され、これにより文字列引数が制限されます。|
|*event_field_name*|述語ソースを識別するイベント フィールドの名前を指定します。|  
|[event_module_guid].event_package_name.predicate_source_name|以下の場合、グローバル述語ソースの名前です。<br /><br /> -   *event_module_guid* は、イベントを含むモジュールの GUID です。<br />-   *event_package_name* は、述語オブジェクトを含むパッケージです。<br />-   *predicate_source_name* は、object_type 'pred_source' として sys.dm_xe_objects ビューに定義されます。|  
|[*event_module_guid*].*event_package_name*.*predicate_compare_name*|以下の場合、イベントに関連付ける述語オブジェクトの名前です。<br /><br /> -   *event_module_guid* は、イベントを含むモジュールの GUID です。<br />-   *event_package_name* は、述語オブジェクトを含むパッケージです。<br />-   *predicate_compare_name* は、object_type 'pred_compare' として sys.dm_xe_objects ビューに定義されるグローバル ソースです。|  
|DROP EVENT \<event_specifier>|*\<event_specifier>* で識別されるイベントを削除します。 \<event_specifier> は、イベント セッションで有効である必要があります。|  
|ADD TARGET \<event_target_specifier>|\<event_target_specifier> で識別されるターゲットをイベント セッションに関連付けます。|
|[*event_module_guid*].*event_package_name*.*target_name*|以下の場合、イベント セッションのターゲットの名前です。<br /><br /> -   *event_module_guid* は、イベントを含むモジュールの GUID です。<br />-   *event_package_name* は、アクション オブジェクトを含むパッケージです。<br />-   *target_name* はアクションです。 アクションは、object_type 'target' として sys.dm_xe_objects ビューに表示されます。|  
|SET { *target_parameter_name*= \<value> [, ...*n*] }|ターゲット パラメーターを設定します。 ターゲット パラメーターは、column_type 'customizable' および object_name = *target_name* として sys.dm_xe_object_columns ビューに表示されます。<br /><br /> **注:** リング バッファー ターゲットを使用している場合、max_memory ターゲット パラメーターを 2048 KB に設定し、XML 出力のデータの切り捨てを回避することをお勧めします。 さまざまなターゲットの種類の使用について詳しくは、「[SQL Server 拡張イベント ターゲット](https://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)」をご覧ください。|  
|DROP TARGET \<event_target_specifier>|\<event_target_specifier> で識別されるターゲットを削除します。 \<event_target_specifier> は、イベント セッションで有効である必要があります。|  
|EVENT_RETENTION_MODE = { **ALLOW_SINGLE_EVENT_LOSS** &#124; ALLOW_MULTIPLE_EVENT_LOSS &#124; NO_EVENT_LOSS }|イベントの削除を処理するために使用するイベント保有モードを指定します。<br /><br /> **ALLOW_SINGLE_EVENT_LOSS**<br /> セッションからイベントを削除できます。 単独のイベントは、すべてのイベント バッファーがいっぱいになった場合にのみ削除されます。 イベント バッファーがいっぱいのときに単独のイベントを削除することで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のパフォーマンス特性が許容可能な状態になり、処理後のイベント ストリームのデータ損失を最小限に抑えることができます。<br /><br /> ALLOW_MULTIPLE_EVENT_LOSS<br /> 複数のイベントでいっぱいのイベント バッファーをセッションから削除できます。 削除されるイベントの数は、セッションに割り当てられているメモリ サイズ、メモリのパーティション分割、バッファー内のイベントのサイズによって異なります。 このオプションを使用すると、イベント バッファーがすぐにいっぱいになるときにサーバーのパフォーマンスに与える影響を最小限に抑えることができますが、多数のイベントがセッションから削除される可能性があります。<br /><br /> NO_EVENT_LOSS<br /> イベントの削除は許可されません。 このオプションを指定した場合、発生したすべてのイベントが保持されます。 このオプションを使用した場合、イベントを開始するすべてのタスクは、イベント バッファーに空きができるまで待機します。 その結果、イベント セッションがアクティブになっている間、検知できる程度のパフォーマンスの問題が発生することがあります。 バッファーからイベントがフラッシュされるのを待機する間、ユーザーの接続に遅延が生じる可能性があります。|  
|MAX_DISPATCH_LATENCY = { *seconds* SECONDS &#124; **INFINITE** }|イベントをイベント セッション ターゲットにディスパッチする前にメモリにバッファリングする時間を指定します。 最小待機値は 1 秒です。 ただし、0 を使用すると、INFINITE 待機を指定できます。 既定では、この値は 30 秒に設定されます。<br /><br /> *seconds* SECONDS<br /> ターゲットへのバッファーのフラッシュを開始する前に待つ秒数を指定します。 *seconds* は整数です。<br /><br /> **INFINITE**<br /> バッファーがいっぱいになっている、またはイベント セッションが閉じられる場合にのみ、バッファーをターゲットにフラッシュします。<br /><br /> **注:** MAX_DISPATCH_LATENCY = 0 SECONDS と MAX_DISPATCH_LATENCY = INFINITE は同じです。|  
|MAX_EVENT_SIZE =*size* [ KB &#124; **MB** ]|イベントの最大許容サイズを指定します。 MAX_EVENT_SIZE は、MAX_MEMORY よりも大きな単独のイベントのみを許可するように設定する必要があります。MAX_MEMORY よりも小さな値を設定した場合はエラーが発生します。 *size* は、キロバイト (KB) またはメガバイト (MB) 数を示す整数値です。 *size* をキロバイト単位で指定する場合、最小許容サイズは 64 KB です。 MAX_EVENT_SIZE を設定すると、MAX_MEMORY に加えて、サイズが *size* のバッファーが 2 つ作成されます。 つまり、イベントのバッファリングに使用されるメモリの合計量は MAX_MEMORY + 2 * MAX_EVENT_SIZE となります。|  
|MEMORY_PARTITION_MODE = { **NONE** &#124; PER_NODE &#124; PER_CPU }|イベント バッファーを作成する場所を指定します。<br /><br /> **NONE**<br /> 1 つのバッファー セットが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内で作成されます。<br /><br /> PER NODE - NUMA ノードごとに 1 つのバッファー セットが作成されます。<br /><br /> PER CPU - CPU ごとに 1 つのバッファー セットが作成されます。|  
|TRACK_CAUSALITY = { ON &#124; **OFF** }|因果関係を追跡するかどうかを指定します。 有効な場合、因果関係により、異なるサーバー接続上の関連イベントを一緒に関連付けることができます。|  
|STARTUP_STATE = { ON &#124; **OFF** }|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動時にこのイベント セッションを自動的に開始するかどうかを指定します。<br /><br /> STARTUP_STATE=ON の場合、イベント セッションは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が停止後に再起動されたときにだけ開始されます。<br /><br /> ON = 起動時にイベント セッションが開始されます。<br /><br /> **OFF** = イベント セッションは起動時に開始されません。|  
  
## <a name="remarks"></a>Remarks  
 `ADD` 引数と `DROP` 引数は同じステートメントで一緒に使用できません。  
  
## <a name="permissions"></a>アクセス許可  
 `ALTER ANY EVENT SESSION` アクセス許可が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、イベント セッションを開始し、いくつかのライブ セッション統計を取得します。次に、既存のセッションに 2 つのイベントを追加します。  
  
```sql  
-- Start the event session  
ALTER EVENT SESSION test_session ON SERVER  
STATE = start;  
GO  

-- Obtain live session statistics   
SELECT * FROM sys.dm_xe_sessions;  
SELECT * FROM sys.dm_xe_session_events;  
GO  
  
-- Add new events to the session  
ALTER EVENT SESSION test_session ON SERVER  
ADD EVENT sqlserver.database_transaction_begin,  
ADD EVENT sqlserver.database_transaction_end;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)   
 [DROP EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)   
 [SQL Server 拡張イベント ターゲット](https://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)   
 [sys.server_event_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)   
 [sys.dm_xe_objects &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql.md)   
 [sys.dm_xe_object_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-object-columns-transact-sql.md)  
  
  
