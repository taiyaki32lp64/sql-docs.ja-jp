---
title: 並列データウェアハウスのコンポーネント
description: この記事では、Analytics Platform System のアプライアンスソフトウェアとアプライアンス以外のソフトウェアコンポーネントについて説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 5e609585e464cb52b996f45c7d8c57aaffcd79fe
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400932"
---
# <a name="parallel-data-warehouse-components---analytics-platform-system"></a>並列データウェアハウスコンポーネント-分析プラットフォームシステム
この記事では、Analytics Platform System のアプライアンスソフトウェアとアプライアンス以外のソフトウェアコンポーネントについて説明します。  
  
<!-- MISSING LINKS

To learn more about Analytics Platform System, see:  
  
-   [Analytics Platform System architecture](architecture-overview.md)  
  
-   [Distributed and Replicated Tables &#40;SQL Server PDW&#41;](../sqlpdw/distributed-and-replicated-tables-sql-server-pdw.md)  
  
-   [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  
  
-   [Clustered Columnstore Indexes &#40;SQL Server PDW&#41;](../sqlpdw/clustered-columnstore-indexes-sql-server-pdw.md)  
  
-   [Query Process &#40;SQL Server PDW&#41;](../sqlpdw/query-process-sql-server-pdw.md)  
  
-   [Minimum and Maximum Values &#40;SQL Server PDW&#41;](../sqlpdw/minimum-and-maximum-values-sql-server-pdw.md)  

-->
   
  
![並列データウェアハウスソフトウェア](media/parallel-data-warehouse-software.png "並列データウェアハウスソフトウェア")  
  
## <a name="sec1"></a>アプライアンスソフトウェア-クエリ処理とユーザーデータストレージ  
  
### <a name="control-node"></a>制御ノード  
MPP エンジン  
MPP エンジンは、超並列処理 (MPP) システムの頭脳です。 その内容は次のとおりです。  
  
-   並列クエリプランを作成し、計算ノードでの並列クエリの実行を調整します。  
  
-   すべてのデータベースのメタデータと構成データを格納および調整します。  
  
-   SQL Server PDW データベースの認証と承認を管理します。  
  
-   ハードウェアとソフトウェアの状態を追跡します。  
  
### <a name="data-movement-service-dms"></a>データ移動サービス (DMS)  
データ移動サービス (DMS) は、PDW の "secret ソース" の一部です。 その内容は次のとおりです。  
  
-   SQL Server PDW のノードとの間でデータを転送します。  
  
-   ノード間でのデータ転送を必要とするクエリ操作を処理します。  
  
-   データ転送速度を最適化することで、クエリのパフォーマンスを向上させます。  
  
### <a name="admin-console"></a>管理コンソール  
管理コンソールは、アプライアンスの状態、正常性、およびパフォーマンスの情報を表示する web アプリケーションです。  
  
### <a name="configuration-manager"></a>構成マネージャー  
Configuration Manager (dwconfig .exe) は、アプライアンス管理者が分析プラットフォームシステムを構成するために使用するツールです。  
  
### <a name="control-node-databases"></a>ノードデータベースの制御  
SQL Server は、コントロールノード上のすべてのデータベースを管理します。  
  
-   シェルデータベースは、すべての分散ユーザーデータベースのメタデータを管理します。  
  
-   TempDB には、アプライアンス全体のすべてのユーザー一時テーブルのメタデータが含まれます。  
  
-   Master は、コントロールノード上の SQL Server のマスターテーブルです。  
  
### <a name="compute-node"></a>計算ノード  
コンピューティングノードは、並列データ処理とストレージユニットです。 直接接続されたストレージがあり、SQL Server を使用してユーザーデータを管理します。  
  
### <a name="data-movement-service-dms"></a>データ移動サービス (DMS)  
データ移動サービス (DMS) は、各コンピューティングノードで次の操作を実行するために実行されます。  
  
-   DMS は、並列クエリの処理の一環として、他のコンピューターノードとコントロールノードとの間でデータを転送します。  
  
-   各コンピューティングノード上で実行される DMS は、並列でデータの読み込みを受け取ります。 データは、読み込みサーバーから計算ノードに直接読み込まれます。  
  
-   DMS は、各コンピューティングノードからバックアップサーバーにデータを直接転送します。  
  
-   PolyBase を使用すると、DMS は外部の Hadoop クラスターまたは Azure Storage Blob との間でデータを転送します。  
  
### <a name="compute-node-databases"></a>計算ノードデータベース 
各コンピューティングノードは、SQL Server のインスタンスを実行してクエリを処理し、ユーザーデータを管理します。  
  
## <a name="appliance-fabric"></a>アプライアンスファブリック  
アプライアンスファブリックは、アプライアンスのオペレーティングシステム、サービス、およびネットワークインフラストラクチャを提供します。  
  
### <a name="domain-controller"></a>ドメイン コントローラー  
Active Directory (AD) ドメインサービス (DS)  
Analytics Platform System は、Analytics Platform システムノード間で認証を実行し、SQL Server PDW Windows 認証ログインの認証を管理します。  
  
DNS サービス  
Windows ドメインネームサービス (DNS) は、ドメイン名を Analytics Platform System アプライアンスの IP アドレスに解決します。  
  
### <a name="windows-deployment-service"></a>Windows 展開サービス  
Windows 展開サービス (WDS) は、Windows Server オペレーティングシステムをアプライアンスに展開します。 アプライアンス全体のすべてのホストとバーチャルマシンに展開されます。  
  
DHCP サービスによって IP アドレスが作成されるため、アプライアンスドメイン内のホストは、事前に構成された IP アドレスがなくてもアプライアンスネットワークに参加できるようになります。  
  
### <a name="virtual-machine-manager"></a>Virtual Machine Manager   
Analytics Platform System は、仮想化を使用して高可用性を実現します。 Virtual Machine Manager は、System Center をホストして、物理ホストにオペレーティングシステムを展開します。  
  
すべてのホストとバーチャルマシンで Windows 更新プログラムを適用または削除するには、Windows Server Update Services (WSUS) をご活用ください。  
  
### <a name="windows-server"></a>Windows Server  
アプライアンス内のすべてのホストとバーチャルマシンは、Windows Server オペレーティングシステムを実行します。  
  
### <a name="failover-clustering"></a>フェールオーバー クラスタリング  
Windows フェールオーバークラスタリングには、ホストで障害が発生した場合にパッシブホスト上のプロセスを再開する機能が用意されています。  
  
### <a name="storage-spaces"></a>記憶域スペース  
Windows 記憶域スペースは、少数のコンピューティングノードグループの記憶域プールとしてユーザーデータを管理します。 コンピューティングノードで障害が発生した場合でも、グループ内の別のコンピューティングノードを介してデータにアクセスできます。  
  
### <a name="hyper-v"></a>Hyper-V  
Microsoft Hyper-V Server は、シンプルで信頼性の高い仮想化ソリューションを提供します。 Analytics Platform System は、仮想化を使用して CPU リソースのバランスを調整し、PDW ノードとアプライアンスファブリックコンポーネントの高可用性を実現します。  
  
## <a name="sec2"></a>非リレーショナルデータ
PolyBase テクノロジは、SQL Server PDW データを外部の Hadoop データと統合します。 Hadoop データは、次のいずれかの Hadoop データソースに格納できます。  
  
-   Hortonworks Hadoop ディストリビューション  
  
-   Hadoop の Cloudera 分布  
  
-   Azure Storage Blob に格納されている HDInsight データ  
  
## <a name="query-tools"></a>クエリ ツール   
  
クエリは、クエリの\-MPP の性質に合わせて変更された Transact SQL を使用して作成されます。 すべてのクエリが制御ノードに送信されます。このノードは、計算ノード全体でクエリを実行するための並列クエリプランを生成します。  
  
### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)  
SQL Server Data Tools は、Visual Studio 内で実行され、クエリを SQL Server PDW に送信するために推奨される GUI ツールです。 オブジェクトエクスプローラー内を移動できるようにすることで、SQL Server Management Studio に似ています。  
  
まだ Visual Studio をお持ちでない場合は、無料で必要なツールをダウンロードできます。 
<!-- MISSING LINKS
For more information, see [Install SQL Server database tooling  for Visual Studio &#40;SQL Server PDW&#41;](../sqlpdw/install-sql-server-database-tooling-for-visual-studio-sql-server-pdw.md).  
-->
  
### <a name="sqlcmd-command-line-query-tool"></a>sqlcmd コマンドラインクエリツール  
sqlcmd は、Transact\-SQL ステートメントおよびシステムコマンドを実行するための SQL Server コマンドラインツールです。 SQL Server PDW と連携し、SQL Server PDW クエリを実行するために推奨されるコマンドラインツールです。 Sqlcmd を使用すると、\-コマンドライン、バッチファイル、または Windows PowerShell から、Transact SQL ステートメントを対話的に実行できます。  
  
<!-- MISSING LINKS

If you don't have SQL Server, you can download this as a standalone package. For more information, see [Install sqlcmd Command-Line Client &#40;SQL Server PDW&#41;](../sqlpdw/install-sqlcmd-command-line-client-sql-server-pdw.md) 
--> 
  
### <a name="integration-services"></a>Integration Services  
Integration Services を使用して SQL Server PDW を照会できます。 

<!-- MISSING LINKS
For more information, see [Connect With SQL Server Integration Services for Querying &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-integration-services-for-querying-sql-server-pdw.md). 

--> 
  
### <a name="linked-server"></a>リンク サーバー  
SQL Server のリンクサーバー接続を使用すると、SQL Server を使用して\-SQL Server PDW に Transact SQL ステートメントを送信できます。 
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Linked Server &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-linked-server-sql-server-pdw.md). 
--> 
  
## <a name="business-intelligence-tools"></a>ビジネス インテリジェンス ツール
  
### <a name="analysis-services"></a>Analysis Services  
SQL Server PDW は Analysis Services データベースおよび Excel PowerPivot モデルの有効なデータソースです。 OLE DB プロバイダーを使用すると、多次元オンライン分析処理 (MOLAP) またはリレーショナルオンライン分析処理 (ROLAP) ストレージのいずれかを使用するように Analysis Services キューブを構成できます。  
  
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Analysis Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-analysis-services-sql-server-pdw.md).  

-->
  
### <a name="report-builder"></a>レポート ビルダー  
SQL Server PDW は、SQL Server レポートビルダーを使用して Reporting Services 用に開発したレポートの SQL Server データソースとして使用できます。 レポートモデルの SQL Server ソースとして SQL Server PDW を使用することもできます。 レポートマネージャーまたはレポートサーバー API を使用して、SQL Server PDW データベースからモデルを生成できます。  
  
<!-- MISSING LINKS

For more information, see [Connect With SQL Server Report Builder &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-report-builder-sql-server-pdw.md) and [Connect With SQL Server Reporting Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-reporting-services-sql-server-pdw.md). 

--> 
  
### <a name="power-pivot-for-excel"></a>Power Pivot for Excel  
Excel のデータ分析機能を大幅に拡張する無料のダウンロードである PowerPivot for Excel を使用して SQL Server PDW に接続できます。  
  
<!-- MISSING LINKS

For more information, see [Connect With PowerPivot for Excel &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-powerpivot-for-excel-sql-server-pdw.md).  

-->
  
## <a name="loading-tools"></a>読み込み (ツールを) 
  
### <a name="integration-services"></a>Integration Services  
SQL ServerIntegration Services を使用して SQL Server PDW にデータを読み込むことができる PDW 固有の変換先アダプターをインストールします。  

<!-- MISSING LINKS
For more information, see [Install Integration Services Destination Adapters &#40;SQL Server PDW&#41;](../sqlpdw/install-integration-services-destination-adapters-sql-server-pdw.md). 
--> 
  
### <a name="dwloader-command-line-loader"></a>dwloader コマンドラインローダー  
dwloader は、読み込みサーバーから SQL Server PDW の計算ノードにデータを並行して読み込むコマンドライン読み込みツールです。 

<!-- MISSING LINKS
For more information, see [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](../sqlpdw/install-dwloader-command-line-loader-sql-server-pdw.md)  
-->
  
### <a name="polybase-for-hadoop-integration"></a>Hadoop 統合用 PolyBase  
PolyBase テクノロジを使用すると、Hadoop クラスターの非リレーショナルデータを SQL Server PDW のリレーショナルテーブルに読み込むことができます。 Hadoop データは、外部の Hadoop クラスターまたは Azure Storage Blob に配置できます。  

<!-- MISSING LINKS
For more information, see [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md).
-->  
  
## <a name="database-backup-and-restore"></a>データベースのバックアップと復元  
SQL Server PDW では、Transact-sql データベースのバックアップおよび復元コマンドを使用して、バックアップサーバーとの間でユーザーデータベースのバックアップと復元を同時に行うことができます。 SQL Server PDW は、Windows ファイル共有のディレクトリにバックアップを書き込み、同様に Windows ファイル共有からデータを復元します。  
  
詳細については、「[バックアップの計画](backup-and-loading-hardware.md)」および「ハードウェアの読み込みと[バックアップと復元の概要](backup-and-restore-overview.md)」を参照してください。  
  
## <a name="remote-table-copy"></a>リモートテーブルのコピー  
リモートテーブルのコピー機能を使用すると、SQL Server PDW データベースからリモート (アプライアンス以外) の SMP SQL Server データベースにテーブルをコピーできます。 これにより、SQL Server PDW のハブとスポークのシナリオが有効になります。  
  
<!-- MISSING LINKS

For more information, see [Remote Table Copy &#40;SQL Server PDW&#41;](../sqlpdw/remote-table-copy-sql-server-pdw.md).  

-->
  
## <a name="monitoring"></a>監視  
Analytics Platform System には、アプライアンスの利用状況を監視する方法がいくつかあります。  
  
### <a name="admin-console"></a>管理コンソール  
管理コンソールでは、アプライアンスの正常性に関する現在の状態を表示できます。 これは、コントロールノードで web アプリケーションとして実行され、https 経由でアクセスできます。  
  
詳細については、「[管理コンソールを使用したアプライアンスの監視 &#40;Analytics Platform System](monitor-the-appliance-by-using-the-admin-console.md) 」を参照してください&#41;  

### <a name="system-views"></a>システム ビュー  
管理コンソールは、システムビューのクエリに基づいています。 システムビューに個別にクエリを実行すると、必要な特定の情報を取得できます。  

詳細については、「[システムビューを使用したアプライアンスの監視 &#40;Analytics Platform System](monitor-the-appliance-by-using-system-views.md) 」を参照してください&#41; 
  
### <a name="system-center-operations-manager"></a>System Center Operations Manager  
SQL Server PDW 用の System Center Operations Manager (SCOM) 管理パックがあります。 

SCOM 用にアプライアンスを構成する方法については、「 [System Center Operations Manager &#40;Analytics Platform System を使用したアプライアンスの監視](monitor-the-appliance-by-using-system-center-operations-manager.md)」を参照してください&#41;  
  
