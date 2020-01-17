---
title: sys.database_connection_stats
titleSuffix: Azure SQL Database
ms.date: 01/28/2019
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.database_connection_stats
- database_connection_stats
- database_connection_stats_TSQL
- sys.database_connection_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_connection_stats
- database_connection_stats
ms.assetid: 5c8cece0-63b0-4dee-8db7-6b43d94027ec
author: stevestein
ms.author: sstein
ms.custom: seo-dt-2019
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 7eb05640fbc702d5c9b01081d462e2c9f0204457
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844470"
---
# <a name="sysdatabase_connection_stats-azure-sql-database"></a>sys.database_connection_stats (Azure SQL データベース)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  データベース接続の成功と失敗の概要を示す [!INCLUDE[ssSDS](../../includes/sssds-md.md)] データベース**接続**イベントの統計が含まれます。 接続イベントの詳細については、「 [event_log &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md)のイベントの種類」を参照してください。  
  
|統計|型|説明|  
|---------------|----------|-----------------|  
|**database_name**|**sysname**|データベースの名前です。|  
|**start_time**|**datetime2**|集計間隔の開始時刻 (UTC)。 この時刻は常に 5 分の倍数です。 例:<br /><br /> ' 2011-09-28 16:00:00 '<br />' 2011-09-28 16:05:00 '<br />' 2011-09-28 16:10:00 '|  
|**end_time**|**datetime2**|集計間隔の終了時刻 (UTC)。 **End_time**は、同じ行の対応する**start_time**よりも常に5分後になります。|  
|**success_count**|**int**|成功した接続の数。|  
|**total_failure_count**|**int**|失敗した接続の合計数。 これは**connection_failure_count**、 **terminated_connection_count**、および**throttled_connection_count**の合計であり、デッドロックイベントは含まれていません。|  
|**connection_failure_count**|**int**|ログインに失敗した回数。|  
|**terminated_connection_count**|**int**|**_[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] v11 にのみ適用されます。_**<br /><br /> 終了した接続の数。|  
|**throttled_connection_count**|**int**|**_[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] v11 にのみ適用されます。_**<br /><br /> スロットルされた接続の数。|  
  
## <a name="remarks"></a>解説  
  
### <a name="event-aggregation"></a>イベント集計

 このビューのイベント情報は、5 分未満の間隔で収集および集計されます。 カウント列は、特定のデータベースで特定の接続イベントが発生した回数を表します。  
  
 たとえば、ユーザーがデータベース Database1 への接続に失敗した場合、11:00 と11:05 の 2/5/2012 (UTC) に7回、この情報はこのビューの1行に表示されます。  
  
|**database_name**|**start_time**|**end_time**|**success_count**|**total_failure_count**|**connection_failure_count**|**terminated_connection_count**|**throttled_connection_count**|  
|------------------------|---------------------|-------------------|------------------------|-------------------------------|------------------------------------|---------------------------------------|--------------------------------------|  
|`Database1`|`2012-02-05 11:00:00`|`2012-02-05 11:05:00`|`0`|`7`|`7`|`0`|`0`|  
  
### <a name="interval-start_time-and-end_time"></a>間隔 start_time と end_time

 イベントが集計間隔に含まれるのは、イベントが **start_time**の_後_、またはその後に発生してから、その間隔の**end_time** _前_です。 たとえば、`2012-10-30 19:25:00.0000000` に発生したイベントは、下に示す例では 2 つ目の間隔にのみ含まれます。  
  
```  
  
start_time                    end_time  
2012-10-30 19:20:00.0000000   2012-10-30 19:25:00.0000000  
2012-10-30 19:25:00.0000000   2012-10-30 19:30:00.0000000  
```  
  
### <a name="data-updates"></a>データの更新

 このビューのデータは、時間の経過と共に累積されます。 通常、データは集計間隔の開始から1時間以内に累積されますが、すべてのデータがビューに表示されるまでに最大で24時間かかることがあります。 その間に、1 つの行内の情報が定期的に更新されることがあります。  
  
### <a name="data-retention"></a>[データ保有期間]

 このビューのデータは、最大で30日間保持されます。データベースの数や、各データベースが生成する一意のイベントの数によっては、それよりも少ない場合があります。 この情報をより長期間にわたって保持するには、データを別のデータベースにコピーします。 ビューの最初のコピーを行った後に、そのビューの行がデータの累積に伴って更新されることがあります。 データのコピーを最新の状態に保つには、定期的に行のテーブル スキャンを行うことにより、既存の行のイベント数の増加を検出し、新しい行を特定して (開始時刻と終了時刻を使用して一意の行を識別できます)、これらの更新内容をデータのコピーに反映させます。  
  
### <a name="errors-not-included"></a>エラーは含まれません

 このビューには、すべての接続とエラー情報が含まれていない可能性があります。  
  
- このビューには、発生する可能性のあるすべての [!INCLUDE[ssSDS](../../includes/sssds-md.md)] データベースエラーは含まれません。 [event_log &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md)のイベントの種類で指定されたものだけです。  
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)] データセンター内にマシン障害が発生した場合は、少量のデータがイベントテーブルに存在しない可能性があります。  
  
- IP アドレスが DoSGuard によってブロックされている場合、その IP アドレスからの接続試行イベントは収集されず、このビューに表示されません。  
  
## <a name="permissions"></a>アクセス許可

 **Master**データベースへのアクセス権限を持つユーザーには、このビューに対する読み取り専用アクセス権があります。  
  
## <a name="example"></a>例

 次の例は、9/25/2011 の正午から 9/28/2011 (UTC) に正午に発生したデータベース接続の概要を返すための、database_connection_stats のクエリを示しています **。** 既定では、クエリの結果は**start_time** (昇順) に並べ替えられます。  
  
```sql
SELECT *  
FROM sys.database_connection_stats
WHERE start_time>='2011-09-25:12:00:00' and end_time<='2011-09-28 12:00:00';  
```  

## <a name="see-also"></a>参照

 [Azure SQL Database への接続に関する問題のトラブルシューティング](/azure/sql-database/sql-database-troubleshoot-common-connection-issues)  
  
  
