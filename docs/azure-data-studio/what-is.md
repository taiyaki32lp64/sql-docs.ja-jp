---
title: Azure Data Studio とは
titleSuffix: Azure Data Studio
description: Azure Data Studio は、SQL Server、Azure SQL Database、および Azure SQL Data Warehouse を管理するために、Windows、macOS、Linux で実行される無償の軽量ツールです。
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: overview
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18, sqlfreshmay19
ms.date: 10/15/2019
ms.openlocfilehash: 9f6be7cbd673a98f8e8934860b0e26d427acac06
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241746"
---
# <a name="what-is-azure-data-studio"></a>Azure Data Studio とは

Azure Data Studio とは、Windows、macOS、Linux 上でオンプレミス プラットフォーム、クラウド データ プラットフォームの Microsoft ファミリを使用するデータ プロフェッショナルを対象にした、クロスプラットフォーム データベース ツールです。

Azure Data Studio では、IntelliSense、コード スニペット、ソース管理の統合、統合されたターミナルを含む最新のエディター エクスペリエンスが提供されています。 これは、データ プラットフォームのユーザーを念頭に置いて設計されており、クエリ結果セットのグラフ化機能とカスタマイズ可能なダッシュボードが組み込まれています。

Azure Data Studio のソース コードとそのデータ プロバイダーは、ソース コード EULA の下の GitHub で利用できます。この EULA では、ソフトウェアを変更および使用する権利が提供されますが、ソフトウェアを再配布したりクラウドサービス内でホストしたりすることはできません。 詳細については、「[Azure Data Studio FAQ](faq.md)」(Azure Data Studio の FAQ) を参照してください。

**[ダウンロードしてインストールする[!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)**

## <a name="sql-code-editor-with-intellisense"></a>IntelliSense を使用した SQL コード エディター

[!INCLUDE[name-sos](../includes/name-sos-short.md)] では、組み込み機能によって日々の作業を容易にする、キーボードに重点を置いた最新の SQL コーディング エクスペリエンスが提供されます。その組み込み機能には、複数のタブ ウィンドウ、充実した SQL エディター、IntelliSense、キーワード補完、コード スニペット、コード ナビゲーション、ソース管理の統合 (Git) などがあります。 オンデマンドの SQL クエリを実行し、結果をテキスト、JSON、または Excel として表示し、保存します。 使い慣れたオブジェクト ブラウズ エクスペリエンスで、データの編集、お気に入りのデータベース接続の整理、データベース オブジェクトの参照を行います。 SQL エディターの使用方法については、「[SQL エディターを使用してデータベース オブジェクトを作成する](tutorial-sql-editor.md)」を参照してください。

## <a name="smart-sql-code-snippets"></a>スマート SQL コード スニペット

SQL コード スニペットにより、データベース、テーブル、ビュー、ストアド プロシージャ、ユーザー、ログイン、ロールなどを作成するため、および既存のデータベース オブジェクトを更新するための適切な SQL 構文が生成されます。 スマート スニペットを使用して、開発またはテストを目的としたデータベースのコピーをすばやく作成したり、CREATE および INSERT スクリプトを生成して実行したりできます。

[!INCLUDE[name-sos](../includes/name-sos-short.md)] には、カスタム SQL コード スニペットを作成する機能も用意されています。 詳細については、「[コード スニペットの作成と使用](code-snippets.md)」を参照してください。

## <a name="customizable-server-and-database-dashboards"></a>カスタマイズ可能なサーバーとデータベースのダッシュボード

充実したカスタマイズ可能なダッシュボードを作成することで、データベースでのパフォーマンスに関するボトルネックを監視し、そのトラブルシューティングを迅速に行うことができます。 分析情報ウィジェットとデータベース (およびサーバー) ダッシュボードの詳細については、「[分析情報ウィジェットを使用したサーバーとデータベースの管理](insight-widgets.md)」を参照してください。

## <a name="connection-management-server-groups"></a>接続管理 (サーバー グループ)

サーバー グループにより、使用するサーバーとデータベースの接続情報を整理するための手段が提供されます。 詳細については、「[サーバー グループ](server-groups.md)」を参照してください。

## <a name="integrated-terminal"></a>統合ターミナル

[!INCLUDE[name-sos](../includes/name-sos-short.md)] ユーザー インターフェイス内の [統合ターミナル] ウィンドウにあるお気に入りのコマンドライン ツール (Bash、PowerShell、sqlcmd、bcp、ssh など) を使用できます。 統合ターミナルの詳細については、「[統合ターミナル](integrated-terminal.md)」を参照してください。

## <a name="extensibility-and-extension-authoring"></a>拡張性と拡張機能の作成

基本インストールの機能を拡張することで、[!INCLUDE[name-sos](../includes/name-sos-short.md)] のエクスペリエンスを向上させることができます。 [!INCLUDE[name-sos](../includes/name-sos-short.md)] では、拡張機能の作成のサポートだけでなく、データ管理アクティビティの機能拡張ポイントも提供されます。

[!INCLUDE[name-sos](../includes/name-sos-short.md)] における機能拡張の詳細については、[機能拡張](extensibility.md)に関するページを参照してください。
拡張機能の作成の詳細については、[拡張機能の作成](extension-authoring.md)に関するページを参照してください。

## <a name="feature-comparison-with-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS) との機能の比較

**Azure Data Studio は次のような場合に使用します。**

- macOS または Linux 上で実行する必要がある
- SQL Server 2019 ビッグ データ クラスターに接続しようとしている
- ほとんどの時間をクエリの編集や実行に使用している
- 結果セットをすばやくグラフ化して視覚化する機能が必要である
- sqlcmd または PowerShell を使用して統合ターミナル経由でほとんどの管理タスクを実行することができる
- ウィザード エクスペリエンスの必要は最小限である
- 詳細な管理構成を行う必要がない

**SQL Server Management Studio は次の場合に使用します。**

- ほとんどの時間をデータベース管理タスクに費やしている
- 詳細な管理構成を実行している
- ユーザー管理、脆弱性評価、セキュリティ機能の構成などのセキュリティ管理を行っている
- SQL Server クエリ ストアのレポートを利用する
- パフォーマンス チューニング アドバイザーとダッシュボードを使用する必要がある
- DACPAC のインポート/エクスポートを行っている
- 登録済みサーバーにアクセスする必要があり、Windows で SQL Server サービスを制御する場合

### <a name="shell"></a>Shell

|機能|Azure Data Studio|SSMS|
|:---|:---|:---|
|Azure サインイン|はい|はい|
|ダッシュボード|はい||
|拡張機能|はい||
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
|スクリプト生成ウィザード||はい|
|DACPAC のインポート/エクスポート||はい|
|オブジェクトのプロパティ||はい|
|テーブル デザイナー (Table Designer)||はい|

### <a name="query-editor"></a>クエリ エディター

|機能|Azure Data Studio|SSMS|
|:---|:---|:---|
|グラフ ビューアー|はい||
|結果を CSV、JSON、XLSX にエクスポート|はい||
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
|ノートブック|はい||
|スニペットとしてクエリを保存|はい||

### <a name="operating-system-support"></a>オペレーティング システムのサポート

|機能|Azure Data Studio|SSMS|
|:---|:---|:---|
|Linux|はい||
|macOS|はい||
|Windows|はい|はい|

### <a name="data-engineering"></a>Data Engineering

|機能|Azure Data Studio|SSMS|
|:---|:---|:---|
|外部テーブルの作成ウィザード|プレビュー||
|HDFS 統合|プレビュー||
|ノートブック|プレビュー||

### <a name="database-administration"></a>データベースの管理

|機能|Azure Data Studio|SSMS|
|:---|:---|:---|
|バックアップ/復元|はい|はい|
|ビッグ データ クラスターのサポート|はい||
|フラット ファイルのインポート|プレビュー|はい|
|SQL エージェント|プレビュー|はい|
|SQL Profiler|プレビュー|はい|
|常時接続||はい|
|Always Encrypted||はい|
|データ コピー ウィザード||はい|
|データ チューニング アドバイザー||はい|
|エラー ログ ビューアー||はい|
|メンテナンス プラン||はい|
|マルチサーバー クエリ||はい|
|ポリシー ベースの管理||はい|
|PolyBase||はい|
|クエリ ストア||はい|
|[登録済みサーバー]||はい|
|レプリケーション||はい|
|セキュリティ管理||はい|
|Service Broker||はい|
|SQL Mail||はい|
|テンプレート エクスプローラー||はい|
|脆弱性評価||はい|
|XEvent 管理||はい|
|SQL Assessment API の統合||はい|

## <a name="next-steps"></a>次のステップ

- [ダウンロードしてインストールする[!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)
- [SQL Server に対する接続およびクエリ](quickstart-sql-server.md)
- [Azure SQL Database に対する接続およびクエリ](quickstart-sql-database.md)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
