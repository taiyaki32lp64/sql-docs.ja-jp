---
title: よく寄せられる質問
titleSuffix: Azure Data Studio
description: Azure Data Studio に関してよく寄せられる質問 (FAQ) について説明します。
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 1916a10a468fdc44c021e410eb1521cb7c219d58
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959548"
---
# <a name="includeazure-data-studioincludesname-sosmd-faq"></a>[!INCLUDE[Azure Data Studio](../includes/name-sos.md)] FAQ

## <a name="what-is-azure-data-studio"></a>Azure Data Studio とは?

Azure Data Studio とは、Windows、MacOS、Linux 上でオンプレミス プラットフォームおよびクラウド データ プラットフォームの Azure Data ファミリを使用するデータ プロフェッショナルを対象にした、新しいオープン ソースのクロスプラットフォーム デスクトップ環境です。 SQL Operations Studio というプレビュー名で以前にリリースされていた Azure Data Studio では、非常に高速な IntelliSense、コード スニペット、ソース管理の統合、統合されたターミナルを含む最新のエディター エクスペリエンスが提供されています。 これは、データ プラットフォームのユーザーを念頭に置いて設計されており、クエリ結果セットのグラフ化機能とカスタマイズ可能なダッシュボードが組み込まれています。

調査によると、ユーザーはクエリの編集作業に、SQL Server Management Studio でのその他の作業よりもはるかに多くの時間を費やしています。 そのため、Azure Data Studio は、最も使用されている機能に重点を置いて設計されていて、オプションの拡張機能として利用できるようにしたエクスペリエンスが製品に追加されています。 これにより、すべてのユーザーは最も頻繁に使用しているワークフローに合わせて自分の環境をカスタマイズできます。


## <a name="how-much-does-azure-data-studio-cost"></a>Azure Data Studio にはどれくらいのコストがかかりますか?

Azure Data Studio は、私的利用または商用利用で無料です。

## <a name="who-should-use-azure-data-studio"></a>どのような人が Azure Data Studio を使用すべきですか

だれでも Azure Data Studio を使用できます。 ただし、データベース開発者、データベース管理者、システム管理者、および独立系ソフトウェア ベンダーによって実行されるタスクを簡素化するように設計されています。

## <a name="what-can-i-do-with-azure-data-studio"></a>Azure Data Studio で何ができますか?

Azure Data Studio は Visual Studio Code の上に構築されていて、SQL Server、Azure SQL Database、Azure SQL DW を操作する際に、キーボードに重点を置いた簡易な最新のコード ワークフロー エクスペリエンスを利用できます。 Azure Data Studio では、ご自分が日々依存しているコア エクスペリエンスが、組み込み機能によってシンプルで使いやすくなっています。その組み込み機能には、複数のタブ ウィンドウ、充実した SQL エディター、IntelliSense、キーワード補完、コード スニペットとコード ナビゲーション、ソース管理の統合 (Git と TFS) などがあります。 オンデマンドでのクエリの実行、テキスト、JSON、または Excel としての結果の表示と保存、データの編集、お気に入りのデータベース接続の整理と管理、馴染みのあるオブジェクト閲覧エクスペリエンスでのデータベース オブジェクトの参照を行うことができます。

Azure Data Studio ユーザー インターフェイス内の [統合ターミナル] ウィンドウにあるお気に入りのコマンドライン ツール (Bash、PowerShell、sqlcmd、bcp、psql、ssh など) を使用できます。 開発目的またはテスト目的でご利用のデータベースのコピーを作成するために、データベース オブジェクトに対して CREATE および INSERT スクリプトを簡単に生成および実行することができます。 データベースおよびデータベース オブジェクト (テーブル、ビュー、ストアド プロシージャ、ユーザー、ログイン、ロールなど) を新規に作成したり、既存のデータベース オブジェクトを更新したりする場合に、スマートなコード スニペットや充実したグラフィカル エクスペリエンスを使用することで生産性を高めることができます。 充実したカスタマイズ可能なダッシュボードを使用することで、オンプレミスのデータベースや、Azure または任意のクラウド内のデータベースでのパフォーマンスに関するボトルネックを監視し、そのトラブルシューティングを迅速に行うことができます。

Azure Data Studio では、ご利用のデータベースをバックアップおよび復元するための一貫したエクスペリエンスが提供されています。 SQL Server Always On 可用性グループの計画的なサポートにより、ご利用のミッションクリティカルな SQL Server データベース用の AG の構成、監視、トラブルシューティングを容易に行うことができ、障害発生時にはセカンダリ データベースに迅速にフェールオーバーすることができます。 Azure Data Studio は、任意のオペレーティングシステム上で選択したデータベースの DevOps ライフサイクルにおいて生産性が向上するように設計されています。 その結果、常に管理状態に置かれるので、リスクを軽減し、問題を迅速に解決し、顧客の期待を超える価値を継続的に提供することができます。

## <a name="is-azure-data-studio-open-source"></a>Azure Data Studio はオープンソースですか?

Azure Data Studio とそのデータ プロバイダーのソース コードは、GitHub で入手できます。 フロントエンド Azure Data Studio のソースコード (Visual Studio Code に基づく) は、ソース コード EULA の下で利用できます。この EULA では、ソフトウェアを変更および使用する権利が提供されますが、ソフトウェアを再配布したりクラウド サービス内でホストしたりすることはできません。 データ プロバイダーのソース コードは、MIT ライセンス ([https://github.com/Microsoft/sqltoolsservice](https://github.com/Microsoft/sqltoolsservice)) の下で利用できます。

## <a name="do-we-plan-to-open-source-ssms"></a>オープン ソースの SSMS を計画していますか?

不可。 ただし、次世代のマルチ OS CLI および GUI ツールはオープンソースです。 たとえば、VS Code、mssql-scripter、および msql CLI の mssql 拡張機能はすべて、GitHub のオープン ソースです。 Azure Data Studio のソース コードは、GitHub で入手できます。  

## <a name="now-that-there-is-azure-data-studio-does-microsoft-plan-to-deprecate-ssms-and-ssdt"></a>Azure Data Studio があるので、Microsoft は SSMS と SSDT を廃止する予定ですか? 

不可。 主力の Windows ツール (SSMS、SSDT、PowerShell) への投資は、次世代のマルチ OS とマルチ DB CLI および GUI ツールに加えて継続されます。 目標は、お客様が自身のシナリオに合わせて選択したプラットフォーム上で希望するツールを選択できるようにすることです。 Azure Data Studio は、クエリの編集とデータ開発に関するエクスペリエンスにより重点を置いています。これらは、調査によれば、SQL Server Management Studio において桁違いに最も使用度の高い機能です。 Azure Data Studio では、拡張機能として、バックアップ、復元、エージェント ジョブ管理、サーバー プロファイリングなどのその他の重要度の高い管理機能を使用することもできます。 Azure Data Studio はクロスプラットフォームでもあるので、ユーザーは自分の選んだプラットフォームで作業を行うことができます。 ただし、SQL Server Management Studio では引き続き最も広範な管理機能が提供しており、これはプラットフォーム管理タスク用の主力ツールであり続けています。 

## <a name="when-should-i-use-azure-data-studio-vs-sql-server-management-studio"></a>Azure Data Studio と SQL Server Management Studio は、どのような場合に使用する必要がありますか?

*Azure Data Studio は次のような場合に使用します。*

- ほとんどの時間をクエリの編集や実行に使用している。
- 結果セットをすばやくグラフ化して視覚化する機能が必要である。
- sqlcmd または Powershell を使用して統合ターミナル経由でほとんどの管理タスクを実行することができる。
- ウィザードのエクスペリエンスが最小限必要である。
- 詳細な管理またはプラットフォームに関連する構成を行う必要はない。
- macOS または Linux 上で実行する必要がある。

*SQL Server Management Studio は次の場合に使用します。*

- ほとんどの時間をデータベース管理タスクに費やしている。
- 複雑な管理またはプラットフォームの構成を行っている。
- ユーザー管理、脆弱性評価、セキュリティ機能の構成など、セキュリティ管理を行っている。
- パフォーマンス チューニング アドバイザーとダッシュボードを使用する必要がある。
- データベース ダイアグラムとテーブル デザイナーを使用する。
- DACPAC のインポート/エクスポートを行っている。
- 登録済みサーバーへのアクセスが必要である。
- Sqlcmd モード、ライブクエリ統計、またはクライアント統計情報を利用する。

## <a name="feature-comparison"></a>機能の比較

### <a name="shell-features"></a>シェルの機能

|機能|Azure Data Studio|SSMS|
|:---|:---|:---|
|Azure サインイン|はい|はい|
|ダッシュボード|はい| |
|拡張機能|はい| |
|統合ターミナル|はい||
|オブジェクト エクスプローラー|はい|はい|
|オブジェクト スクリプト作成|はい|はい|
|プロジェクト システム|はい||
|テーブルからの選択|はい|はい|
|ソース コード管理|はい||
|タスク ウィンドウ|はい||
|テーマ|はい||
|ダーク モード|はい||
|Azure Resource Explorer|プレビュー||
|スクリプト生成ウィザード||はい
|DACPAC のインポート/エクスポート||はい|
|オブジェクトのプロパティ||はい|
|テーブル デザイナー (Table Designer)||はい|

### <a name="query-editor"></a>クエリ エディター

|機能|Azure Data Studio|SSMS|
|:---|:---|:---|
|グラフ ビューアー|はい||
|結果を CSV、JSON、.XLSX にエクスポート|はい||
|IntelliSense|はい|はい|
|スニペット|はい|はい|
|プラン表示|プレビュー|はい|
|クライアント統計||はい|
|ライブ クエリ統計||はい|
|[クエリ オプション]||はい|
|[結果をファイルに出力]||はい|
|[結果をテキストで表示]||はい|
|空間ビューアー||はい|
|sqlcmd||はい|
|T-SQL デバッガー||はい|

### <a name="operating-system-support"></a>オペレーティング システムのサポート

|機能|Azure Data Studio|SSMS|
|:---|:---|:---|
|Windows|はい|はい|
|macOS|はい||
|Linux|はい||

### <a name="data-engineering"></a>Data Engineering

|機能|Azure Data Studio|SSMS|
|:---|:---|:---|
|外部データウィザード|プレビュー||
|HDFS 統合|プレビュー||
|ノートブック|プレビュー||

### <a name="database-administration"></a>データベースの管理

|機能|Azure Data Studio|SSMS|
|:---|:---|:---|
|バックアップ/復元|はい|はい|
|フラット ファイルのインポート|プレビュー|はい|
|SQL エージェント|プレビュー|はい|
|SQL Profiler|プレビュー|はい|
|Always On||はい|
|Always Encrypted||はい|
|データ ウィザードのコピー||はい|
|データ チューニング アドバイザー||はい|
|データベース ダイアグラム||はい|
|エラー ログ ビューアー||はい|
|メンテナンス プラン||はい|
|マルチサーバー クエリ||はい|
|ポリシー ベースの管理||はい|
|PolyBase||はい|
|クエリ ストア||はい|
|[登録済みサーバー]||はい|
|のレプリケーション||はい|
|セキュリティ管理||はい|
|Service Broker||はい|
|SQL Mail||はい|
|テンプレート エクスプローラー||はい|
|脆弱性評価||はい|
|XEvent 管理||はい|


## <a name="azure-data-studio-is-missing-a-feature-that-is-in-ssmsssdt-will-you-add-it"></a>Azure Data Studio には、SSMS/SSDT にある機能がありません。 それを追加しますか?

それは、シナリオと顧客/ビジネス ニーズによって決まります。 優先順位を付けるために、[GitHub](https://github.com/microsoft/azuredatastudio/issues) に提案を提出してください。

## <a name="i-understand-azure-data-studio-and-the-mssql-extension-for-vs-code-are-powered-by-a-new-tools-service-that-uses-smo-apis-under-the-covers-is-smo-available-on-linux-and-macos"></a>Azure Data Studio と VS Code 用の mssql 拡張機能は、内部的に SMO API を使用する新しいツール サービスによって強化されていると理解しています。 SMO は Linux と macOS 上で利用できますか?

SMO API は、Linux または macOS に対してまだ使いやすい方法で提供されていません。 Microsoft は Azure Data Studio で必要としていて、ロードマップの一環として拡張する予定である SMO API のサブセットを .NET Core に移植済みです。 SQL Tools Service は GitHub 上の次の場所にあります: [https://github.com/Microsoft/sqltoolsservice](https://github.com/Microsoft/sqltoolsservice)。

## <a name="do-you-plan-to-port-the-dacfx-apis-andor-sqlpackageexe-andor-ssdt-to-linux-and-macos"></a>DACFx API、sqlpackage.exe、SSDT を Linux や macOS に移植する予定はありますか?

それは長期的なロードマップにあります。 優先順位を付けるために、[GitHub](https://github.com/microsoft/azuredatastudio/issues) に提案を提出してください。

## <a name="will-sql-powershell-cmdlets-be-available-on-linux-and-macos"></a>SQL PowerShell コマンドレットは、Linux および macOS 上で利用できますか?

SQL PowerShell は、現在 PowerShell ギャラリーで入手できます。これを Windows 上で使用すれば、Linux 上の SQL など、あらゆる場所で実行されている SQL Server を操作できます。 Linux および macOS 用の SQL PowerShell コマンドレットを提供することは、ロードマップにあります。 優先順位を付けるために、[GitHub](https://github.com/microsoft/azuredatastudio/issues) に提案を提出してください。

## <a name="who-usually-uses-azure-data-studio"></a>通常、だれが Azure Data Studio を使用しますか?

開発者と DBA が通常は、Azure Data Studio のユーザーです。

## <a name="does-azure-data-studio-integrate-with-azure-sql-data-warehouse"></a>Azure Data Studio は Azure SQL Data Warehouse に統合されていますか?

可能。 Azure SQL Data Warehouse に対する Azure Data Studio のサポートは、Azure SQL Database Managed Instance および SQL Server 2019 Big Data と共に現在プレビュー段階にあります。

## <a name="why-is-azure-data-studio-important-for-the-new-version-of-sql-server"></a>新しいバージョンの SQL Server にとって Azure Data Studio が重要である理由は何ですか?

SQL Server ではその機能が Big Data 領域にまで拡張されているので、それらのユースケースをサポートするために新しいツールが必要とされています。 そのため、Azure Data Studio では現在、SQL Server Big Data をサポートする新しいプレビュー エクスペリエンスが出荷されています。これには、SQL Server ツールセットで初めてのノートブック エクスペリエンスや、リモート SQL Server および Oracle インスタンスからデータへのアクセスを簡単かつ迅速にする新しい [外部テーブルを作成する] ウィザードが含まれます。
