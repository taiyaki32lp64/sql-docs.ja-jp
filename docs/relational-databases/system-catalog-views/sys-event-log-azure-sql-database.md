---
title: sys.event_log (Azure SQL データベース) |Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- event_log
- sys.event_log_TSQL
- event_log_TSQL
- sys.event_log
dev_langs:
- TSQL
helpviewer_keywords:
- event_log
- sys.event_log
ms.assetid: ad5496b5-e5c7-4a18-b5a0-3f985d7c4758
author: MashaMSFT
ms.author: mathoma
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: a239624fcbc3913d636f7f57b496c006d06a64b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061385"
---
# <a name="syseventlog-azure-sql-database"></a>sys.event_log (Azure SQL データベース)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  成功が返される[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]データベース接続、接続エラー、およびデッドロックします。 この情報を使用して、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] でのデータベースの利用状況の追跡またはトラブルシューティングを行うことができます。  
  
> [!CAUTION]  
> 大量のデータベースまたはログインの大きい数値を持つインストールの場合、sys.event_log 内のアクティビティと制限事項、パフォーマンス、CPU 使用率が高くと可能性があるログイン エラーが発生します。 Sys.event_log のクエリは、問題に投稿できます。 マイクロソフトは、この問題を解決するのには中です。 それまでは、この問題の影響を小さくには、sys.event_log のクエリを制限します。 NewRelic SQL Server プラグインのユーザーがアクセスする必要があります[Microsoft Azure SQL Database プラグインのチューニングとパフォーマンスの調整](https://discuss.newrelic.com/t/microsoft-azure-sql-database-plugin-tuning-performance-tweaks/30729)の追加の構成情報。  
  
 `sys.event_log` ビューには、次の列が含まれています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|データベースの名前です。 接続が失敗し、ユーザーがデータベース名を指定していない場合、この列は空白です。|  
|**start_time**|**datetime2**|集計の間隔の開始日時 (UTC)。 集計されるイベントの場合、この時刻は常に 5 分の倍数です。 以下に例を示します。<br /><br /> '2011-09-28 16:00:00'<br />'2011-09-28 16:05:00'<br />'2011-09-28 16:10:00'|  
|**end_time**|**datetime2**|集計の間隔の終了日時 (UTC)。 集計されるイベントは、 **End_time**は常に 5 分後に、対応するよりも**start_time**同じ行にします。 集計されないイベント**start_time**と**end_time**実際の UTC 日付とイベントの時刻を等しきます。|  
|**event_category**|**nvarchar(64)**|このイベントを生成した上位レベルのコンポーネント。<br /><br /> 参照してください[イベントの種類](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes)使用可能な値の一覧についてはします。|  
|**event_type**|**nvarchar(64)**|イベントの種類。<br /><br /> 参照してください[イベントの種類](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes)使用可能な値の一覧についてはします。|  
|**event_subtype**|**int**|発生したイベントのサブタイプ。<br /><br /> 参照してください[イベントの種類](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes)使用可能な値の一覧についてはします。|  
|**event_subtype_desc**|**nvarchar(64)**|イベントのサブタイプの説明。<br /><br /> 参照してください[イベントの種類](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes)使用可能な値の一覧についてはします。|  
|**severity**|**int**|エラーの重大度。 有効な値は次のとおりです。<br /><br /> 0 = 情報<br />1 = 警告<br />2 = エラー|  
|**event_count**|**int**|時刻をこのイベントが発生した、指定されたデータベースで指定された時間間隔の数 (**start_time**と**end_time**)。|  
|**description**|**nvarchar(max)**|イベントの詳細な説明。<br /><br /> 参照してください[イベントの種類](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes)使用可能な値の一覧についてはします。|  
|**additional_data**|**XML**|*注:この値は、Azure SQL Database V12 の NULL は常にします。参照してください[例](#Deadlock)V12 のデッドロック イベントを取得する方法についてのセクション。*<br /><br /> **デッドロック**イベントでは、この列には、デッドロック グラフが含まれています。 それ以外の種類のイベントの場合、この列は NULL です。 |  
  
##  <a name="EventTypes"></a> イベントの種類

 このビューの各行によって記録されたイベントは、カテゴリによって識別されます (**event_category**)、イベントの種類 (**event_type**)、およびサブタイプ (**event_subtype**)。 次の表に、このビューで収集されるイベントの種類を示します。  
  
 イベントを**接続**カテゴリで、概要情報は、sys.database_connection_stats ビューで使用できます。  
  
> [!NOTE]  
> このビューには、発生する可能性のあるすべての [!INCLUDE[ssSDS](../../includes/sssds-md.md)] データベース イベントが表示されるわけではなく、この表に示されているイベントのみが表示されます。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] の今後のリリースで他のカテゴリ、イベントの種類、およびサブタイプが報告対象として追加される可能性はあります。  
  
|**event_category**|**event_type**|**event_subtype**|**event_subtype_desc**|**severity**|**description**|  
|-------------------------|---------------------|------------------------|------------------------------|------------------|---------------------|  
|**接続**|**connection_successful**|0|**connection_successful**|0|データベースに正常に接続されました。|  
|**接続**|**connection_failed**|0|**invalid_login_name**|2|ログイン名がこのバージョンの SQL Server では無効です。|  
|**接続**|**connection_failed**|1|**windows_auth_not_supported**|2|Windows ログインは、このバージョンの SQL Server ではサポートされていません。|  
|**接続**|**connection_failed**|2|**attach_db_not_supported**|2|ユーザーがサポートされていないデータベース ファイルをアタッチしようとしました。|  
|**接続**|**connection_failed**|3|**change_password_not_supported**|2|ユーザーがユーザーのログイン用のパスワードを変更しようとしました。これはサポートされていません。|  
|**接続**|**connection_failed**|4|**login_failed_for_user**|2|ユーザーはログインできませんでした。|  
|**接続**|**connection_failed**|5|**login_disabled**|2|ログインが無効でした。|  
|**接続**|**connection_failed**|6|**failed_to_open_db**|2|*注:Azure SQL Database V11 にのみ適用されます。*<br /><br /> データベースを開くことができませんでした。 これはデータベースが存在しないか、データベースを開くための認証が正常に行われなかったため発生した可能性があります。|  
|**接続**|**connection_failed**|7|**blocked_by_firewall**|2|クライアントの IP アドレスからサーバーにアクセスすることが許可されていません。|  
|**接続**|**connection_failed**|8|**client_close**|2|*注:Azure SQL Database V11 にのみ適用されます。*<br /><br /> クライアントが接続の確立中にタイムアウトした可能性があります。 接続タイムアウトを増やしてください。|  
|**接続**|**connection_failed**|9|**再構成**|2|*注:Azure SQL Database V11 にのみ適用されます。*<br /><br /> データベースが再構成中であったため接続に失敗しました。|  
|**接続**|**connection_terminated**|0|**idle_connection_timeout**|2|*注:Azure SQL Database V11 にのみ適用されます。*<br /><br /> 接続がシステム定義のしきい値よりも長い時間にわたってアイドル状態でした。|  
|**接続**|**connection_terminated**|1|**再構成**|2|*注:Azure SQL Database V11 にのみ適用されます。*<br /><br /> データベース再構成が原因で、セッションが終了しました。|  
|**接続**|**調整**|*\<理由コード >*|**reason_code**|2|*注:Azure SQL Database V11 にのみ適用されます。*<br /><br /> 要求が調整されています。  調整理由コード: *\<理由コード >* します。 詳細については、次を参照してください。[エンジン調整](https://msdn.microsoft.com/library/windowsazure/dn338079.aspx)します。|  
|**接続**|**throttling_long_transaction**|40549|**long_transaction**|2|*注:Azure SQL Database V11 にのみ適用されます。*<br /><br /> トランザクションが長時間実行されているため、セッションを終了しました。 トランザクションを短くしてください。 詳細については、次を参照してください。[リソース制限](https://msdn.microsoft.com/library/windowsazure/dn338081.aspx)します。|  
|**接続**|**throttling_long_transaction**|40550|**excessive_lock_usage**|2|*注:Azure SQL Database V11 にのみ適用されます。*<br /><br /> 取得したロックの数が多すぎるため、セッションを終了しました。 1 つのトランザクションで読み取る行または変更する行の数を減らしてください。 詳細については、次を参照してください。[リソース制限](https://msdn.microsoft.com/library/windowsazure/dn338081.aspx)します。|  
|**接続**|**throttling_long_transaction**|40551|**excessive_tempdb_usage**|2|*注:Azure SQL Database V11 にのみ適用されます。*<br /><br /> TEMPDB の使用領域が多すぎるため、セッションを終了しました。 クエリを変更して一時テーブルの使用領域を減らしてください。 詳細については、次を参照してください。[リソース制限](https://msdn.microsoft.com/library/windowsazure/dn338081.aspx)します。|  
|**接続**|**throttling_long_transaction**|40552|**excessive_log_space_usage**|2|*注:Azure SQL Database V11 にのみ適用されます。*<br /><br /> トランザクション ログの使用領域が多すぎるため、セッションを終了しました。 1 回のトランザクションで変更する行を減らしてください。 詳細については、次を参照してください。[リソース制限](https://msdn.microsoft.com/library/windowsazure/dn338081.aspx)します。|  
|**接続**|**throttling_long_transaction**|40553|**excessive_memory_usage**|2|*注:Azure SQL Database V11 にのみ適用されます。*<br /><br /> メモリの使用量が多すぎるため、セッションを終了しました。 クエリを変更して、処理する行を減らしてください。 詳細については、次を参照してください。[リソース制限](https://msdn.microsoft.com/library/windowsazure/dn338081.aspx)します。|  
|**エンジン**|**デッドロック**|0|**デッドロック**|2|デッドロックが発生しました。|  
  
## <a name="permissions"></a>アクセス許可

 アクセス許可を持つユーザー、**マスター**データベースは、このビューに読み取り専用のアクセス権を持ちます。  
  
## <a name="remarks"></a>コメント  
  
### <a name="event-aggregation"></a>イベント集計

 このビューのイベント情報は、5 分未満の間隔で収集および集計されます。 **Event_count**列が特定の時間数を表す**event_type**と**event_subtype**一定の時間間隔内で特定のデータベースが発生しました。  
  
> [!NOTE]  
> デッドロックなどの一部のイベントは集計されません。 これらのイベントの**event_count**は 1 になりますと**start_time**と**end_time**実際の UTC 日付と時刻のイベントが発生したときになります。  
  
 たとえば、2012 年 2 月 5 日 の 11:00 から 11:05 まで (UTC) の間にログイン名が無効であったため Database1 データベースへの接続が 7 回失敗した場合、この情報はこのビューの 1 つの行に表示されます。  
  
|**database_name**|**start_time**|**end_time**|**event_category**|**event_type**|**event_subtype**|**event_subtype_desc**|**severity**|**event_count**|**description**|**additional_data**|  
|------------------------|---------------------|-------------------|-------------------------|---------------------|------------------------|------------------------------|------------------|----------------------|---------------------|--------------------------|  
|`Database1`|`2012-02-05 11:00:00`|`2012-02-05 11:05:00`|`connectivity`|`connection_failed`|`4`|`login_failed_for_user`|`2`|`7`|`Login failed for user.`|`NULL`|  
  
### <a name="interval-starttime-and-endtime"></a>間隔の start_time と end_time  
 イベントの発生時に、集計間隔にイベントが含まれている*で*または_後_**start_time**と_する前に_**end_time**その間隔。 たとえば、`2012-10-30 19:25:00.0000000` に発生したイベントは、下に示す例では 2 つ目の間隔にのみ含まれます。  
  
```
start_time                    end_time  
2012-10-30 19:20:00.0000000   2012-10-30 19:25:00.0000000  
2012-10-30 19:25:00.0000000   2012-10-30 19:30:00.0000000  
```

### <a name="data-updates"></a>データの更新

 このビューのデータは、時間の経過と共に累積されます。 通常、データは集計の間隔が開始してから 1 時間以内に累積されますが、すべてのデータがビューに表示されるまでに最大で 24 時間かかることがあります。 その間に、1 つの行内の情報が定期的に更新されることがあります。  
  
### <a name="data-retention"></a>[データ保有期間]

 このビュー内のデータには、最大 30 日間、またはデータベースの数と各データベースが生成される一意のイベント数によっては短く場合によっては保持されます。 この情報をより長期間にわたって保持するには、データを別のデータベースにコピーします。 ビューの最初のコピーを行った後に、そのビューの行がデータの累積に伴って更新されることがあります。 データのコピーを最新の状態に保つには、定期的に行のテーブル スキャンを行うことにより、既存の行のイベント数の増加を検出し、新しい行を特定して (開始時刻と終了時刻を使用して一意の行を識別できます)、これらの更新内容をデータのコピーに反映させます。  
  
### <a name="errors-not-included"></a>含まれていないエラー

 すべての接続情報とエラー情報がこのビューに含まれるわけではありません。  
  
- このビューにすべて含まれていない[!INCLUDE[ssSDS](../../includes/sssds-md.md)]データベースのみで指定されているエラーが発生する可能性があります、[イベントの種類](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes)このトピックの「します。  
- 内でコンピューター障害がある場合、[!INCLUDE[ssSDS](../../includes/sssds-md.md)]データ センター、少量のデータがイベント テーブルからない可能性があります。  
- IP アドレスが DoSGuard によってブロックされている場合、その IP アドレスからの接続の試みのイベントは収集できないため、このビューに表示されません。  
  
## <a name="examples"></a>使用例  
  
### <a name="simple-examples"></a>簡単な例

 次のクエリは、2011 年 9 月 25 日の正午から 2011 年 9 月 28 日の正午まで (UTC) の間に発生したすべてのイベントを返します。 既定では、クエリの結果は並べ**start_time** (昇順)。  

```sql
SELECT * FROM sys.event_log
WHERE start_time >= '2011-09-25 12:00:00'
    AND end_time <= '2011-09-28 12:00:00';  
```

次のクエリでは、Database1 データベース (Azure SQL Database V11 にのみ適用されます) のすべてのデッドロック イベントを返します。  

```sql
SELECT * FROM sys.event_log
WHERE event_type = 'deadlock'
    AND database_name = 'Database1';  
```

<a name="Deadlock"></a> 次のクエリでは、Database1 データベース (Azure SQL Database V12 にのみ適用されます) のすべてのデッドロック イベントを返します。  

```sql
WITH CTE AS (  
       SELECT CAST(event_data AS XML)  AS [target_data_XML]  
   FROM sys.fn_xe_telemetry_blob_target_read_file('dl', null, null, null)  
)  
SELECT target_data_XML.value('(/event/@timestamp)[1]', 'DateTime2') AS Timestamp,  
target_data_XML.query('/event/data[@name=''xml_report'']/value/deadlock') AS deadlock_xml,  
target_data_XML.query('/event/data[@name=''database_name'']/value').value('(/value)[1]', 'nvarchar(100)') AS db_name  
FROM CTE  
```

次のクエリは、2011 年 9 月 25 日の 10:00 から 11:00 まで (UTC) の間に発生した SQL のワーカー スレッドでのスロットル イベントを返します。  

```sql
SELECT * FROM sys.event_log
WHERE event_type = 'throttling'
    AND event_subtype = 4194307
    AND start_time >= '2011-09-25 10:00:00'
    AND end_time <= '2011-09-25 11:00:00';  
```

### <a name="db-scoped-extended-event"></a>DB スコープの拡張イベント

 Db スコープの拡張イベント (XEvent) セッションをセットアップするには、次のサンプル コードを使用します。  

```sql
IF EXISTS  
    (SELECT * from sys.database_event_sessions  
        WHERE name = 'azure_monitor_deadlock_session')  
BEGIN  
    ALTER EVENT SESSION azure_monitor_deadlock_session  
        ON DATABASE  
        DROP TARGET package0.ring_buffer;  
  
    DROP EVENT SESSION azure_monitor_deadlock_session  
        ON DATABASE;  
END  
  
CREATE EVENT SESSION azure_monitor_deadlock_session  
    ON DATABASE  
    ADD EVENT sqlserver.database_xml_deadlock_report  
    ADD TARGET package0.ring_buffer  
    (  
        SET max_memory = 2048, max_events_limit = 10  
    )  
    WITH (STARTUP_STATE = ON,  
          EVENT_RETENTION_MODE = ALLOW_SINGLE_EVENT_LOSS);  
  
ALTER EVENT SESSION azure_monitor_deadlock_session  
    ON DATABASE  
    STATE = START;  
```

### <a name="check-for-deadlock"></a>デッドロックの確認

デッドロックがあるかどうかは確認するのにには、次のクエリを使用します。  

```sql
WITH CTE AS (  
    SELECT CAST(xet.target_data AS XML)  AS [target_data_XML]  
        FROM            sys.dm_xe_database_session_targets AS xet  
             INNER JOIN sys.dm_xe_database_sessions        AS xe  
                 ON (xe.address = xet.event_session_address)  
        WHERE xe.name = 'azure_monitor_deadlock_session'  
)  
, CTE2 AS (  
    SELECT  
            T2.EventData.query('.').value(  
                '(/event/@timestamp)[1]', 'DateTime2') AS Timestamp,  
            T2.EventData.query('.').query(  
                '(/event/data/value/deadlock)[1]')     AS deadlock_xml  
        FROM CTE  
            CROSS Apply [target_data_XML].nodes(  
                '/RingBufferTarget/event') AS T2(EventData)  
)  
SELECT * FROM CTE2;  
```

## <a name="see-also"></a>参照

 [Azure SQL Database での拡張イベント](https://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)  
 