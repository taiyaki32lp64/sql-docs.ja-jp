---
title: データベース エンジンのアップグレード | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], after upgrade
- Database Engine [SQL Server], upgrading
ms.assetid: 3c036813-36cf-4415-a0c9-248d0a433859
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 84f032e89730aa9828dada1208c6d794db97260b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774980"
---
# <a name="upgrade-database-engine"></a>データベース エンジンのアップグレード
  ここでは、アップグレード プロセスの準備および理解に必要な情報を提供します。内容は以下のとおりです。  
  
-   アップグレードに関する既知の問題  
  
-   アップグレード前の作業と注意点  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]をアップグレードするための手順のトピックへのリンク  
  
-   データベースを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に移行するための手順のトピックへのリンク  
  
-   フェールオーバー クラスターに関する注意点  
  
-   アップグレード後の作業と注意点  
  
## <a name="known-upgrade-issues"></a>アップグレードに関する既知の問題  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] をアップグレードする前に、「[SQL Server データベース エンジンの旧バージョンとの互換性](../sql-server-database-engine-backward-compatibility.md)」を確認してください。 サポートされるアップグレード シナリオとアップグレードの既知の問題については、「[サポートされているバージョンとエディションのアップグレード](supported-version-and-edition-upgrades.md)」を参照してください。 その他の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントの旧バージョンとの互換性の内容については、「[旧バージョンとの互換性](../../getting-started/backward-compatibility.md)」を参照してください。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のいずれかのエディションから別のエディションへアップグレードする前に、現在使用している機能がアップグレード先のエディションでサポートされているかどうかを確認します。  
  
> [!NOTE]  
>  アップグレードすると[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]の以前のバージョンから[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Enterprise edition、Enterprise Edition を選択します。コア ベース ライセンスと Enterprise Edition。 これらの Enterprise エディションは、ライセンス モードのみが異なります。 詳細については、「 [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)」を参照してください。  
  
## <a name="pre-upgrade-checklist"></a>アップグレード前のチェック リスト  
 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアップグレードは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ プログラムでサポートされています。 また、以前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョンのデータベースを移行することもできます。 移行は、同じコンピューター上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス間で行うことも、別のコンピューター上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスから行うこともできます。 移行オプションには、データベース コピー ウィザードの使用、バックアップ機能と復元機能、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] インポート/エクスポート ウィザードの使用、一括エクスポート/一括インポート方式があります。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]をアップグレードする前に、次のトピックを確認してください。  
  
-   「 [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)」を確認します。  
  
-   「 [Check Parameters for the System Configuration Checker](check-parameters-for-the-system-configuration-checker.md)」を確認します。  
  
-   「 [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)」を確認します。  
  
-   「[サポートされているバージョンとエディションのアップグレード](supported-version-and-edition-upgrades.md)」を確認してください。  
  
-   「[アップグレード アドバイザーを使用したアップグレードの準備](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)」を確認してください。  
  
-   「[分散再生ユーティリティを使用したアップグレードの準備](../../sql-server/install/use-the-distributed-replay-utility-to-prepare-for-upgrades.md)」を確認してください。  
  
-   「 [SQL Server データベース エンジンの旧バージョンとの互換性](../sql-server-database-engine-backward-compatibility.md)」を確認してください。  
  
-   「[クエリ プランの移行](change-the-database-compatibility-mode-and-use-the-query-store.md)」を確認してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をアップグレードする前に、以下の問題点を確認して変更を行います。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが MSX/TSX リレーションシップに参加している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスをアップグレードする場合は、マスター サーバーをアップグレードする前に、対象サーバーをアップグレードします。 ターゲット サーバーより前にマスター サーバーをアップグレードすると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマスター インスタンスに接続できなくなります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 64 ビット版から [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の 64 ビット版にアップグレードする場合は、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] をアップグレードしてから [!INCLUDE[ssDE](../../includes/ssde-md.md)] をアップグレードする必要があります。  
  
-   アップグレード対象のインスタンスからすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース ファイルをバックアップして、必要な場合はこれらのファイルを復元できるようにします。  
  
-   アップグレード対象のデータベース上で適切なデータベース コンソール コマンド (DBCC) を実行して、データベースの一貫性を確保します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントおよびユーザー データベースのアップグレードに必要なディスク容量を見積もります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントで必要とされるディスク容量については、「[SQL Server 2014 のインストールに必要なハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)」を参照してください。  
  
-   既存の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム データベース (master、model、msdb、tempdb) が自動拡張するように構成されていることを確認し、それらが十分なハード ディスク容量を備えていることを確認します。  
  
-   すべてのデータベース サーバーが master データベースにログオン情報を持っていることを確認します。 システム ログオン情報は master データベースに格納されるので、データベースを復元するにはこの作業が重要になります。  
  
-   すべての起動ストアド プロシージャを無効にします。アップグレード プロセスでは、サービスの起動および停止はアップグレード中の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス上で行われます。 起動時にストアド プロシージャを実行すると、アップグレード プロセスをブロックする可能性があります。  
  
-   レプリケーションが最新であることを確認してから、レプリケーションを停止します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] との従属関係を持つすべてのサービスを含むすべてのアプリケーションを終了します。 アップグレード実行中のインスタンスにローカル アプリケーションが接続されている場合は、アップグレード操作が失敗する場合があります。  
  
-   データベース ミラーリングを使用する場合は、「[サーバー インスタンスのアップグレード時に、ミラー化されたデータベースのダウンタイムを最小化する](../database-mirroring/upgrading-mirrored-instances.md)」を参照してください。  
  
## <a name="upgrading-the-database-engine"></a>データベース エンジンのアップグレード  
 現在インストールされている [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンを、バージョン アップグレードで上書きすることができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップの実行時に以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が検出された場合は、以前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プログラム ファイルがすべてアップグレードされ、以前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに保存されているすべてのデータが保持されます。 また、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックがコンピューター上に元の状態のまま残ります。  
  
> [!WARNING]  
>  SQL Server 2014 セットアップ プログラムの実行中に、アップグレード前チェックの実行の一部として、SQL Server インスタンスが停止し、再起動します。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をアップグレードすると、以前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスは上書きされて、コンピューター上に存在しなくなります。 アップグレードする前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースおよび以前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに関連するその他のオブジェクトをバックアップしてください。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] をアップグレードするには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール ウィザードを使用します。  
  
### <a name="database-compatibility-level-after-upgrade"></a>アップグレード後のデータベース互換性レベル  
 互換性レベル、 `tempdb`、 `model`、`msdb`と**リソース**データベースはアップグレード後に 120 に設定されます。 `master` システム データベースの互換性レベルは、アップグレード前と同じです。  
  
 アップグレード前のユーザー データベースの互換性レベルが 100 以上の場合は、アップグレード後も互換性レベルは変わりません。 アップグレード前の互換性レベルが 90 の場合、アップグレードされたデータベースの互換性レベルは 100 に設定されます。これは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]でサポートされている下限の互換性レベルです。  
  
> [!NOTE]  
>  新しいユーザー データベースには、`model` データベースの互換性レベルが継承されます。  
  
## <a name="migrating-databases"></a>データベースの移行  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でバックアップと復元またはデタッチとアタッチの機能を使用して、ユーザー データベースを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスに移行することができます。 詳細については、「[バックアップと復元によるデータベースのコピー](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)」または「[データベースのデタッチとアタッチ &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)」を参照してください。  
  
> [!IMPORTANT]  
>  ソースや対象サーバーで同じ名前を持つデータベースは移動またはコピーすることはできません。 このような場合は、"既に存在します" と通知されます。  
  
 詳細については、「 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)」を参照してください。  
  
## <a name="after-upgrading-the-database-engine"></a>データベース エンジンのアップグレード後の作業  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]をアップグレードした後は、次の作業を実行します。  
  
-   サーバーを再登録します。 サーバーの登録の詳細については、「[サーバーの登録](../../ssms/register-servers/register-servers.md)」を参照してください。  
  
-   クエリ結果のセマンティクスの一貫性を維持するために、フルテキスト カタログを再作成します。  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] により、フルテキスト検索およびセマンティック検索に使用する新しいワード ブレーカーがインストールされます。 ワード ブレーカーは、インデックスの作成時とクエリ時の両方に使用されます。 フルテキスト カタログを再構築しない場合は、検索結果の一貫性が失われる可能性があります。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のワード ブレーカーと現在のワード ブレーカーで区切りが異なるフレーズを検索するフルテキスト クエリを発行すると、そのフレーズを含むドキュメントまたは行が検索されない場合があります。 これはインデックスされたフレーズがクエリとは異なるロジックで区切られたためです。 この問題を解決するには、新しいワード ブレーカーを使用してフルテキスト カタログを再作成 (再構築) し、インデックス時とクエリ時の動作が同一になるようにします。  
  
     詳細については、「[sp_fulltext_catalog &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql)」を参照してください。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストールを構成します。 システムのセキュリティを向上させるため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、主要なサービスと機能を個別にインストールし、有効化できるようになっています。  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] によって生成され、パーティション テーブルおよびパーティション インデックスに対するクエリに適用される USE PLAN ヒントを検証または削除します。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、パーティション テーブルとインデックスでのクエリの処理方法が異なります。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] で生成されたプランに USE PLAN ヒントを使用する、パーティション分割されたオブジェクトのクエリには、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]で使用できないプランが含まれる場合があります。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]にアップグレードした後は、次の手順を実行することをお勧めします。  
  
     **USE PLAN ヒントをクエリで直接指定した場合。**  
  
    1.  USE PLAN ヒントをクエリから削除します。  
  
    2.  クエリをテストします。  
  
    3.  オプティマイザーによって適切なプランが選択されない場合は、クエリをチューニングし、USE PLAN ヒントを必要なクエリ プランと共に指定することを検討します。  
  
     **USE PLAN ヒントをプラン ガイドで指定した場合。**  
  
    1.  sys.fn_validate_plan_guide 関数を使用して、プラン ガイドの有効性を確認します。 また、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]で、Plan Guide Unsuccessful イベントを使用して無効なプラン ガイドを確認することもできます。  
  
    2.  プラン ガイドが有効でない場合は、プラン ガイドを削除します。 オプティマイザーによって適切なプランが選択されない場合は、クエリをチューニングし、USE PLAN ヒントを必要なクエリ プランと共に指定することを検討します。  
  
     USE PLAN ヒントがプラン ガイドで指定されている場合、無効なプランが原因でクエリが失敗することはありません。 この場合、USE PLAN ヒントを使用せずにクエリがコンパイルされます。  
  
 アップグレード前にフルテキストが有効または無効にマーク付けされていたデータベースは、アップグレード後もその状態を維持します。 アップグレード後は、フルテキストが許可されているすべてのデータベースで、フルテキスト カタログが再構築され、自動的に生成されます。 この処理には、多くの時間とリソースが必要になります。 次のステートメントを実行すると、フルテキストのインデックス処理を一時停止することができます。  
  
```  
EXEC sp_fulltext_service 'pause_indexing', 1;  
```  
  
 フルテキスト インデックスの作成を再開するには、次のステートメントを実行します。  
  
```  
EXEC sp_fulltext_service 'pause_indexing', 0;  
```  
  
## <a name="see-also"></a>参照  
 [サポートされているバージョンとエディションのアップグレード](supported-version-and-edition-upgrades.md)   
 [複数のバージョンおよび SQL Server のインスタンスを使用します。](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)   
 [旧バージョンとの互換性](../../getting-started/backward-compatibility.md)   
 [レプリケートされたデータベースのアップグレード](upgrade-replicated-databases.md)  
  
  
