---
title: ページの自動修復 (可用性グループとデータベース ミラーリング) の |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- automatic page repair
- Availability Groups [SQL Server], automatic page repair
- database mirroring [SQL Server], automatic page repair
- suspect pages [SQL Server]
ms.assetid: cf2e3650-5fac-4f34-b50e-d17765578a8e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f4f39024817d3d0aa35c015ed815eb8f412f1c8e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63137515"
---
# <a name="automatic-page-repair-for-availability-groups-and-database-mirroring"></a>ページの自動修復 (可用性グループとデータベース ミラーリング)
  ページの自動修復は、データベース ミラーリングおよび [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]でサポートされます。 特定の種類のエラーによってページが破損し、読み取りができなくなると、データベース ミラーリング パートナー (プリンシパルまたはミラー) または可用性レプリカ (プライマリまたはセカンダリ) が自動的にページの修復を試みます。 ページの読み取りができないパートナー/レプリカは、そのページの新しいコピーを自分のパートナーまたは別のレプリカから要求します。 要求が受け入れられ、新しいコピーを取得できた場合は、読み取り不可能なページが読み取り可能なコピーに置き換えられます。通常、これによりエラーは解決します。  
  
 一般に、データベース ミラーリングと [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] は、I/O エラーが同じ方法で処理されます。 ただし、わずかながら異なる部分もあります。ここでは、そうした違いについて説明します。  
  
> [!NOTE]  
>  ページの自動修復は DBCC 修復とは異なります。 ページの自動修復では、すべてのデータが保持されます。 一方、DBCC REPAIR_ALLOW_DATA_LOSS オプションを使用してエラーを修正すると、一部のページ (データ) が削除されることがあります。  
  
  
  
##  <a name="ErrorTypes"></a> ページの自動修復が試行されるエラーの種類  
 次の表に示すいずれかのエラーが原因でデータ ファイル操作が失敗した場合のみ、そのページにデータベース ミラーリングの自動修復が適用されます。  
  
|エラー番号|説明|ページの自動修復の原因となるインスタンス|  
|------------------|-----------------|---------------------------------------------------------|  
|[823](../../relational-databases/errors-events/mssqlserver-823-database-engine-error.md)|オペレーティング システムがデータの巡回冗長検査 (CRC) を実行し、それに失敗した場合のみ処理が行われます。|ERROR_CRC。 このエラーのオペレーティング システムの値は 23 です。|  
|[824](../../relational-databases/errors-events/mssqlserver-824-database-engine-error.md)|論理エラー。|破損した書き込みや不適切なページ チェックサムなどの論理データ エラー。|  
|829|ページが復元待ちとしてマークされています。|すべて。|  
  
 最近発生した 823 CRC エラーおよび 824 エラーを確認するには、 [msdb](/sql/relational-databases/system-tables/suspect-pages-transact-sql) データベースの [suspect_pages](../../relational-databases/databases/msdb-database.md) テーブルを参照してください。  
  
  
  
##  <a name="UnrepairablePageTypes"></a> Page Types That Cannot Be Automatically Repaired  
 次のコントロール ページの種類は、ページの自動修復機能では修復できません。  
  
-   ファイル ヘッダー ページ (ページ ID 0)。  
  
-   ページ 9 (データベースのブート ページ)。  
  
-   アロケーション ページ:グローバル アロケーション マップ (GAM) ページ、共有グローバル アロケーション マップ (SGAM) ページ、およびページ空き容量 (PFS) ページ。  
  

  
##  <a name="PrimaryIOErrors"></a> プリンシパル/プライマリ データベースでの I/O エラーの処理  
 プリンシパル/プライマリ データベースでページの自動修復が試行されるのは、データベースが SYNCHRONIZED 状態にあり、そのデータベースのログ レコードがプリンシパル/プライマリ サーバーからミラー/セカンダリへ送信され続けている場合だけです。 ページの自動修復が試行される場合の基本的な処理順序を次に示します。  
  
1.  プリンシパル/プライマリ データベースのデータ ページで読み取りエラーが発生すると、プリンシパル/プライマリは、該当するエラー状態が記録された行を [suspect_pages](/sql/relational-databases/system-tables/suspect-pages-transact-sql) テーブルに挿入します。 この後、データベース ミラーリングの場合は、プリンシパルがミラーに対してページのコピーを要求します。 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]の場合は、プライマリが、すべてのセカンダリに要求をブロードキャストし、最初に応答したセカンダリからページを取得します。 この要求では、ページ ID と、現在フラッシュされたログの最後にある LSN を指定します。 要求対象のページは、 *復元待ち*としてマークされます。 これにより、ページの自動修復の試行時、このページにはアクセスできなくなります。 修復の試行時にこのページにアクセスしようとすると、エラー 829 (復元待ち) が発生して失敗します。  
  
2.  ページ要求を受け取ったミラー/セカンダリは、まず、その要求で指定されている LSN までログを再実行し、 その後、データベースのコピーに存在する該当ページへのアクセスを試みます。 該当ページにアクセスできた場合は、そのページのコピーをプリンシパル/プライマリに送信します。 アクセスできない場合、ミラー/セカンダリはプリンシパル/プライマリにエラーを返します。つまり、ページの自動修復は失敗となります。  
  
3.  要求したページの新しいコピーが含まれている応答をプリンシパル/プライマリが処理します。  
  
4.  ページの自動修復機能によって問題のあるページが修正されると、 **suspect_pages** テーブルで、そのページが復元済み (**event_type** = 5) としてマークされます。  
  
5.  ページ I/O エラーによって [遅延トランザクション](../../relational-databases/backup-restore/deferred-transactions-sql-server.md)が発生した場合は、ページを修復した後で、プリンシパル/プライマリがそれらのトランザクションを解決しようとします。  
  

  
##  <a name="SecondaryIOErrors"></a> ミラー/セカンダリ データベースでの I/O エラーの処理  
 ミラー/セカンダリ データベースで発生したデータ ページの I/O エラーは通常、データベース ミラーリングでも [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]でも同じように処理されます。  
  
1.  データ ミラーリングでは、ミラーがログ レコードを再実行している最中にページ I/O エラーが 1 回でも検出されると、そのミラーリング セッションは SUSPENDED 状態になります。 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]では、セカンダリ レプリカがログ レコードを再実行している最中にページ I/O エラーが 1 回でも検出されると、そのセカンダリ データベースは SUSPENDED 状態になります。 この時点で、ミラー/セカンダリは、該当するエラー状態が記録された行を **suspect_pages** テーブルに挿入します。 次に、ミラー/セカンダリは、プリンシパル/プライマリにそのページのコピーを要求します。  
  
2.  プリンシパル/プライマリは、そのデータベースのコピーに存在する該当ページにアクセスを試みます。 該当ページにアクセスできた場合は、そのページのコピーをミラー/セカンダリに送信します。  
  
3.  要求したすべてのページのコピーを受け取った時点で、ミラー/セカンダリはミラーリング セッションの再開を試行します。 ページの自動修復機能によって問題のあるページが修正されると、 **suspect_pages** テーブルで、そのページが復元済み (**event_type** = 4) としてマークされます。  
  
     要求したページをプリンシパル/プライマリから受信できない場合、ページの自動修復の試行は失敗です。 データベース ミラーリングでは、ミラーリング セッションは中断されたままになります。 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]では、セカンダリ データベースが中断されたままになります。 ミラーリング セッションまたはセカンダリ データベースを手動で再開すると、破損したページが同期フェーズ時に再びヒットします。  

  
##  <a name="DevBP"></a> Developer Best Practice  
 ページの自動修復は、バックグラウンドで実行される非同期プロセスです。 したがって、読み取ることのできないページを要求した場合はデータベース操作に失敗し、その原因を示すエラー コードが返されます。 ミラー化されたデータベースまたは可用性データベースのアプリケーションを開発するときは、失敗した操作を例外として処理できるようにする必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー コードが 823、824、または 829 のときは、その操作を後で再試行してください。  
  

  
##  <a name="ViewAPRattempts"></a> 方法:ページの自動修復の試行の表示  
 以下の動的管理ビューは、特定の可用性データベースまたはミラー化された特定のデータベースに対して最近試行されたページの自動修復に対応する行を返します (データベースあたり最大 100 行)。  
  
-   **AlwaysOn 可用性グループ:**  
  
     [sys.dm_hadr_auto_page_repair &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-auto-page-repair-transact-sql)  
  
     サーバー インスタンスで任意の可用性グループに対してホストされている可用性レプリカの可用性データベースに対するページの自動修復の試行ごとに 1 行のデータを返します。  
  
-   **データベース ミラーリング:**  
  
     [sys.dm_db_mirroring_auto_page_repair &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-auto-page-repair)  
  
     サーバー インスタンス上のミラー化されたデータベースに対して試行されたページの自動修復ごとに 1 行を返します。  
  
 
  
## <a name="see-also"></a>関連項目  
 [suspect_pages テーブルの管理 &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)   
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
