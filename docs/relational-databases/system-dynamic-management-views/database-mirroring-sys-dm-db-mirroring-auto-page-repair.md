---
title: sys.dm_db_mirroring_auto_page_repair (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_mirroring_auto_page_repair_TSQL
- sys.dm_db_mirroring_auto_page_repair_TSQL
- sys.dm_db_mirroring_auto_page_repair
- dm_db_mirroring_auto_page_repair
dev_langs:
- TSQL
helpviewer_keywords:
- automatic page repair
- database mirroring [SQL Server], automatic page repair
- sys.dm_db_mirroring_auto_page_repair dynamic management view
ms.assetid: 49f0fc2a-e25e-47e1-a135-563adb509af1
author: stevestein
ms.author: sstein
ms.openlocfilehash: e08aa031af0bd8c9d5c5ad012d11c534281f92f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017908"
---
# <a name="database-mirroring---sysdmdbmirroringautopagerepair"></a>データベース ミラーリング - sys.dm_db_mirroring_auto_page_repair
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  サーバー インスタンス上のミラー化されたデータベースに対して試行されたページの自動修復ごとに 1 行を返します。 このビューには、ミラー化された特定のデータベースに対して最近試行されたページの自動修復に対応する行が含まれます (データベースあたり最大 100 行)。 データベースあたりの最大行数に達すると、その後に試行されたページの自動修復の行によって、既存のエントリが置き換えられます。 次の表では、さまざまな列の意味を定義します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|この行に対応するデータベースの ID。|  
|**file_id**|**int**|ページが配置されているファイルの ID。|  
|**page_id**|**bigint**|ファイル内のページの ID です。|  
|**error_type**|**int**|エラーの種類です。 値を指定できます。<br /><br /> **-** 1 = すべてのハードウェア 823 エラー<br /><br /> 1 = 824 以外は、不適切なチェックサムまたは破損ページ (不適切なページ ID) などのエラー<br /><br /> 2 = 不適切なチェックサム<br /><br /> 3 = 破損ページ|  
|**page_status**|**int**|ページ修復の試行ステータスです。<br /><br /> 2 = パートナーからの要求を待機中。<br /><br /> 3 = 送信される要求をパートナーにします。<br /><br /> 4 = ページの自動修復 (パートナーから受信した応答) の待機中です。<br /><br /> 5 = ページの自動修復に成功し、ページは使用可能。<br /><br /> 6 = Irreparable します。 これは、パートナーで、ページが破損していることも、パートナーが切断された場合、またはネットワークの問題が発生したため、たとえば、エラーを発生ページ修復の試行中にしたことを示します。 この状態がターミナルです。破損は、ページでもう一度発生した場合、ページが、パートナーからもう一度要求されます。|  
|**modification_time**|**datetime**|ページの状態の最終変更時刻。|  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [ページの自動修復 &#40;可用性グループ:データベース ミラーリング&#41;](../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [suspect_pages &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md)   
 [suspect_pages テーブルの管理 &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  


