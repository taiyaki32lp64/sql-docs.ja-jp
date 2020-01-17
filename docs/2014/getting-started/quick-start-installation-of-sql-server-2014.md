---
title: SQL Server 2014 | のクイックスタートインストールMicrosoft Docs
ms.custom: ''
ms.date: 11/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- quick start installation [SQL Server]
- installation [SQL Server]
- installing SQL Server, quick start installations
ms.assetid: 672afac9-364d-4946-ad5d-8a2d89cf8d81
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8bd173abbb6ee355429d891a49f672bb0ac818d2
ms.sourcegitcommit: 7183735e38dd94aa3b9bab2b73ccab54c916ff86
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2019
ms.locfileid: "74683611"
---
# <a name="quick-start-installation-of-sql-server-2014"></a>SQL Server 2014 のクイック スタート インストール
    
## <a name="introduction"></a>はじめに  
 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インストール ウィザードは、Windows インストーラーをベースにしています。 このインストール ウィザードの 1 つの機能ツリーから次の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] コンポーネントをインストールできます。  
  
-   [!INCLUDE[ssDE](../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]  
  
-   [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)]  
  
-   管理ツール  
  
-   接続コンポーネント  
  
 各コンポーネントを個別にインストールするか、上記のコンポーネントを組み合わせて選択できます。 で[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]使用できるエディションとコンポーネントを選択するには、「 [SQL Server 2014 のエディションとコンポーネント](../sql-server/editions-and-components-of-sql-server-2016.md)」を参照してください。  
  
 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] には 32 ビット版と 64 ビット版があります。 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] セットアップでは、次のインストール方法がサポートされています。  
  
-   **インストールウィザード**  
  
     インストールウィザードを使用してをインストールする[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]手順については、「インストール[ウィザードから SQL Server 2014 をインストールする」 &#40;セットアップ&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)を参照してください。  
  
-   **コマンドプロンプト**  
  
     無人セットアップを実行するためのサンプル構文とインストールパラメーターについては[、「コマンドプロンプトから SQL Server 2014 をインストール](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)する」を参照してください。  
  
-   **構成ファイル**  
  
     構成ファイルを使用してセットアップを実行するためのサンプル構文とインストールパラメーターについては[、構成ファイルを使用した SQL Server 2014 のインストール](../database-engine/install-windows/install-sql-server-using-a-configuration-file.md)に関する参照してください。  
  
-   **SysPrep**  
  
     SysPrep を使用したのインストール[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の手順については、「 [Sysprep を使用して SQL Server 2014 をインストール](../database-engine/install-windows/install-sql-server-using-sysprep.md)する」を参照してください。  
  
-   **Server Core のインストール**  
  
     Windows Server Core へののインストール[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の手順については、「 [server core に SQL Server 2014 をインストール](../database-engine/install-windows/install-sql-server-on-server-core.md)する」を参照してください。  
  
-   **[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] BI 機能のインストール**  
  
     Microsoft bi プラットフォームの一部である機能のインストールについては、「 [SQL Server 2014 bi 機能のインストール](../sql-server/install/install-sql-server-business-intelligence-features.md)」 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]を[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]参照[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]し[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]てください。これには、、、、、および分析データの作成または操作に使用されるいくつかのクライアントアプリケーションが含まれます。  
  
-   **フェールオーバー クラスター インストール**  
  
     フェールオーバークラスターへののインストール[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の手順について[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]は、「 [SQL Server フェールオーバークラスターのインストール](../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)」を参照してください。  
  
 既定では、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のセットアップ時にサンプル データベースとサンプル コードはインストールされません。 Express 以外のエディションの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のサンプル データベースとサンプル コードをインストールするには、[CodePlex Web サイト](https://go.microsoft.com/fwlink/?LinkId=87843)をご覧ください。 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のサンプル データベースと [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] のサンプル コードのサポートについては、「[データベースとサンプルの概要](https://go.microsoft.com/fwlink/?LinkId=110391)」をご覧ください。  
  
## <a name="includessnoversionincludesssnoversion-mdmd-installation"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]スト  
 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インストール ウィザードを使用する場合でも、コマンド プロンプトから [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] をインストールする場合でも、セットアップ時には以下の 1 つ以上の手順を実行する必要があります。  
  
-   インストール要件、システム構成チェック、および [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインストールに関するセキュリティ上の考慮事項を確認します。  詳細については、「[SQL Server のインストール計画](quick-start-installation-of-sql-server-2014.md#BKMK_BeforeYouInstall)」を参照してください。  
  
-   
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] セットアップを実行して、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の既存のバージョンを [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] にアップグレードします。 詳細については、「 [SQL Server 2014 へのアップグレード](#BKMK_Upgrading)」を参照してください。  
  
-   
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] セットアップを実行して、[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] の新しいインスタンスをインストールします。 詳細については、「 [SQL Server 2014 のインストール](#BKMK_Install)」を参照してください。  
  
-   
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインストールが完了したら、次に、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] とそのコンポーネントを構成します。これは重要な手順です。 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティを使用して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]を構成します。 詳細については、「 [SQL Server 2014 の構成](#BKMK_Configure)」を参照してください。  
  
 次のセクションでは、これらのタスクについて詳しく説明します。  
  
## <a name="related-tasks"></a>Related Tasks  
  
###  <a name="BKMK_BeforeYouInstall"></a>インストールの[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]計画  
 
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] をインストールする前に、ハードウェアとソフトウェアの要件、ネットワークとインターネットに関する考慮事項、および [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] をインストールして実行するためのセキュリティ上の考慮事項を確認する必要があります。 詳細については、「 [SQL Server のインストールの計画](../../2014/sql-server/install/planning-a-sql-server-installation.md)」と、次のトピックも参照してください。  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|ハードウェアとソフトウェアの要件、オペレーティング システムのサポート、ネットワークとインターネットに関する考慮事項、および必要なハード ディスク領域について確認します。|[インストールの前提条件](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]インストールのセキュリティに関する考慮事項を確認します。|[セキュリティに関する考慮事項](../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)|  
|
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] のさまざまなエディションでサポートされる機能の詳細を確認します。|[機能とエディション](features-supported-by-the-editions-of-sql-server-2014.md)|  
|
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の最適なエディションおよびコンポーネントを決定します。|[SQL Server 2014 のエディションとコンポーネント](../sql-server/editions-and-components-of-sql-server-2016.md)|  
|ハードウェア構成を確認し、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] フェールオーバー クラスターのインストールの準備について学習します。|[フェールオーバークラスタリングをインストールする前に](../sql-server/failover-clusters/install/before-installing-failover-clustering.md)|  
  
###  <a name="BKMK_Upgrading"></a>へのアップグレード[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 
  [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]、[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] の既存のインスタンスを [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] にアップグレードできます。 詳細については、「 [SQL Server 2014 へのアップグレード](../database-engine/install-windows/upgrade-sql-server.md)」を参照してください。 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] セットアップを実行して [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] にアップグレードする前に、アップグレード プロセスに関する以下のトピックを参照してください。  
  
|説明|トピック|  
|-----------------|-----------|  
|サポートされる [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] へのアップグレード パスについて説明します。|[サポートされるアップグレード](../database-engine/install-windows/supported-version-and-edition-upgrades.md)|  
|アップグレード アドバイザーについて説明します。アップグレード アドバイザーは、[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]、[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] のインスタンスを分析し、アップグレードに関する既知の問題を報告するツールです。|[アップグレードアドバイザーを使用してアップグレードを準備する](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)|  
|分散再生ユーティリティについて説明します。分散再生ユーティリティは、複数のコンピューターを使用してトレース データを再生し、ミッションクリティカルなワークロードをシミュレートできるツールです。 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] アップグレードの前後でテスト サーバーの再生を実行することで、パフォーマンスの差を測定したり、アップグレード時にアプリケーションに非互換性が発生するかどうかを調べることができます。|[分散再生ユーティリティを使用したアップグレードの準備](../../2014/sql-server/install/use-the-distributed-replay-utility-to-prepare-for-upgrades.md)|  
|
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] へのアップグレード後にアプリケーションに影響を及ぼす可能性のある重要な変更内容を一覧表示します。|[旧バージョンとの互換性](backward-compatibility.md)|  
|
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のスタンドアロン インスタンスを [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] にアップグレードする手順に関するトピックです。|[インストールウィザード &#40;セットアップを使用して SQL Server 2014 にアップグレード&#41;](../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)|  
|
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] のエディションを別のエディションにアップグレードする手順に関するトピックです。 各エディションでサポートされるアップグレード パスについては、「 [サポートされているバージョンとエディションのアップグレード](../database-engine/install-windows/supported-version-and-edition-upgrades.md)」をご覧ください。|[SQL Server 2014 の別のエディションにアップグレードする &#40;セットアップ&#41;](../database-engine/install-windows/upgrade-to-a-different-edition-of-sql-server-setup.md)|  
|
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、すべてのフェールオーバー クラスター ノードで個別に、[!INCLUDE[ssDE](../includes/ssde-md.md)]、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]、[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] から [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] のフェールオーバー クラスターに[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]および [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] をアップグレードすることがサポートされています。 詳細については、このトピックを参照してください。|[SQL Server フェールオーバークラスターのアップグレード](../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)|  
  
###  <a name="BKMK_Install"></a>中[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 次のトピックで、[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] のさまざまなインストール シナリオを確認してください。  
  
|説明|トピック|  
|-----------------|-----------|  
|
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] のさまざまなコンポーネントのインストールに関するトピックと、[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] のインストール手順に関するトピックへのリンクが記載されています。|[SQL Server 2014 をインストールする](../database-engine/install-windows/install-sql-server.md)|  
|このトピックを参照して、Windows Server Core に [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] をインストールします。|[Server Core への SQL Server 2014 のインストール](../database-engine/install-windows/install-sql-server-on-server-core.md)|  
|このトピックを参照して、既存の [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] インスタンスに個々の機能を追加します。|[SQL Server 2014 &#40;セットアップのインスタンスに機能を追加&#41;](../database-engine/install-windows/add-features-to-an-instance-of-sql-server-setup.md)|  
|このトピックを参照して、新しい [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスを作成します。|[セットアップ &#40;新しい SQL Server フェールオーバークラスターを作成し&#41;](../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)|  
|このトピックを参照して、既存の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスのノードを管理します。|[SQL Server フェールオーバークラスターのノードを追加または削除する &#40;セットアップ&#41;](../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)|  
|このトピックを参照して、フェールオーバー クラスターに [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クライアント ツールをインストールします。|[SQL Server フェールオーバー クラスターへのクライアント ツールのインストール](../sql-server/failover-clusters/install/install-client-tools-on-a-sql-server-failover-cluster.md)|  
|コンピューターにインストールされている [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のバージョンおよび [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の機能を確認するための SQL の検出レポートの使用方法を確認します。|[SQL Server のインストールの検証](../database-engine/install-windows/validate-a-sql-server-installation.md)|  
|インストール ウィザード、コマンド プロンプト、構成ファイル、および SysPrep を使用して [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] をインストールするための手順に関するトピックへのリンクが記載されています。|[インストール方法に関するトピック](../../2014/sql-server/install/installation-how-to-topics.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
 このセクションでは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の構成およびアンインストールについて説明します。  
  
###  <a name="BKMK_Configure"></a>構成[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインストールが完了したら、グラフィカル ユーティリティやコマンド プロンプト ユーティリティを使用して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] をさらに構成できます。 初めて [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] を構成する場合は、次のトピックを参照してください。  
  
|説明|トピック|  
|-----------------|-----------|  
|このトピックでは、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] または PowerPivot for SharePoint へのアクセスを許可するためにファイアウォールのポートのブロックを解除する必要があるかどうかを判断するための情報を提供します。 このトピックで示す手順に従って、ポートとファイアウォールを構成できます。|[Analysis Services アクセスを許可するように Windows ファイアウォールを構成する](https://docs.microsoft.com/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access)|  
|このトピックでは、ファイアウォール構成の概要について説明し、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理者を対象とした情報がまとめられています。|[SQL Server アクセスを許可するように Windows ファイアウォールを構成する](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|  
|このトピックでは、マルチホーム環境内の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスへのネットワーク接続用に [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] とセキュリティが強化された Windows ファイアウォールを構成する方法について説明します。|[SQL Server アクセス用にマルチホームコンピューターを構成する](../../2014/sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|  
  
###  <a name="BKMK_Uninstalling"></a>取り外し[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 次のトピックでは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のスタンドアロン インスタンスとフェールオーバー クラスター インスタンスを手動でアンインストールする方法について説明します。  
  
|説明|トピック|  
|-----------------|-----------|  
|このトピックでは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のスタンドアロン インスタンスを手動でアンインストールする方法について説明します。|[SQL Server 2014 のアンインストール](../sql-server/install/uninstall-sql-server.md)|  
|このトピックでは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のフェールオーバー クラスター インスタンスをアンインストールする方法について説明します。|[SQL Server のフェールオーバークラスターインスタンスを削除する &#40;セットアップ&#41;](../sql-server/failover-clusters/install/remove-a-sql-server-failover-cluster-instance-setup.md)|  
|このトピックでは、[!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] または DQS サーバーのみをアンインストールした後に [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (DQS) オブジェクトを手動で削除する方法について説明します。|[Data Quality Server オブジェクトの削除](../../2014/sql-server/install/remove-data-quality-server-objects.md)|  
  
## <a name="see-also"></a>参照  
 [SQL Server 2014 の製品仕様](sql-server-2014-product-specifications.md)   
 SQL Server[旧バージョン](backward-compatibility.md)[との互換性を維持するための製品ドキュメントを使って](../2014-toc/index.yml)みる  
  
  
