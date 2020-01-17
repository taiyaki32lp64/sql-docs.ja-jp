---
title: sys.dm_db_missing_index_group_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_missing_index_group_stats_TSQL
- sys.dm_db_missing_index_group_stats
- dm_db_missing_index_group_stats_TSQL
- dm_db_missing_index_group_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_missing_index_group_stats dynamic management view
- missing indexes feature [SQL Server], sys.dm_db_missing_index_group_stats dynamic management view
ms.assetid: c2886986-9e07-44ea-a350-feeac05ee4f4
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fa4da39290590591af30e259db910fdc9e5600ac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68051560"
---
# <a name="sysdmdbmissingindexgroupstats-transact-sql"></a>sys.dm_db_missing_index_group_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  空間インデックスを除く、欠落インデックス グループに関する概要を返します。  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]では、動的管理ビューでデータベースの包含に影響を与える情報を公開することや、ユーザーがアクセスできる他のデータベースに関する情報を公開することはできません。 この情報を公開することを避けるため、接続されているテナントに属していないデータが含まれるすべての行はフィルターで除外します。  
    
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**group_handle**|**int**|欠落インデックス グループの識別子。 この識別子はサーバー内で一意です。<br /><br /> 他の列では、グループ内のインデックスが欠落していると考えられる、すべてのクエリに関する情報が提供されます。<br /><br /> インデックス グループには、インデックスが 1 つだけ含まれます。|  
|**unique_compiles**|**bigint**|この欠落インデックス グループによって影響を受けるコンパイルおよび再コンパイルの数。 多くの異なるクエリでコンパイルおよび再コンパイルが行われるほど、この列の値は大きくなります。|  
|**user_seeks**|**bigint**|グループ内の推奨インデックスを使用できたユーザー クエリによって発生したシーク数。|  
|**user_scans**|**bigint**|グループ内の推奨インデックスを使用できたユーザー クエリによって発生したスキャン数。|  
|**last_user_seek**|**datetime**|グループ内の推奨インデックスを使用できたユーザー クエリによって発生した前回のシークの日時。|  
|**last_user_scan**|**datetime**|グループ内の推奨インデックスを使用できたユーザー クエリによって発生した前回のスキャンの日時。|  
|**avg_total_user_cost**|**float**|グループ内のインデックスによって削減できたユーザー クエリの平均コスト。|  
|**avg_user_impact**|**float**|この欠落インデックス グループが実装されていた場合のユーザー クエリへの効果の平均パーセンテージ (%)。 この値は、この欠落インデックス グループが実装されていた場合に減少したクエリ コストの平均パーセンテージを示します。|  
|**system_seeks**|**bigint**|グループ内の推奨インデックスを使用できたシステム クエリ (Auto Stats クエリなど) によって発生したシーク数。 詳細については、次を参照してください。 [Auto Stats イベント クラス](../../relational-databases/event-classes/auto-stats-event-class.md)します。|  
|**system_scans**|**bigint**|グループ内の推奨インデックスを使用できたシステム クエリによって発生したスキャン数。|  
|**last_system_seek**|**datetime**|グループ内の推奨インデックスを使用できたシステム クエリによって発生した前回のシステム シークの日時。|  
|**last_system_scan**|**datetime**|グループ内の推奨インデックスを使用できたシステム クエリによって発生した前回のシステム スキャンの日時。|  
|**avg_total_system_cost**|**float**|グループ内のインデックスによって削減できたシステム クエリの平均コスト。|  
|**avg_system_impact**|**float**|この欠落インデックス グループが実装されていた場合のシステム クエリへの効果の平均パーセンテージ (%)。 この値は、この欠落インデックス グループが実装されていた場合に減少したクエリ コストの平均パーセンテージを示します。|  
  
## <a name="remarks"></a>コメント  
 によって返される情報**sys.dm_db_missing_index_group_stats**すべてのクエリのコンパイルまたは再コンパイルではなく、クエリを実行するたびに更新されます。 使用状況の統計は保存されません。統計が保持されるのは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の再起動までです。 使用状況の統計をサーバーの再利用後も保持する場合は、データベース管理者が欠落インデックスの情報のバックアップ コピーを定期的に作成する必要があります。  

  >[!NOTE]
  >この DMV の結果セットは、600 行に制限されます。 各行には、1 つの欠落インデックスが含まれています。 まで 600 を超える欠落したインデックスがあれば、新しいものを表示できるように、既存の欠落したインデックスに対処する必要があります。
  
## <a name="permissions"></a>アクセス許可  
 この動的管理ビューを照会するには、VIEW SERVER STATE 権限または VIEW SERVER STATE 権限が暗黙的にすべてのアクセス権にユーザーを許可する必要があります。  
  
## <a name="examples"></a>使用例  
 次の例を使用する方法を示して、 **sys.dm_db_missing_index_group_stats**動的管理ビュー。  
  
### <a name="a-find-the-10-missing-indexes-with-the-highest-anticipated-improvement-for-user-queries"></a>A. ユーザー クエリで最も高いパフォーマンス向上が見込める、上位 10 個の欠落インデックスを検索する  
 次のクエリでは、ユーザー クエリで最も高い累積のパフォーマンス向上が見込める、上位 10 個の欠落インデックスを特定します。  
  
```  
SELECT TOP 10 *  
FROM sys.dm_db_missing_index_group_stats  
ORDER BY avg_total_user_cost * avg_user_impact * (user_seeks + user_scans)DESC;  
```  
  
### <a name="b-find-the-individual-missing-indexes-and-their-column-details-for-a-particular-missing-index-group"></a>B. 特定の欠落インデックス グループについて、個別の欠落インデックスとその列の詳細を検索する  
 次のクエリでは、特定の欠落インデックス グループを構成しているインデックスを特定し、その列の詳細を表示します。 この例では、欠落インデックス グループのハンドルを 24 としています。  
  
```  
SELECT migs.group_handle, mid.*  
FROM sys.dm_db_missing_index_group_stats AS migs  
INNER JOIN sys.dm_db_missing_index_groups AS mig  
    ON (migs.group_handle = mig.index_group_handle)  
INNER JOIN sys.dm_db_missing_index_details AS mid  
    ON (mig.index_handle = mid.index_handle)  
WHERE migs.group_handle = 24;  
```  
  
 このクエリを実行すると、インデックスが欠落しているデータベース、スキーマ、テーブルの名前が返されます。 また、インデックス キーに使用される列の名前も返されます。 欠落したインデックスを実装するには、リストの先頭に等号列、CREATE INDEX DDL ステートメントとし、非等値列を ON に書き込むときに\< *table_name*> CREATE INDEX ステートメントの句。 付加列は、CREATE INDEX ステートメントの INCLUDE 句で指定します。 等値列の有効な順序を決定するには、最初に最も高い列を一覧表示、選択度に基づいてそれらを注文 (左端の列リストで)。  
  
## <a name="see-also"></a>参照  
 [sys.dm_db_missing_index_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sys.dm_db_missing_index_groups &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
  
