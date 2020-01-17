---
title: 変更データ キャプチャとその他の SQL Server 機能
ms.custom: seo-dt-2019
ms.date: 01/02/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- change data capture [SQL Server], other SQL Server features and
ms.assetid: 7dfcb362-1904-4578-8274-da16681a960e
author: rothja
ms.author: jroth
ms.openlocfilehash: e29ad6de65172b08bb3f35aa89820ca817a9e1d3
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095295"
---
# <a name="change-data-capture-and-other-sql-server-features"></a>変更データ キャプチャとその他の SQL Server 機能
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]
  このトピックでは、次の機能と変更データ キャプチャとの連携について説明します。  
  
-   [変更の追跡](#ChangeTracking)  
  
-   [データベース ミラーリング](#DatabaseMirroring)  
  
-   [トランザクション レプリケーション](#TransReplication)  
  
-   [変更データ キャプチャが有効になっているデータベースの復元またはアタッチ](#RestoreOrAttach)

-   [包含データベース](#Contained)
  
##  <a name="ChangeTracking"></a> 変更の追跡  
 変更データ キャプチャと [変更の追跡](../../relational-databases/track-changes/about-change-tracking-sql-server.md) は、同じデータベースで有効にすることができます。 特に注意が必要な点はありません。 詳細については、「[変更の追跡のしくみ &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-tracking-sql-server.md)」を参照してください。  
  
##  <a name="DatabaseMirroring"></a> データベース ミラーリング  
 変更データ キャプチャが有効になっているデータベースをミラー化できます。 フェールオーバー後にキャプチャとクリーンアップが自動的に行われるようにするには、次の手順を実行します。  
  
1.  新しいプリンシパル サーバー インスタンスで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行されていることを確認します。  
  
2.  新しいプリンシパル データベース (以前のミラー データベース) にキャプチャ ジョブとクリーンアップ ジョブを作成します。 ジョブを作成するには、 [sp_cdc_add_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md) ストアド プロシージャを使用します。  
  
 クリーンアップまたはキャプチャ ジョブの現在の構成を表示するには、新しいプリンシパル サーバー インスタンスで [sys.sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md) ストアド プロシージャを使用します。 特定のデータベースに対し、キャプチャ ジョブの名前は cdc.*database\_name*\_capture に、クリーンアップ ジョブの名前は cdc.*database\_name*\_cleanup になります (*database_name* はデータベースの名前)。  
  
 ジョブの構成を変更するには、 [sys.sp_cdc_change_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md) ストアド プロシージャを使用します。  
  
 データベース ミラーリングの詳細については、「[データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)」を参照してください。  
  
##  <a name="TransReplication"></a> Transactional Replication  
 変更データ キャプチャとトランザクション レプリケーションは、同じデータベースで共存できます。ただし、両方の機能が有効になっている場合、変更テーブルが異なる方法で作成されます。 変更データ キャプチャとトランザクション レプリケーションでは、トランザクション ログから変更を読み取る際に、常に同じプロシージャ ( [sp_replcmds](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)) が使用されます。 変更データ キャプチャのみが有効になっている場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブによって **sp_replcmds**が呼び出されます。 同じデータベースで両方の機能が有効になっている場合は、ログ リーダー エージェントによって **sp_replcmds**が呼び出されます。 このエージェントは、変更テーブルとディストリビューション データベース テーブルの両方を作成します。 詳細については、「 [Replication Log Reader Agent](../../relational-databases/replication/agents/replication-log-reader-agent.md)」を参照してください。  
  
 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースで変更データ キャプチャが有効になっており、2 つのテーブルでキャプチャが有効になっているシナリオについて考えてみます。 変更テーブルを作成するために、キャプチャ ジョブによって **sp_replcmds**が呼び出されます。 データベースでトランザクション レプリケーションが有効になり、パブリケーションが作成されます。 次に、ログ リーダー エージェントがデータベースに対して作成され、キャプチャ ジョブが削除されます。 ログ リーダー エージェントは、変更テーブルにコミットされた最後のログ シーケンス番号からログのスキャンを続行します。 これにより、変更テーブル内のデータの一貫性が確保されます。 このデータベースでトランザクション レプリケーションが無効になっている場合、ログ リーダー エージェントが削除され、キャプチャ ジョブが再作成されます。  
  
> [!NOTE]  
>  変更データ キャプチャとトランザクション レプリケーションの両方でログ リーダー エージェントを使用している場合、レプリケートされた変更が最初にディストリビューション データベースに書き込まれます。 次に、キャプチャされた変更が変更テーブルに書き込まれます。 両方の操作は同時にコミットされます。 ディストリビューション データベースへの書き込みの際に遅延が生じた場合、変更テーブルに変更が表示される前に、それに対応する遅延が発生します。  
  
 変更データ キャプチャが有効な場合、トランザクション レプリケーションの **proc exec** オプションは使用できません。  
  
##  <a name="RestoreOrAttach"></a> 変更データ キャプチャが有効になっているデータベースの復元またはアタッチ  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、データベースが復元またはアタッチされた後に変更データ キャプチャを有効のままにするかどうかを、次のロジックに従って判断します。  
  
-   データベースを同じサーバーに同じデータベース名で復元した場合、変更データ キャプチャは有効のままです。  
  
-   データベースを別のサーバーに復元した場合、既定では変更データ キャプチャが無効になり、関連するメタデータがすべて削除されます。  
  
     変更データ キャプチャを保持するには、データベースを復元する際に **KEEP_CDC** オプションを使用します。 このオプションの詳細については、「 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)」を参照してください。  
  
-   データベースをデタッチしてから、同じサーバーまたは別のサーバーにアタッチした場合、変更データ キャプチャは有効のままです。  
  
-   **KEEP_CDC** オプションを使用してデータベースを Standard または Enterprise 以外のエディションにアタッチまたは復元しようとすると、操作がブロックされます。これは変更データ キャプチャを使用するには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard または Enterprise Edition が必要であるためです。 エラー メッセージ 934 が表示されます。  
  
     `SQL Server cannot load database '%.*ls' because Change Data Capture is enabled. The currently installed edition of SQL Server does not support Change Data Capture. Either restore database without KEEP_CDC option, or upgrade the instance to one that supports Change Data Capture.`  
  
 [sys.sp_cdc_disable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md) を使用すると、復元またはアタッチされたデータベースから変更データ キャプチャを削除できます。  
  
##  <a name="Contained"></a> 包含データベース  
 変更データ キャプチャは、[包含データベース](../../relational-databases/databases/contained-databases.md)ではサポートされていません。
  
## <a name="change-data-capture-and-always-on"></a>変更データ キャプチャと AlwaysOn  
 AlwaysOn を使用する場合、セカンダリ レプリケーションに対して変更の列挙を行うことにより、プライマリへのディスク負荷を減らす必要があります。  
  
## <a name="see-also"></a>参照  
 [変更データ キャプチャの管理と監視 &#40;SQL Server&#41;](../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
