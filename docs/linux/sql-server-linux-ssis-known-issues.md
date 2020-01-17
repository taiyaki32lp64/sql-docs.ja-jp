---
title: Linux での SSIS に関する制限事項と既知の問題
description: この記事では、Linux コンピューターでの SQL Server Integration Services (SSIS) に関する制限事項と既知の問題について説明します。
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 06/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 45e5d9b36b6fd75db7bbc3c5ea397ee9226e2771
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "68032231"
---
# <a name="limitations-and-known-issues-for-ssis-on-linux"></a>Linux での SSIS に関する制限事項と既知の問題

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、Linux での SQL Server Integration Services (SSIS) に関する制限事項と既知の問題について説明します。

## <a name="general-limitations-and-known-issues"></a>一般的な制限事項と既知の問題

Linux での SSIS パッケージのこのリリースでは、次の機能はサポートされていません。
  - SSIS カタログ データベース
  - SQL エージェントによるスケジュールされたパッケージの実行
  - [Windows 認証]
  - サードパーティ コンポーネント
  - 変更データ キャプチャ (CDC)
  - SSIS Scale Out
  - SSIS 用の Azure Feature Pack
  - Hadoop と HDFS のサポート
  - Microsoft Connector for SAP BW

Linux での SSIS のその他の制限事項と既知の問題については、[リリース ノート](sql-server-linux-release-notes.md#ssis)を参照してください。

## <a name="components"></a> サポートされているコンポーネントとサポートされていないコンポーネント

Linux では、次の組み込みの Integration Services コンポーネントがサポートされています。 これらの一部については、Linux プラットフォームでは制限があります。 ここに記載されていない組み込みコンポーネントは、Linux ではサポートされていません。

## <a name="supported-control-flow-tasks"></a>サポートされている制御フロー タスク
- 一括挿入タスク
- [データ フロー タスク]
- データ プロファイル タスク
- SQL 実行タスク
- T-SQL ステートメントの実行タスク
- 式タスク
- FTP タスク
- Web サービス タスク
- XML タスク

## <a name="control-flow-tasks-supported-with-limitations"></a>制限付きでサポートされている制御フロー タスク

| タスク | 制限事項 |
|------------|---|
| プロセス実行タスク | インプロセス モードのみがサポートされます。 |
| ファイル システム タスク | "*ディレクトリの移動*" 操作と "*ファイル属性の設定*" 操作はサポートされていません。 |
| スクリプト タスク | 標準の .NET Framework API のみがサポートされます。 |
| メール送信タスク | 匿名ユーザー モードのみがサポートされます。 |
| データベース転送タスク | UNC パスはサポートされません。 |
| | |

## <a name="supported-and-unsupported-maintenance-plan-tasks"></a>サポート対象およびサポート対象外のメンテナンス プランのタスク

SQL Server メンテナンス プランでは、通常、さまざまな SSIS タスクを使用できます。

次のメンテナンス プランのタスクは、Linux ではサポートされていません。
- オペレーターへの通知
- SQL Server エージェント ジョブの実行

次のメンテナンス プランのタスクは、Linux でサポートされています。
- データベースの整合性確認
- データベースの圧縮
- [インデックスの再構成]
- インデックスの再構築
- 統計の更新
- 履歴のクリーンアップ
- データベースのバックアップ
- T-SQL ステートメント

## <a name="supported-control-flow-containers"></a>サポートされている制御フロー コンテナー
- シーケンス コンテナー
- For ループ コンテナー
- Foreach ループ コンテナー

## <a name="supported-data-flow-sources-and-destinations"></a>サポートされているデータ フローの変換元と変換先
- 生ファイルの変換元と接続先
- XML ソース

## <a name="data-flow-sources-and-destinations-supported-with-limitations"></a>制限付きでサポートされているデータ フローの変換元と変換先

| コンポーネント | 制限事項 |
|------------|---|
| ADO.NET の変換元と変換先 | SQLClient データ プロバイダーのみがサポートされます。 |
| フラット ファイルの変換元と変換先 | 既定のパス マッピング規則が適用される、Windows スタイルのファイル パスのみがサポートされます。 たとえば、`D:\home\ssis\travel.csv` は `/home/ssis/travel.csv` になります。 |
| OData の変換元 | 基本認証のみがサポートされます。 |
| ODBC のソースとターゲット | Linux では 64 ビットの Unicode ODBC ドライバーがサポートされます。 Linux では UnixODBC ドライバー マネージャーに依存します。 |
| OLE DB の変換元と変換先 | SQL Server Native Client 11.0 と Microsoft OLE DB Provider for SQL Server のみがサポートされます。 |
| | |

## <a name="supported-data-flow-transformations"></a>サポートされているデータ フロー変換
- Aggregate
- 監査
- Balanced Data Distributor
- 文字マップ
- 条件分割
- 列コピー
- データ変換
- [派生列]
- 列エクスポート
- あいまいグループ化
- あいまい参照
- 列インポート
- Lookup
- Merge
- マージ結合
- マルチキャスト
- ピボット
- 行数
- 緩やかに変化するディメンション
- 並べ替え
- 用語参照
- UNION ALL
- ピボット解除

## <a name="data-flow-transformations-supported-with-limitations"></a>制限付きでサポートされているデータ フロー変換

| コンポーネント | 制限事項 |
|------------|---|
| OLE DB コマンド変換 | OLE DB の変換元と変換先と同じ制限事項があります。 |
| スクリプト コンポーネント | 標準の .NET Framework API のみがサポートされます。 |
| | |

## <a name="supported-and-unsupported-log-providers"></a>サポートされているログ プロバイダーとサポートされていないログ プロバイダー
Linux では、Windows イベント ログ プロバイダーを除くすべての組み込み SSIS ログ プロバイダーがサポートされています。

SQL Server ログ プロバイダーでは、SQL 認証のみがサポートされています。Windows 認証はサポートされていません。

テキスト ファイル、XML ファイル、および SQL Server Profiler の SSIS ログ プロバイダーでは、指定したファイルに出力が書き込まれます。 ファイル パスには以下の考慮事項が適用されます。
-   パスを指定しない場合、ログ プロバイダーではホストの現在のディレクトリに対して書き込みが行われます。 現在のユーザーがホストの現在のディレクトリへの書き込みアクセス許可を持っていない場合、ログ プロバイダーでエラーが発生します。
-   ファイル パスでは環境変数を使用できません。 環境変数を指定すると、指定したリテラル テキストがファイル パスに表示されます。 たとえば、`%TMP%/log.txt` と指定した場合、ログ プロバイダーでは現在のホスト ディレクトリにリテラル テキスト `/%TMP%/log.txt` が追加されます。

## <a name="related-content-about-ssis-on-linux"></a>Linux 上の SSIS の関連コンテンツ
-   [SSIS で Linux 上のデータの抽出、変換、読み込みを行う](sql-server-linux-migrate-ssis.md)
-   [SQL Server Integration Services (SSIS) on Linux をインストールする](sql-server-linux-setup-ssis.md)
-   [ssis-conf を使用して Linux で SQL Server Integration Services を構成する](sql-server-linux-configure-ssis.md)
-   [cron を利用して Linux で SQL Server Integration Services パッケージのスケジュールを設定する](sql-server-linux-schedule-ssis-packages.md)
