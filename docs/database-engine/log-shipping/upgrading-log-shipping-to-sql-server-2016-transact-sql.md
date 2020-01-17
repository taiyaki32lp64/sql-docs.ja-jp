---
title: SQL Server 2016 以降へのログ配布のアップグレード
description: 以前のバージョンから SQL Server 2016 以降にアップグレードするときに、ログ配布のディザスター リカバリー ソリューションを保持するための適切な順序について説明します。
ms.custom: seo-lt-2019
ms.date: 02/01/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], upgrading
ms.assetid: b1289cc3-f5be-40bb-8801-0e3eed40336e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c3ebe7da68b057e9f84d2b83572a337ede278401
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258567"
---
# <a name="upgrading-log-shipping-to-sql-server-2016-transact-sql"></a>SQL Server 2016 へのログ配布のアップグレード (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログ配布構成を新しい [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョン、新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス パック、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の累積的な更新プログラムにアップグレードする場合、適切な順序でログ配布サーバーをアップグレードすることで、ログ配布のディザスター リカバリー ソリューションが保持されます。  
  
> [!NOTE]  
>  [バックアップの圧縮](../../relational-databases/backup-restore/backup-compression-sql-server.md) は [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]で導入されました。 アップグレードされたログ配布構成では、 **バックアップの圧縮の既定** サーバー レベル構成オプションを使用して、トランザクション ログ バックアップ ファイルにバックアップ圧縮を使用するかどうかを制御します。 ログ バックアップのバックアップ圧縮動作は、ログ配布構成ごとに指定できます。 詳細については、「 [ログ配布の構成 &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md)で導入されました。  
  
 **このトピックの内容**  
  
-   [前提条件](#Prerequisites)  
  
-   [アップグレード前のデータの保護](#ProtectData)  
  
-   [監視サーバー インスタンスのアップグレード](#UpgradeMonitor)  
  
-   [セカンダリ サーバー インスタンスのアップグレード](#UpgradeSecondaries)  
  
-   [プライマリ インスタンスのアップグレード](#UpgradePrimary)  
  
##  <a name="Prerequisites"></a> 前提条件  
 作業を開始する前に、次の重要な情報を確認してください。  
  
-   [サポートされているバージョンとエディションのアップグレード](../../database-engine/install-windows/supported-version-and-edition-upgrades.md):使用している Windows オペレーティング システムと SQL Server のバージョンから SQL Server 2016 にアップグレードできることを確認します。 たとえば、SQL Server 2005 インスタンスから [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]に直接アップグレードすることはできません。  
  
-   [データベース エンジンのアップグレード方法の選択](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md):サポートされるバージョンとエディションのアップグレードを確認して、適切なアップグレードの方法と手順を選択します。また、環境にインストールされているその他のコンポーネントに基づいて、正しい順序でコンポーネントをアップグレードします。  
  
-   [データベース エンジンのアップグレード計画の策定およびテスト](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md):リリース ノート、アップグレードに関する既知の問題、アップグレード前のチェックリストを確認して、アップグレードの計画を作成およびテストします。  
  
-   [SQL Server 2016 のインストールに必要なハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のインストールにおけるソフトウェア要件を確認します。 その他のソフトウェアが必要な場合は、ダウンタイムを最小限に抑えるために、アップグレード プロセスを開始する前に、各ノードにソフトウェアをインストールします。  
  
##  <a name="ProtectData"></a> アップグレード前のデータの保護  
 ログ配布のアップグレードを行う前にデータを保護することをお勧めします。  
  
 **データを保護するには**  
  
1.  すべてのプライマリ データベースを対象にデータベースの完全バックアップを実行します。  
  
     詳細については、「[データベースの完全バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)」を参照してください。  
  
2.  すべてのプライマリ データベースで [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) コマンドを実行します。  
  
> [!IMPORTANT]  
>  セカンダリのアップグレードで見込まれる時間内はログのバックアップ コピーが保持されるように、プライマリ サーバーに十分な領域があることを確認します。  セカンダリにフェールオーバーする場合は、同じ問題がセカンダリ (新しいプライマリ) にも適用されます。  
  
##  <a name="UpgradeMonitor"></a> (省略可能な) 監視サーバー インスタンスのアップグレード  
 監視サーバー インスタンスがある場合、そのインスタンスはいつアップグレードしてもかまいません。 ただし、プライマリとセカンダリ サーバーをアップグレードするときに、省略可能な監視サーバーをアップグレードする必要はありません。  
  
 監視サーバーのアップグレード中もログ配布構成は引き続き機能しますが、その状態は監視テーブルに記録されません。 また、監視サーバーをアップグレードしている間は、構成されている警告がトリガーされません。 アップグレードの完了後、[sp_refresh_log_shipping_monitor](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md) システム ストアド プロシージャを実行して監視テーブルの情報を更新できます。   監視サーバーの詳細については、「[ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)」を参照してください。  
  
##  <a name="UpgradeSecondaries"></a> セカンダリ サーバー インスタンスのアップグレード  
 このアップグレード プロセスでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセカンダリ サーバー インスタンスを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] にアップグレードしてからプライマリ サーバー インスタンスをアップグレードします。 常にセカンダリの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを最初にアップグレードしてください。 アップグレードされたセカンダリ サーバーでは引き続き [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のプライマリ サーバー インスタンスからログ バックアップの復元が行われるため、アップグレード プロセスの間もログ配布は継続されます。 セカンダリ サーバー インスタンスより先にプライマリ サーバー インスタンスをアップグレードすると、ログ配布が失敗します。これは、新しいバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で作成されたバックアップを古いバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で復元することはできないためです。 セカンダリ インスタンスは同時でも順番にでもアップグレードできますが、ログ配布のエラーを避けるため、プライマリ インスタンスのアップグレード前にすべてのセカンダリ インスタンスをアップグレードする必要があります。  
  
 セカンダリ サーバー インスタンスをアップグレードしている間はログ配布のコピーと復元のジョブは実行されません。 つまり、復元されていないトランザクション ログのバックアップがプライマリに蓄積されるため、その復元されていないバックアップを保持するための十分な領域が必要です。 蓄積される量は、プライマリ サーバー インスタンスでスケジュールされているバックアップの頻度と、セカンダリ インスタンスをアップグレードする順序によって異なります。 また、独立した監視サーバーが構成されている場合は、構成されている間隔を経過しても復元が行われないことを知らせる警告が生成されることがあります。  
  
 セカンダリ サーバー インスタンスのアップグレードが完了すると、ログ配布エージェント ジョブが再開され、引き続きプライマリ サーバー インスタンスのログ バックアップがセカンダリ サーバー インスタンスにコピーおよび復元されます。 セカンダリ サーバー インスタンスでセカンダリ データベースが最新の状態になるまでにかかる時間は、セカンダリ サーバー インスタンスのアップグレードにかかった時間とプライマリ サーバーのバックアップの頻度に依存します。  
  
> [!NOTE]  
>  サーバー アップグレードの過程では、セカンダリ データベース自体は [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] データベースにアップグレードされません。 ログ配布済みデータベースのフェールオーバーを開始してオンラインになるとアップグレードされます。 理論上は、この状況は無限に続きます。 フェールオーバーが開始され、データベースのメタデータのアップグレードにかかる時間はわずかです。  
  
> [!IMPORTANT]  
>  アップグレードが必要なデータベースに対しては RESTORE WITH STANDBY オプションはサポートされません。 アップグレードされたセカンダリ データベースが RESTORE WITH STANDBY を使用して構成されている場合、アップグレード後にトランザクション ログを復元できなくなります。 そのセカンダリ データベースでのログ配布を再開するには、そのスタンバイ サーバーでもう一度ログ配布を設定する必要があります。 STANDBY オプションの詳細については、「[トランザクション ログ バックアップの復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)」を参照してください。  
  
##  <a name="UpgradePrimary"></a> プライマリ サーバー インスタンスのアップグレード  
 ログ配布は主にディザスター リカバリー ソリューションであるため、最も単純で一般的なシナリオは、プライマリ インスタンスを適切にアップグレードすることです。データベースはこのアップグレード中は使用できなくなります。 サーバーのアップグレードが完了すると、データベースが自動的にオンラインに戻り、データベースのアップグレードが行われます。 データベースのアップグレードが完了すると、ログ配布ジョブが再開されます。  
  
> [!NOTE]  
>  ログ配布では、[ログ配布のセカンダリへのフェールオーバー &#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)のオプションもサポートしています。また、[プライマリ ログ配布サーバーとセカンダリ ログ配布サーバー間でのロールの変更 &#40;SQL Server&#41;](../../database-engine/log-shipping/change-roles-between-primary-and-secondary-log-shipping-servers-sql-server.md)もできます。 ただし、ログ配布が高可用性ソリューションとして構成されることは今後ほとんどないため (新しいオプションの方が堅牢性がかなり高い)、フェールオーバーでは通常ダウンタイムが最小化されません。フェールオーバーではシステム データベース オブジェクトが同期されず、昇格したセカンダリを見つけて接続しやすくするためのクライアントを有効にする方が難しいためです。  
  
## <a name="see-also"></a>参照  
 [インストール ウィザードを使用した SQL Server 2016 へのアップグレード &#40;セットアップ&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [コマンド プロンプトからの SQL Server 2016 のインストール](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [ログ配布の構成 &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md)   
 [ログ配布の監視 &#40;Transact-SQL&#41;](../../database-engine/log-shipping/monitor-log-shipping-transact-sql.md)   
 [ログ配布テーブルとストアド プロシージャ](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)  
  
  
