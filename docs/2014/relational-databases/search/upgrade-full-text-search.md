---
title: フルテキスト検索のアップグレード | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], installing
- migrating full-text indexes [SQL Server]
- upgrading Full-Text Search
- installing Full-Text Search
- full-text search [SQL Server], upgrading
ms.assetid: 2fee4691-f2b5-472f-8ccc-fa625b654520
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 43ef487dc2049d3ca95f4cddff72a005c98a5d19
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010958"
---
# <a name="upgrade-full-text-search"></a>フルテキスト検索のアップグレード
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] へのフルテキスト検索のアップグレードは、セットアップ時のほか、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータベース ファイルとフルテキスト カタログのアタッチ時、復元時、またはデータベース コピー ウィザードによるコピー時に行われます。  
  
 このトピックでは、フルテキスト検索のアップグレードに関して、次の点について説明します。  
  
-   [サーバー インスタンスのアップグレード](#Upgrade_Server)  
  
-   [フルテキスト アップグレード オプション](#FT_Upgrade_Options)  
  
-   [アップグレード オプションの完全なテキストの選択に関する注意点](#Choosing_Upgade_Option)  
  
-   [データベースを SQL Server 2014 にアップグレードするときに、フルテキスト インデックスの移行](#Upgrade_Db)  
  
-   [SQL Server 2014 への SQL Server 2005 フルテキスト カタログの復元に関する注意点](#Considerations_for_Restore)  
  
-   [SQL Server 2014 への SQL Server 2005 データベースのアタッチ](#Attaching_2005_ft_catalogs)  
  
##  <a name="Upgrade_Server"></a> サーバー インスタンスのアップグレード  
 インプレース アップグレードでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のインスタンスが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の旧バージョンとサイド バイ サイドでセットアップされ、データが移行されます。 旧バージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にフルテキスト検索がインストールされている場合、新しいバージョンのフルテキスト検索が自動的にインストールされます。 サイド バイ サイド インストールとは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスごとに次のコンポーネントが存在することを意味します。  
  
 ワード ブレーカー、ステミング機能、フィルター  
 各インスタンスは、オペレーティング システムのバージョンと関係なく、固有のワード ブレーカー、ステミング機能、フィルターのセットを使用するようになりました。 これらのコンポーネントは、インスタンス レベルで簡単に登録し、構成できます。 詳細については、「 [検索用のワード ブレーカーとステミング機能の構成と管理](configure-and-manage-word-breakers-and-stemmers-for-search.md) 」と「 [検索用フィルターの構成と管理](configure-and-manage-filters-for-search.md)」を参照してください。  
  
 フィルター デーモン ホスト  
 フルテキスト フィルター デーモン ホストは、インデックスとクエリに使用する外部の拡張コンポーネント (ワード ブレーカー、ステミング機能、フィルターなど) を、Full-Text Engine の整合性を損なわずに安全に読み込み、駆動するプロセスです。 サーバー インスタンスでは、マルチスレッド フィルターに対してはすべてマルチスレッド処理が使用され、シングル スレッド フィルターに対してはすべてシングル スレッド処理が使用されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] では、FDHOST ランチャー サービス (MSSQLFDLauncher) のサービス アカウントが導入されました。 このサービスにより、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の特定インスタンスのフィルター デーモン ホスト プロセスに対してサービス アカウント情報が反映されます。 サービス アカウントの設定の詳細については、「 [フルテキスト フィルター デーモン ランチャーのサービス アカウントの設定](set-the-service-account-for-the-full-text-filter-daemon-launcher.md)」を参照してください。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]では、各フルテキスト インデックスは、ファイル グループに属するフルテキスト カタログに存在し、物理パスを持ち、データベース ファイルとして扱われます。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンでは、フルテキスト カタログは、フルテキスト インデックスのグループを含んだ論理的 (仮想) オブジェクトです。 したがって、新しいフルテキスト カタログは、物理パスを持つデータベース ファイルとしては扱われません。 ただし、データ ファイルを含むフルテキスト カタログのアップグレード時に、新しいファイル グループが同じディスク上に作成されます。 これにより、アップグレード後も以前のディスク I/O 動作が維持されます。 ルート パスが存在する場合、そのカタログのフルテキスト インデックスは、すべて新しいファイル グループに配置されます。 前のフルテキスト カタログのパスが無効の場合、フルテキスト インデックスは、ベース テーブルと同じファイル グループで保持されるか、パーティション テーブルの場合にはプライマリ ファイル グループで保持されます。  
  
> [!NOTE]  
>  フルテキスト カタログを指定する [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] の [!INCLUDE[tsql](../../includes/tsql-md.md)] DDL ステートメントは、引き続き正常に動作します。  
  
##  <a name="FT_Upgrade_Options"></a> フルテキスト アップグレード オプション  
 サーバー インスタンスを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]にアップグレードする場合、次のいずれかのフルテキスト アップグレード オプションをユーザー インターフェイスで選択できます。  
  
 [インポート]  
 フルテキスト カタログがインポートされます。 通常、インポートの方が再構築よりもかなり高速に処理されます。 たとえば、CPU を 1 つだけ使用している場合、インポートは、再構築の約 10 倍の速さで実行されます。 ただし、インポートされたフルテキスト カタログでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の最新バージョンでインストールされる新しいワード ブレーカーが使用されません。 クエリ結果の一貫性を維持するためには、フルテキスト カタログを再作成する必要があります。  
  
> [!NOTE]  
>  再構築はマルチスレッド モードで実行できます。10 を超える CPU が使用可能な場合に、再構築でそれらの CPU をすべて使用できるようにすると、再構築の方がインポートよりも高速に実行されることがあります。  
  
 フルテキスト カタログが使用できない場合は、関連付けられたフルテキスト インデックスが再構築されます。 このオプションは [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] データベースでのみ使用できます。  
  
 フルテキスト インデックスのインポートによる影響については、後の「フルテキスト アップグレード オプションの選択に関する注意点」を参照してください。  
  
 Rebuild  
 フルテキスト カタログは、導入された新しい拡張機能であるワード ブレーカーを使用して再構築されます。 インデックスの再構築には時間がかかり、アップグレード後に膨大な量の CPU とメモリが必要になる可能性があります。  
  
 リセット  
 フルテキスト カタログがリセットされます。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]からのアップグレード時には、フルテキスト カタログ ファイルは削除されますが、フルテキスト カタログのメタデータおよびフルテキスト インデックスは保持されます。 アップグレード後、すべてのフルテキスト インデックスで変更の追跡は無効化されており、クロールは自動的には開始されません。 アップグレードの完了後、手動で完全作成を実行するまで、カタログは空のままになります。  
  
##  <a name="Choosing_Upgade_Option"></a> アップグレード オプションの完全なテキストの選択に関する注意点  
 アップグレードのためにアップグレード オプションを選択する際は、次の点を考慮してください。  
  
-   クエリ結果の一貫性が必要かどうか。  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] により、フルテキスト検索およびセマンティック検索に使用する新しいワード ブレーカーがインストールされます。 ワード ブレーカーは、インデックスの作成時とクエリ時の両方に使用されます。 フルテキスト カタログを再構築しない場合は、検索結果の一貫性が失われる可能性があります。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のワード ブレーカーと現在のワード ブレーカーで区切りが異なるフレーズを検索するフルテキスト クエリを発行すると、そのフレーズを含むドキュメントまたは行が検索されない場合があります。 これはインデックスされたフレーズがクエリとは異なるロジックで区切られたためです。 この問題を解決するには、新しいワード ブレーカーを使用してフルテキスト カタログを再作成 (再構築) し、インデックス時とクエリ時の動作が同一になるようにします。 これは [再構築] オプションを選択することによって実現できます。または、[インポート] オプションを選択した後で、手動で再構築することもできます。  
  
-   整数型のフルテキスト キー列に基づいて構築されているフルテキスト インデックスがあるかどうか。  
  
     再構築では内部最適化処理が実行されます。これにより、アップグレードされたフルテキスト インデックスのクエリ パフォーマンスが向上することがあります。 具体的には、ベース テーブルのフルテキスト キー列が整数データ型であるフルテキスト インデックスを含むフルテキスト カタログがある場合、再構築によって、アップグレード後のフルテキスト クエリのパフォーマンスが理想的なものになります。 この場合は、 **[再構築]** オプションを使用することを強くお勧めします。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のフルテキスト インデックスでは、フルテキスト キーとして機能する列を整数データ型にすることをお勧めします。 詳細については、「 [フルテキスト インデックスのパフォーマンスの向上](improve-the-performance-of-full-text-indexes.md)」を参照してください。  
  
-   サーバー インスタンスをオンラインにする場合に何を優先するか。  
  
     アップグレード時のインポートまたは再構築では CPU リソースを大量に消費するので、その他のサーバー インスタンスがアップグレードされてオンラインになるのが遅れます。 できるだけ早くサーバー インスタンスをオンラインにすることが重要であり、アップグレード後に手動作成を実行してもよい場合は、 **[リセット]** が最適です。  
  
## <a name="ensuring-consistent-query-results-after-importing-a-sql-server-2005-full-text-index"></a>SQL Server 2005 フルテキスト インデックスのインポート後にクエリ結果の一貫性を確保する  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] データベースから [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]へのアップグレード時にフルテキスト カタログをインポートした場合、新旧のワード ブレーカーにおける動作の違いから、クエリとフルテキスト インデックスの内容との間に不一致が生じる可能性があります。 この場合、クエリとフルテキスト インデックスの内容を確実に完全一致させるためには、次のいずれかのオプションを選択します。  
  
-   フルテキスト インデックスを含むフルテキスト カタログを再構築します ([ALTER FULLTEXT CATALOG](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql)*catalog_name* REBUILD)。  
  
-   フルテキスト インデックスに FULL POPULATION を実行します ([ALTER FULLTEXT INDEX](/sql/t-sql/statements/alter-fulltext-index-transact-sql) ON *table_name* START FULL POPULATION)。  
  
 ワード ブレーカーの詳細については、「 [検索用のワード ブレーカーとステミング機能の構成と管理](configure-and-manage-word-breakers-and-stemmers-for-search.md)」を参照してください。  
  
## <a name="upgrading-noise-word-files-to-stoplists"></a>ノイズ ワード ファイルからストップリストへのアップグレード  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] のノイズ ワードは、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンではストップワードになりました。 データベースが [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] から [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]にアップグレードされると、ノイズ ワード ファイルは使用されなくなります。 ただし、古いノイズ ワード ファイルは FTDATA\ FTNoiseThesaurusBak フォルダーに保存され、後で更新する際、または対応する [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ストップリストを作成する際に使用できます。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]からのアップグレード後  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]のインストール時のノイズ ワード ファイルを追加、変更、または削除しなかった場合は、システム ストップリストでニーズが満たされます。  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]でノイズ ワード ファイルが変更された場合は、アップグレード時にその変更が失われます。 このような更新を再作成するには、対応する [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] のストップリストで、これらの変更を手動で再作成する必要があります。 詳細については、「[ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)」を参照してください。  
  
-   フルテキスト インデックスにストップワードを適用しない場合 (たとえば、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] のインストールでノイズ ワード ファイルを削除または消去した場合) は、アップグレードされたフルテキスト インデックスごとに、ストップリストを無効にする必要があります。 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行します ( *database* をアップグレードされたデータベースの名前に置き換え、 *table* を *table*の名前に置き換えます)。  
  
    ```  
    Use database;   
    ALTER FULLTEXT INDEX ON table  
       SET STOPLIST OFF;  
    GO  
    ```  
  
     STOPLIST OFF 句は、ストップワードのフィルター処理を削除し、テーブル作成のトリガーとなります。このとき、ノイズと見なされたワードはフィルター処理されません。  
  
## <a name="backup-and-imported-full-text-catalogs"></a>バックアップとインポートされたフルテキスト カタログ  
 アップグレード時に再構築またはリセットされたフルテキスト カタログ (および新しいフルテキスト カタログ) は論理的概念であり、ファイル グループ内には存在しません。 そのため、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]でフルテキスト カタログをバックアップするには、カタログのフルテキスト インデックスが含まれるファイル グループをすべて特定し、1 つずつバックアップする必要があります。 詳細については、「 [フルテキスト カタログとフルテキスト インデックスのバックアップおよび復元](back-up-and-restore-full-text-catalogs-and-indexes.md)」を参照してください。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]からインポートされたフルテキスト カタログは、元のファイル グループ内のデータベース ファイルのままです。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] におけるフルテキスト カタログのバックアップ プロセスが引き続き適用されます。ただし、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]には MSFTESQL サービスが存在しません。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] におけるプロセスの詳細については、SQL Server 2005 オンライン ブックの「 [フルテキスト カタログのバックアップと復元](https://go.microsoft.com/fwlink/?LinkId=209154) 」を参照してください。  
  
##  <a name="Upgrade_Db"></a> データベースをアップグレードする際のフルテキスト インデックスの移行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータベース ファイルおよびフルテキスト カタログは、アタッチ、復元、またはデータベース コピー ウィザードを使用して、既存の [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] サーバー インスタンスにアップグレードできます。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] のフルテキスト インデックスがある場合は、インポート、リセット、または再構築されます。 **upgrade_option** サーバー プロパティは、これらのデータベース アップグレード時にサーバー インスタンスで使用されるフルテキスト アップグレード オプションを制御します。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] のデータベースを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]にアタッチ、復元、またはコピーした後は、データベースが直ちに使用可能となり、自動的にアップグレードされます。 インデックスを作成するデータ量によって、インポートには数時間、再構築には最大でその 10 倍の時間がかかることがあります。 なお、アップグレード オプションがインポートに設定されており、フルテキスト カタログが使用できない場合は、関連付けられたフルテキスト インデックスが再構築されます。  
  
 **サーバー インスタンスでフルテキスト アップグレード動作を変更するには**  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)]:[sp\_fulltext\_service](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql) の **upgrade\_option** アクションを使用します  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **:** **[サーバーのプロパティ]** ダイアログ ボックスの **[フルテキスト アップグレード オプション]** を使用します。 詳細については、「 [サーバー インスタンスでのフルテキスト検索の管理と監視](manage-and-monitor-full-text-search-for-a-server-instance.md)」を参照してください。  
  
##  <a name="Considerations_for_Restore"></a>[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] のフルテキスト カタログを復元する際の注意点: [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] データベースのフルテキスト データを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] にアップグレードするには、データベースの完全バックアップを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]に復元する方法があります。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] フルテキスト カタログのインポート中に、データベースとカタログ ファイルをバックアップおよび復元できます。 次に示すように、動作は [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]と同じです。  
  
-   データベースの完全バックアップには、フルテキスト カタログが含まれます。 フルテキスト カタログを参照するには、その [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ファイル名 sysft_+*catalog-name*を使用します。  
  
-   フルテキスト カタログがオフラインの場合、バックアップは失敗します。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]フルテキスト カタログのバックアップと復元の詳細については、 オンライン ブックの「[フルテキスト カタログのバックアップと復元 ](https://go.microsoft.com/fwlink/?LinkId=121052)」および「[ファイルのバックアップと復元およびフルテキスト カタログ](https://go.microsoft.com/fwlink/?LinkId=121053)」[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] を参照してください。  
  
 データベースを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]に復元すると、フルテキスト カタログ用の新しいデータベース ファイルが作成されます。 このファイルの既定の名前は、ftrow_*catalog-name*.ndf です。 たとえば、 *catalog-name* が `cat1`の場合、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] データベース ファイルの既定の名前は `ftrow_cat1.ndf`となります。 ただし、作成先のディレクトリでこの既定の名前が既に使用されている場合は、新しいデータベース ファイルの名前は `ftrow_`*catalog-name*`{`*GUID*`}.ndf`となります。 *GUID* は、新しいファイルのグローバル一意識別子です。  
  
 カタログのインポート後、 **sys.database_files** と **sys.master_files**が更新されてカタログ エントリが削除され、 **sys.fulltext_catalogs** の **path** 列が NULL に設定されます。  
  
 **データベースをバックアップするには**  
  
-   [データベースの完全バックアップ &#40;SQL Server&#41;](../backup-restore/full-database-backups-sql-server.md)  
  
-   [トランザクション ログのバックアップ &#40;SQL Server&#41;](../backup-restore/transaction-log-backups-sql-server.md) (完全復旧モデルのみ)  
  
 **データベースのバックアップを復元するには**  
  
-   [データベースの全体復元 &#40;単純復旧モデル&#41;](../backup-restore/complete-database-restores-simple-recovery-model.md)  
  
-   [データベースの全体復元 &#40;完全復旧モデル&#41;](../backup-restore/complete-database-restores-full-recovery-model.md)  
  
### <a name="example"></a>例  
 次の例では、 [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) ステートメントの MOVE 句を使用して、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] という `ftdb1`データベースを復元する方法を示しています。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] のデータベース ファイル、ログ ファイル、およびカタログ ファイルは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] サーバー インスタンス上の新しい場所に、次のように移動されます。  
  
-   データベース ファイル `ftdb1.mdf`は `C:\Program Files\Microsoft SQL Server\MSSQL.1MSSQL12.MSSQLSERVER\MSSQL\DATA\ftdb1.mdf`に移動されます。  
  
-   ログ ファイル `ftdb1_log.ldf`は、ログ ディスク ドライブ上のログ ディレクトリ *log_drive*`:\`*log_directory*`\ftdb1_log.ldf`に移動されます。  
  
-   `sysft_cat90` カタログに対応するカタログ ファイルは、 `C:\temp`に移動されます。 フルテキスト インデックスは、インポートされた後、データベース ファイル C:\ftrow_sysft_cat90.ndf 内に自動的に格納されます。C:\temp は削除されます。  
  
```  
RESTORE DATABASE [ftdb1] FROM  DISK = N'C:\temp\ftdb1.bak' WITH  FILE = 1,  
   MOVE N'ftdb1' TO N'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\ftdb1.mdf',  
    MOVE N'ftdb1_log' TO N'log_drive:\log_directory\ftdb1_log.ldf',  
    MOVE N'sysft_cat90' TO N'C:\temp';  
```  
  
##  <a name="Attaching_2005_ft_catalogs"></a> SQL Server 2005 データベースのアタッチ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンでは、フルテキスト カタログは、フルテキスト インデックスのグループを指す論理的概念です。 フルテキスト カタログは、ファイル グループに属さない仮想オブジェクトです。 しかし、フルテキスト カタログ ファイルを含む [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] データベースを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] サーバー インスタンスにアタッチする場合、カタログ ファイルは [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]と同様に他のデータベース ファイルと一緒に以前の場所からアタッチされます。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] にアタッチされた各フルテキスト カタログの状態は、データベースが [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]からデタッチされたときと同じです。 フルテキスト インデックスの作成がデタッチ操作により中断されていた場合、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]でその作成が再開され、このフルテキスト インデックスがフルテキスト検索に使用できるようになります。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] がフルテキスト カタログ ファイルを見つけられない場合、またはアタッチ操作時に新しい場所を指定せずにフルテキスト ファイルが移動された場合、選択したフルテキスト アップグレード オプションによって動作が異なります。 フルテキスト アップグレード オプションが **[インポート]** または **[再構築]** の場合、アタッチされたフルテキスト カタログは再構築されます。 フルテキスト アップグレード オプションが **[リセット]** の場合、アタッチされたフルテキスト カタログはリセットされます。  
  
 データベースのデタッチとアタッチの詳細については、「[データベースのデタッチとアタッチ &#40;SQL Server&#41;](../databases/database-detach-and-attach-sql-server.md)」、「[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)」、「[sp_attach_db](/sql/relational-databases/system-stored-procedures/sp-attach-db-transact-sql)」、「[sp_detach_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-detach-db-transact-sql)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [フルテキスト検索の概要](get-started-with-full-text-search.md)   
 [検索用のワード ブレーカーとステミング機能の構成と管理](configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [検索用フィルターの構成と管理](configure-and-manage-filters-for-search.md)  
  
  
