---
title: SQL Server 2014 のエディションとコンポーネント |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Enterprise Edition [SQL Server]
- Developer Edition [SQL Server]
- 32-bit vs. 64-bit editions [SQL Server]
- default components
- Workgroup Edition [SQL Server]
- Internet servers [SQL Server]
- installing SQL Server, components
- Setup [SQL Server], components
- SQL Server, editions
- SQL Server, components
- client/server applications [SQL Server]
- editions [SQL Server]
- versions [SQL Server]
- Setup [SQL Server], editions
- SQL Server Installation Wizard
- components [SQL Server]
- Standard Edition [SQL Server]
- 64-bit edition [SQL Server]
- IIS [SQL Server]
- installing SQL Server, editions
- editions [SQL Server], about edition options
- Setup [SQL Server]
ms.assetid: e5186f02-dd91-47d0-8fa4-de3f41c76903
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9610dc1cc729dc555d42c0dfe5eeb117f9cfba18
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62806350"
---
# <a name="editions-and-components-of-sql-server-2014"></a>SQL Server 2014 のエディションとコンポーネント
  インストールの前提条件は、アプリケーションのニーズによって異なります。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] にはさまざまなエディションがあり、組織や個人の独自のパフォーマンス、ランタイム、および価格に関する要件に対応できます。 インストールする [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] コンポーネントは、ユーザーの特定の要件によっても異なります。 この後のセクションでは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の最適なエディションおよびコンポーネントを選択する方法について説明します。  
  
## <a name="principal-editions-of-includesscurrentincludessscurrent-mdmd"></a>[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] のプリンシパル エディション  
 次の表で、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のプリンシパル エディションについて説明します。 詳細については、次を参照してください[SQL Server 2014 の各エディションでサポートされる機能。](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エディション|定義|  
|---------------------------------------|----------------|  
|Enterprise (64 ビットおよび 32 ビット)|プレミアム製品である [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Enterprise Edition は、非常に優れたパフォーマンス、無制限の仮想化、およびエンド ツー エンドのビジネス インテリジェンスを備えた包括的なハイエンド データセンター機能を提供することで、ミッション クリティカルなワークロードのための高水準のサービス レベルを実現し、エンド ユーザーがデータの意味を理解できるようにします。|  
|Business Intelligence (64 ビットおよび 32 ビット)|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Business Intelligence Edition は、安全かつスケーラブルで管理しやすい BI ソリューションのビルドおよび配置を可能にする包括的なプラットフォームを提供します。 ブラウザー ベースのデータ探索と視覚化; など、魅力的な機能を提供します。強力なデータのマッシュ アップ機能と強化された統合管理します。|  
|Standard (64 ビットおよび 32 ビット)|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Standard Edition は、企業部門や小規模組織がアプリケーションを実行するための基本的なデータ管理/ビジネス インテリジェンス データベースを提供し、内部設置型およびクラウド用の一般的な開発ツールをサポートすることで、最小限の IT リソースでデータベースを効果的に管理することを可能にします。|  
  
## <a name="specialized-editions-of-includesscurrentincludessscurrent-mdmd"></a>[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] の特別エディション  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の特別エディションは、ビジネス ワークロードを対象とするエディションです。 次の表で、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の特別エディションについて説明します。  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エディション|説明|  
|---------------------------------------|-----------------|  
|Web (64 ビットおよび 32 ビット)|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Web Edition は、大小さまざまな規模の Web 資産に対応できるスケーラビリティ、経済性、および管理性を備えた、Web ホスティング企業および Web VAP 向けの総保有コストの低いオプションです。|  
  
## <a name="breadth-editions-of-includesscurrentincludessscurrent-mdmd"></a>[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] の拡張エディション  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の拡張エディションは、特定の顧客シナリオに合わせて設計されており、無料または非常に低い価格で提供されます。 次の表で、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の拡張エディションについて説明します。  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エディション|説明|  
|---------------------------------------|-----------------|  
|Developer (64 ビットおよび 32 ビット)|開発者は、[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Developer Edition を使用して、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上で動作するあらゆる種類のアプリケーションを開発できます。 このエディションには Enterprise Edition の機能がすべて含まれていますが、実稼動サーバーとして使用するのではなく、開発およびテスト システムとしての利用に対してライセンスが供与されます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer は、アプリケーションを作成し、テストするユーザーに適しています。|  
|Express (64 ビットおよび 32 ビット) エディション|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Express Edition はエントリレベルの無料のデータベースで、学習や、デスクトップおよび小規模サーバー データ ドリブン アプリケーションの構築などに適しています。 このエディションは、独立系ソフトウェア ベンダー、開発者、クライアント アプリケーションを趣味で開発する開発者などに最適です。 さらに高度なデータベース機能が必要な場合には、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express を [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の他の上位バージョンにシームレスにアップグレードできます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express LocalDB は、Express の簡易バージョンです。Express のプログラミング機能をすべて備えながら、ユーザー モードで実行でき、前提条件が少なく構成不要の高速インストールが可能です。|  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-an-internet-server"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] とインターネット サーバーの使用  
 インターネット インフォメーション サービス (IIS) を実行するサーバーなどのインターネット サーバーでは、一般に [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クライアント ツールをインストールします。 クライアント ツールには、アプリケーションが [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のインスタンスに接続する際に使用するクライアント接続コンポーネントが含まれています。  
  
> [!NOTE]  
>  IIS を実行しているコンピューターに [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスをインストールすることは可能ですが、通常はサーバー コンピューターが 1 台の小規模 Web サイトの場合に行います。 ほとんどの Web サイトでは、その中層 IIS システムが 1 つまたはクラスター構成の複数サーバーに配置され、データベースは 1 つの独立したサーバーまたは連合構成の複数サーバーに配置されます。  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-clientserver-applications"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] とクライアント/サーバー アプリケーションの使用  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のクライアント コンポーネントだけを、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のインスタンスに直接接続するクライアント/サーバー アプリケーションを実行するコンピューターにインストールできます。 クライアント コンポーネントをインストールすることは、データベース サーバー上にある [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスを管理する場合、または [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] アプリケーションを開発しようとしている場合にも適切なオプションです。  
  
 クライアント ツールをインストールするオプションを選択すると、下位互換コンポーネント、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 、接続コンポーネント、管理ツール、ソフトウェア開発キット、 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]オンライン ブック コンポーネントなどの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 機能がインストールされます。 詳細については、次を参照してください。[インストール ウィザードからの SQL Server 2014 のインストール&#40;セットアップ&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)します。  
  
## <a name="deciding-among-includessnoversionincludesssnoversion-mdmd-components"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] コンポーネントの決定  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインストールに含めるコンポーネントを選択するには、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]インストール ウィザードの [機能の選択] ページを使用します。 既定では、ツリーの中に、選択されている機能はありません。  
  
 以下の表の情報を参照し、ニーズに最も合う機能を判断してください。  
  
|サーバー コンポーネント|説明|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]には、データを格納、処理、およびセキュリティで保護するための主要サービスである[!INCLUDE[ssDE](../includes/ssde-md.md)]、レプリケーション、フルテキスト検索、リレーショナル データと XML データの管理ツール、および [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) が含まれます。|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] には、オンライン分析処理 (OLAP) アプリケーションおよびデータ マイニング アプリケーションを作成および管理するためのツールが含まれます。|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] には、表形式、マトリックス形式、グラフィカル形式、および自由形式のレポートを作成、管理、配置するためのサーバー コンポーネントとクライアント コンポーネントが含まれます。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] は、レポート アプリケーション開発用の拡張可能プラットフォームとしても使用できます。|  
|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] は、データを移動、コピー、変換するためのグラフィカル ツールおよびプログラミング可能なオブジェクトのセットです。 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] 用の [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)](DQS) コンポーネントも含まれています。|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) は、マスター データ管理のための [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ソリューションです。 MDS は、あらゆるドメイン (製品、顧客、アカウント) を管理するように構成できます。MDS には、データの管理に使用できる [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] のほかに、階層、きめ細かいセキュリティ、トランザクション、データのバージョン管理、およびビジネス ルールが含まれています。|  
  
|管理ツール|説明|  
|----------------------|-----------------|  
|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のコンポーネントを構成、管理、開発し、それらのコンポーネントへアクセスするための統合環境です。 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] では、すべてのスキル レベルの開発者と管理者が [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]を使用できます。|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャー|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーを使用して、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] サービス、サーバー プロトコル、クライアント プロトコル、およびクライアントの別名に関する基本的な構成管理を行います。|  
|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] には、 [!INCLUDE[ssDE](../includes/ssde-md.md)] または [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]のインスタンスを監視するためのグラフィカル ユーザー インターフェイスが備わっています。|  
|[!INCLUDE[ssDE](../includes/ssde-md.md)] チューニング アドバイザー|[!INCLUDE[ssDE](../includes/ssde-md.md)] チューニング アドバイザーは、最適なインデックスのセット、インデックス付きビュー、およびパーティションの作成に役立ちます。|  
|Data Quality クライアント|DQS サーバーに接続し、データ クレンジング操作を実行するための、非常にシンプルで直感的なグラフィカル ユーザー インターフェイスを備えています。 データ クレンジング操作の際に行われるさまざまな処理を一元的に監視することもできます。|  
|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] は、ビジネス インテリジェンス コンポーネント ( [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]) のソリューションをビルドするための IDE です。<br /><br /> (以前の Business Intelligence Development Studio)。<br /><br /> [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] には、Visual Studio 内で [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プラットフォーム (社内および社外の両方) のデータベース設計を行うデータベース開発者用の統合環境である "データベース プロジェクト" も含まれます。 データベース開発者は、強化された Visual Studio のサーバー エクスプローラーを使用して、データベース オブジェクトおよびデータの作成または編集、クエリの実行を簡単に行うことができます。|  
|接続コンポーネント|クライアントとサーバー間の通信用コンポーネント、および DB-Library、ODBC、OLE DB 用のネットワーク ライブラリをインストールします。|  
  
|ドキュメント|説明|  
|-------------------|-----------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] オンライン ブック|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の主要マニュアル。|  
  
## <a name="see-also"></a>参照  
 [SQL Server のインストール計画](install/planning-a-sql-server-installation.md)   
 [SQL Server 2014 インストール ウィザードからインストール&#40;セットアップ&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)  
  
  
