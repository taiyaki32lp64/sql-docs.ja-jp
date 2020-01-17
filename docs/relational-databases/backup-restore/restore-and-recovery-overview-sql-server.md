---
title: 復元と復旧の概要 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/23/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring tables [SQL Server]
- backups [SQL Server], restore scenarios
- database backups [SQL Server], restore scenarios
- database restores [SQL Server]
- restoring [SQL Server]
- restores [SQL Server]
- table restores [SQL Server]
- restoring databases [SQL Server], about restoring databases
- database restores [SQL Server], scenarios
- accelerated database recovery
ms.assetid: e985c9a6-4230-4087-9fdb-de8571ba5a5f
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 9b034e43f918a0f6c198c29cf2f6618ba38638f8
ms.sourcegitcommit: e7c3c4877798c264a98ae8d51d51cb678baf5ee9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916074"
---
# <a name="restore-and-recovery-overview-sql-server"></a>復元と復旧の概要 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースをエラーから復旧するには、データベース管理者が論理的に正しく意味のある復元シーケンスで一連の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップを復元する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の復元および復旧では、次に示すように、データベース全体、データ ファイル、またはデータ ページの各バックアップからのデータの復元をサポートしています。  
  
-   データベース ( *データベースの全体復元*)  
  
     データベース全体を復元および復旧します。復元および復旧の操作中は、データベースはオフラインになります。  
  
-   データ ファイル ( *ファイル復元*)  
  
     データ ファイルまたはファイルのセットを復元および復旧します。 ファイル復元中は、ファイルを含むファイル グループが自動的にオフラインになります。 オフラインのファイル グループにアクセスするとエラーが発生します。  
  
-   データ ページ ( *ページ復元*)  
  
     完全復旧モデルまたは一括ログ復旧モデルでは、個々のデータベースを復元できます。 ページ復元は、ファイル グループの数に関係なく、どのデータベースでも実行できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバックアップと復元は、サポートされるすべてのオペレーティング システムで機能します。 サポートされているオペレーティング システムについては、「 [SQL Server 2016 のインストールに必要なハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)」を参照してください。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]からのバックアップに対するサポートの情報については、「 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)」の「互換性サポート」のセクションを参照してください。  
  
##  <a name="RestoreScenariosOv"></a> 復元シナリオの概要  
 *の* 復元シナリオ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] とは、1 つ以上のバックアップからデータを復元した後にデータベースを復旧するプロセスです。 サポートされている復元シナリオは、データベースの復旧モデルおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のエディションによって異なります。  
  
 次の表では、さまざまな復旧モデルでサポートされている復元シナリオについて説明しています。  
  
|の|単純復旧モデルの場合|完全/一括ログ復旧モデルの場合|  
|----------------------|---------------------------------|----------------------------------------------|  
|データベースの全体復元|基本的な復元ストラテジです。 データベースの全体復元では、データベースの完全バックアップを復元し復旧するだけになる場合があります。 また、データベースの完全バックアップを復元した後で差分バックアップを復元し復旧する場合もあります。<br /><br /> 詳細については、「[データベースの全体復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)」を参照してください。|基本的な復元ストラテジです。 データベースの全体復元を行うには、データベースの完全バックアップと、必要に応じて差分バックアップ (存在する場合) を復元し、その後で後続のすべてのログ バックアップを順番に復元する必要があります。 データベースの全体復元を完了するには、最新のログ バックアップを復旧して、さらにそれを復元します (RESTORE WITH RECOVERY)。<br /><br /> 詳細については、「[データベースの全体復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)」を参照してください。|  
|File restore **\***|データベース全体を復元することなく、破損した 1 つ以上の読み取り専用ファイルを復元します。 ファイル復元は、データベースに読み取り専用のファイル グループが少なくとも 1 つ含まれている場合だけ使用できます。|データベース全体を復元することなく、1 つ以上のファイルを復元します。 ファイル復元は、データベースがオフラインのときに実行できますが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のエディションによってはオンラインのままでも実行できます。 ファイル復元の間、復元対象のファイルを含むファイル グループは常にオフラインです。|  
|ページ復元|適用なし|破損した 1 つ以上のページを復元します。 ページ復元は、データベースがオフラインのときに実行できますが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のエディションによってはオンラインのままでも実行できます。 ページ復元の間、復元対象のページは常にオフラインです。<br /><br /> 現在のログ ファイルまで、ログ バックアップのチェーンが途切れていないことが必要です。ページを現在のログ ファイルまでの最新状態にするためには、それらをすべて適用する必要があります。<br /><br /> 詳細については、「[ページ復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)」を参照してください。|  
|段階的な部分復元 **\***|データベースをファイル グループ レベルで段階的に復元および復旧します。プライマリ ファイル グループとすべての読み書き可能セカンダリ ファイル グループの復元から行います。|データベースをファイル グループ レベルでプライマリ ファイル グループから段階的に復元および復旧します。<br /><br /> 詳細については、「[段階的な部分復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)」を参照してください|  
  
 **\*** オンライン復元は、Enterprise Edition でのみサポートされます。  

### <a name="steps-to-restore-a-database"></a>データベースを復元する手順
ファイルの復元を実行するために、[!INCLUDE[ssde_md](../../includes/ssde_md.md)] によって次の 2 つの手順が実行されます。 

-   不足しているデータベース ファイルを作成する。

-   バックアップ デバイスからデータベース ファイルにデータをコピーする。

データベースの復元を実行するために、[!INCLUDE[ssde_md](../../includes/ssde_md.md)] によって次の 3 つの手順が実行されます。 

-   データベースとトランザクション ログ ファイルがまだ存在しない場合、作成する。

-   すべてのデータ、ログ、およびインデックス ページを、データベースのバックアップ メディアからデータベース ファイルにコピーする。 

-   [復旧プロセス](#TlogAndRecovery)と呼ばれるものでトランザクション ログを適用する。

 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] では、データの復元方法に関係なく、データベース全体の論理的な一貫性が確保されないと、データベースを復旧できません。 たとえば、ファイルを復元する場合、データベースとの一貫性を維持できるように十分なロールフォワードを行うまでは、ファイルを復旧してオンラインにすることはできません。  
  
### <a name="advantages-of-a-file-or-page-restore"></a>ファイルまたはページを復元する利点  
 データベース全体ではなく、ファイルやページを復元して復旧すると、次のような利点があります。  
  
-   復元するデータが少ないので、コピーと復旧にかかる時間が短縮されます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ファイルまたはページを復元する場合、復元操作中にデータベース内の他のデータをオンラインのままにすることができます。  

## <a name="TlogAndRecovery"></a> 復旧とトランザクション ログ
ほとんどの復元シナリオでは、トランザクション ログ バックアップを適用し、オンラインにするデータベースのために [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] で**復旧プロセス**を実行できるようにする必要があります。 復旧とは、トランザクション的に一貫した (クリーンな) 状態で各データベースを開始させるために、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用されるプロセスです。

フェールオーバーやその他のクリーンでないシャットダウンが発生した場合、データベースは一部の変更がバッファー キャッシュからデータ ファイルに書き込まれない状態になる場合があり、未完了のトランザクションによる変更がデータ ファイル内に存在している可能性もあります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが開始されると、各データベースの復旧が実行されます。これは 3 つのフェーズで構成され、最後の[データベース チェックポイント](../../relational-databases/logs/database-checkpoints-sql-server.md)に基づいています。

-   **分析フェーズ**では、最後のチェックポイントを決定するためにトランザクション ログが分析され、ダーティ ページ テーブル (DPT) とアクティブなトランザクション テーブル (ATT) が作成されます。 DPT には、このデータベースがシャットダウンされたときにダーティだったページのレコードが含まれています。 ATT には、このデータベースがクリーンにシャットダウンされなかったときにアクティブだったトランザクションのレコードが含まれています。

-   **再実行フェーズ**では、データベースがシャットダウンされたときにデータ ファイルに書き込まれていない可能性がある、ログに記録されたすべての変更がロールフォワードされます。 データベース全体の復旧を成功させるために必要な[最小ログ シーケンス番号](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#minlsn) (minLSN) は DPT 内にあり、すべてのダーティ ページで必要な再実行操作の開始がマークされます。 このフェーズでは、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] によって、コミットされたトランザクションに属するすべてのダーティ ページがディスクに書き込まれます。

-   **元に戻すフェーズ**では、ATT 内にある未完了のトランザクションがロールバックされ、データベースの整合性が確保されます。 ロールバック後、データベースはオンラインになり、そのデータベースにそれ以上のトランザクション ログ バックアップを適用できなくなります。

各データベース復旧ステージの進行状況に関する情報は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の[エラーログ](../../tools/configuration-manager/viewing-the-sql-server-error-log.md)に記録されます。 データベース復旧の進行状況は、拡張イベントを使って追跡することもできます。 詳細については、ブログ記事「[データベース復旧の進行状況のための新しい拡張イベント](https://blogs.msdn.microsoft.com/sql_server_team/new-extended-events-for-database-recovery-progress/)」をご覧ください。

> [!NOTE]
> 段階的な部分復元のシナリオでは、読み取り専用ファイル グループがファイルのバックアップの作成前から読み取り専用だった場合は、ログ バックアップをファイル グループに適用する必要はないので、ファイルの復元の際にスキップされます。 

<a name="FastRecovery"></a>
> [!NOTE]
> エンタープライズ環境でデータベースの可用性を最大にするために、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition では、再実行フェーズの後に、元に戻すフェーズを実行したまま、データベースをオンラインにすることができます。 これは、高速復旧と呼ばれます。

##  <a name="RMsAndSupportedRestoreOps"></a> 復旧モデルとサポートされる復元操作  
 データベースで使用できる復元操作は、そのデータベースの復旧モデルによって決まります。 次の表では、特定の復元シナリオごとに、各復旧モデルによりサポートされるかどうかと、どの程度までサポートされるかを示します。  
  
|復元操作|完全復旧モデル|一括ログ復旧モデル|単純復旧モデル|  
|-----------------------|-------------------------|---------------------------------|---------------------------|  
|データの復旧|完全な復旧 (ログが使用可能な場合)。|一部データ損失の可能性。|最新の完全バックアップまたは差分バックアップ以降のデータが損失。|  
|特定の時点での復元|ログ バックアップに含まれる任意の時点。|ログ バックアップに一括ログ記録された変更が含まれている場合は不可。|サポートされていません。|  
|File restore **\***|完全にサポートされます。|場合によりサポートされます。 **\*\***|読み取り専用セカンダリ ファイルの場合のみ使用可能です。|  
|Page restore **\***|完全にサポートされます。|場合によりサポートされます。 **\*\***|[なし] :|  
|段階的な (ファイル グループ レベルの) 部分復元 **\***|完全にサポートされます。|場合によりサポートされます。 **\*\***|読み取り専用セカンダリ ファイルの場合のみ使用可能です。|  
  
 **\*** の Enterprise Edition でのみ使用できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 **\*\*** 必要な条件については、このトピックの「 [単純復旧モデルの復元に関する制限事項](#RMsimpleScenarios)」を参照してください。  
  
> [!IMPORTANT]  
> データベースの復旧モデルにかかわらず、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップを、そのバックアップを作成したバージョンより古いバージョンの [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] に復元することはできません。  
  
## <a name="RMsimpleScenarios"></a> 単純復旧モデルでの復元シナリオ  
 単純復旧モデルの復元操作には次の制限があります。  
  
-   ファイルの復元および段階的な部分復元は、読み取り専用のセカンダリ ファイル グループでのみ使用可能です。 これらの復元シナリオの詳細については、「[ファイルの復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)」および「[段階的な部分復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)」を参照してください。  
  
-   ページ復元は実行できません。  
  
-   特定の時点への復元は実行できません。  
  
 これらの制限事項のいずれかが復旧要件に適合しない場合は、完全復旧モデルの使用を検討することをお勧めします。 詳細については、「 [バックアップの概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)」を参照してください。  
  
> [!IMPORTANT]  
> データベースの復旧モデルにかかわらず、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップは、バックアップを作成したバージョンより古いバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では復元できません。  
  
##  <a name="RMblogRestore"></a> 一括ログ復旧モデルを使用した復元  
 このセクションでは、一括ログ復旧モデルを使用した復元の考慮事項について説明します。一括ログ復旧モデルは、完全復旧モデルの補完のみを目的としたモデルです。  
  
> [!NOTE]  
> 一括ログ復旧モデルの概要については、「[トランザクション ログ &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)」を参照してください。  
  
 全般的には、一括ログ復旧モデルは完全復旧モデルに似ており、完全復旧モデルで説明されている情報はどちらにも適用されます。 ただし、特定の時点への復旧とオンライン復元は、一括ログ復旧モデルの影響を受けます。  
  
### <a name="restrictions-for-point-in-time-recovery"></a>特定の時点への復旧に関する制限  
 一括ログ復旧モデルで作成されたログ バックアップに一括ログ記録された変更が含まれている場合、特定の時点への復旧は実行できません。 一括変更を含むログ バックアップに対して特定の時点への復旧を実行しようとすると、復元操作が失敗します。  
  
### <a name="restrictions-for-online-restore"></a>オンライン復元に関する制限  
 オンライン復元シーケンスは、次の条件を満たしている場合のみ実行できます。  
  
-   復元シーケンスを開始する前に、必要なログ バックアップがすべて作成されていること。  
  
-   オンライン復元シーケンスを開始する前に、一括変更のバックアップが作成されていること。  
  
-   データベースに一括変更が存在する場合、すべてのファイルがオンラインであるか、[機能していない](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md)こと。 (つまり、このデータベースの一部ではなくなっていること)。  
  
 上記の条件を満たしていない場合、オンライン復元シーケンスは失敗します。  
  
> [!NOTE]  
>  オンライン復元を開始する前に、完全復旧モデルに切り替えることをお勧めします。 詳細については、「[復旧モデル &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)」を参照してください。  
  
 オンライン復元の実行方法の詳細については、「[オンライン復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)」を参照してください。  
  
##  <a name="DRA"></a> データベース復旧アドバイザー (SQL Server Management Studio)  
データベース復旧アドバイザーにより、最適な復元シーケンスを実装する復元プランを容易に構築できるようになります。 お客様からご要望のあった、データベース復元に関するさまざまな既知の問題の解決や機能強化が実施されました。 データベース復旧アドバイザーによって導入された主な機能強化は次のとおりです。  
  
-   **復元プラン アルゴリズム:** 特に、複雑な復元シナリオの復元プランの構築に使用されるアルゴリズムが大幅に改善されました。 特定の時点への復元時の分岐シナリオなど、多数のエッジ ケースが以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]よりも効率的に処理されます。  
  
-   **特定の時点への復元:** データベース復旧アドバイザーにより、特定の時点へのデータベースの復元が大幅に簡素化されます。 バックアップの視覚的タイムラインにより、特定の時点への復元のサポートが大幅に強化されています。 この視覚的タイムラインにより、データベースを復元する際の目的の復旧ポイントとして適切な時点を特定できます。 タイムラインにより、分岐した復旧パス (複数の復旧分岐にまたがるパス) をたどることが容易になります。 特定の時点への復元プランには、目的の時点 (日時) への復元に関連するバックアップが自動的に含まれます。 詳細については、「[SQL Server データベースを特定の時点に復元する &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)」を参照してください。  
  
データベース復旧アドバイザーの詳細については、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manageability の次のブログを参照してください。  
  
-   [復旧アドバイザー: 概要](https://blogs.msdn.com/b/managingsql/archive/2011/07/13/recovery-advisor-an-introduction.aspx)  
  
-   [復旧アドバイザー: SSMS を使用して分割バックアップを作成/復元する](https://blogs.msdn.com/b/managingsql/archive/2011/07/13/recovery-advisor-using-ssms-to-create-restore-split-backups.aspx)  

## <a name="adr"></a> 高速データベース復旧
[高速データベース復旧](/azure/sql-database/sql-database-accelerated-database-recovery/)は [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] で利用できます。 高速データベース復旧では、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] の[復旧プロセス](#TlogAndRecovery)の再設計により、データベースの可用性が大幅に向上します (長時間トランザクションが存在する場合は特に)。 高速データベース復旧が有効にされたデータベースでは、フェールオーバーまたは他のクリーンではないシャットダウンの後の復旧プロセスが、非常に速く完了します。 高速データベース復旧を有効にした場合、取り消された長時間トランザクションのロールバックも非常に速く完了します。

[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] では、次の構文を使用して、データベースごとに高速データベース復旧を有効にできます。

```sql
ALTER DATABASE <db_name> SET ACCELERATED_DATABASE_RECOVERY = ON;
```

> [!NOTE]
> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] では、高速データベース復旧が既定で有効になります。

## <a name="RelatedContent"></a> 参照  
 [バックアップの概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)      
 [トランザクション ログ &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)     
 [SQL Server トランザクション ログのアーキテクチャと管理ガイド](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)     
 [SQL Server データベースのバックアップと復元](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)     
 [トランザクション ログ バックアップの適用 (SQL Server)](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)    
