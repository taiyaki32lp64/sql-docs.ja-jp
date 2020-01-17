---
title: データ仮想化の拡張機能
titleSuffix: Azure Data Studio
description: Azure Data Studio 用のデータ仮想化の拡張機能
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: rajmera3
ms.author: raajmera
ms.custom: seodec18
ms.date: 11/04/2019
ms.openlocfilehash: 98a93895b8f552bf7506880a612ab2ae68c48afb
ms.sourcegitcommit: db715cad313055c8b42d547be686de8755342d65
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73801128"
---
# <a name="data-virtualization-extension-for-azure-data-studio"></a>Azure Data Studio 用のデータ仮想化の拡張機能

Azure Data Studio 用のデータ仮想化の拡張機能では、PolyBase [[Create External Table]\(外部テーブルの作成\) ウィザード](../relational-databases/polybase/data-virtualization.md?toc=/sql/toc/toc.json)がサポートされています。

## <a name="install-the-data-virtualization-extension"></a>データ仮想化の拡張機能のインストール

データ仮想化の拡張機能をインストールするには、Azure Data Studio を開き、[拡張機能] タブからダウンロードします。[こちら](extensions.md)の指示に従います。

## <a name="changes-in-release-10"></a>リリース 1.0 での変更点
* 拡張機能名がデータ仮想化に変更されました。
* [Create External Table]\(外部テーブルの作成\) ウィザード:
    * 仮想化 MongoDB および Teradata ソース用のガイド付きノートブックが含まれています。
    * MongoDB および Teradata 仮想化ノートブックに変数を入力するためのダイアログが追加されました。 

## <a name="changes-in-release-016"></a>リリース 0.16 での変更点
* [Create External Table]\(外部テーブルの作成\) ウィザード:
  * オブジェクト マッピング ページでテーブルとビューを読み込むときのエラー処理が改善されました。

## <a name="changes-in-release-015"></a>リリース 0.15 での変更点
* [Create External Table]\(外部テーブルの作成\) ウィザード:
  * オブジェクト マッピング ページ上でテーブルと列の情報の読み込みにかかる時間が短縮されました。
  * 接続の詳細ページ上で、既存のデータベース スコープの資格情報の読み込みに関するバグを修正しました。
* CSV ファイルからの外部テーブルの作成ウィザード:
  * PROSE の解析に使用される既定のサンプル サイズが増加しました。

## <a name="changes-in-release-0141"></a>リリース 0.14.1 での変更点
* CTP 3.1 データ ソース サポートのサポート

## <a name="changes-in-release-0121"></a>リリース 0.12.1 での変更点

* このリリースでは、**SQL Server ビッグ データ クラスター**の接続の種類が削除されています。 以前に SQL Server ビッグ データ クラスター接続から提供されていた機能はすべて、SQL Server 接続で使用できるようになりました。
* HDFS の参照は、**Data Services** フォルダーにあります
* ノートブックの場合、PySpark およびその他のビッグ データ カーネルは、ご利用の SQL Server ビッグ データ クラスター内の SQL Server マスター インスタンスに接続されると、動作します。
* [Create External Table]\(外部テーブルの作成\) ウィザード:
  * 既存の外部データ ソースを使用した外部テーブルの作成をサポートします。
  * ウィザード全体のパフォーマンスが向上しました。
  * 特殊文字を使用したオブジェクト名の処理が改善されています。 それらが原因でウィザードが失敗することがありました
  * オブジェクト マッピング ページの信頼性が向上しました。
  * データベースのドロップダウンから、システム データベース ('DWConfiguration'、'DWDiagnostics'、'DWQueue') が削除されました。
  * **[Create External Table from CSV Files]\(CSV ファイルからの外部テーブルの作成\)** ウィザードで、外部ファイル形式オブジェクトの名前を設定できるようになりました。
  * **[Create External Table from CSV Files]\(CSV ファイルからの外部テーブルの作成\)** ウィザードの最初のページに更新ボタンが追加されました。

## <a name="release-notes-v0110"></a>リリース ノート (v0.11.0)

* Jupyter Notebook のサポート (特に Python3 と Spark カーネルのサポート) が Azure Data Studio に移動されました。 Notebooks を使用する上で、この拡張機能はもはや必要でなくなりました。
* 外部データ ウィザードでの次の複数のバグが修正されました。
  * SQL Server 2019 CTP 2.3 で提供された変更に一致するように Oracle 型マッピングが更新されました。
  * テーブル マッピング コントロールに入力された新しいスキーマが失われるという問題が修正されました。
  * テーブル マッピング内のデータベース ノードをチェックしてもすべてのテーブルとビューがチェックされるわけではないという問題が修正されました。


## <a name="release-notes-v0102"></a>リリース ノート (v0.10.2)
### <a name="sql-server-2019-support"></a>SQL Server 2019 のサポート
SQL Server 2019 のサポートが更新されました。 SQL Server ビッグ データ クラスター インスタンスに接続すると、新しい _Data Services_ フォルダーがエクスプローラー ツリーに表示されます。 このフォルダーには、接続に対して新しいノートブックを開く、Spark ジョブを送信する、HDFS を操作するといったアクション用の起動ポイントが用意されています。 HDFS ファイル/フォルダーに対する_外部データの作成_などの一部の操作については、_SQL Server 2019_ の拡張機能をインストールする必要があります。

### <a name="notebook-support"></a>Notebook のサポート
このリリースでは、Notebook ユーザー インターフェイスを大幅に更新しました。 Microsoft は、お客様と共有している Notebooks を読みやすくすることに重点を置きました。 つまり、選択されていない場合またはマウス ポインターが置かれていない場合にセルの周囲のすべてのアウトライン ボックスが削除されます。また、ホバー サポートの追加により、セルを選択することなく、セル レベルのアクションが簡単に行えます。さらに、実行カウントやアニメーション化された_実行停止ボタン_の追加などにより、実行状態が明確に示されます。 _新しいノートブック_ (`Ctrl+Shift+N`)、_セルの実行_ (`F5`)、_新しいコード セル_ (`Ctrl+Shift+C`)、_新しいテキスト セル_ (`Ctrl+Shift+T`) として、キーボード ショートカットを追加しました。 今後、Microsoft はすべての主要なアクションをショートカットで起動できるようにすることを目指していますので、不足しているものをお知らせください。

その他の機能強化と修正には次のようなものがあります。
* _SQL Server 2019_ の拡張機能では、Python 依存関係用のインストール ディレクトリを選択するように求めるメッセージが表示されるようになりました。 また、`.vsix file` に Python が含まれなくなり、拡張機能の全体的なサイズが小さくなりました。 Python の依存関係では、Spark カーネルと Python3 カーネルがサポートされます。
* コマンドラインから新しいノートブックを起動するためのサポートが追加されました。 引数 `--command=notebook.command.new --server=myservername` を指定して起動すると、新しいノートブックが開き、このサーバーに接続します。
* ノートブックにおいてセル内のコードが長い場合のパフォーマンスの修正。 コード セルが 250 行を超えると、スクロールバーが追加されます。
* 改善された .ipynb ファイルのサポート。 バージョン 3 以降がサポートされるようになりました。 保存時にファイルのバージョンが 4 以上に更新されることに注意してください。
* 組み込みの Notebook ビューアーが安定しているため、`notebook.enabled` ユーザー設定は削除されました
* この場合はオブジェクト レイアウトに加えた複数の修正により、ハイコント ラスト テーマがサポートされるようになりました。
* 出力において複数の `,,,` 文字が誤って表示される場合があるという #3680 が修正されました
* Azure Data Studio から移動したら、セルのエディターが表示されないという #3602 を修正しました
* `application/vnd.dataresource+json` 出力の MIME の種類に対してグリッド ビューを使用するようにサポートが追加されました。 つまり、これを使用する多くの Notebook では (たとえば、Python ノートブック内で `pd.options.display.html.table_schema` を設定することで)、表形式の出力がさらに良くなります。ノートブックを閉じたら、Azure Data Studio によってノートブック サーバーのシャットダウンが 2 度試行されるという #3959 が修正されました

#### <a name="known-issues"></a>既知の問題
* Notebook を開くと、Python のインストール用のダイアログが表示されます。 このインストールをキャンセルすると、[カーネル] および [アタッチ先] ドロップダウンに期待する値が表示されません。 この回避策は、Python のインストールを完了することです。
* サポートされていないカーネルでノートブックを開くと、[カーネル] と _[アタッチ先]_ ドロップダウンによって Azure Data Studio が応答を停止します。 Azure Data Studio を閉じて、サポートされているカーネル (Python3、Spark | R、Spark | Scala、PySpark、PySpark3) を使用していることを確認する必要があります
* PySpark3 またはその他の Spark カーネルを SQL Server エンドポイントに対して使用すると、Spark UI リンクが失敗します。 回避策としては、ダッシュボードから Spark UI をクリックします。または、SQL Server ビッグ データ クラスターの接続の種類には正しい Spark UI ハイパーリンクが含まれているので、これを使用して接続します。

### <a name="extensibility-improvements"></a>拡張性の向上
このリリースには、エクステンダーを支援する多くの改良点が追加されています
* 新しい `ObjectExplorerNodeProvider` API を使用すると、SQL Server またはその他の接続ノードの下にフォルダーを投稿できます。 これは SQL Server 2019 インスタンスの下に `Data Services` ノードを追加する方法ですが、この方法を使用して、監視フォルダーやその他のフォルダーを UI に簡単に追加することも可能です。
* 2 つの新しいコンテキスト キー値を使用すれば、ダッシュボードへのコントリビューションを容易に表示/非表示にすることができます。
  * `mssql:iscluster` は、これが SQL Server 2019 ビッグ データ クラスターであるかどうかを示します
  * `mssql:servermajorversion` にはサーバー バージョンがあります (SQL Server 2019 の場合は 15、SQL Server 2017 の場合は 14 といった具合に)。 これは、たとえば、SQL Server 2017 以上用の機能を表示する必要がある場合に役立ちます。


## <a name="release-notes-v080"></a>リリース ノート (v0.8.0)
*Notebooks*:
* [その他のアクション] セル ボタンをクリックすることで、既存のセルの前後へのセルの追加がサポートされるようになりました
* **[新しい接続の追加]** オプションが [アタッチ先] ドロップダウン内の接続に追加されました
* Python パッケージの更新を支援するため、およびアプリケーションを終了するとインストールが途中で停止するというケースを解決するために、 **[Reinstall Notebook Dependencies]\(Notebook の依存関係の再インストール\)** コマンドが追加されました。 これは、コマンド パレットから実行できます (`Ctrl/Cmd+Shift+P` キーを使用し、`Reinstall Notebook Dependencies` と入力する)
* PROSE python パッケージが 1.1.0 に更新されました。これには、複数のバグ修正が含まれています。 **[Reinstall Notebook Dependencies]\(Notebook の依存関係の再インストール\)** コマンドを使用して、このパッケージを更新します
* **[その他のアクション]** セル ボタンをクリックすることで、 **[出力をクリア]** コマンドがサポートされるようになりました
* ユーザーから報告された次の問題が修正されました。
  * パスの問題が原因で、Windows 上で Notebook セッションを開始できませんでした
  * ドライブのルート フォルダー (C:\ や D:\ など) から Notebook を起動できませんでした
  * [#2820](https://github.com/Microsoft/azuredatastudio/issues/2820) VS Code で ADS から作成されたノートブックを編集できません
  * Spark カーネルを実行すると、Spark UI リンクが機能するようになりました
  * "マネージド パッケージ" という名前が "インストール パッケージ" に変更されました

*外部データの作成*:

* エラー メッセージはコピー可能であり、よりわかりやすくするために概要と詳細ビューに分けられています
* UI レイアウトが改善されると共に、信頼性とエラー処理が大幅に強化されました
* ユーザーから報告された次の問題が修正されました。
  * 無効な列マッピングを含むテーブルは無効として表示され、警告によってそのエラーが説明されます

## <a name="release-notes-v072"></a>リリース ノート (v0.7.2)
* Azure Resource Explorer は Azure Data Studio に組み込まれ、この拡張機能からは削除されています。 これに関するフィードバックをお送りいただきありがとうございました。
* Markdown セルを多く含むノートブックのパフォーマンスが改善されました。
* Notebook 内の自動サイズ調整のコード セル。 これによって、セル ツールバーに基づく最小サイズが引き続き保持されます。
* Notebook の依存関係をインストールするときにユーザーに通知します。 Windows では特に長い時間がかかることがあるため、通知が [タスク] ビューに表示されるようになりました。
* Notebook の依存関係の再インストールをサポートします。 これは、ユーザーが前にインストールの途中で Azure Data Studio を閉じた場合に便利です。
* Notebook でのセルの実行のキャンセルをサポートします。
* [Create External Data]\(外部データの作成\) ウィザードを使用する場合 (特に接続エラーが発生する場合) の信頼性が向上しました。
* PolyBase が有効にされていない場合、またはターゲット サーバーで実行されていない場合は、[Create External Data]\(外部データの作成\) ウィザードの使用をブロックします。
* SQL Server 2019 と [Create External Data]\(外部データの作成\) に関連するスペルおよび名前付けの修正プログラム。
* Azure Data Studio デバッグ コンソールからエラーの多くが削除されました。
