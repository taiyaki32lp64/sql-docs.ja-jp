---
title: SQL Server 2017 の各エディションとサポートされる機能 - Linux
ms.date: 01/14/2020
ms.prod: sql
ms.technology: linux
ms.topic: conceptual
helpviewer_keywords:
- Enterprise Edition [SQL Server]
- Developer Edition [SQL Server]
- default components
- installing SQL Server, components
- Setup [SQL Server], components
- SQL Server, editions
- SQL Server, components
- editions [SQL Server]
- versions [SQL Server]
- Setup [SQL Server], editions
- SQL Server Installation Wizard
- components [SQL Server]
- Standard Edition [SQL Server]
- installing SQL Server, editions
- editions [SQL Server], about edition options
- Setup [SQL Server]
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.openlocfilehash: a652bc56a826469017ba4de643c9d3e1822d4c22
ms.sourcegitcommit: 0a9058c7da0da9587089a37debcec4fbd5e2e53a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2020
ms.locfileid: "75952528"
---
# <a name="editions-and-supported-features-of-sql-server-2017-on-linux"></a>Linux 上の SQL Server 2017 のエディションとサポートされる機能

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、SQL Server 2017 on Linux のさまざまなエディションでサポートされている機能の詳細を説明します。 SQL Server on Windows の各エディションとサポートされている機能については、「[SQL Server 2017 - Windows](../sql-server/editions-and-components-of-sql-server-2017.md)」を参照してください。  
  
インストールの前提条件は、アプリケーションのニーズによって異なります。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] にはさまざまなエディションがあり、組織や個人の独自のパフォーマンス、ランタイム、および価格に関する要件に対応できます。 インストールする [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] コンポーネントは、ユーザーの特定の要件によっても異なります。 この後のセクションでは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の最適なエディションおよびコンポーネントを選択する方法について説明します。  

最新のリリース ノートと新機能については、以下の情報を参照してください。
- [SQL Server 2017 on Linux のリリース ノート](sql-server-linux-release-notes.md)
- [SQL Server 2017 on Linux の新機能](sql-server-linux-whats-new.md)

Linux 上で使用できない SQL Server の機能の一覧については、[「サポートされていない機能とサービス](#Unsupported)」を参照してください。

### <a name="try-sql-server"></a>SQL Server を試してください    
    
[SQL Server 2017 をダウンロードする](https://www.microsoft.com/sql-server/sql-server-2017)

## <a name="includessnoversionincludesssnoversion-mdmd-editions"></a>[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] のエディション  
 次の表で、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のエディションについて説明します。 
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エディション|定義|  
|---------------------------------------|----------------|  
|Enterprise|プレミアム製品である [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Enterprise Edition では、非常に優れたパフォーマンスを備えた包括的なハイエンド データセンター機能を提供することで、ミッション クリティカルなワークロードのための高水準のサービス レベルが実現されます。|  
|Standard|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Standard Edition では、企業部門や小規模組織がアプリケーションを実行するための基本的なデータ管理を提供し、オンプレミスとクラウド用の一般的な開発ツールをサポートすることで、最小限の IT リソースでデータベースを効果的に管理することを可能にします。|  
|Web|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Web Edition は、大小さまざまな規模の Web 資産に対応できるスケーラビリティ、経済性、および管理性を備えた、Web ホスティング企業および Web VAP 向けの総保有コストの低いオプションです。|  
|Developer|開発者は、[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Developer Edition を使用して、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上で動作するあらゆる種類のアプリケーションを開発できます。 このエディションには Enterprise Edition の機能がすべて含まれていますが、実稼動サーバーとして使用するのではなく、開発およびテスト システムとしての利用に対してライセンスが供与されます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer は、アプリケーションを作成し、テストするユーザーに適しています。|  
|Express Edition|Express Edition はエントリレベルの無料のデータベースで、学習や、デスクトップおよび小規模サーバー データ ドリブン アプリケーションの構築などに適しています。 このエディションは、独立系ソフトウェア ベンダー、開発者、クライアント アプリケーションを趣味で開発する開発者などに最適です。 さらに高度なデータベース機能が必要な場合には、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express を [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の他の上位バージョンにシームレスにアップグレードできます。|  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-clientserver-applications"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] とクライアント/サーバー アプリケーションの使用  

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のクライアント コンポーネントだけを、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のインスタンスに直接接続するクライアント/サーバー アプリケーションを実行するコンピューターにインストールできます。 クライアント コンポーネントをインストールすることは、データベース サーバー上にある [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスを管理する場合、または [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] アプリケーションを開発しようとしている場合にも適切なオプションです。  
  
## <a name="includessnoversionincludesssnoversion-mdmd-components"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のコンポーネント  

SQL Server 2017 on Linux では、SQL Server データベース エンジンがサポートされています。 次の表で、データベース エンジンの機能について説明します。   
  
|サーバー コンポーネント|[説明]|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] には、[!INCLUDE[ssDE](../includes/ssde-md.md)]、データを格納、処理、およびセキュリティで保護するための主要サービス、レプリケーション、フルテキスト検索、リレーショナル データと XML データを管理するためのツール、およびデータベース内分析の統合が含まれます。|  

**Developer Edition、Enterprise Core Edition、および Evaluation Edition**  
Developer Edition、Enterprise Core Edition、および Evaluation Edition でサポートされている機能については、次の表に記載されている SQL Server Enterprise Edition の機能をご覧ください。

Developer Edition では引き続き、[SQL Server 分散再生](../tools/distributed-replay/sql-server-distributed-replay.md)のクライアントが 1 つだけサポートされます。 
  
##  <a name="Cross-BoxScaleLimits"></a> スケールの制限  
  
|機能|Enterprise|Standard|Web|Express| 
|-------------|----------------|--------------|---------|------------------------|
|1 つのインスタンスで使用される最大計算容量 - [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|オペレーティング システムの最大容量|4 ソケットまたは 24 コアのいずれか小さいほうに制限|4 ソケットまたは 16 コアのいずれか小さいほうに制限|1 ソケットまたは 4 コアのいずれか小さいほうに制限| 
|1 つのインスタンスで使用される最大計算容量 - [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] または [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|オペレーティング システムの最大容量|4 ソケットまたは 24 コアのいずれか小さいほうに制限|4 ソケットまたは 16 コアのいずれか小さいほうに制限|1 ソケットまたは 4 コアのいずれか小さいほうに制限|
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] のインスタンスごとのバッファー プールの最大メモリ|オペレーティング システムの最大容量|128 GB|64 GB|1410 MB|
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] のインスタンスごとの列ストア セグメント キャッシュの最大メモリ|メモリ制限なし| 32 GB| 16 GB| 352 MB|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] のデータベースごとの最大メモリ最適化データ サイズ|メモリ制限なし| 32 GB| 16 GB| 352 MB|
|リレーショナル データベースの最大サイズ|524 PB|524 PB|524 PB|10 GB|  
  
<sup>1</sup> Enterprise Edition with Server + Client Access License (CAL) に基づくライセンス (新しい使用許諾契約では利用できません) は、SQL Server インスタンスあたり最大 20 コアに制限されています。 コアベースのサーバー ライセンス モデルでは、制限はありません。 詳細については、「[SQL Server のエディション別の計算容量制限](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)」を参照してください。  
 
##  <a name="RDBMSHA"></a> RDBMS の高可用性  
  
|機能|Enterprise|Standard|Web|Express|  
|-------------|----------------|--------------|---------|------------------------|  
|ログ配布|はい|はい|はい|いいえ|  
|バックアップ圧縮|はい|はい|いいえ|いいえ| 
|データベース スナップショット|はい|いいえ|いいえ|いいえ|
|Always On フェールオーバー クラスター インスタンス<sup>1</sup>|はい|はい|いいえ|いいえ| 
|Always On 可用性グループ<sup>2</sup>|はい|いいえ|いいえ|いいえ|
|基本的な可用性グループ <sup>3</sup>|いいえ|はい|いいえ|いいえ|
|最小レプリカ コミット可用性グループ|はい|はい|いいえ|いいえ|
|クラスターを使用しない可用性グループ|はい|はい|いいえ|いいえ|
|オンライン ページおよびファイルの復元|はい|いいえ|いいえ|いいえ|
|オンラインのインデックス構築|はい|いいえ|いいえ|いいえ|
|再開可能なオンライン インデックス再構築|はい|いいえ|いいえ|いいえ|
|オンラインのスキーマ変更|はい|いいえ|いいえ|いいえ|
|高速復旧|はい|いいえ|いいえ|いいえ|
|ミラー化バックアップ|はい|いいえ|いいえ|いいえ|
|ホット アド メモリと CPU|はい|いいえ|いいえ|いいえ|
|暗号化されたバックアップ|はい|はい|いいえ|いいえ|
|Azure へのハイブリッド バックアップ (URL へのバックアップ)|はい|はい|いいえ|いいえ|
  
<sup>1</sup> Enterprise Edition では、ノードの数はオペレーティング システムの最大容量です。 Standard Edition では、2 つのノードがサポートされます。 

<sup>2</sup> Enterprise Edition では、2 個の同期セカンダリ レプリカを含む最大 8 個のセカンダリ レプリカがサポートされます。 

<sup>3</sup> Standard Edition では、基本的な可用性グループがサポートされます。 基本的な可用性グループは、1 つのデータベースで、2 つのレプリカをサポートします。 基本的な可用性グループの詳細については、「[基本的な可用性グループ](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md)」を参照してください。    

##  <a name="RDBMSSP"></a> RDBMS のスケーラビリティとパフォーマンス  
  
|機能|Enterprise|Standard|Web|Express|  
|-------------|----------------|--------------|---------|------------------------| 
|列ストア <sup>1</sup>|はい|はい|はい|はい|  
|クラスター化列ストア インデックス内のラージ オブジェクト バイナリ|はい|はい|はい|はい|  
|オンライン非クラスター化列ストア インデックスの再構築|はい|いいえ|いいえ|いいえ|
|インメモリ OLTP <sup>1</sup>|はい|はい|はい|はい|
|恒久的なメイン メモリ|はい|はい|はい|はい|
|テーブルとインデックスのパーティション分割|はい|はい|はい|はい|  
|データ圧縮|はい|はい|はい|はい|
|[リソース ガバナー]|はい|いいえ|いいえ|いいえ|  
|パーティション テーブルの並列処理|はい|いいえ|いいえ|いいえ|
|NUMA 対応のラージ ページ メモリとバッファー配列の割り当て|はい|いいえ|いいえ|いいえ|
|IO リソース管理|はい|いいえ|いいえ|いいえ|  
|遅延持続性|はい|はい|はい|はい|
|自動調整|はい|いいえ|いいえ|いいえ|
|バッチ モードの適応型結合|はい|いいえ|いいえ|いいえ|
|バッチ モード メモリ許可フィードバック|はい|いいえ|いいえ|いいえ|
|複数ステートメントのテーブル値関数のインターリーブ実行|はい|はい|はい|はい|
|一括挿入の機能強化|はい|はい|はい|はい|


<sup>1</sup> インメモリ OLTP データ サイズおよび列ストア セグメント キャッシュは、「スケールの制限」セクションでエディションごとに指定されているメモリ量に制限されます。 並列処理には最大限度があります。 インデックス構築のための並列処理の度合い (DOP) は、Standard Edition では 2 DOP に、Web Edition と Express Edition では 1 DOP に制限されます。 これは、ディスク ベース テーブルとメモリ最適化テーブルで作成された列ストア インデックスに当てはまります。

##  <a name="RDBMSS"></a> RDBMS のセキュリティ  
  
|機能|Enterprise|Standard|Web|Express|
|-------------|----------------|--------------|---------|------------------------------------| 
|行レベルのセキュリティ|はい|はい|はい|はい|  
|Always Encrypted|はい|はい|はい|はい| 
|動的データ マスク|はい|はい|はい|はい|   
|基本的な監査|はい|はい|はい|はい| 
|詳細な監査|はい|はい|はい|はい| 
|透過的なデータベースの暗号化|はい|いいえ|いいえ|いいえ|   
|ユーザー定義ロール|はい|はい|はい|はい| 
|包含データベース|はい|はい|はい|はい| 
|バックアップの暗号化|はい|はい|いいえ|いいえ|  

##  <a name="RDBMSM"></a> RDBMS の管理の容易性  
  
|機能|Enterprise|Standard|Web|Express|   
|-------------|----------------|--------------|---------|------------------------|  
|専用管理者接続|はい|はい|はい|はい (トレース フラグを使用)|   
|PowerShell スクリプティングのサポート|はい|はい|はい|はい| 
|データ層アプリケーション コンポーネントの操作のサポート - 抽出、配置、アップグレード、削除|はい|はい|はい|はい| 
|ポリシー オートメーション (変更時とスケジュールに基づいて確認)|はい|はい|はい|いいえ|  
|パフォーマンス データ コレクター|はい|はい|はい|いいえ|
|標準的なパフォーマンス レポート|はい|はい|はい|いいえ|
|プラン ガイドおよびプラン ガイドの固定計画|はい|はい|はい|いいえ| 
|NOEXPAND ヒントを使用したインデックス付きビューの直接クエリ|はい|はい|はい|はい| 
|インデックス付きビューの自動メンテナンス|はい|はい|はい|いいえ|
|分散パーティション ビュー|はい|いいえ|いいえ|いいえ| 
|並列インデックス操作|はい|いいえ|いいえ|いいえ|  
|クエリ オプティマイザーによる自動的なインデックス付きのビュー使用|はい|いいえ|いいえ|いいえ| 
|並列整合性チェック|はい|いいえ|いいえ|いいえ| 
|SQL Server ユーティリティ コントロール ポイント|はい|いいえ|いいえ|いいえ|    

##  <a name="Programmability"></a> Programmability  
  
|機能|Enterprise|Standard|Web|Express 
|-------------|----------------|--------------|---------|------------------------|  
|JSON|はい|はい|はい|はい|   
|クエリ ストア|はい|はい|はい|はい|   
|テンポラル|はい|はい|はい|はい|   
|ネイティブ XML サポート|はい|はい|はい|はい| 
|XML インデックスの作成|はい|はい|はい|はい| 
|MERGE と UPSERT の機能|はい|はい|はい|はい|   
|日付および時刻データ型|はい|はい|はい|はい|  
|国際化サポート|はい|はい|はい|はい| 
|フルテキストおよびセマンティック検索|はい|はい|はい|はい|
|クエリ内の言語指定|はい|はい|はい|はい|
|Service Broker (メッセージング)|はい|はい|不可 (クライアントのみ)|不可 (クライアントのみ)|
|Transact-SQL エンドポイント|はい|はい|はい|いいえ|
|グラフ|はい|はい|はい|はい|  


<sup>1</sup> 複数のコンピューティング ノードでのスケール アウトにはヘッド ノードが必要です。

## <a name="IS"></a> Integration Services

[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] の各エディションがサポートする Integration Services (SSIS) の機能については、「[SQL Server の各エディションがサポートする Integration Services の機能](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md)」をご覧ください。

##  <a name="SLS"></a> 空間およびロケーション サービス  
  
|機能名|Enterprise|Standard|Web|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|空間インデックス|はい|はい|はい|はい|   
|平面データ型と測地データ型|はい|はい|はい|はい| 
|高度な空間的なライブラリ|はい|はい|はい|はい|   
|業界標準の空間データ形式のインポート/エクスポート|はい|はい|はい|はい|   
## <a name="Unsupported"></a> サポートされていない機能とサービス

次の機能とサービスは、SQL Server 2017 on Linux では利用できません。 これらの機能のサポートは、今後ますます使用可能になります。

| 領域 | サポートされていない機能またはサービス |
|-----|-----|
| **データベース エンジン** | マージ レプリケーション |
| &nbsp; | Stretch DB |
| &nbsp; | PolyBase |
| &nbsp; | サード パーティの接続を使用した分散クエリ |
| &nbsp; | [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 以外のデータ ソースへのリンク サーバー  |
| &nbsp; | システム拡張ストアド プロシージャ (XP_CMDSHELL など) |
| &nbsp; | Filetable、FILESTREAM |
| &nbsp; | EXTERNAL_ACCESS 権限または UNSAFE 権限が設定された CLR アセンブリ |
| &nbsp; | バッファー プール拡張 |
| **SQL Server エージェント** |  サブシステム: CmdExec、PowerShell、キュー リーダー、SSIS、SSAS、SSRS |
| &nbsp; | 警告 |
| &nbsp; | ログ リーダー エージェント (Log Reader Agent) |
| &nbsp; | 管理対象のバックアップ |
| **高可用性** | データベース ミラーリング  |
| **セキュリティ** | 拡張キー管理 |
| &nbsp; | リンク サーバーに対する AD 認証 | 
| &nbsp; | 可用性グループに対する AD 認証 (AG) | 
| **サービス** | SQL Server Browser |
| &nbsp; | SQL Server R サービス |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | マスター データ サービス |
  
## <a name="next-steps"></a>次のステップ
 [SQL Server 2019 の各エディションとサポートされる機能 - Windows](../sql-server/editions-and-components-of-sql-server-version-15.md)  
 [SQL Server 2017 の各エディションとサポートされる機能 - Windows](../sql-server/editions-and-components-of-sql-server-2017.md)  
 [SQL Server 2016 の各エディションとサポートされる機能 - Windows](../sql-server/editions-and-components-of-sql-server-2016.md)  
 [SQL Server 2014 の各エディションとサポートされる機能 - Windows](https://msdn.microsoft.com/library/cc645993(v=sql.120).aspx)  
 [SQL Server をインストールする](../database-engine/install-windows/installation-for-sql-server-2016.md)  
 [SQL Server の製品仕様](https://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)
