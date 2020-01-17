---
title: 変更データ キャプチャとその他の SQL Server 機能 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- change data capture [SQL Server], other SQL Server features and
ms.assetid: 7dfcb362-1904-4578-8274-da16681a960e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 87fcd7656ff1e86522e4ea398fc49d91acde9a34
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62672072"
---
# <a name="change-data-capture-and-other-sql-server-features"></a>変更データ キャプチャとその他の SQL Server 機能
  このトピックでは、次の機能と変更データ キャプチャとの連携について説明します。  
  
-   [変更の追跡](#ChangeTracking)  
  
-   [データベース ミラーリング](#DatabaseMirroring)  
  
-   [トランザクション レプリケーション](#TransReplication)  
  
-   [変更データ キャプチャが有効になっているデータベースの復元またはアタッチ](#RestoreOrAttach)  
  
##  <a name="ChangeTracking"></a> Change Tracking  
 変更データ キャプチャと [変更の追跡](about-change-tracking-sql-server.md) は、同じデータベースで有効にすることができます。 特に注意が必要な点はありません。 詳細については、「[変更の追跡のしくみ &#40;SQL Server&#41;](work-with-change-tracking-sql-server.md)」を参照してください。  
  
##  <a name="DatabaseMirroring"></a> データベース ミラーリング  
 変更データ キャプチャが有効になっているデータベースをミラー化できます。 フェールオーバー後にキャプチャとクリーンアップが自動的に行われるようにするには、次の手順を実行します。  
  
1.  新しいプリンシパル サーバー インスタンスで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行されていることを確認します。  
  
2.  新しいプリンシパル データベース (以前のミラー データベース) にキャプチャ ジョブとクリーンアップ ジョブを作成します。 ジョブを作成するには、 [sp_cdc_add_job](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql) ストアド プロシージャを使用します。  
  
 クリーンアップまたはキャプチャ ジョブの現在の構成を表示するには、新しいプリンシパル サーバー インスタンスで [sys.sp_cdc_help_jobs](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql) ストアド プロシージャを使用します。 特定のデータベースに対し、キャプチャ ジョブの名前は cdc.*database_name*_capture に、クリーンアップ ジョブの名前は cdc.*database_name*_cleanup になります ( *database_name* はデータベースの名前)。  
  
 ジョブの構成を変更するには、[sys.sp_cdc_change_job](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql) ストアド プロシージャを使用します。  
  
 データベース ミラーリングの詳細については、「[データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)」を参照してください。  
  
##  <a name="TransReplication"></a> Transactional Replication  
 変更データ キャプチャとトランザクション レプリケーションは、同じデータベースで共存できます。ただし、両方の機能が有効になっている場合、変更テーブルが異なる方法で作成されます。 変更データ キャプチャとトランザクション レプリケーションでは、トランザクション ログから変更を読み取る際に、常に同じプロシージャ ( [sp_replcmds](/sql/relational-databases/system-stored-procedures/sp-replcmds-transact-sql)) が使用されます。 自身で変更データ キャプチャが有効にすると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント ジョブによって`sp_replcmds`します。 同じデータベースでは、両方の機能が有効な場合、ログ リーダー エージェントを呼び出す`sp_replcmds`します。 このエージェントは、変更テーブルとディストリビューション データベース テーブルの両方を作成します。 詳細については、「 [Replication Log Reader Agent](../replication/agents/replication-log-reader-agent.md)」を参照してください。  
  
 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースで変更データ キャプチャが有効になっており、2 つのテーブルでキャプチャが有効になっているシナリオについて考えてみます。 変更テーブルを作成するために、キャプチャ ジョブによって `sp_replcmds` が呼び出されます。 データベースでトランザクション レプリケーションが有効になり、パブリケーションが作成されます。 次に、ログ リーダー エージェントがデータベースに対して作成され、キャプチャ ジョブが削除されます。 ログ リーダー エージェントは、変更テーブルにコミットされた最後のログ シーケンス番号からログのスキャンを続行します。 これにより、変更テーブル内のデータの一貫性が確保されます。 このデータベースでトランザクション レプリケーションが無効になっている場合、ログ リーダー エージェントが削除され、キャプチャ ジョブが再作成されます。  
  
> [!NOTE]  
>  変更データ キャプチャとトランザクション レプリケーションの両方でログ リーダー エージェントを使用している場合、レプリケートされた変更が最初にディストリビューション データベースに書き込まれます。 次に、キャプチャされた変更が変更テーブルに書き込まれます。 両方の操作は同時にコミットされます。 ディストリビューション データベースへの書き込みの際に遅延が生じた場合、変更テーブルに変更が表示される前に、それに対応する遅延が発生します。  
  
 変更データ キャプチャが有効な場合、トランザクション レプリケーションの **proc exec** オプションは使用できません。  
  
##  <a name="RestoreOrAttach"></a> 変更データ キャプチャが有効になっているデータベースの復元またはアタッチ  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、データベースが復元またはアタッチされた後に変更データ キャプチャを有効のままにするかどうかを、次のロジックに従って判断します。  
  
-   データベースを同じサーバーに同じデータベース名で復元した場合、変更データ キャプチャは有効のままです。  
  
-   データベースを別のサーバーに復元した場合、既定では変更データ キャプチャが無効になり、関連するメタデータがすべて削除されます。  
  
     変更データ キャプチャを保持するには、データベースを復元する際に `KEEP_CDC` オプションを使用します。 このオプションの詳細については、「 [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql)」を参照してください。  
  
-   データベースをデタッチしてから、同じサーバーまたは別のサーバーにアタッチした場合、変更データ キャプチャは有効のままです。  
  
-   データベースをアタッチまたは復元、`KEEP_CDC`変更データ キャプチャが必要なため、操作、エンタープライズ以外のエディションにオプションがブロックされている[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Enterprise。 エラー メッセージ 934 が表示されます。  
  
     `SQL Server cannot load database '%.*ls' because change data capture is enabled. The currently installed edition of SQL Server does not support change data capture. Either disable change data capture in the database by using a supported edition of SQL Server, or upgrade the instance to one that supports change data capture.`  
  
 [sys.sp_cdc_disable_db](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql) を使用すると、復元またはアタッチされたデータベースから変更データ キャプチャを削除できます。  
  
## <a name="change-data-capture-and-alwayson"></a>変更データ キャプチャと AlwaysON  
 AlwaysON を使用する場合、セカンダリ レプリケーションに対して変更の列挙を行うことにより、プライマリへのディスク負荷を減らす必要があります。  
  
## <a name="see-also"></a>関連項目  
 [変更データ キャプチャの管理と監視 &#40;SQL Server&#41;](../track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
