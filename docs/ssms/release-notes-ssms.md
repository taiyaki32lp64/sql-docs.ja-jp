---
title: SQL Server Management Studio (SSMS) のリリース ノート | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 3dc76cc1-3b4c-4719-8296-f69ec1b476f9
author: markingmyname
ms.author: maghan
ms.custom: ''
ms.date: 11/04/2019
ms.openlocfilehash: cdcc955050ebab5702d22fef60628876bd367757
ms.sourcegitcommit: db715cad313055c8b42d547be686de8755342d65
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73801152"
---
# <a name="release-notes-for-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS) のリリース ノート

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

この記事では、SSMS の現在と以前のバージョンの更新、機能強化、およびバグの修正に関する詳細を提供します。

<!--
The latest ## H2 section of this Release Notes article has been reformatted to match the new standard.
The new standard replaces the use of bullet lists with the 2-column markdown table format.
Please use the new 2-column table format going forward.
And please do include the final blank row of "| &nbsp;| &nbsp;|".

The ## H2 titles are also being shortened, by the removal of unnecessary repetitive strings.
In this case, "## SSMS 17.9" is being shortened to "## 17.9" (as one standard actual example).
Also, we are appending the 'Month yyyy.'

Also, this file has been renamed to the new standard, which calls for the file name to be with "release-notes-[techAreaName].md."
The old name for this file was 'sql-server-management-studio-changelog-ssms.md'.
But today the new file name is 'release-notes-ssms.md' (still in 'docs/ssms/').

Thank you.
GeneMi. 2019/04/02.
-->

## <a name="ssms-184"></a>SSMS 18.4

ダウンロード:[SSMS 18.4 のダウンロード](download-sql-server-management-studio-ssms.md)  
ビルド番号:15.0.18206.0  
リリース日:2019 年 11 月 4 日

SSMS 18.4 は SSMS の最新の一般提供 (GA) リリースです。 SSMS の以前のバージョンが必要な場合は、[以前のリリースの SSMS](release-notes-ssms.md#previous-ssms-releases) を参照してください。

18.4 は、18.3.1 に次の新しい項目とバグ修正を加えた更新プログラムです。

## <a name="whats-new-in-184"></a>18.4 の新機能

| [新しい項目] | 詳細 |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| データ分類 | データ分類に対してカスタム情報保護ポリシーのサポートが追加されました。 |
| クエリ ストア | ダイアログのプロパティに "*クエリごとに最大プラン*" の値が追加されました。 |
| クエリ ストア | 新しいカスタム キャプチャ ポリシーのサポートが追加されました。 |
| SMO/スクリプト作成 | SQL DW で具体化されたビューのスクリプトをサポートします。 |
| SMO/スクリプト作成 | *SQL On Demand* のサポートが追加されました。 |
| SMO/スクリプト作成 | [SQL Assessment API](../sql-assessment-api/sql-assessment-api-overview.md) - 50 個の評価規則が追加されました (GitHub の詳細を参照)。 |
| SMO/スクリプト作成 | [SQL Assessment API](../sql-assessment-api/sql-assessment-api-overview.md) - ルールの条件に基になる計算式と比較が追加されました。 |
| SMO/スクリプト作成 | [SQL Assessment API](../sql-assessment-api/sql-assessment-api-overview.md) - RegisteredServer オブジェクトのサポートが追加されました。 |
| SMO/スクリプト作成 | [SQL Assessment API](../sql-assessment-api/sql-assessment-api-overview.md) - JSON 形式での規則の格納方法が更新され、オーバーライド/カスタマイズを適用するメカニズムも更新されました。 |
| SMO/スクリプト作成 | [SQL Assessment API](../sql-assessment-api/sql-assessment-api-overview.md) - Linux で SQL をサポートするための規則が更新されました。 |
| SMO/スクリプト作成 | [SQL Assessment API](../sql-assessment-api/sql-assessment-api-overview.md) - 規則セットの JSON 形式が更新され、SCHEMA バージョンが追加されました。 |
| SMO/スクリプト作成 | [SQL Assessment API](../sql-assessment-api/sql-assessment-api-overview.md) - 推奨事項の読みやすさが向上するように、コマンドレットの出力が更新されました。 |
| XEvent プロファイラー | XEvent プロファイラー セッションに *error_reported* イベントが追加されました。 |

## <a name="bug-fixes-in-184"></a>18.4 でのバグの修正

| 新しい項目 | 詳細 |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Analysis Services | 多次元データベース用 DAX スクリプト エディターで IntelliSense にテーブルが表示されない問題を修正しました。 |
| Analysis Services | DAX パーサーを使用して、エンジン文字列に変換します。 これは、国際的な区切り記号、小数点、および空白文字を対象としています。 |
| Always Encrypted | "*要求の検証*" で "*大文字と小文字が区別されない*" 問題を修正しました。 |
| Always Encrypted | エラー/警告レポートが正しく機能しない問題を修正しました。 |
| データベース コピー ウィザード | このダイアログのレンダリングにおけるさまざまな切り捨てとレイアウトの問題を修正しました。 |
| SSMS 全般 | SQL ファイルも指定されたときにコマンド ラインで渡された接続情報が SSMS で優先されない、長い間解決されなかった問題を修正しました。 |
| SSMS 全般 | "レプリケーションフィルター" オブジェクトでセキュリティ保護可能なリソースを表示しようとしたときの SSMS のクラッシュを修正しました。 |
| SSMS 全般 | SSMS で資格情報のキャッシュを参照することにより、-P コマンド ライン オプションの削除を軽減しました。必要な資格情報が見つかった場合は、それを使用して接続が確立されます。 |
| フラット ファイルのインポート | "*フラット ファイルのインポート*" 機能でテキスト修飾子が正しく処理されない問題を修正しました。 |
| オブジェクト エクスプローラー | オブジェクト エクスプローラーでの Azure SQL Database の削除で正しくないメッセージが表示される問題を修正しました。 |
| クエリ結果 | SSMS 18.3.1 で発生するようになった問題を修正しました。グリッドが少し狭すぎて、すべての列で最長文字列の末尾に *...* が表示されました。 |
| レプリケーション ツール | SQL エージェント ジョブを編集しようとすると、アプリケーションでエラー ("ファイルまたはアセンブリ ... が読み込めませんでした") がスローされる原因となった問題を修正しました。 |
| SMO/スクリプト作成 | 照合順序が Japanese_BIN2 である SQL DW に対する *[テーブルをスクリプト化...]* が動作しない問題を修正しました。|
| SMO/スクリプト作成 | ScriptAlter() でサーバーでのステートメントの実行が終了する問題を修正しました。|
| SQL エージェント | エージェント オペレーターの名前が UI で変更されたときに、オペレーターが UI でもスクリプトでも更新されないという問題を修正しました。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/32897647)」を参照してください。|

### <a name="known-issues-184"></a>既知の問題 (18.4)

* マシン A 上で実行されている SSMS から作成されたデータベース ダイアグラムは、マシン B からは変更できません (SSMS がクラッシュします)。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/37992649)」を参照してください。

* 複数のクエリ ウィンドウを切り替えると再描画の問題が発生します。 詳細については、UserVoice を参照してください。 この問題を回避するには、 *[ツール] > [オプション]* でハードウェア アクセラレータを無効にします。

他の既知の問題と製品チームへのフィードバックの提供については、「[UserVoice](https://feedback.azure.com/forums/908035-sql-server)」を参照してください。

## <a name="previous-ssms-releases"></a>以前のリリースの SSMS

以前のバージョンの SSMS をダウンロードするには、次のセクションのタイトル リンクをクリックします。

## <a name="downloadssdtmediadownloadpng-ssms-1831httpsgomicrosoftcomfwlinklinkid2105412"></a>![ダウンロード](../ssdt/media/download.png) [SSMS 18.3.1](https://go.microsoft.com/fwlink/?linkid=2105412)

リリース番号:18.3.1  
ビルド番号:15.0.18183.0  
リリース日:2019 年 10 月 2 日

SSMS 18.3.1 は SSMS の最新の一般提供 (GA) リリースです。 SSMS の以前のバージョンが必要な場合は、[以前のリリースの SSMS](release-notes-ssms.md#previous-ssms-releases) を参照してください。

18.3.1 は、18.2 に次の新しい項目とバグ修正を加えた更新プログラムです。

## <a name="whats-new-in-1831"></a>18.3.1 の新機能

| [新しい項目] | 詳細 |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| データ分類 | データ分類情報が列のプロパティ UI に追加されます ("*情報の種類*"、"*情報の種類 ID*"、"*機密ラベル*"、および "*機密ラベル ID*" は SSMS UI では公開されません)。 |
| Intellisense/エディター | SQL Server 2019 に最近追加された機能のサポートを更新しました (たとえば、"ALTER SERVER CONFIGURATION")。 |
| Integration Services | 新しい選択メニュー項目 `Tools > Migrate to Azure > Configure Azure-enabled DTExec` が追加されます。これにより、Azure-SSIS Integration Runtime 上で SSIS パッケージ実行が ADF パイプラインでの SSIS パッケージの実行アクティビティとして呼び出されます。 |
| SMO/スクリプト作成 | Azure SQL DW 固有の制約のスクリプト作成サポートに対するサポートを追加しました。 |
| SMO/スクリプト作成 | データ分類 </br> - SQL バージョン 10 (SQL 2008) 以降のサポートを追加しました。 </br> - SQL バージョン 15 (SQL 2019) 以降および Azure SQL DB に新しい機密属性 ' rank' を追加しました。 |
| SMO/スクリプト作成 | [SQL Assessment API](../sql-assessment-api/sql-assessment-api-overview.md) - ルールセットの形式にバージョン管理を追加しました。 |
| SMO/スクリプト作成 | [SQL Assessment API](../sql-assessment-api/sql-assessment-api-overview.md) - 新しいチェックを追加しました。 |
| SMO/スクリプト作成 | [SQL Assessment API](../sql-assessment-api/sql-assessment-api-overview.md) - Azure SQL Database Managed Instance のサポートを追加しました。 |
| SMO/スクリプト作成 | [SQL Assessment API](../sql-assessment-api/sql-assessment-api-overview.md) - 結果を表で表示するようコマンドレットの既定のビューを更新しました。 |

## <a name="bug-fixes-in-1831"></a>18.3.1 でのバグの修正

| 新しい項目 | 詳細 |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Analysis Services | MDX クエリ エディターの拡大縮小の問題を修正します。|
| Analysis Services | ユーザーが新しいセッションを作成できない原因である XEvent UI の問題を修正しました。 |
| SQL Azure へのデータベースの配置 | この機能が動作しない原因となっていた (DacFx の) 問題を修正しました。|
| SSMS 全般 | XEvent ビューアーの並べ替え機能を使用すると SSMS がクラッシュする原因となっていた問題を修正しました。 |
| SSMS 全般 | SSMS のデータベース復元が無期限にハングする可能性があるという、長い間未解決だった問題を修正しました。 </br></br> 詳細については、UserVoice 項目を参照してください: </br> [データベースの復元 - [バックアップ デバイスの選択] で読み込み処理が遅い](https://feedback.azure.com/forums/908035/suggestions/32899099/)。  </br> [SSMS 2016 のデータベース復元ダイアログでの処理が遅い](https://feedback.azure.com/forums/908035/suggestions/32900767/)。 </br> [データベースの復元処理が遅い](https://feedback.azure.com/forums/908035/suggestions/32900224/)。  </br> [デバイスからのデータベース復元で "..." をクリックするとハングする](https://feedback.azure.com/forums/908035/suggestions/34281658/)。  |
| SSMS 全般 | すべてのログインの既定の言語がアラビア語として表示される問題を修正しました。 </br></br> 詳細については、UserVoice 項目を参照してください: [SSMS 18.2 の既定言語の表示に関するバグ](https://feedback.azure.com/forums/908035/suggestions/38236363)。 |
| SSMS 全般 | (ユーザーが T-SQL エディター ウィンドウを右クリックしたときに) " *[クエリ オプション]* " のダイアログが適切に表示されない問題を、サイズを変更可能にすることによって修正しました。|
| SSMS 全般 | 結果グリッド/ファイル (SSMS 18.2 で導入) に表示される " *[完了時刻]* " メッセージが、[ツール] > [オプション] > [クエリ実行] > [SQL Server] > [詳細] > [完了時刻の表示] で構成できるようになりました。 |
| SSMS 全般 | 接続ダイアログで、" *[Active Directory - パスワード]* " と " *[Active Directory - 統合]* " を、" *[Azure Active Directory - パスワード]* " と " *[Azure Active Directory - 統合]* " にそれぞれ置き換えました。 |
| SSMS 全般 | 負の UTC オフセットの TZ にいるユーザーが SSMS を使用して SQL Azure マネージド インスタンスに対する監査を構成できない原因である問題を修正しました。 |
| SSMS 全般 | XEvent UI で、グリッド上にカーソルを置いたときに行が選択されていた問題を修正しています。 </br></br> 詳細については、UserVoice 項目を参照してください: [SSMS 拡張イベント UI でのカーソルを置いたときの選択アクション](https://feedback.azure.com/forums/908035/suggestions/38262124)。 |
| フラット ファイルのインポート | 単純または豊富なデータ型の検出をユーザーが選択できるようにすることで、フラット ファイルのインポートですべてのデータがインポートされない問題を修正しました。</br></br> 詳細については、UserVoice 項目を参照してください: [SSMS のフラット ファイルのインポートですべてのデータがインポートされない](https://feedback.azure.com/forums/908035/suggestions/38096989)。 |
| Integration Services | 新しい操作の種類 *StartNonCatalogExecution* が SSIS 操作レポートに追加されます。|
| Integration Services | Azure 対応の `DTExec` ユーティリティによって生成される Azure Data Factory パイプラインの問題を修正して、適切なパラメーターの型が使用されるようにしました。 (18.3.1 の場合は明示的) |
| SMO/スクリプト作成 | **SMO.Server.SetDefaultInitFields(true)** が使用されているときにプロパティをフェッチすると SMO からエラーがスローされる原因となっていた問題を修正しました。|
| クエリ ストア UI | *[追跡対象クエリ]* ビューで *[実行回数]* メトリックが選択されている場合に Y 軸がスケーリングされない問題を修正しました。 |
| 脆弱性評価 | Azure SQL DB のベースラインのクリアと承認が無効になりました。|

### <a name="known-issues-1831"></a>既知の問題 (18.3.1)

- マシン A 上で実行されている SSMS から作成されたデータベース ダイアグラムは、マシン B からは変更できません (SSMS がクラッシュします)。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/37992649)」を参照してください。

- 複数のクエリ ウィンドウを切り替えると再描画の問題が発生します。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/37474042)」を参照してください。 この問題を回避するには、[ツール] > [オプション] でハードウェア アクセラレータを無効にします。

他の既知の問題と製品チームへのフィードバックの提供については、「[UserVoice](https://feedback.azure.com/forums/908035-sql-server)」を参照してください。

## <a name="downloadssdtmediadownloadpng-ssms-182httpsgomicrosoftcomfwlinklinkid2099720"></a>![](../ssdt/media/download.png) [SSMS 18.2](https://go.microsoft.com/fwlink/?linkid=2099720) のダウンロード

リリース番号:18.2  
ビルド番号:15.0.18142.0  
リリース日:2019 年 7 月 25 日

18.2 は、18.1 に次の新しい項目とバグ修正を加えた更新プログラムです。

## <a name="whats-new-in-182"></a>18.2 の新機能

|  新しい項目  |  詳細  |
|-------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Integration Services (SSIS) | Azure の SSIS パッケージ スケジューラに対するパフォーマンスの最適化。 |
| Intellisense/エディター | データ分類に対するサポートを追加しました。 |
| OPTIMIZE_FOR_SEQUENTIAL_KEY | Intellisense サポートを追加しました。 |
| OPTIMIZE_FOR_SEQUENTIAL_KEY | インデックスへの高コンカレンシーの挿入のスループット向上に役立つ、データベース エンジン内での最適化を有効にします。 このオプションは、最終ページ挿入の競合が起きやすいインデックスを対象としています。これは、一般に、ID 列、シーケンス、または日付/時刻列などの連続したキーを持つインデックスでよく見られます。 詳細については、「[CREATE INDEX](../t-sql/statements/create-index-transact-sql.md#sequential-keys)」を参照してください。 |
| クエリの実行または結果 | 指定したクエリによってその実行が完了したときを指す "*完了時刻*" を、追跡するメッセージに追加しました。 |
| クエリの実行または結果 | より多くのデータを表示し (結果をテキストで表示)、セルに格納することを許可します (結果をグリッドに表示)。 SSMS では、どちらも最大 200 万文字まで許可されるようになりました (それぞれ 256 および 64,000 から増加)。 これにより、ユーザーがグリッドのセルから 43,680 文字を超えて取得できないという問題にも対処しました。 |
| プラン表示 | [インライン スカラー UDF 機能](../relational-databases/performance/intelligent-query-processing.md#scalar-udf-inlining)が有効な場合、QueryPlan に新しい属性を追加しました (ContainsInlineScalarTsqludfs)。 |
| SMO | *SQL Assessment API* のサポートが追加されました。 詳細については、「[SQL Assessment API](https://docs.microsoft.com/sql/sql-assessment-api/sql-assessment-api-overview)」を参照してください。 |
|  |  |

## <a name="bug-fixes-in-182"></a>18.2 でのバグの修正

|  新しい項目  |  詳細  |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ユーザー補助 | F3 キーを押して並べ替えられるように XEvent UI (グリッド) を更新しました。 |
| Always On | 可用性グループ (AG) を削除しようとすると、SSMS からエラーがスローされる問題を修正しました |
| Always On | 読み取りスケール AG (クラスターの種類 = NONE) を使用しているときにレプリカを Synchronous と構成すると、SSMS で不適切なフェールオーバー ウィザードが表示されていた問題を修正しました。 SSMS では、Force_Failover_Allow_Data_Loss オプションのウィザードが表示されるようになりました。これは、クラスターの種類 NONE Availability に対して許可されている唯一のオプションです。 |
| Always On | ウィザードで、許可される同期数が 3 に制限されていた問題を修正しました |
| データ分類 | CompatLevel が 150 未満のデータベース上でデータ分類レポートを表示しようとすると、SSMS から "*インデックス (ゼロベース) は 0 以上でなければなりません*" のエラーがスローされる問題を修正しました。 |
| SSMS 全般 | ユーザーがマウス ホイールを使って結果ウィンドウを水平方向にスクロールできなかった問題を修正しました。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/34145641)」を参照してください。 |
| SSMS 全般 | 無害な待機の種類 SQLTRACE_WAIT_ENTRIES を無視するように "*利用状況モニター*" を更新しました |
| SSMS 全般 | 一部の色オプション *([テキスト エディター] > [エディターのタブとステータス バー])* が保存されない問題を修正しました。 「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/37924165)」を参照してください
| SSMS 全般 | 接続ダイアログで、 *[Azure Active Directory - Universal with MFA のサポート]* を *[Azure Active Directory - Universal with MFA]* に置き換えました (機能は同じですが、混乱を軽減するため)。 |
| SSMS 全般 | Azure SQL Database を作成するときに正しい既定値を使用するように SSMS を更新しました。 |
| SSMS 全般 | サーバーが [SQL Linux コンテナー](../linux/quickstart-install-connect-docker.md)の場合に [[サーバーの登録]](register-servers/register-servers.md) のノードからユーザーが "*PowerShell を起動*" できなかった問題を修正しました。 |
| フラット ファイルのインポート | SSMS 18.0 から 18.1 にアップグレードした後に *[フラット ファイルのインポート]* が機能しなかった問題を修正しました。 「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/37912636)」を参照してください |
| フラット ファイルのインポート | Unicode 文字のヘッダーを持つ .csv ファイルの場合に "*フラット ファイルのインポート ウィザードで重複または無効な列*" が報告されていた問題を修正しました。 |
| オブジェクト エクスプローラー | SQL Express に接続したときに一部のメニュー項目 (たとえば、SQL サーバーの "*インポートおよびエクスポート ウィザード*") が見つからないか無効になる問題を修正しました。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/37500016)」を参照してください。 |
| オブジェクト エクスプローラー | オブジェクトをオブジェクト エクスプローラーからエディターにドラッグすると、SSMS がクラッシュする問題を修正しました。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/37887988)」を参照してください。 |
| オブジェクト エクスプローラー | データベースの名前を変更すると、正しくないデータベース名がオブジェクト エクスプローラーに表示される問題を修正しました。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/37638472)」を参照してください。 |
| オブジェクト エクスプローラー | Windows でサポートされなくなった照合順序を使用するように設定されているデータベースに対して、オブジェクト エクスプローラーで *Tables* ノードを展開しようとするとエラーがトリガーされる (また、ユーザーは自分のテーブルを展開できない) という長い間未解決だった問題を修正しました。 そのような照合順序の例は、Korean_Wansung_Unicode_CI_AS です。 |
| [サーバーの登録](register-servers/register-servers.md) | [登録済みサーバー] で *[Active Directory - 統合]* または *[Azure Active Directory - Universal with MFA]* のいずれかが使用されている場合に、複数のサーバーに対して ([登録済みサーバー] の *[グループ]* ) クエリを発行しようとしても、SSMS 接続の失敗のために機能しない問題を修正しました。 |
| [サーバーの登録](register-servers/register-servers.md) | 登録済みサーバーで *[Active Directory - パスワード]* または *[SQL Auth]\(SQL 認証\)* のいずれかが使用され、ユーザーがパスワードを記憶しないことを選択している場合に、複数のサーバーに対して ([登録済みサーバー] の *[グループ]* で) クエリを発行しようとしても、SSMS がクラッシュする問題を修正しました。 |
| [レポート] | データ ファイルのエクステント数が膨大な場合にレポートが失敗する "*ディスク使用量*" レポートの問題を修正しました。 |
| レプリケーション ツール | レプリケーション モニターが AG のパブリッシャー DB および AG のディストリビューターで機能しない問題を修正しました (これは以前に SSMS 17.x で修正済み) |
| SQL エージェント | ジョブ ステップの追加、挿入、編集、または削除時に、アクティブな行ではなく最初の行でフォーカスがリセットされる問題を修正しました。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/38070892)」を参照してください。 |
| SMO/スクリプト作成 | *CREATE OR ALTER* で拡張プロパティを持つオブジェクトがスクリプト化されない問題を修正しました。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035-sql-server/suggestions/37236748)」を参照してください。 |
| SMO/スクリプト作成 | SSMS が CREATE EXTERNAL LIBRARY を正しくスクリプト化できない問題を修正しました。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/37868089)」を参照してください。 |
| SMO/スクリプト作成 | 数千のテーブルを持つデータベースに対して "*スクリプトの生成*" を実行しようとしたときの問題 (進行状況ダイアログが停止しているように見える) を修正しました。 |
| SMO/スクリプト作成 | SQL 2019 で "*外部テーブル*" のスクリプトが機能しない問題を修正しました。 |
| SMO/スクリプト作成 | SQL 2019 で "*外部データ ソース*" のスクリプトが機能しない問題を修正しました。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/34295080)」を参照してください。 |
| SMO/スクリプト作成 | Azure SQL DB をターゲットにしているときに列の "*拡張プロパティ*" がスクリプト化されない問題を修正しました。 詳細については「[stackoverflow](https://stackoverflow.com/questions/56952337/how-can-i-script-the-descriptions-of-columns-in-ms-sql-server-management-studio)」を参照してください。 |
| SMO/スクリプト作成 | 最後のページ挿入:SMO - Add property *Index.IsOptimizedForSequentialKey* |
|**SSMS セットアップ**| **SSMS のセットアップで、言語の不一致を報告する SSMS のインストールが誤ってブロックされていた問題を軽減しました。これは、セットアップの中止や SSMS の以前のバージョンの誤ったアンインストールなど、一部の異常な状況で問題になる可能性がありました。詳細については、「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/37483594/)」を参照してください。** |
| XEvent プロファイラー | ビューアーが閉じられるときのクラッシュを修正しました。 |

### <a name="known-issues-182"></a>既知の問題 (18.2)

- マシン A 上で実行されている SSMS から作成されたデータベース ダイアグラムは、マシン B からは変更できません (SSMS がクラッシュします)。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/37992649)」を参照してください。

- 複数のクエリ ウィンドウを切り替えると再描画の問題が発生します。 「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/37474042)」を参照してください この問題を回避するには、 **[ツール]**  >  **[オプション]** でハードウェア アクセラレータを無効にします。

- SSMS のグリッド、テキスト、またはファイルの結果のデータ サイズに制限があります。

- オブジェクト エクスプローラーで Azure SQL Database を削除した場合、実際には成功しているにもかかわらず、エラーが表示される問題があります。

- 実際のログイン用の既定の言語設定にかかわらず、[ログインのプロパティ] ダイアログにアラビア語が SQL ログインの既定の言語として表示される場合があります。 このログインの実際の既定の言語を表示するには、T-SQL を使用して **master.sys.server_principles** からログインの **default_language_name** を選択します。

## <a name="downloadssdtmediadownloadpng-ssms-181httpsgomicrosoftcomfwlinklinkid2094583"></a>[SSMS 18.1](https://go.microsoft.com/fwlink/?linkid=2094583) ![のダウンロード](../ssdt/media/download.png)

- リリース番号:18.1  
- ビルド番号:15.0.18131.0  
- リリース日:2019 年 6 月 11 日  

[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x40a)

18.1 は 18.0 に対する小規模な更新であり、次の新しい項目とバグ修正が含まれています。

## <a name="whats-new-in-181"></a>18.1 の新機能

| [新しい項目]| 詳細|
| :-------| :------|
| データベース ダイアグラム | [データベース ダイアグラムが SSMS に戻りました](https://feedback.azure.com/forums/908035/suggestions/37507828)。
| SSBDIAGNOSE.EXE |SQL Server Diagnose (コマンドライン ツール) が SSMS パッケージに戻りました。|
| Integration Services (SSIS) | Azure で、Azure またはファイル システムの SSIS カタログにある SSIS パッケージのスケジュールがサポートされます。 [新しいスケジュール] ダイアログを起動するためのエントリが 3 つあります。Azure の SSIS カタログにある SSIS パッケージを右クリックしたときに表示される *[新しいスケジュール]* メニュー項目、 *[ツール]* メニュー項目の *[Azure への移行]* メニュー項目にある *[Azure での SSIS パッケージのスケジュール設定]* メニュー項目、Azure SQL Database マネージド インスタンスの SQL Server エージェントの下で [ジョブ] フォルダーを右クリックしたときに表示される [Azure での SSIS のスケジュール設定] です。|

## <a name="bug-fixes-in-181"></a>18.1 でのバグの修正

| 新しい項目 | 詳細 |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ユーザー補助 | エージェント ジョブ UI のユーザー補助が改善されました。 |
| ユーザー補助 | [Stretch Monitor]\(ストレッチ モニター\) ページに *[自動更新]* ボタンのアクセス可能な名前が追加され、どのボタンがオンの状態であるかだけでなく、そのボタンを押すことによる影響がユーザーにわかるインテリジェントなアクセス可能な名前も追加され、ユーザー補助が改善されました。 |
| ADS 統合| ADS 登録サーバーの使用にあたり発生する恐れのある SSMS のクラッシュを修正しました。|
| データベース デザイナー | Latin1_General_100_BIN2_UTF8 照合順序に対するサポートが追加されました (SQL Server 2019 CTP3.0 で使用できます)。 |
| データ分類 | 履歴テーブルの列への機密ラベルの追加はサポートされていないため、これが阻止されます。 |
| データ分類 | 互換性レベル (サーバーとデータベース) の不適切な処理に関する問題に対処しました。 |
| データベース デザイナー | Latin1_General_100_BIN2_UTF8 照合順序に対するサポートが追加されました (SQL 2019 CTP3.0 で使用できます)。 |
| SSMS 全般 | インデックス内の疑似列のスクリプト作成が正しく行われない問題を修正しました。 |
| SSMS 全般 | *[資格情報の追加]* ボタンをクリックすると null 参照の例外がスローされることがあるという、[ログインのプロパティ] ページの問題を修正しました。 |
| SSMS 全般 | [インデックスのプロパティ] ページの money 列サイズ表示を修正しました。 |
| SSMS 全般 | [SQL エディター] ウィンドウの *[ツール] メニューの [オプション]* の [Intellisense] 設定が SSMS で適用されない問題を修正しました。 |
| SSMS 全般 | [ヘルプ] 設定 (オンラインとオフライン) が SSMS で適用されない問題を修正しました。 |
| 高 DPI | サポート対象外のクエリ オプションに関するエラー ダイアログ内のコントロールのレイアウトを修正しました。 |
| 高 DPI | SSMS のローカライズ版の一部にある、 *[新しい可用性グループ]* ページ内のコントロールのレイアウトを修正しました。 |
| 高 DPI | *[新しいジョブ スケジュール]* ページのレイアウトを修正しました。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/37632094)」を参照してください。 |
| フラット ファイルのインポート | インポート中に通知なく行が失われる場合がある問題を修正しました。|
| Intellisense/エディター | IntelliSense の Azure SQL データベースに対する SMO ベースのクエリ トラフィックを減らしました。 |
| Intellisense/エディター | ユーザー作成のために T-SQL を入力しているときに表示されるヒントの文法エラーを修正しました。 また、ユーザーとログインの間を明確に区別するためのエラー メッセージを修正しました。 |
| ログ ビューアー | オブジェクト エクスプローラーで古いアーカイブ サインインをダブルクリックしたときであっても、SSMS で常に現在のサーバー (またはエージェント) のログが開かれる問題を修正しました。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/37633648)」を参照してください。 |
| SSMS セットアップ | セットアップ ログのパスにスペースが含まれている場合 SSMS セットアップが失敗する原因となっていた問題を修正しました。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/37496110)」を参照してください。 |
| SSMS セットアップ | スプラッシュ スクリーンの表示後すぐに SSMS が終了する問題を修正しました。 </br> 詳細については、次のサイトを参照してください。[UserVoice](https://feedback.azure.com/forums/908035/suggestions/37502512)、「[SSMS Refuses to Start](https://dba.stackexchange.com/questions/238609/ssms-refuses-to-start)」 (SSMS が開始を拒否する)、「[Database Administrators](https://dba.stackexchange.com/questions/237086/sql-server-management-studio-18-wont-open-only-splash-screen-pops-up)」 (データベース管理者) のページ。 |
| オブジェクト エクスプローラー | Linux 上で SQL に接続したときに *[PowerShell の起動]* を有効にするための制限を解除しました。 |
| オブジェクト エクスプローラー | Polybase/スケールアウト グループ ノード (計算ノードに接続されている場合) を展開しようとしたときに SSMS がクラッシュする原因となっていた問題を修正しました。 |
| オブジェクト エクスプローラー | 指定のインデックスを無効にした後であっても、 *[無効]* メニュー項目が依然として有効な状態である問題を修正しました。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/37735375)」を参照してください。 |
| [レポート] | レポートで GrantedQueryMemory を KB 単位で表示するように修正しました (SQL パフォーマンス ダッシュボード レポート)。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/37167289)」を参照してください。 |
| [レポート] | Always-On シナリオでのログ ブロックのトレースが改善されました。 |
| プラン表示 | 新しいプラン表示要素 *SpillOccurred* をプラン表示スキーマに追加しました。 |
| プラン表示 | リモートの読み取り (*ActualPageServerReads*、*ActualPageServerReadAheads*、*ActualLobPageServerReads*、*ActualLobPageServerReadAheads*) をプラン表示スキーマに追加しました。 |
| SMO/スクリプト作成 | グラフではないテーブルのスクリプト作成中のエッジ制約のクエリを回避します。 |
| SMO/スクリプト作成 | *データ分類*を使用した列のスクリプト作成時の機密分類に関する制約を削除しました。 |
| SMO/スクリプト作成 | データ生成時にグラフ テーブルでの "スクリプトの生成" が失敗する問題を修正しました。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898466)」を参照してください。 |
| SMO/スクリプト作成 | EnumObjects() メソッドでシノニムのスキーマ名が取り込まれない問題を修正しました。 |
| SMO/スクリプト作成 | UIConnectionInfo.LoadFromStream() で (パスワードが指定されていない場合に) *AdvancedOptions* セクションが読み込まれない問題を修正しました。 |
| SQL エージェント | [ジョブのプロパティ] ウィンドウでの作業中に SSMS がクラッシュする問題を修正しました。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/37164244)」を参照してください。 |
| SQL エージェント | *[ジョブ ステップのプロパティ]* 上の [表示] ボタンが常に有効ではないため、指定のジョブ ステップの出力を表示できなかった問題を修正しました。 |
| XEvent の UI | 同じ名前のイベントと明確に区別するために、[パッケージ] 列を XEvent のリストに追加しました。 |
| XEvent の UI | これまでなかった "EXTERNAL LIBRARY" クラス型マッピングを XEvent の UI に追加しました。 |

### <a name="known-issues-181"></a>既知の問題 (18.1)

- オブジェクト エクスプローラーからクエリ エディターにテーブル オブジェクトをドラッグすると、エラーが表示される場合があります。 Microsoft ではこの問題を認識しており、次のリリースで修正される予定です。

- [オプション]、[テキスト エディター]、[エディターのタブとステータス バー]、[ステータス バーのレイアウトと色] にある、 *[グループ接続]* と *[単一のサーバー接続]* の色オプションが、SSMS 18.1 を閉じた後に保持されません。 SSMS を再度開くと、[ステータス バーのレイアウトと色] のオプションは既定 (白) に戻ります。

- SSMS の結果から表示されるデータのサイズには、グリッド、テキスト、またはファイルに制限があります。

- マシン A 上で実行されている SSMS から作成されたデータベース ダイアグラムは、マシン B からは変更できません (SSMS がクラッシュします)。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/37992649)」を参照してください。

## <a name="downloadssdtmediadownloadpng-ssms-180httpsgomicrosoftcomfwlinklinkid2088649"></a>![ダウンロード](../ssdt/media/download.png) [SSMS 18.0](https://go.microsoft.com/fwlink/?linkid=2088649)

- リリース番号:18.0  
- ビルド番号:15.0.18118.0  
- リリース日:2019 年 4 月 24 日

[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x804)| [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x404)| [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x409)| [フランス語](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x40c)| [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x407)| [イタリア語](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x410)| [日本語](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x411)| [韓国語](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x412)| [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x416)| [ロシア語](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x419)| [スペイン語](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x40a)

### <a name="whats-new-in-180"></a>18.0 の新機能

| [新しい項目]| 詳細|
| :-------| :------|
|SQL Server 2019 のサポート|SSMS 18.0 は、SQL Server 2019 (compatLevel 150). を完全に*認識*する最初のリリースです。|
|SQL Server 2019 のサポート|SQL Server 2019 および SQL マネージド インスタンスでの "BATCH_STARTED_GROUP" と "BATCH_COMPLETED_GROUP" のサポート。|
|SQL Server 2019 のサポート|SMO:UDF のインライン化のサポートが追加されました。|
|SQL Server 2019 のサポート|GraphDB:Graph TC Sequence のプラン表示にフラグが追加されます。|
|SQL Server 2019 のサポート|Always Encrypted: AEv2 / エンクレーブのサポートが追加されました。|
|SQL Server 2019 のサポート|Always Encrypted: ユーザーがエンクレーブのサポートを有効にする/構成する [オプション] ボタンをクリックすると、新しいタブの [Always Encrypted] が表示されます。|
|SSMS のダウンロード サイズの縮小| 現在のサイズは 500 MB 以下で、SSMS 17.x バンドルの約半分です。
|SSMS は Visual Studio 2017 Isolated Shell に基づきます|新しいシェル (SSMS は Visual Studio 2017 15.9.11 に基づく) で、SSMS と Visual Studio の両方に行われたアクセシビリティに関するすべての修正のロックが解除され、最新のセキュリティ修正プログラムが含まれます。|
|SSMS アクセシビリティの機能強化| すべてのツール (SSMS、DTA、Profiler) のアクセシビリティの問題を解決するためにさまざまな作業が行われました|
|SSMS をカスタム フォルダーにインストールできるようになりました| このオプションは、コマンドライン (無人インストールに便利です) と、セットアップ UI の両方から利用できます。 コマンド ラインから、この追加の引数を SSMS-Setup-ENU.exe に渡します。 SSMSInstallRoot=C:\MySSMS18  既定では、SSMS の新しいインストール場所は %ProgramFiles(x86)%\Microsoft SQL Server Management Studio 18\Common7\IDE\ssms.exe です。  これは、SSMS がマルチインスタンスであるという意味ではありません。|
|SSMS を OS の言語以外の言語でインストールできます|言語が混在するセットアップに関するブロックが解除されました。 たとえば、フランス語の Windows にドイツ語の SSMS をインストールすることができます。 OS の言語が SSMS の言語と異なる場合、ユーザーは **[ツール]**  >  **[オプション]**  >  **[国際対応の設定]** の下で言語を変更する必要があります。変更しないと、SSMS の UI が英語で表示されます。|
|SSMS と SQL エンジンでコンポーネントは共有されなくなりました|SQL エンジンとコンポーネントを共有しないようにさまざまな作業が行われました。このような共有によって、保守性の問題 (他のコンポーネントによってインストールされたファイルが上書きされる) がたびたび発生していました。|
|SSMS には NetFx 4.7.2 以降が必要です|最小要件を NetFx4.6.1 から NetFx4.7.2 にアップグレードしました。その結果、新しいフレームワークで公開されている新しい機能を利用できるようになりました。|
|SSMS 設定の移行機能| SSMS 18 を最初に起動したときに、17.x 設定を移行するように求めるメッセージがユーザーに表示されます。 ユーザーの設定ファイルはプレーン XML ファイルとして格納されるようになりました。そのため移植性が向上し、編集も場合によって可能となります。|
|高 DPI のサポート| 高 DPI は既定で有効となりました。|
|SSMS には Microsoft OLE DB ドライバーが付属しています| 詳細については、「[Microsoft OLE DB Driver for SQL Server のダウンロード](https://docs.microsoft.com/sql/connect/oledb/download-oledb-driver-for-sql-server)」を参照してください。|
|SSMS は Windows 8 ではサポートされていません。 Windows 10 と Windows Server 2016 にはバージョン 1607 (10.0.14393) 以降が必要になりました|NetFx 4.7.2 への新しい依存関係があるので、SSMS 18.0 は、Windows 8、Windows 10 の旧バージョン、および Windows Server 2016 にはインストールされません。 SSMS の設定では、これらのシステムはブロックされます。 Windows 8.1 はまだサポートされています。|
|SSMS は PATH 環境変数に追加されなくなりました|SSMS.EXE (および一般的なツール) のパスは、パスに追加されなくなりました。 ユーザーは手動で追加するか、最新の Windows コンピューターの場合は [スタート] メニューを使用することができます。|
|SSMS 拡張機能を開発するためのパッケージ ID が不要になりました| これまで、SSMS では既知のパッケージのみが選択されて読み込まれていたので、開発者は自分のパッケージを登録する必要がありました。 この点は変更されました。|
|SSMS 全般|SSMS の Filegroups に関する AUTOGROW_ALL_FILES 構成オプションを公開しています。|
|SSMS 全般|SSMS GUI から、危険な 'lightweight pooling' と 'priority boost' オプションを削除しました。 詳細については、「[Priority boost details – and why it’s not recommended](https://blogs.msdn.microsoft.com/arvindsh/2010/01/26/priority-boost-details-and-why-its-not-recommended/)」 (priority boost の詳細 - 推奨されない理由) を参照してください。
|SSMS 全般|ファイルを作成するための新しいメニューとキー バインド:**CTRL+ALT+N**。 **CTRL + N** でも引き続き新しいクエリを作成できます。|
|SSMS 全般|**[新しいファイアウォール規則]** ダイアログで、自動的に生成される規則名ではなく、ユーザーが規則名を指定できるようになりました。|
|SSMS 全般|特に v140+ T-SQL に合わせてエディターの IntelliSense が改善されました。|
|SSMS 全般|SSMS UI の照合順序ダイアログに UTF-8 のサポートが追加されました。|
|SSMS 全般|接続ダイアログの MRU パスワードの場合に [Windows Credential Manager] に切り替わりました。 これで、パスワードの持続性が信頼できない場合があった長時間保留の問題が解決されます。|
|SSMS 全般|目的のモニター上にダイアログとウィンドウのポップアップがより多く表示されるように、マルチモニター システムのサポートが改善されました。|
|SSMS 全般|[サーバーのプロパティ] ダイアログの新しい [データベースの設定] ページで、'バックアップ チェックサムの既定値' サーバー構成を公開しました。 詳細については、[https://feedback.azure.com/forums/08035-sql-server/suggestions/34634974](https://feedback.azure.com/forums/08035-sql-server/suggestions/34634974) を参照してください。|
|SSMS 全般|[SQL Server エラー ログの構成] の下に "エラー ログ ファイルの最大サイズ" を公開しました。 詳細については、[https://feedback.azure.com/forums/908035/suggestions/33624115](https://feedback.azure.com/forums/908035/suggestions/33624115)を参照してください。|
|SSMS 全般|[ツール] メニューに [Azure への移行] が追加されました。Data Migration Assistant と Azure Database Migration Service を統合することで、すばやく簡単にアクセスして Azure により迅速に移行できるようにしました。|
|SSMS 全般|"接続の変更" が使用されている場合に、ユーザーに開いているトランザクションをコミットするよう求めるロジックが追加されました。|
|Azure Data Studio との統合|Azure Data Studio を起動またはダウンロードするためのメニュー項目が追加されました。|
|Azure Data Studio との統合|オブジェクト エクスプローラーに [Azure Data Studio の起動] メニュー項目が追加されました。|
|Azure Data Studio との統合|OE でデータベース ノードを右クリックすると、Azure Data Studio でクエリを実行するか新しいノートブックを作成するためのコンテキスト メニューがユーザーに表示されます。|
|Azure SQL サポート| SLO/Edition/MaxSize データベース プロパティにカスタム名を使用できるようになり、今後の Azure SQL データベースのエディションのサポートが簡単になりました。|
|Azure SQL サポート| 最近追加された仮想コア SKU (General Purpose および Business Critical) のサポートの追加:Gen4_24 およびすべての Gen5|
|Azure SQL マネージド インスタンス|SMO と SSMS で、Azure SQL マネージド インスタンスに接続した場合の新しいログインの種類として、新しい "AAD ログイン" が追加されました。|
|Always On|SSMS の Always on ダッシュボードで RTO (推定復旧時間) と RPO (推定データ損失) を再ハッシュします。 [https://docs.microsoft.com/sql/database-engine/availability-groups/windows/monitor-performance-for-always-on-availability-groups](../database-engine/availability-groups/windows/monitor-performance-for-always-on-availability-groups.md) の更新されたドキュメントを参照してください。|
|Always Encrypted| [サーバーに接続] ダイアログの新しい [Always Encrypted] タブにある [Always Encrypted を有効にする] チェックボックスで、データベース接続での Always Encrypted の有効化/無効化を簡単に切り替えられるようになりました。|
|セキュア エンクレーブを使用する Always Encrypted| SQL Server 2019 では、セキュリティで保護されたエンクレーブが設定された Always Encrypted をサポートするためにいくつかの機能強化が加えられました。[サーバーに接続] ダイアログ (新しい [Always Encrypted] タブ) にエンクレーブの構成証明の URL を指定するテキスト フィールド。  [新しい列マスター キー] ダイアログに、新しい列マスターキーでエンクレーブ計算を許可するかどうかを制御する新しいチェックボックスが追加されました。  他の Always Encrypted キー管理ダイアログに、エンクレーブ計算を許可する列マスター キーの情報が表示されるようになりました。|
|監査ファイル|認証方法をストレージ アカウント キー ベースから Azure AD ベースの認証に変更しました。|
|データ分類| データ分類タスク メニューを再構成しました。データベース タスク メニューにサブメニューが追加され、最初に分類データ ウィンドウを開かなくても、メニューからレポートを開くためのオプションが追加されました。|
|データ分類|SMO に新機能 'データ分類' が追加されました。 Column オブジェクトで新たに公開されたプロパティ:SensitivityLabelName、SensitivityLabelId、SensitivityInformationTypeName、SensitivityInformationTypeId、IsClassified (読み取り専用)。 詳細については、「[ADD SENSITIVITY CLASSIFICATION (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/add-sensitivity-classification-transact-sql)」を参照してください。|
|データ分類|[データ分類] ポップアップに新しい [Classification Report]\(分類レポート\) メニュー項目が追加されました。|
|データ分類| 推奨事項が更新されました。|
|データベース互換性レベルのアップグレード|***[データベース名]*** > ***[タスク]*** > ***[データベースのアップグレード]*** に新しいオプションを追加しました。 これにより、ユーザーに次のプロセスをガイドする、新しい**クエリ調整アシスタント (QTA)** が開始されます。データベースの互換性レベルをアップグレードする前にパフォーマンスのベースラインを収集する。 目的のデータベース互換性レベルにアップグレードする。  同じワークロードを介してパフォーマンス データの 2 番目の受け渡しを収集する。 ワークロードの低下を検出し、ワークロードのパフォーマンスを改善するためのテスト済みのレコメンデーションを提供する。  これは、「[クエリ ストアの使用シナリオ](https://docs.microsoft.com/sql/relational-databases/performance/query-store-usage-scenarios#CEUpgrade)」に記載されているデータベースのアップグレード プロセスに似ていますが、最後の手順 (QTA はレコメンデーションを生成するために以前の正常起動時の状態に依存しない) が異なります。|
|データ層アプリケーションのウィザード|グラフ テーブルを使用したデータ層アプリケーションのインポート/エクスポートのサポートが追加されました。|
|フラット ファイルのインポート ウィザード|インポートで列の名前が変更された可能性があることをユーザーに通知するロジックが追加されました。|
|Integration Services (SSIS)|顧客が Azure Government クラウド内にある Azure-SSIS IR で SSIS パッケージをスケジュールできるようにするためのサポートが追加されました。|
|Integration Services (SSIS)|Azure SQL マネージド インスタンスの SQL エージェントを SSMS を介して使用するときに、SSIS エージェント ジョブ ステップでパラメーターと接続マネージャーを構成できます。|
|Integration Services (SSIS)|Azure SQL DB/マネージド インスタンスに接続するときに、*既定*を初期データベースとして使用して接続できます。|
|Integration Services (SSIS)|[Integration Services カタログ] の下に新しい項目 **[Try SSIS in Azure Data Factory]\(Azure Data Factory で SSIS を試す\)** が追加されました。これは、統合ランタイムの作成ウィザードを起動して Azure-SSIS Integration Runtime をすばやく作成するのに使用できます。
|Integration Services (SSIS)|カタログ作成ウィザードに **[Create SSIS IR]\(SSIS IR の作成\)** ボタンが追加されました。これは、統合ランタイムの作成ウィザードを起動して Azure-SSIS Integration Runtime をすばやく作成するのに使用できます。|
|Integration Services (SSIS)|ISDeploymentWizard で、SQL 認証、Azure Active Directory 統合認証、および Azure Active Directory パスワード認証がコマンド ライン モードでサポートされるようになりました。|
|Integration Services (SSIS)|配置ウィザードで、Azure Data Factory SSIS Integration Runtime の作成とこれに対する配置がサポートされるようになりました。|
|オブジェクト スクリプト作成|オブジェクト スクリプト作成時に、"CREATE OR ALTER" の新しいメニュー項目が追加されます。|
|クエリ ストア|グラフの Y 軸に表示される数字に桁区切り記号を追加することで、一部のレポート (全体的なリソースの消費) の使いやすさを改善しました。|
|クエリ ストア|新しいクエリ待機統計レポートが追加されました。|
|クエリ ストア|[Tracked Query]\(追跡対象クエリ\) ビューに [実行回数] メトリックが追加されました。|
|レプリケーション ツール|レプリケーション モニターと SSMS に既定以外のポート指定機能のサポートが追加されました。|
|プラン表示|使用できる場合、ShowPlan 演算子ノードに実際の経過時間、実際の行と推定の行が追加されました。 これにより、実際のプランが、ライブ クエリの統計プランと一貫した外観になります。|
|プラン表示|クエリが 4,000 文字を超える場合に、SQL エンジンによって ShowPlan が切り捨てられる可能性があることをユーザーに示すために、ShowPlan の [クエリの編集] ボタンをクリックしたときのツールヒントが変更され、コメントが追加されました。|
|プラン表示|"Materializer Operator (External Select)" を表示するロジックを追加しました。|
|プラン表示|"行ストアに対するバッチモード スキャン" 機能を使用しているクエリを簡単に識別できるように、新しい showplan 属性 BatchModeOnRowStoreUsed を追加します。 クエリが行ストアでバッチモード スキャンを実行するたびに、新しい属性 (BatchModeOnRowStoreUsed="true") が StmtSimple 要素に追加されます。|
|プラン表示|DW ROLLUP および CUBE の LocalCube RelOp にプラン表示のサポートが追加されました。|
|プラン表示|Azure SQL Data Warehouse の新しい ROLLUP および CUBE 集計の機能用の、新しい LocalCube 演算子。|
|SMO| 再開可能なインデックス作成の SMO サポートを拡張します。|
|SMO| アプリケーション作成者が SMO のパフォーマンスの問題を早期に検出できるように、SMO オブジェクト ("PropertyMissing") に対する新しいイベントを追加しました。|
|SMO| "バックアップ チェックサムの既定" サーバー構成にマップされる、Configuration オブジェクトに対する新しい DefaultBackupChecksum プロパティを公開しました。|
|SMO| 使用中の SQL のバージョンのサービス レベル (CU12、RTM など) にマップする、新しい ProductUpdateLevel プロパティをサーバー オブジェクト上に公開しました。|
|SMO| "lastgoodcheckdbtime" データベース プロパティにマップする、新しい LastGoodCheckDbTime プロパティをデータベース オブジェクト上に公開しました。 これらのプロパティが使用できない場合、既定値の 1/1/1900 12:00:00 AM が返されます。|
|SMO|RegSrvr.xml ファイル (登録済みサーバーの構成ファイル) の場所を "%AppData%\Microsoft\SQL Server Management Studio" に移動しました (バージョン管理されないため、SSMS のバージョン間で共有できます)。|
|SMO|新しいクォーラムの種類および新しいリソースの種類として "クラウド監視" が追加されました。|
|SMO|SMO と SSMS の両方で "エッジ制約" のサポートが追加されました。|
|SMO|SMO と SSMS の両方に "エッジ制約" の連鎖削除のサポートを追加しました。|
|SMO|データ分類の "読み書き" のアクセス許可のサポートを追加しました。|
|脆弱性評価| Azure SQL DW で脆弱性評価タスク メニューが有効化されました。|
|脆弱性評価|脆弱性評価スキャンの結果が Azure SQL DB での結果と一致するように、Azure SQL マネージド インスタンス サーバーで実行される一連の脆弱性評価規則を変更しました。|
|脆弱性評価| "脆弱性評価" で Azure SQL DW がサポートされるようになりました。|
|脆弱性評価|脆弱性評価スキャンの結果を Excel にエクスポートする、新しいエクスポート機能が追加されました。|
|XEvent ビューアー|XEvent ビューアー: より多くの XEvent のプラン表示のウィンドウが有効化されました。|

### <a name="bug-fixes-in-180"></a>18.0 でのバグの修正

| [新しい項目]| 詳細|
| :-------| :------|
|クラッシュとフリーズ|GDI オブジェクトに関連する一般的な SSMS クラッシュの原因を修正しました。|
|クラッシュとフリーズ|[Script as Create/Update/Drop]\(作成/更新/ドロップとしてスクリプト化\) を選択したときの停止とパフォーマンス低下の一般的な原因を修正しました (SMO オブジェクトの不要なフェッチを削除しました)。|
|クラッシュとフリーズ|ADAL トレースが有効なときに MFA を使用して Azure SQL DB に接続するとハングする問題を修正しました。|
|クラッシュとフリーズ|アクティビティ モニターから呼び出されたときにライブ クエリの統計情報のハングを修正しました ([セキュリティ情報を保持する] を設定せずに SQL Server 認証を使用するときにマニフェストに含まれる問題)。|
|クラッシュとフリーズ|オブジェクト エクスプローラーで [レポート] を選択したときのハングを修正しました。この問題で、長い接続の待機時またはリソースの一時的にアクセス不能に関するマニフェストが含まれる可能性があります。|
|クラッシュとフリーズ|中央管理サーバーと Azure SQL サーバーの使用にあたり発生する SSSM のクラッシュを修正しました。 詳細については、「[SMSS 17.5 application error and crash when using Central Management Server](https://feedback.azure.com/forums/908035/suggestions/33374884)」 (中央管理サーバーを使用するときの SMSS 17.5 アプリケーションのエラーとクラッシュ) を参照してください。|
|クラッシュとフリーズ|IsFullTextEnabled プロパティを取得する方法を最適化することによって、オブジェクト エクスプローラーでのハングを修正しました。|
|クラッシュとフリーズ|データベース プロパティを取得する不要なクエリの作成を回避することで、"データベース コピー ウィザード" でのハングを修正しました。|
|クラッシュとフリーズ|T-SQL の編集中に SSMS がハングまたはクラッシュする問題を修正しました。|
|クラッシュとフリーズ|大規模な T-SQL スクリプトを編集しているときに SSMS が応答しなくなる問題を軽減しました。|
|クラッシュとフリーズ|SSMS でクエリから返された大きなデータセットを処理しているときにメモリ不足となる原因となっていた問題を修正しました。|
|SSMS 全般|"登録済みサーバー" での接続で "ApplicationIntent" が渡されないという問題を修正しました。|
|SSMS 全般|高 DPI モニターで "新しい XEvent セッション ウィザードの UI" フォームが正しくレンダリングされない問題を修正しました。|
|SSMS 全般|bacpac ファイルをインポートしようとする問題を修正しました。|
|SSMS 全般|データベース (FILEGROWTH > 2048 GB) のプロパティを表示しようとすると、算術オーバーフロー エラーがスローされる問題を修正しました。|
|SSMS 全般|パフォーマンス ダッシュボード レポートに、サブレポートにはない PAGELATCH および PAGEIOLATCH による待機がレポートされる問題を修正しました。|
|SSMS 全般|正しいモニターでダイアログを開くことで SSMS のマルチモニター対応を高度化させるよう、再度修正を行いました。|
|Analysis Services (AS)|AS XEvent UI に対する [詳細設定] がクリップされてしまう問題を修正しました。|
|Analysis Services (AS)|DAX の解析でファイルが見つからないことを示す例外がスローされる問題を修正しました。|
|Azure SQL データベース|Azure SQL Database でマスター データベースではなくユーザー データベースに接続したときに、Azure SQL DB クエリ ウィンドウにデータベース リストが正しく入力されない問題を修正しました。|
|Azure SQL データベース|Azure SQL データベースに "テンポラル テーブル" を追加できない問題を修正しました。|
|Azure SQL データベース|Azure の [統計] メニューの下にある統計プロパティのサブメニュー オプションを有効にしました。これは、もうだいぶ前から完全にサポートされていたためです。|
|Azure SQL - 一般的なサポート|(50 を超える場合に) Azure サブスクリプションを表示できない一般的な Azure UI コントロールの問題を修正しました。 また、サブスクリプション ID ではなく名前による並べ替えに変更されました。 たとえば、URL からバックアップを復元するときに、ユーザーはこれを実行できます。|
|Azure SQL - 一般的なサポート|サブスクリプションを列挙するときに発生する一般的な Azure UI コントロールの問題を修正しました。この問題で "インデックスが範囲を超えています。 負でない値で、コレクションのサイズよりも小さくなければなりません" エラーがユーザーが一部のテナントについてサブスクリプションがない場合に表示されることがあります。 たとえば、URL からバックアップを復元するときに、ユーザーはこれを実行できます。|
|Azure SQL - 一般的なサポート|SSMS による新しい Azure SQL SLO のサポートを困難にしていた、サービス レベルの目標のハードコードの問題を修正しました。 これでユーザーは Azure にサインインし、SSMS では該当するすべての SLO データ (エディションおよび最大サイズ) を取得できるようになりました。|
|Azure SQL DB マネージド インスタンスのサポート|マネージド インスタンスのサポートの改善/調整: UI でサポートされていないオプションが無効になり、URL 監査ターゲットを処理するために [監査ログの表示] オプションが修正されました。|
|Azure SQL DB マネージド インスタンスのサポート|[スクリプトの生成とパブリッシュ] ウィザードでサポートされていない CREATE DATABASE 句のスクリプトが生成されます。|
|Azure SQL DB マネージド インスタンスのサポート|マネージド インスタンスのライブ クエリ統計が有効になりました。|
|Azure SQL DB マネージド インスタンスのサポート|[データベースのプロパティ] -> [ファイル] で ALTER DB ADD FILE が誤ってスクリプトされていました。|
|Azure SQL DB マネージド インスタンスのサポート|他のスケジュールの種類が選択されている場合でも、ONIDLE スケジュールが選択される SQL エージェント スケジューラによる回帰を修正しました。|
|Azure SQL DB マネージド インスタンスのサポート|Azure Storage でバックアップを行う MAXTRANSFERRATE、MAXBLOCKSIZE の調整。|
|Azure SQL DB マネージド インスタンスのサポート|RESTORE 操作の前にテール ログ バックアップがスクリプト化される問題 (これは CL ではサポートされていません)。|
|Azure SQL DB マネージド インスタンスのサポート|[データベースの作成] ウィザードで CREATE DATABASE ステートメントが正しくスクリプト化されない。|
|Azure SQL DB マネージド インスタンスのサポート|マネージド インスタンスに接続しているときの SSMS 内の SSIS パッケージの特殊処理。|
|Azure SQL DB マネージド インスタンスのサポート|マネージド インスタンスに接続するときに "利用状況モニター" を使用しようとしたときにエラーが表示される問題を修正しました。|
|Azure SQL DB マネージド インスタンスのサポート|(SSMS エクスプローラーでの) AAD ログインのサポートの強化。|
|Azure SQL DB マネージド インスタンスのサポート|SMO ファイル グループ オブジェクトのスクリプト作成の改善。|
|Azure SQL DB マネージド インスタンスのサポート|資格情報のための UI が改善されました。|
|Azure SQL DB マネージド インスタンスのサポート|論理レプリケーションのサポートが追加されました。|
|Azure SQL DB マネージド インスタンスのサポート|データベースを右クリックして [データ層アプリケーションのインポート] を選択するとエラーになる問題を修正しました。|
|Azure SQL DB マネージド インスタンスのサポート|"TempDB" を右クリックするとエラーが表示される問題を修正しました。|
|Azure SQL DB マネージド インスタンスのサポート|SMO で ALTER DB ADD FILE ステートメントをスクリプト作成しようとすると、生成された T-SQL スクリプトが空になる問題を修正しました。|
|Azure SQL DB マネージド インスタンスのサポート|マネージド インスタンスのサーバー固有のプロパティ (ハードウェア生成、Service レベル、使用および予約されているストレージ) の表示を改善しました。|
|Azure SQL DB マネージド インスタンスのサポート|データベースのスクリプト作成 ("作成としてスクリプト...") で、追加のファイル グループとファイルがスクリプト作成されない問題を修正しました。 詳細については、[https://feedback.azure.com/forums/908035/suggestions/37326799](https://feedback.azure.com/forums/908035/suggestions/37326799) を参照してください。 |
|DB のバックアップ/復元/アタッチ/デタッチ|.mdf ファイルの物理ファイル名が元のファイル名と一致しない場合に、ユーザーがデータベースをアタッチできない問題を修正しました。|
|DB のバックアップ/復元/アタッチ/デタッチ|SSMS で有効な復元プランを見つけられない問題、または最適ではない復元プランが見つかることがある問題を修正しました。 詳細については、[https://feedback.azure.com/forums/908035-sql-server/suggestions/32897752](https://feedback.azure.com/forums/908035-sql-server/suggestions/32897752) を参照してください。 |
|DB のバックアップ/復元/アタッチ/デタッチ|"データベースのアタッチ" ウィザードで名前が変更されたセカンダリ ファイルが表示されない問題を修正しました。 現在は、ファイルが表示され、そのファイルについてのコメント ("見つかりません" など) が追加されています。 詳細については、[https://feedback.azure.com/forums/908035/suggestions/32897434](https://feedback.azure.com/forums/908035/suggestions/32897434) を参照してください。 |
|データベース コピー ウィザード|スクリプトの生成/転送/データベース コピー ウィザードでインメモリ テーブルを使用してテーブルを作成しようとすると、ansi_padding on が強制されません。|
|データベース コピー ウィザード|SQL Server 2017 および SQL Server 2019 のデータベース転送タスク/データベース コピー ウィザードは壊れています。|
|データベース コピー ウィザード|スクリプトの生成/転送/データベース コピー ウィザードでは、関連付けられている外部データ ソースが作成される前に、テーブルの作成がスクリプト化されます。|
|接続ダイアログ|Del キーを押して、以前のユーザー名リストからユーザー名を削除できるようになりました。 詳細については、「[Allow deletion of users from SSMS login window](https://feedback.azure.com/forums/908035/suggestions/32897632)」 (SSMS ログイン ウィンドウからのユーザーの削除を許可する) を参照してください。|
|DAC インポート ウィザード|AAD を使用して接続すると、DAC インポート ウィザードが動作しない問題を修正しました。|
|データ分類|データ分類ウィンドウで分類を保存するときに、他のデータベースで別のデータ分類ウィンドウが開いている問題が修正されました。|
|データ層アプリケーションのウィザード|サーバーへのアクセス制限のために、ユーザーがデータ層アプリケーション (.dacpac) をインポートできない問題を修正しました (たとえば、同じサーバーにおいてすべてのデータベースへのアクセスがないなど)。|
|データ層アプリケーションのウィザード|多数のデータベースが同じ Azure の SQL server にホストされている場合に、インポートが非常に遅くなる問題を修正しました。|
|外部テーブル|テンプレート、SMO、IntelliSense、プロパティ グリッドに Rejected_Row_Location のサポートが追加されました。|
|フラット ファイルのインポート ウィザード|[フラット ファイルのインポート ウィザード] が二重引用符を正しく処理しない (エスケープしない) 問題を修正しました。 詳細については、[https://feedback.azure.com/forums/908035/suggestions/32897998](https://feedback.azure.com/forums/908035/suggestions/32897998) を参照してください。 |
|フラット ファイルのインポート ウィザード|(浮動小数点の異なる区切り文字を使用するロケールに対する) 浮動小数点型の不適切な処理に関する問題を修正しました。|
|フラット ファイルのインポート ウィザード|値が 0 または 1 のときのビットのインポートに関する問題を修正しました。 詳細については、[https://feedback.azure.com/forums/908035-sql-server/suggestions/32898535](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898535) を参照してください。 |
|フラット ファイルのインポート ウィザード|*float* データ型が *null* として入力された問題を修正しました。|
|フラット ファイルのインポート ウィザード|インポート ウィザードが負の 10 進値を処理できない問題を修正しました。|
|フラット ファイルのインポート ウィザード|ウィザードが 1 列の CSV ファイルからインポートできない問題を修正しました。|
|フラット ファイルのインポート ウィザード|SSMS 17.9 で対応予定] テーブルが既に存在する場合、フラット ファイルのインポートでターゲット テーブルを変更できない問題を修正しました。 詳細については、[https://feedback.azure.com/forums/908035-sql-server/suggestions/32896186](https://feedback.azure.com/forums/908035-sql-server/suggestions/32896186) を参照してください。 |
|ヘルプ ビューアー|オンライン/オフライン モードの準拠に関するロジックを改善しました (対処が必要な問題がまだいくつかある可能性があります)。|
|ヘルプ ビューアー|オンライン/オフライン設定に従うように [ヘルプの表示] を修正しました。 詳細については、[https://feedback.azure.com/forums/908035-sql-server/suggestions/32897791](https://feedback.azure.com/forums/908035-sql-server/suggestions/32897791) を参照してください。 |
|高可用性ディザスター リカバリー (HADR)<BR> 可用性グループ (AG)|"可用性グループのフェールオーバー" ウィザードでロールが常に "解決中" と表示される問題を修正しました。|
|高可用性ディザスター リカバリー (HADR)<BR> 可用性グループ (AG)|"AG ダッシュ ボード" で SSMS が切り捨ての警告を示していた問題を修正しました。|
|Integration Services (IS)|SQL Server 2019 と SSMS 18.0 が同じコンピューターにインストールされている場合、配置ウィザードで SQL Server への接続に失敗する、SxS の問題を修正しました。|
|Integration Services (IS)|メンテナンス プランの作成時に、メンテナンス プランのタスクを編集できない問題を修正しました。|
|Integration Services (IS)|配置中のプロジェクトの名前が変更されると、配置ウィザードが停止する問題を修正しました。|
|Integration Services (IS)|Azure SSIS IR のスケジュール機能での環境設定を有効にしました。|
|Integration Services (IS)|顧客アカウントが複数のテナントに属している場合、SSIS Integration Runtime の作成ウィザードが応答を停止する問題を修正しました。|
|[ジョブの利用状況モニター]|ジョブの利用状況モニター (フィルターあり) の使用中にクラッシュする問題を修正しました。|
|オブジェクト エクスプローラー|OE (誤って構成された DataCollector) の [管理] ノードを展開しようとすると、SSMS から "オブジェクトを DBNull から他のタイプにキャストすることはできません" のような例外がスローされる問題を修正しました。|
|オブジェクト エクスプローラー|[上位 N の編集] を呼び出す前に OE で引用符がエスケープ処理されず、混乱を引き起こしている問題を修正しました|
|オブジェクト エクスプローラー|[データ層アプリケーションのインポート] ウィザードが Azure Storage ツリーから起動できない問題を修正しました。|
|オブジェクト エクスプローラー|SSL チェックボックスの状態が保持されない [データベース メール構成] の問題を修正しました。 詳細については、[https://feedback.azure.com/forums/908035-sql-server/suggestions/32895541](https://feedback.azure.com/forums/908035-sql-server/suggestions/32895541) を参照してください。 |
|オブジェクト エクスプローラー|SSMS で is_auto_update_stats_async_on を使用してデータベースを復元しようとすると、既存の接続を閉じるオプションが淡色表示される問題を修正しました。|
|オブジェクト エクスプローラー|OE でノードを右クリックした場合の問題を修正しました (たとえば、"Tables" を右クリックして、[フィルター] > [フィルターの設定] に移動してテーブルをフィルター処理するなどの操作を実行したい場合、[フィルターの設定] フォームが、SSMS が現在アクティブではない画面に表示される可能性があります)。 詳細については、[https://feedback.azure.com/forums/908035-sql-server/suggestions/34284106](https://feedback.azure.com/forums/908035-sql-server/suggestions/34284106) を参照してください。 |
|オブジェクト エクスプローラー|オブジェクトの名前を変更しようとすると、OE で Del キーが機能しないという、長い間未解決の問題が修正されました。 詳細については、[https://feedback.azure.com/forums/908035-sql-server/suggestions/33073510](https://feedback.azure.com/forums/908035-sql-server/suggestions/33073510)、[https://feedback.azure.com/forums/908035/suggestions/32910247](https://feedback.azure.com/forums/908035/suggestions/32910247)、およびその他の同じような記事を参照してください。|
|オブジェクト エクスプローラー|既存のデータベース ファイルのプロパティを表示すると、新しいデータベースの作成時に表示される [初期サイズ (MB)] ではなく [サイズ (MB)] 列にサイズが表示されます。 詳細については、[https://feedback.azure.com/forums/908035-sql-server/suggestions/32629024](https://feedback.azure.com/forums/908035-sql-server/suggestions/32629024) を参照してください。 |
|オブジェクト エクスプローラー|現在のバージョンの SSMS ではこのようなテーブルをサポートしていないため、[グラフ テーブル] の [デザイン] コンテキスト メニュー項目を無効にしました。|
|オブジェクト エクスプローラー|[新しいジョブ スケジュール] ダイアログが高 DPI モニターで正しくレンダリングされない問題を修正しました。 詳細については、[https://feedback.azure.com/admin/v3/suggestions/35541262](https://feedback.azure.com/admin/v3/suggestions/35541262) を参照してください。 |
|オブジェクト エクスプローラー|オブジェクト エクスプローラーでのデータベース サイズ ([サイズ (MB)]) の表示方法を修正/改善しました。つまり、小数点以下を 2 桁のみにし、桁区切り記号を使用して書式設定しました。 詳細については、[https://feedback.azure.com/forums/908035/suggestions/34379308](https://feedback.azure.com/forums/908035/suggestions/34379308) を参照してください。|
|オブジェクト エクスプローラー|"空間インデックス" の作成が "このアクションを完了するには、プロパティ PartitionScheme を設定してください" のようなエラーで失敗する原因となっていた問題を修正しました。|
|オブジェクト エクスプローラー|オブジェクト エクスプローラーのパフォーマンスを若干改善して、可能な場合には、余分なクエリの発行を回避するようにしました。|
|オブジェクト エクスプローラー|データベースの名前を変更するときに、すべてのスキーマ オブジェクトに対して確認を要求するためのロジックが拡張されました (この設定は構成可能です)。|
|オブジェクト エクスプローラー|オブジェクト エクスプローラーのフィルター処理に適切なエスケープを追加しました。 詳細については、[https://feedback.azure.com/forums/908035/suggestions/36678803](https://feedback.azure.com/forums/908035/suggestions/36678803) を参照してください。 |
|オブジェクト エクスプローラー|[オブジェクト エクスプローラーの詳細] のビューで数字が適切な区切り記号で表示されるよう、修正/改善しました。 詳細については、[https://feedback.azure.com/forums/908035/suggestions/32900944](https://feedback.azure.com/forums/908035/suggestions/32900944) を参照してください。 |
|オブジェクト エクスプローラー|SQL Express に接続しているときの [テーブル] ノードのコンテキスト メニューを修正しました。ここには、[新規] ポップアップが表示されず、[グラフ] テーブルが誤って一覧表示され、[システム バージョン管理] テーブルが表示されていませんでした。 詳細については、[https://feedback.azure.com/forums/908035/suggestions/37245529](https://feedback.azure.com/forums/908035/suggestions/37245529) を参照してください。 |
|オブジェクト スクリプト作成|全体的なパフォーマンスの改善: WideWorldImporters のスクリプト生成にかかる時間が SSMS 17.7 と比べて半分になりました。|
|オブジェクト スクリプト作成|オブジェクトのスクリプト作成時に、既定値がある DB のスコープ設定の構成は省略されています。|
|オブジェクト スクリプト作成|スクリプト作成時に動的 T-SQL を生成しないでください。 詳細については、[https://feedback.azure.com/forums/908035-sql-server/suggestions/32898391](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898391) を参照してください。 |
|オブジェクト スクリプト作成|SQL Server 2016 以前のテーブルをスクリプト化するときに、"エッジとして" および "ノードとして" のグラフ構文を省略します。|
|オブジェクト スクリプト作成|MFA で AAD を使用して Azure SQL DB に接続している場合、データベース オブジェクトのスクリプト作成が失敗する問題を修正しました。|
|オブジェクト スクリプト作成|Azure SQL DB で GEOMETRY_AUTO_GRID/GEOGRAPHY_AUTO_GRID を使用して、空間インデックスのスクリプトを作成しようとするとエラーがスローされていた問題を修正しました。|
|オブジェクト スクリプト作成|"オブジェクト エクスプローラー" のスクリプト設定がソースと一致するように設定されている場合でも、(Azure SQL データベースの) データベース スクリプトが常にオンプレミスの SQL をターゲットとする問題を修正しました。|
|オブジェクト スクリプト作成|不適切な T-SQL ステートメントを生成する、クラスター化されたインデックスおよびクラスター化されていないインデックスを含む SQL DW データベース内にテーブルをスクリプト作成しようとする問題を修正しました。|
|オブジェクト スクリプト作成|不適切な T-SQL ステートメント (重複したステートメント) を生成する、"クラスター化された列ストア インデックス" と "クラスター化されたインデックス" の両方を持つ SQL DW データベース内にテーブルをスクリプト作成しようとする問題を修正しました。|
|オブジェクト スクリプト作成|範囲値なしでのパーティション テーブルのスクリプト作成を修正しました (SQL DW データベース)。|
|オブジェクト スクリプト作成|ユーザーが監査/監査仕様 SERVER_PERMISSION_CHANGE_GROUP をスクリプト作成できなくなる問題を修正しました。|
|オブジェクト スクリプト作成|ユーザーが SQL DW からの統計をスクリプト作成できない問題を修正しました。 詳細については、[https://feedback.azure.com/forums/908035-sql-server/suggestions/32897296](https://feedback.azure.com/forums/908035-sql-server/suggestions/32897296) を参照してください。 |
|オブジェクト スクリプト作成|[エラー発生時にスクリプトを続行] が false に設定されている場合に、スクリプト作成エラーが含まれている誤ったテーブルが "スクリプトの生成ウィザード" に表示される問題を修正しました。|
|オブジェクト スクリプト作成|SQL Server 2019 上のスクリプト生成を改善しました。|
|プロファイラー|Profiler イベントに "Aggregate Table Rewrite Query" イベントが追加されました。|
|クエリ データ ストア|"DocumentFrame (SQLEditors)" 例外がスローされる可能性がある問題が修正されました。|
|クエリ データ ストア|組み込みのクエリ ストア レポートでカスタム時間間隔を設定しようとしたときに、ユーザーが開始/終了間隔で AM や PM を選択できなかった問題が修正されました。|
|結果グリッド|高コントラスト モードの (選択された行番号が表示されない) 問題を修正しました。|
|結果グリッド|グリッドをクリックすると "インデックスが範囲外です" となる問題を修正しました。|
|結果グリッド|グリッド結果の背景色が無視される問題を修正しました。 詳細については、[https://feedback.azure.com/forums/908035/suggestions/32895916](https://feedback.azure.com/forums/908035/suggestions/32895916) を参照してください。 |
|プラン表示|複数のスレッドが存在する場合、新しい memory grant 演算子プロパティが正しく表示されません。|
|プラン表示|実際の実行プラン xml の RunTimeCountersPerThread に、次の 4 つの属性を追加しました。HpcRowCount (*hpc* デバイスが処理した行数)、HpcKernelElapsedUs (使用中のカーネルの実行待機の経過時間)、HpcHostToDeviceBytes (ホストからデバイスに転送されたバイト数)、および HpcDeviceToHostBytes (デバイスからホストに転送されたバイト数)。|
|プラン表示|類似するプラン ノードが誤った位置で強調表示される問題を修正しました。|
|SMO|SMO/ServerConnection で SqlCredential ベースの接続が正しく行われない問題を修正しました。 詳細については、[https://feedback.azure.com/forums/908035-sql-server/suggestions/33698941](https://feedback.azure.com/forums/908035-sql-server/suggestions/33698941) を参照してください。 |
|SMO|SMO を使用して作成されたアプリケーションで、複数のスレッドで同じサーバーのデータベースを列挙しようとした場合に、各スレッドで別の SqlConnection インスタンスを使用していてもエラーが発生していた問題が修正されました。|
|SMO|外部テーブルからの転送でのパフォーマンスの低下を修正しました。|
|SMO|Azure をターゲットとする場合に、SMO で SqlConnection インスタンスのリークを引き起こしていた ServerConnection スレッド セーフでの問題を修正しました。|
|SMO|名前に中かっこが入っているデータベースを復元しようとすると、StringBuilder.FormatError を引き起こしていた問題を修正しました。|
|SMO|SMO の Azure データベースが、文字列のすべての比較で、データベースに指定された照合順序を使用する代わりに、大文字と小文字が区別される照合順序を既定としていた問題を修正しました。|
|SSMS エディター|"SQL システム テーブル" の問題を修正しました。この問題で、既定の色を復元すると、既定の緑色ではなく、ライム グリーン色に変わり、白い背景では読みにくくなります。 詳細については、「[Restoring wrong default color for SQL System Table](https://feedback.azure.com/forums/908035-sql-server/suggestions/32896906)」 (SQL システム テーブルの不適切な既定の色を復元する) を参照してください。 この問題は、英語以外のバージョンの SSMS では引き続き発生します。|
|SSMS エディター|AAD 認証を使用して Azure SQLDW に接続したときに IntelliSense が動作しない問題を修正しました。|
|SSMS エディター|ユーザーが**マスター** データベースへのアクセス権を持たない場合の Azure の IntelliSense が修正されました。|
|SSMS エディター|ターゲット データベースの照合順序で大文字と小文字が区別されているときに破損した "テンポラル テーブル" が作成されるコード スニペットを修正しました。|
|SSMS エディター|新しい TRANSLATE 関数が、Intellisense によって認識されるようになりました。 詳細については、[https://feedback.azure.com/forums/908035-sql-server/suggestions/32898430](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898430) を参照してください。 |
|SSMS エディター|組み込み関数 FORMAT の Intellisense が改善されました。 詳細については、[https://feedback.azure.com/forums/908035-sql-server/suggestions/32898676](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898676) を参照してください。 |
|SSMS エディター|LAG と LEAD が組み込み関数として認識されるようになりました。 詳細については、[https://feedback.azure.com/forums/908035-sql-server/suggestions/32898757](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898757) を参照してください。 |
|SSMS エディター|"ALTER TABLE...ADD CONSTRAINT...WITH(ONLINE=ON)" の使用時に IntelliSense で警告が表示されていた問題を修正しました。|
|SSMS エディター|いくつかのシステム ビューおよびテーブル値関数が正しく色付けされない問題を修正しました。|
|SSMS エディター|エディターのタブをクリックすると、タブにフォーカスが移る代わりに閉じてしまうことがある問題を修正しました。 詳細については、[https://feedback.azure.com/forums/908035/suggestions/37291114](https://feedback.azure.com/forums/908035/suggestions/37291114) を参照してください。 |
|SSMS のオプション|**[ツール]**  >  **[オプション]**  >  **[SQL Server オブジェクト エクスプローラー]**  >  **[コマンド]** ページのサイズが正しく調整されない問題を修正しました。|
|SSMS のオプション|SSMS では既定で、XMLA エディターでの DTD の自動ダウンロードが無効化されるようになります。(xml 言語サービスを使用する) XMLA スクリプト エディターでは既定で、悪意がある可能性のある xmla ファイルの DTD が自動的にダウンロードされないようになります。 これは、 **[ツール]**  >  **[オプション]**  >  **[環境]**  >  **[テキスト エディター]**  >  **[XML]**  >  **[その他]** で [DTD とスキーマを自動的にダウンロードする] 設定をオフにすることで制御されます。|
|SSMS のオプション|以前のバージョンの SSMS にあった **CTRL + D** のショートカットを復元しました。 詳細については、[https://feedback.azure.com/forums/908035/suggestions/35544754](https://feedback.azure.com/forums/908035/suggestions/35544754) を参照してください。 |
|テーブル デザイナー (Table Designer)|"200 行の編集" 時のクラッシュを修正しました。|
|テーブル デザイナー (Table Designer)|Azure SQL Database に接続したときにデザイナーがテーブルを追加できていた問題を修正しました。|
|脆弱性評価|スキャン結果が適切に読み込まれない問題を修正しました。|
|XEvent|読み込みできる文字列としてアクション ID フィールドとクラスの型フィールドを示す 2 つの列 "action_name" と "class_type_desc" が追加されました。|
|XEvent|1,000,000 イベントのイベント XEvent Viewer 上限を削除しました。|
|XEvent プロファイラー|96 コアの SQL Server に接続したときに XEvent Profiler が起動できなかった問題を修正しました。|
|XEvent ビューアー|"拡張イベントのツールバー オプション" を使用してイベントをグループ化しようとすると、XEvent ビューアーがクラッシュする問題を修正しました。|

### <a name="deprecated-and-removed-features-in-180"></a>18.0 で非推奨とされた、または削除された機能

非推奨とされた、または削除された機能
- T-SQL デバッガー
- データベース ダイアグラム
- 次のツールは、SSMS でインストールされなくなりました。
  - OSQL.EXE
  - DReplay.exe
  - SQLdiag.exe
  - SSBDiagnose.exe
  - bcp.exe
  - sqlcmd.exe
- Configuration Manager ツール:
  - SQL Server Configuration Manager と Reporting Server Configuration Manager のどちらも SSMS セットアップに含まれなくなりました。
- DMF の標準ポリシー
  - SSMS でポリシーはインストールされなくなりました。 これらは Git に移動されます。 ユーザーは必要に応じて投稿し、ダウンロード/インストールすることができるようになります。
- SSMS コマンド ライン オプション -P が削除されました
  - セキュリティに関する懸案事項であるため、コマンド ラインでクリア テキストのパスワードを指定するオプションが削除されました。
- [スクリプトの生成] > [Web サービスにパブリッシュ] が削除されました
  - この非推奨の機能は SSMS UI から削除されました。
- オブジェクト エクスプローラーでノード [メンテナンス] > [レガシ] が削除されました。
  - 非常に古い ''データベース メンテナンス プラン'' と ''SQL メール'' ノードにはアクセスできなくなりました。 新しい [データベース メール] と [メンテナンス プラン] ノードは、引き続き通常どおり動作します。

### <a name="known-issues-180"></a>既知の問題 (18.0)

- バージョン 18.0 のインストールでは、SQL Server Management Studio を実行できないため、問題が発生する可能性があります。 この問題が発生した場合は、「[SSMS2018 - Installed, but will not run](https://feedback.azure.com/forums/908035-sql-server/suggestions/37502512-ssms2018-installed-but-will-not-run)」 (SSMS2018 - インストールされたが起動しない) の記事の手順に従ってください。

- SSMS の結果から表示されるデータのサイズには、グリッド、テキスト、またはファイルに制限があります。

- 複数のクエリ ウィンドウを切り替えると再描画の問題が発生します。 詳細については、「[UserVoice](https://feedback.azure.com/forums/908035/suggestions/37474042)」を参照してください。 この問題を回避するには、[ツール] > [オプション] でハードウェア アクセラレータを無効にします。

## <a name="downloadssdtmediadownloadpng-ssms-1791httpsgomicrosoftcomfwlinklinkid2043154clcid0x409"></a>[SSMS 17.9.1](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x409) ![のダウンロード](../ssdt/media/download.png)

- リリース番号:17.9.1<br>
- ビルド番号:14.0.17289.0<br>
- リリース日:2018 年 11 月 21 日

17.9.1 は 17.9 に対する小規模な更新であり、次のバグが修正されています。

- "Azure Active Directory - Universal with MFA のサポート" 認証を SQL クエリ エディターと共に使用すると、クエリを呼び出すたびに接続が終了し、再び開かれることがある、という問題を修正しました。 接続が終了する副作用として、グローバル一時テーブルが予期せず削除されること、また場合によって接続に新しい SPID が付与されることがあります。
- 復元プランが復元プランを発見できない、または特定の条件下で非効率的な復元プランが生成されるという、長いあいだ未解決であった問題を修正しました。
- Azure SQL データベースへの接続時にエラーが発生する原因であった "データ層アプリケーションのインポート" ウィザードでの問題を修正しました。

> [!NOTE]
> SSMS 17.x の英語以外のローカライズされたリリースでは、次のものにインストールする場合、[KB 2862966 セキュリティ更新プログラム パッケージ](https://support.microsoft.com/kb/2862966)が必要です:Windows 8、Windows 7、Windows Server 2012、Windows Server 2008 R2。

[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x804)| [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x404)| [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x409)| [フランス語](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x40c)| [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x407)| [イタリア語](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x410)| [日本語](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x411)| [韓国語](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x412)| [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x416)| [ロシア語](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x419)| [スペイン語](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x40a)

## <a name="downloadssdtmediadownloadpng-ssms-1653httpsgomicrosoftcomfwlinklinkid840946"></a>![ダウンロード](../ssdt/media/download.png) [SSMS 16.5.3](https://go.microsoft.com/fwlink/?LinkID=840946)
一般公開 | ビルド番号:13.0.16106.4

[簡体中国語](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x804)| [繁体中国語](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x404)| [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x409)| [フランス語](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40c)| [ドイツ語](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x407)| [イタリア語](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x410)| [日本語](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x411)| [韓国語](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x412)| [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x416)| [ロシア語](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x419)| [スペイン語](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40a)

このリリースでは次の問題が修正されました。

* SSMS 16.5.2 で、テーブルに複数のスパース列がある場合に 'Table' ノードが拡張される原因となっていた問題が修正されました。

* ユーザーは、SSIS カタログに、Microsoft Dynamics AX/CRM Online のリソースに接続される OData 接続マネージャーを含む SSIS パッケージを展開できます。 詳細については、「[OData 接続マネージャー](../integration-services/connection-manager/odata-connection-manager.md)」を参照してください。

* 関連付けられていないオブジェクトで既存のテーブルに対して Always Encrypted を構成すると、エラーが発生して実行できない ( [Connect ID 3103181](https://connect.microsoft.com/SQLServer/feedback/details/3103181/setting-up-always-encrypted-on-an-existing-table-fails-with-errors-on-unrelated-objects) を参照)。

* 複数のスキーマを持つ既存のデータベースに対して Always Encrypted を構成できない ( [Connect ID 3109591](https://connect.microsoft.com/SQLServer/feedback/details/3109591/sql-server-2016-always-encrypted-against-existing-database-with-multiple-schemas-doesnt-work) を参照)。

* データベースにシステム ビューを参照するビューが含まれているため、Always Encrypted の暗号化された列ウィザードでエラーが発生する ( [Connect ID 3111925](https://connect.microsoft.com/SQLServer/feedback/details/3111925/sql-server-2016-always-encrypted-encrypted-column-wizard-failed-task-failed-due-to-following-error-cannot-save-package-to-file-the-model-has-build-blocking-errors) を参照)。

* Always Encrypted を使用して暗号化する場合、暗号化が正しく処理されていない状態でモジュールを更新するとエラーが発生する。

* *[最近使用した項目を開く]* メニューに、最近保存したファイルが表示されない ( [Connect ID 3113288](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files) を参照)。

* テーブルのインデックスを右クリックすると SSMS の動作が遅くなる (リモート (インターネット) 接続経由の場合)。 [Connect ID 3114074](https://connect.microsoft.com/SQLServer/feedback/details/3114074/ssms-slow-when-right-clicking-an-index-for-a-table-over-a-remote-internet-connection) を参照)。

* SQL デザイナーのスクロール バーの問題が修正されました ( [Connect ID 3114856](https://connect.microsoft.com/SQLServer/feedback/details/3114856/bug-in-scrollbar-on-sql-desginer-in-ssms-2016) を参照)。

* テーブルのコンテキスト メニューがすぐにハングする。 

* SSMS で利用状況モニターの例外がスローされ、クラッシュする場合がある ( [Connect ID 697527](https://connect.microsoft.com/SQLServer/feedback/details/697527/) を参照)。

* ".NET ランタイムの内部エラーにより、処理が中止されました。IP 71AF8579 (71AE0000)、終了コード 80131506" という内容のエラーで SSMS 2016 がクラッシュする。


## <a name="uninstall-and-reinstall-ssms-17x"></a>SSMS 17.x をアンインストールおよび再インストールする

SSMS のインストールで問題があり、標準のアンインストールと再インストールでは解決されない場合、最初に Visual Studio 2015 IsoShell の[修復](https://support.microsoft.com/help/4028054/windows-10-repair-or-remove-programs)をお試しください。 Visual Studio 2015 IsoShell の修復で問題が解決しない場合、多数のランダムな問題は次の手順で修正されることが確認されています。

1. アプリケーションをアンインストールする場合と同じ方法で、SSMS をアンインストールします (Windows のバージョンに応じて *[アプリと機能]* 、 *[プログラムと機能]* を使用する)。

2. **管理者特権でのコマンド プロンプトから** Visual Studio 2015 IsoShell をアンインストールします。

    ```PUSHD "C:\ProgramData\Package Cache\FE948F0DAB52EB8CB5A740A77D8934B9E1A8E301\redist"```

    ```vs_isoshell.exe /Uninstall /Force /PromptRestart```

3. アプリケーションをアンインストールする場合と同じ方法で、Microsoft Visual C++ 2015 再頒布可能パッケージをアンインストールします。 コンピューター上に x86 と x64 がある場合は、両方ともアンインストールします。

4. **管理者特権でのコマンド プロンプトから** Visual Studio 2015 IsoShell を再インストールします。  

    ```PUSHD "C:\ProgramData\Package Cache\FE948F0DAB52EB8CB5A740A77D8934B9E1A8E301\redist"```  

    ```vs_isoshell.exe /PromptRestart```

5. SSMS を再インストールします。

6. 最新バージョンでない場合は、[最新バージョンの Visual C++ 2015 再頒布可能パッケージ](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads)にアップグレードします。

## <a name="additional-downloads"></a>追加のダウンロード

すべての SQL Server Management Studio ダウンロードの一覧については、「[Microsoft ダウンロード センター](https://www.microsoft.com/download/search.aspx?q=sql%20server%20management%20studio&p=0&r=10&t=&s=Relevancy~Descending)」を検索してください。  
  
SQL Server Management Studio の最新リリースについては、「[SQL Server Management Studio &#40;SSMS&#41; のダウンロード](../ssms/download-sql-server-management-studio-ssms.md)」を参照してください。