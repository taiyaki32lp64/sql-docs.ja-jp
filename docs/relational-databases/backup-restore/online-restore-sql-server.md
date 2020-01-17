---
title: オンライン復元 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- online restores [SQL Server]
- online restores [SQL Server], about online restores
ms.assetid: 7982a687-980a-4eb8-8e9f-6894148e7d8c
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: e4f5817fe575422dddeedd525b077dbf643a29b2
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908881"
---
# <a name="online-restore-sql-server"></a>オンライン復元 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  オンライン復元は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition でのみサポートされています。 このエディションの既定で、ファイル復元、ページ復元、または段階的な部分復元はオンラインで行われます。 このトピックの内容は、複数のファイルまたはファイル グループを含むデータベース (単純復旧モデルでは、読み取り専用ファイル グループのみ) に関連しています。  
  
 データベースがオンラインのときにデータを復元する処理を *オンライン復元*といいます。 プライマリ ファイル グループがオンラインの場合、1 つ以上のセカンダリ ファイル グループがオフラインでも、そのデータベースはオンラインと見なされます。 どの復旧モデルでも、データベースがオンラインであれば、オフラインのファイルを復元できます。 完全復旧モデルでは、データベースがオンラインであれば、ページも復元できます。  
  
> [!NOTE]  
>  オンライン復元は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise で自動的に実行されるため、ユーザーが操作を行う必要はありません。 オンライン復元を使用しない場合は、復元を開始する前にデータベースをオフラインにできます。 詳細については、このトピックの「 [データベースまたはファイルのオフライン化](#taking_db_or_file_offline)」を参照してください。  
  
 オンライン ファイル復元では、復元するファイルとそのファイル グループがオフラインになります。 オンライン復元を開始するときに、復元するいずれかのファイルがオンラインの場合、そのファイルのファイル グループは最初の復元ステートメントによってオフラインになります。 一方、オンラインのページ復元では、ページのみがオフラインになります。  
  
 オンライン復元シナリオには、次の基本的な手順が含まれます。  
  
1.  データを復元します。  
  
2.  最後のログの復元に WITH RECOVERY を使用します。 この操作により、復元したデータがオンラインになります。  

 場合によっては、ロールバックに必要なデータが起動時にオフラインになっているために、コミットされていないトランザクションをロールバックできないことがあります。 このような場合は、トランザクションの処理が遅延されます。 詳細については、「 [遅延トランザクション &#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md)」を参照してください。  
  
> [!NOTE]  
>  データベースで一括ログ復旧モデルを使用している場合は、完全復旧モデルに切り替えてからオンライン復元を開始することをお勧めします。 詳細については、「[データベースの復旧モデルの表示または変更 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)」を参照してください。  
  
> [!IMPORTANT]  
>  サーバーに接続された複数のデバイス使用してバックアップを行った場合は、オンライン復元時に同じ数のデバイスを使用できるようにしておく必要があります。  
  
> [!CAUTION]  
>  スナップショット バックアップを使用する場合は、 **オンライン復元**を実行できません。 **スナップショット バックアップ**の詳細については、「 [Azure でのデータベース ファイルのスナップショット バックアップ](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)」を参照してください。  
  
## <a name="log-backups-for-online-restore"></a>オンライン復元のログ バックアップ  
 オンライン復元の場合、復旧ポイントとは、復元しているデータがオフラインになった時点、または前回読み取り専用に設定された時点です。 復旧ポイントに至るまでのトランザクション ログ バックアップ、およびこの復旧ポイントを含むトランザクション ログ バックアップが、すべて使用可能になっている必要があります。 通常、ファイルの復旧ポイントに対応するには、復旧ポイント以降のログ バックアップが必要です。 唯一の例外は、データが読み取り専用になった後に作成されたデータ バックアップから、読み取り専用データのオンライン復元を実行する場合です。 この場合、ログ バックアップは必要ありません。  
  
 通常、データベースがオンラインの間は、復元シーケンスを開始した後でも、トランザクション ログ バックアップを実行できます。 最後のログ バックアップのタイミングは、復元されるファイルのプロパティによって異なります。  
  
-   読み取り専用のオンライン ファイルの場合、最初の復元シーケンスの前または最中に、復旧に必要な最後のログ バックアップを実行できます。 読み取り専用ファイル グループでは、ファイル グループが読み取り専用になった後にデータ バックアップまたは差分バックアップが実行された場合、ログ バックアップは不要です。  
  
    > [!NOTE]  
    >  上記の情報は、オフライン ファイルにも当てはまります。  
  
-   最初の復元ステートメントが実行された時点でオンラインになっていた読み取りと書き込みが可能なファイル、またはその復元ステートメントで自動的にオフラインになった読み取りと書き込みが可能なファイルは、特殊なケースです。 この場合、最初の *復元シーケンス* (復元、ロールフォワード、およびデータの復旧を行う、1 つ以上の RESTORE ステートメントのシーケンス) の間にログ バックアップを実行する必要があります。 通常、このログ バックアップは、すべての完全バックアップの復元後かつデータ復旧の前に行われる必要があります。 ただし、特定のファイル グループに対して複数のファイル バックアップが存在する場合、ログ バックアップの最小復旧ポイントはそのファイル グループがオフラインになった後の時点になります。 このデータ復元後のログ バックアップにより、ファイルがオフラインになった時点がキャプチャされます。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ではオンライン復元のオンライン ログを使用できないので、データ復元後のログ バックアップが必要です。  
  
    > [!NOTE]  
    >  または、復元シーケンスの前に手動でファイルをオフラインにすることもできます。 詳細については、このトピックの「データベースまたはファイルのオフライン化」を参照してください。  
  
##  <a name="taking_db_or_file_offline"></a> データベースまたはファイルのオフライン化  
 オンライン復元を使用しない場合、次のいずれかの方法で、復元シーケンスを開始する前にデータベースをオフラインにできます。  
  
-   どの復旧モデルでも、次の [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) ステートメントを使用することにより、データベースをオフラインにできます。  
  
     ALTER DATABASE *database_name* SET OFFLINE  
  
-   完全復旧モデルでは、次の [BACKUP LOG](../../t-sql/statements/backup-transact-sql.md) ステートメントを使用してデータベースを復元状態にすることにより、ファイル復元またはページ復元を強制的にオフラインで実行することができます。  
  
     BACKUP LOG *database_name* WITH NORECOVERY.  
  
 データベースがオフライン状態の間、すべての復元処理はオフライン復元になります。  
  
## <a name="examples"></a>使用例  
  
> [!NOTE]  
>  オンライン復元シーケンスでは、オフライン復元シーケンスと同じ構文を使用します。  
  
-   [例: データベースの段階的な部分復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [例: 一部のファイル グループのみを復元する段階的な部分復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [例: 読み取り専用ファイルのオンライン復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [例: データベースの段階的な部分復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [例: 一部のファイル グループのみを復元する段階的な部分復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [例: 読み取り/書き込みファイルのオンライン復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [例: 読み取り専用ファイルのオンライン復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [ファイルおよびファイル グループの復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [ページ復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)  
  
-   [suspect_pages テーブルの管理 &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
-   [データを復元しないデータベースの復旧 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)  
  
-   [機能していないファイル グループの削除 &#40;SQL Server&#41;](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [ファイル復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [ファイルの復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [ページ復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [段階的な部分復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [復元と復旧の概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)  
  
  
