---
title: SQL Server 2014 | の各エディションがサポートする機能Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 5da61ff5-12b9-48e6-b3c8-0dacca1751c4
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: caae4212e2182ae6afde29b0fed1aaee4f05645a
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176128"
---
# <a name="features-supported-by-the-editions-of-sql-server-2014"></a>SQL Server 2014 の各エディションがサポートする機能


  このトピックでは、 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]のさまざまなエディションでサポートされる機能の詳細について説明します。 

 > **注:** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は、180日間の評価版で利用できます。 詳細については、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][評価版ソフトウェア Web サイト](https://go.microsoft.com/fwlink/?LinkId=190955)を参照してください。  
> 
> **注:** 評価版と Developer edition でサポートされている機能については、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise 機能セットを参照してください。  
  
 各 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] テクノロジの表に移動するには、それぞれのリンクをクリックしてください。  
  
 [クロスボックスのスケールの制限](#CrossBoxScale)  
  
 [高可用性](#High_availability)  
  
 [スケーラビリティとパフォーマンス](#Scalability)  
  
 [セキュリティ](#Enterprise_security)  
  
 [レプリケーション](#Replication)  
  
 [管理ツール](#Mgmt_Tools)  
  
 [RDBMS の管理の容易性](#RDBMS_mgmt)  
  
 [開発ツール](#Dev_tools)  
  
 [ティ](#Programmability)  
  
 [Integration Services](#SSIS)  
  
 [Integration Services-高度なアダプター](#SSIS_AA)  
  
 [Integration Services-高度な変換](#SSIS_AT)  
  
 [マスター データ サービス](#MDS)  
  
 [データ ウェアハウス](#Data_warehouse)  
  
 [Analysis Services](#SSAS)  
  
 [BI セマンティックモデル (多次元)](#BISemModel_multi)  
  
 [BI セマンティック モデル (テーブル)](#BISemModel_tabular)  
  
 [PowerPivot for SharePoint](#PowerPivot)  
  
 [データ マイニング](#DataMining)  
  
 [Reporting Services](#Reporting)  
  
 [Business Intelligence クライアント](#BIClients)  
  
 [空間サービスとロケーションサービス](#Spatial)  
  
 [その他のデータベースサービス](#Add_DBServices)  
  
 [その他のコンポーネント](#Other_Components)  
  
##  <a name="CrossBoxScale"></a> クロスボックスのスケールの制限  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|1つのインスタンスで使用される最大計算容量 ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースエンジン)<sup>1</sup>|オペレーティング システムの最大容量|4 ソケットまたは 16 コアのいずれか小さいほうに制限|4 ソケットまたは 16 コアのいずれか小さいほうに制限|4 ソケットまたは 16 コアのいずれか小さいほうに制限|1 ソケットまたは 4 コアのいずれか小さいほうに制限|1 ソケットまたは 4 コアのいずれか小さいほうに制限|1 ソケットまたは 4 コアのいずれか小さいほうに制限|  
|1つのインスタンスで使用される最大計算容量 (Analysis Services、Reporting Services) <sup>1</sup>|オペレーティング システムの最大容量|オペレーティング システムの最大容量|4 ソケットまたは 16 コアのいずれか小さいほうに制限|4 ソケットまたは 16 コアのいずれか小さいほうに制限|1 ソケットまたは 4 コアのいずれか小さいほうに制限|1 ソケットまたは 4 コアのいずれか小さいほうに制限|1 ソケットまたは 4 コアのいずれか小さいほうに制限|  
|利用可能な最大メモリ サイズ ( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベース エンジンのインスタンスごと)|オペレーティング システムの最大容量|128 GB|128 GB|64 GB|1 GB|1 GB|1 GB|  
|利用可能な最大メモリ サイズ ( [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]のインスタンスごと)|オペレーティング システムの最大容量|オペレーティング システムの最大容量|64 GB|なし|なし|なし|なし|  
|利用可能な最大メモリ サイズ ( [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]のインスタンスごと)|オペレーティング システムの最大容量|オペレーティング システムの最大容量|64 GB|64 GB|4 GB|なし|なし|  
|リレーショナル データベースの最大サイズ|524 PB|524 PB|524 PB|524 PB|10 GB|10 GB|10 GB|  
  
 <sup>1</sup> Enterprise Edition with Server および Client Access LICENSE (CAL) に基づくライセンス (新しい契約では利用できません) は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスあたり最大20コアに制限されています。 コアベースのサーバー ライセンス モデルでは、制限はありません。 詳細については、「 [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)」を参照してください。  
  
##  <a name="High_availability"></a> 高可用性  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Server Core サポート<sup>1</sup>|はい|はい|はい|はい|はい|はい|はい|  
|ログ配布|はい|はい|はい|はい||||  
|データベース ミラーリング|はい|可 (安全性レベルが FULL の場合のみ)|可 (安全性レベルが FULL の場合のみ)|ミラーリング監視のみ|ミラーリング監視のみ|ミラーリング監視のみ|ミラーリング監視のみ|  
|バックアップ圧縮|はい|はい|はい|||||  
|データベース スナップショット|はい|||||||  
|AlwaysOn フェールオーバー クラスター インスタンス|可 (ノード サポート: オペレーティング システムの最大容量)|可 (ノード サポート: 2)|可 (ノード サポート: 2)|||||  
|AlwaysOn 可用性グループ|可 (2 個の同期セカンダリ レプリカを含む最大 8 個のセカンダリ レプリカ)|||||||  
|接続ディレクター|はい|||||||  
|オンライン ページおよびファイルの復元|はい|||||||  
|オンラインのインデックス構築|はい|||||||  
|オンラインのスキーマ変更|はい|||||||  
|高速復旧|はい|||||||  
|ミラー化バックアップ|はい|||||||  
|ホットアドメモリと CPU<sup>2</sup>|はい|||||||  
|データベース復旧アドバイザー|はい|はい|はい|はい|はい|はい|はい|  
|暗号化されたバックアップ|はい|はい|はい|||||  
|スマート バックアップ|はい|はい|はい|[いいえ]||||  
  
 <sup>1</sup>Server Core への [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] のインストールの詳細については、「 [Server core で SQL Server 2014 をインストール](../database-engine/install-windows/install-sql-server-on-server-core.md)する」を参照してください。  
  
 <sup>2</sup>この機能は、64ビット [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]でのみ使用できます。  
  
##  <a name="Scalability"></a>スケーラビリティとパフォーマンス  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|複数インスタンスのサポート|50|50|50|50|50|50|50|  
|テーブルとインデックスのパーティション分割|はい|||||||  
|データ圧縮|はい|||||||  
|[リソース ガバナー]|はい|||||||  
|パーティション テーブルの並列処理|はい|||||||  
|複数の Filestream コンテナー|はい|||||||  
|NUMA 対応のラージ ページ メモリとバッファー配列の割り当て|はい|||||||  
|バッファープール拡張<sup>1</sup>|はい|はい|はい|||||  
|IO リソース管理|はい|||||||  
|インメモリ OLTP <sup>1</sup>|はい|||||||  
|遅延持続性|はい|はい|はい|はい|はい|はい|はい|  
  
 <sup>1</sup>この機能は、64ビット [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]でのみ使用できます。  
  
##  <a name="Enterprise_security"></a> セキュリティ  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|基本的な監査|はい|はい|はい|はい|はい|はい|はい|  
|詳細な監査|はい|||||||  
|透過的なデータベースの暗号化|はい|||||||  
|拡張キー管理|はい|||||||  
|ユーザー定義ロール|はい|はい|はい|はい|はい|はい|はい|  
|包含データベース|はい|はい|はい|はい|はい|はい|はい|  
|バックアップの暗号化|はい|はい|はい|||||  
  
##  <a name="Replication"></a> レプリケーション  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 変更の追跡|はい|はい|はい|はい|はい|はい|はい|  
|マージ レプリケーション|はい|はい|はい|可 (サブスクライバーのみ)|可 (サブスクライバーのみ)|可 (サブスクライバーのみ)|可 (サブスクライバーのみ)|  
|トランザクション レプリケーション|はい|はい|はい|可 (サブスクライバーのみ)|可 (サブスクライバーのみ)|可 (サブスクライバーのみ)|可 (サブスクライバーのみ)|  
|スナップショット レプリケーション|はい|はい|はい|可 (サブスクライバーのみ)|可 (サブスクライバーのみ)|可 (サブスクライバーのみ)|可 (サブスクライバーのみ)|  
|異種サブスクライバー|はい|はい|はい|||||  
|Oracle パブリッシュ|はい|||||||  
|ピア ツー ピア トランザクション レプリケーション|はい|||||||  
  
##  <a name="Mgmt_Tools"></a> Management Tools  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|SQL 管理オブジェクト (SMO)|はい|はい|はい|はい|はい|はい|はい|  
|SQL 構成マネージャー|はい|はい|はい|はい|はい|はい|はい|  
|SQL CMD (コマンド プロンプト ツール)|はい|はい|はい|はい|はい|はい|はい|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Studio|はい|はい|はい|はい|はい|はい||  
|分散再生 - 管理ツール|はい|はい|はい|はい|はい|はい||  
|分散再生 - クライアント|はい|[いいえ]|はい|はい||||  
|分散再生 - コントローラー|可 (Enterprise では最大 16 クライアントのサポート、Developer では 1 クライアントのみサポート)|[いいえ]|可 (1 クライアントのサポートのみ)|可 (1 クライアントのサポートのみ)||||  
|SQL Profiler|はい|はい|はい|×<sup>2</sup>|×<sup>2</sup>|×<sup>2</sup>|×<sup>2</sup>|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェント|はい|はい|はい|はい||||  
|Microsoft System Center Operations Manager 管理パック|はい|はい|はい|はい||||  
|データベース チューニング アドバイザー (DTA)|はい|はい|可 <sup>3</sup>|可 <sup>3</sup>||||  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースを Azure VM ウィザードにデプロイする|はい|はい|はい|はい|はい|はい|はい|  
|Azure でのデータファイルの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|はい|はい|はい|はい|はい|はい|はい|  
  
 <sup>2</sup> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Web、[!INCLUDE[ssExpress](../includes/ssexpress-md.md)]、[!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Tools、および [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] With Advanced Services は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard および [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise エディションを使用してプロファイルできます。  
  
 <sup>3</sup>チューニングは Standard edition 機能でのみ有効です。  
  
##  <a name="RDBMS_mgmt"></a> RDBMS Manageability  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|ユーザー インスタンス|||||はい|はい|はい|  
|LocalDB|||||はい|はい||  
|専用管理者接続|はい|はい|はい|はい|可 (トレース フラグでサポートされている)|可 (トレース フラグでサポートされている)|可 (トレース フラグでサポートされている)|  
|PowerShell スクリプティングのサポート|はい|はい|はい|はい|はい|はい|はい|  
|SysPrep サポート<sup>1</sup>|はい|はい|はい|はい|はい|はい|はい|  
|データ層アプリケーションコンポーネントの操作 (抽出、配置、アップグレード、削除) のサポート|はい|はい|はい|はい|はい|はい|はい|  
|ポリシー オートメーション (変更時とスケジュールに基づいて確認)|はい|はい|はい|はい||||  
|パフォーマンス データ コレクター|はい|はい|はい|はい||||  
|複数インスタンス管理でマネージド インスタンスとして登録できる|はい|はい|はい|はい||||  
|標準的なパフォーマンス レポート|はい|はい|はい|はい||||  
|プラン ガイドおよびプラン ガイドの固定計画|はい|はい|はい|はい||||  
|NOEXPAND ヒントを使用したインデックス付きビューの直接クエリ|はい|はい|はい|はい||||  
|インデックス付きビューの自動メンテナンス|はい|はい|はい|はい||||  
|分散パーティション ビュー|はい|部分的。 分散パーティション ビューは更新できない|部分的。 分散パーティション ビューは更新できない|部分的。 分散パーティション ビューは更新できない|部分的。 分散パーティション ビューは更新できない|部分的。 分散パーティション ビューは更新できない|部分的。 分散パーティション ビューは更新できない|  
|並列インデックス操作|はい|||||||  
|クエリ オプティマイザーによる自動的なインデックス付きのビュー使用|はい|||||||  
|並列整合性チェック|はい|||||||  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティ コントロール ポイント|はい|||||||  
|包含データベース|はい|はい|はい|はい|はい|はい|はい|  
|バッファープール拡張<sup>2</sup>|はい|はい|はい|||||  
  
 <sup>1</sup> 詳細については、「[SysPrep を使用した SQL Server のインストールに関する注意点](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md)」を参照してください。  
  
 <sup>2</sup>この機能は、64ビット [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]でのみ使用できます。  
  
##  <a name="Dev_tools"></a> Development Tools  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Studio との統合|はい|はい|はい|はい|はい|はい|はい|  
|Intellisense ([!INCLUDE[tsql](../includes/tsql-md.md)] および MDX)|はい|はい|はい|はい|はい|はい|はい|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|はい|はい|はい|はい|はい|||  
|SQL クエリの編集およびデザインツール<sup>1</sup>|はい|はい|はい|||||  
|バージョン管理のサポート<sup>1</sup>|はい|はい|はい|||||  
|MDX 編集、デバッグ、およびデザインツール<sup>1</sup>|はい|はい|はい|||||  
  
 <sup>1</sup>この機能は、64ビット版の Standard edition では使用できません。  
  
##  <a name="Programmability"></a> プログラミング  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|共通言語ランタイム (CLR) 統合|はい|はい|はい|はい|はい|はい|はい|  
|ネイティブ XML サポート|はい|はい|はい|はい|はい|はい|はい|  
|XML インデックスの作成|はい|はい|はい|はい|はい|はい|はい|  
|UPSERT 機能をマージ &|はい|はい|はい|はい|はい|はい|はい|  
|FILESTREAM のサポート|はい|はい|はい|はい|はい|はい|はい|  
|FileTable|はい|はい|はい|はい|はい|はい|はい|  
|日付および時刻データ型|はい|はい|はい|はい|はい|はい|はい|  
|国際化サポート|はい|はい|はい|はい|はい|はい|はい|  
|フルテキストおよびセマンティック検索|はい|はい|はい|はい|はい|||  
|クエリ内の言語指定|はい|はい|はい|はい|はい|||  
|Service Broker (メッセージング)|はい|はい|はい|不可 (クライアントのみ)|不可 (クライアントのみ)|不可 (クライアントのみ)|不可 (クライアントのみ)|  
|[!INCLUDE[tsql](../includes/tsql-md.md)] エンドポイント|はい|はい|はい|はい||||  
  
##  <a name="SSIS"></a> Integration Services  
  
|機能|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|-------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザード|はい|はい|はい|はい|はい|はい|はい|  
|組み込みのデータ ソース コネクタ|はい|はい|はい|はい|はい|はい|はい|  
|SSIS デザイナーおよびランタイム|はい|はい|はい|||||  
|基本的な変換|はい|はい|はい|||||  
|基本的なデータ プロファイリング ツール|はい|はい|はい|||||  
|Attunity の Change Data Capture Service for Oracle|はい|||||||  
|Attunity の Change Data Capture Designer for Oracle|はい|||||||  
  
###  <a name="SSIS_AA"></a> Integration Services – 拡張アダプター  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|高パフォーマンスの Oracle 変換先|はい|||||||  
|高パフォーマンスの Teradata 変換先|はい|||||||  
|SAP BW 変換元と変換先|はい|||||||  
|データ マイニング モデル トレーニング変換先アダプター|はい|||||||  
|ディメンション処理の変換先アダプター|はい|||||||  
|パーティション処理の変換先アダプター|はい|||||||  
|Attunity 変更データ キャプチャ コンポーネント|はい|||||||  
|Attunity ODBC (Open Database Connectivity) 接続|はい|||||||  
  
###  <a name="SSIS_AT"></a>Integration Services – 詳細な変換  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|永続性 (高パフォーマンス) 参照|はい|||||||  
|データ マイニング クエリ変換|はい|||||||  
|あいまいグループ化変換とあいまい参照変換|はい|||||||  
|用語抽出と用語参照変換|はい|||||||  
  
##  <a name="MDS"></a> Master Data Services  
  
> [!NOTE]  
>  -   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] は、64 ビット エディションの Business Intelligence と Enterprise でのみ使用できます。  
  
|機能|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|-------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベース (database)|はい|はい||||||  
|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーション|はい|はい||||||  
  
##  <a name="Data_warehouse"></a> Data Warehouse  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|データベースを使用しないキューブ作成|はい|はい|はい|||||  
|自動生成ステージングとデータ ウェアハウス スキーマ|はい|はい|はい|||||  
|変更データ キャプチャ|はい|||||||  
|スター結合クエリ最適化|はい|||||||  
|スケーラブルな読み取り専用の Analysis Services 構成|はい|||||||  
|パーティション テーブルとパーティション インデックスに対する並列クエリ処理|はい|||||||  
|xVelocity メモリ最適化列ストア インデックス|はい|||||||  
|グローバル バッチ集計|はい|||||||  
  
##  <a name="SSAS"></a> Analysis Services  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|スケーラブルな共有データベース (アタッチ/デタッチ、読み取り専用データベース)|はい|はい||||||  
|データベースのバックアップ/復元、アタッチ/デタッチ|はい|はい|はい|||||  
|データベースの同期|はい|はい||||||  
|高可用性|はい|はい|はい|||||  
|プログラミング (AMO、ADOMD.Net、OLEDB、XML/A、ASSL)|はい|はい|はい|||||  
  
###  <a name="BISemModel_multi"></a>BI セマンティックモデル (多次元)  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|準加法メジャー|はい|はい|なし<sup>1</sup>|||||  
|[階層]|はい|はい|はい|||||  
|KPI|はい|はい|はい|||||  
|パースペクティブ|はい|はい||||||  
|アクション|はい|はい|はい|||||  
|勘定科目インテリジェンス|はい|はい|はい|||||  
|タイム インテリジェンス|はい|はい|はい|||||  
|カスタム ロールアップ|はい|はい|はい|||||  
|キューブの書き戻し|はい|はい|はい|||||  
|ディメンションの書き戻し|はい|はい||||||  
|セルの書き戻し|はい|はい|はい|||||  
|詳細|はい|はい|はい|||||  
|高度な階層の種類 (親子、不規則階層)|はい|はい|はい|||||  
|高度なディメンション (参照ディメンション、多対多ディメンション)|はい|はい|はい|||||  
|リンク メジャーとディメンション|はい|はい||||||  
|翻訳|はい|はい|はい|||||  
|集計|はい|はい|はい|||||  
|複数パーティション|はい|はい|可 (3 つまで)|||||  
|プロアクティブ キャッシュ|はい|はい||||||  
|カスタム アセンブリ (ストアド プロシージャ)|はい|はい|はい|||||  
|MDX クエリおよびスクリプト|はい|はい|はい|||||  
|DAX クエリ|はい|はい||||||  
|ロールベースのセキュリティ モデル|はい|はい|はい|||||  
|ディメンションおよびセル レベルのセキュリティ|はい|はい|はい|||||  
|スケーラブルな文字列ストレージ|はい|はい|はい|||||  
|MOLAP、ROLAP、HOLAP ストレージ モード|はい|はい|はい|||||  
|バイナリおよび圧縮 XML の転送|はい|はい|はい|||||  
|プッシュモード処理|はい|はい||||||  
|直接書き戻し|はい|はい||||||  
|メジャー式|はい|はい||||||  
  
 <sup>1</sup>LastChild 準加法メジャーは standard edition でサポートされていますが、他の準加法メジャー (None、FirstChild、Firstchild でない、Lastchild、ByAccount など) はサポートされていません。 加法メジャー (Sum、Count、Min、Max など) や非加法メジャー (DistinctCount) はすべてのエディションでサポートされます。  
  
###  <a name="BISemModel_tabular"></a> BI セマンティック モデル (テーブル)  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[階層]|はい|はい||||||  
|KPI|はい|はい||||||  
|パースペクティブ|はい|はい||||||  
|翻訳|はい|はい||||||  
|DAX 計算、DAX クエリ、MDX クエリ|はい|はい||||||  
|行レベルのセキュリティ|はい|はい||||||  
|[メジャー グループ]|はい|はい||||||  
|In-Memory および DirectQuery ストレージ モード (テーブルのみ)|はい|はい||||||  
  
###  <a name="PowerPivot"></a>PowerPivot for SharePoint  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|共有サービス アーキテクチャに基づく SharePoint ファーム統合|はい|はい||||||  
|使用状況レポート|はい|はい||||||  
|状態の監視のルール|はい|はい||||||  
|PowerPivot ギャラリー|はい|はい||||||  
|PowerPivot のデータ更新|はい|はい||||||  
|PowerPivot データ フィード|はい|はい||||||  
  
###  <a name="DataMining"></a> Data Mining  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|標準アルゴリズム|はい|はい|はい|||||  
|データ マイニング ツール (ウィザード、エディター、クエリ ビルダー)|はい|はい|はい|||||  
|相互検証|はい|はい||||||  
|マイニング構造データのフィルター選択したサブセットのモデル|はい|はい||||||  
|時系列: ARTXP 法と ARIMA 法のカスタムな組み合わせ|はい|はい||||||  
|時系列: 新しいデータでの予測|はい|はい||||||  
|無制限の同時 DM クエリ|はい|はい||||||  
|データマイニングアルゴリズムの詳細な構成 & チューニングオプション|はい|はい||||||  
|プラグイン アルゴリズムのサポート|はい|はい||||||  
|並列モデル処理|はい|はい||||||  
|時系列: 系列のクロス予測|はい|はい||||||  
|アソシエーション ルールの無制限の属性|はい|はい||||||  
|シーケンス予測|はい|はい||||||  
|複数の Naïve Bayes の予測ターゲット、ニューラル ネットワーク、およびロジスティック回帰|はい|はい||||||  
  
##  <a name="Reporting"></a> Reporting Services  
  
###  <a name="Reporting_features"></a>Reporting Services 機能  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|サポートされているカタログ DB の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エディション|Standard 以上|Standard 以上|Standard 以上|Web|Express|||  
|サポートされているデータ ソースの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エディション|すべての   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エディション|すべての [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エディション|すべての [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エディション|Web|Express|||  
|レポート サーバー|はい|はい|はい|はい|はい|||  
|レポート デザイナー|はい|はい|はい|はい|はい|||  
|レポート マネージャー|はい|はい|はい|はい|はい|||  
|ロール ベース セキュリティ|はい|はい|はい|はい|はい|||  
|ワード エクスポートおよびリッチ テキストのサポート|はい|はい|はい|はい|はい|||  
|強化されたゲージとグラフ|はい|はい|はい|はい|はい|||  
|Excel、PDF、およびイメージへのエクスポート|はい|はい|はい|はい|はい|||  
|カスタム認証|はい|はい|はい|はい|はい|||  
|データ フィードとしてのレポート|はい|はい|はい|はい|はい|||  
|モデルのサポート|はい|はい|はい|はい||||  
|ロールベースのセキュリティのカスタム ロールの作成|はい|はい|はい|||||  
|モデル アイテムのセキュリティ|はい|はい|はい|||||  
|無限クリック スルー|はい|はい|はい|||||  
|共有コンポーネント ライブラリ|はい|はい|はい|||||  
|電子メールおよびファイル共有のサブスクリプションとスケジュール設定|はい|はい|はい|||||  
|レポート履歴、実行スナップショット、およびキャッシュ|はい|はい|はい|||||  
|SharePoint 統合|はい|はい|はい|||||  
|リモートおよび非 SQL データ ソースのサポート<sup>1</sup>|はい|はい|はい|||||  
|データ ソース、配信およびレンダリング、RDCE の拡張性|はい|はい|はい|||||  
|データ ドリブン レポート サブスクリプション|はい|はい||||||  
|スケール アウト配置 (Web ファーム)|はい|はい||||||  
|警告<sup>2</sup>|はい|はい||||||  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] <sup>2</sup>|はい|はい||||||  
  
 <sup>1</sup>[!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]でサポートされているデータソースの詳細については、「 [ &#40;Reporting Services SSRS&#41;でサポートされるデータソース](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)」を参照してください。  
  
 <sup>2</sup>SharePoint モードの [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] が必要です。 詳細については、「sharepoint[モード&#40;のインストール Reporting Services SharePoint 2010&#41;および sharepoint 2013](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)」を参照してください。  
  
### <a name="report-server-database-server-edition-requirements"></a>レポート サーバー データベースのサーバー エディション  
 レポート サーバー データベースを作成するときは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のすべてのエディションでデータベースをホストできるわけではないことに注意してください。 次の表に、 [!INCLUDE[ssDE](../includes/ssde-md.md)] の特定のエディションで使用できる [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]のエディションを示します。  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services のエディション|データベースをホストするために使用するデータベース エンジン インスタンスのエディション|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|Standard Edition、Business Intelligence Enterprise Edition (ローカルまたはリモート)|  
|Business Intelligence|Standard Edition、Business Intelligence Enterprise Edition (ローカルまたはリモート)|  
|Standard|Standard Edition、Enterprise Edition (ローカルまたはリモート)|  
|Web|Web Edition (ローカルのみ)|  
|Express with Advanced Services|Express with Advanced Services (ローカルのみ)|  
|Evaluation|Evaluation|  
  
##  <a name="BIClients"></a> Business Intelligence Clients  
 次のソフトウェア クライアント アプリケーションを Microsoft ダウンロード センターから入手できます。これらのアプリケーションは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスで使用するビジネス インテリジェンス ドキュメントの作成に役立ちます。 作成したドキュメントをサーバー環境でホストする場合は、そのドキュメントの種類でサポートされている [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のエディションを使用してください。 これらのクライアント アプリケーションで作成したドキュメントをホストするのに必要なサーバー機能を備えた [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エディションを次の表に示します。  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)]|はい|はい|はい|||||  
|Excel および Visio 2010 用データ マイニング アドイン|はい|はい|はい|||||  
|[!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 2010|はい|はい||||||  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]|はい|はい||||||  
  
> [!NOTE]
>  1.  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] は Excel アドインで、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] には依存しません。 ただし、SharePoint で [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] ワークブックの共有およびコラボレーションを行うには、 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] が必要です。この機能は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise および Business Intelligence エディションの一部として使用できます。  
> 2.  上記の表は、これらのクライアント ツールを有効にするために必要な [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エディションを示しています。ただし、これらの機能は、どのエディションの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]にホストされているデータにもアクセスできます。  
  
##  <a name="Spatial"></a> Spatial and Location Services  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|空間インデックス|はい|はい|はい|はい|はい|はい|はい|  
|平面データ型と測地データ型|はい|はい|はい|はい|はい|はい|はい|  
|高度な空間的なライブラリ|はい|はい|はい|はい|はい|はい|はい|  
|業界標準の空間データ形式のインポート/エクスポート|はい|はい|はい|はい|はい|はい|はい|  
  
##  <a name="Add_DBServices"></a> Additional Database Services  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration Assistant|はい|はい|はい|はい|はい|はい|はい|  
|データベース メール|はい|はい|はい|はい||||  
  
##  <a name="Other_Components"></a> その他のコンポーネント  
  
|機能名|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Data Quality Services|はい|はい||||||  
|StreamInsight|StreamInsight Premium Edition|StreamInsight Standard Edition|StreamInsight Standard Edition|StreamInsight Standard Edition||||  
|StreamInsight HA|StreamInsight Premium Edition|||||||  
  
## <a name="see-also"></a>参照  
 [SQL Server 2014  の製品仕様](../../2014/getting-started/sql-server-2014-product-specifications.md)  
 [SQL Server 2014  用のインストール](../database-engine/install-windows/installation-for-sql-server.md)  
 [SQL Server 2014 のクイックスタート インストール](../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)  
  
  
