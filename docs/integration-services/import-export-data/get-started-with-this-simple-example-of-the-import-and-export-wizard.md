---
title: 簡単な例によるインポートおよびエクスポート ウィザードの概要 | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: quickstart
ms.assetid: ea3db39b-698b-4a74-8eb8-21dc7252dc1a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 40b71d77727435316c2595abba6db70119d4b152
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285214"
---
# <a name="get-started-with-this-simple-example-of-the-import-and-export-wizard"></a>簡単な例によるインポートおよびエクスポート ウィザードの概要

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Excel スプレッドシートから SQL Server データベースにデータをインポートするというよくあるシナリオを使って、SQL Server インポートおよびエクスポート ウィザードの機能について説明します。 別の変換元および別の変換先を使う予定の場合でも、このトピックを読むとウィザードの実行について知っておく必要があるほとんどのことがわかります。

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>前提条件 - コンピューターへのウィザードのインストール
ウィザードを実行する必要はあるが、コンピューターに [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールしていない場合は、SQL Server Data Tools (SSDT) をインストールすることで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードをインストールできます。 詳細については、「 [SQL Server Data Tools (SSDT) のダウンロード](https://msdn.microsoft.com/library/mt204009.aspx)」を参照してください。

## <a name="heres-the-excel-source-data-for-this-example"></a>この例の Excel ソース データ
このソース データをコピーします。WizardWalkthrough.xlsx Excel ブックの WizardWalkthrough ワークシートの 2 列の小さいテーブルです。

![Excel のソース データ](../../integration-services/import-export-data/media/excel-source-data.jpg)

## <a name="heres-the-sql-server-destination-database-for-this-example"></a>この例の SQL Server 変換先データベース
次に示すのが (SQL Server Management Studio の図)、ソース データをコピーする SQL Server 変換先データベースです。 変換先テーブルはまだありません。ウィザードで作成します。

![SQL Server の変換先データベース](../../integration-services/import-export-data/media/sql-server-destination-database.jpg)

## <a name="step-1---start-the-wizard"></a>ステップ 1 - ウィザードを開始する
Windows の [スタート] メニューの [Microsoft SQL Server 2016] グループからウィザードを開始します。

![ウィザードを開始する](../../integration-services/import-export-data/media/start-wizard.jpg)

> [!NOTE]
> この例では、32 ビット バージョンの Microsoft Office がインストールされているため、32 ビットのウィザードを選びます。 その結果、32 ビットのデータ プロバイダーを使って Excel に接続する必要があります。 他の多くのデータ ソースでは、通常、64 ビットのウィザードを選ぶことができます。
>
> 64 ビット バージョンの SQL Server インポートおよびエクスポート ウィザードを使用するには、SQL Server をインストールする必要があります。 SQL Server Data Tools (SSDT) および SQL Server Management Studio (SSMS) は 32 ビット アプリケーションであり、32 ビット バージョンのウィザードを含む、32 ビット ファイルのみがインストールされます。

詳細については、「 [Start the SQL Server Import and Export Wizard](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)」(SQL Server インポートおよびエクスポート ウィザードを開始する) を参照してください。

## <a name="step-2---view-the-welcome-page"></a>ステップ 2 - ウェルカム ページを表示する
ウィザードの最初のページは **[ようこそ]** ページです。 

通常、このページを再び表示する必要はないので、 **[次回からこの開始ページを表示しない]** をオンにします。

![ウィザードへようこそ](../../integration-services/import-export-data/media/welcome-to-the-wizard.jpg)

## <a name="step-3---pick-excel-as-your-data-source"></a>ステップ 3 - データ ソースとして Excel を選ぶ
次の **[データ ソースの選択]** ページで、データ ソースとして Microsoft Excel を選びます。 それから、Excel ファイルを参照して選びます。 最後に、ファイルの作成に使った Excel のバージョンを指定します。

> [!IMPORTANT]
> Excel ファイルへの接続、および Excel から、または Excel へのデータの読み込みに関する制限事項と既知の問題については、「[Load data from or to Excel with SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)」 (SQL Server Integration Services (SSIS) を使用して Excel から、または Excel にデータを読み込む) を参照してください。

![Excel データ ソースを選ぶ](../../integration-services/import-export-data/media/choose-the-excel-data-source.jpg)

ウィザードのこのページについて詳しくは、「[Choose a Data Source](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)」([データ ソースの選択]) をご覧ください。

## <a name="step-4---pick-sql-server-as-your-destination"></a>ステップ 4 - 変換先として SQL Server を選択する
次の **[変換先の選択]** ページで、Microsoft SQL Server に接続するデータ プロバイダーの 1 つを一覧で選ぶことで、変換先として SQL Server を選びます。 この例では、 **[.Net Framework Data Provider for SQL Server]** を選びます。

ページにプロバイダーのプロパティの一覧が表示されます。 これらの多くは、わかりにくい名前となじみのない設定です。 幸い、任意のエンタープライズ データベースに接続するには、通常、3 つの情報を提供するだけで済みます。 他の設定の既定値は無視できます。

|必要な情報|.NET Framework Data Provider for SQL Server プロパティ|
|---|---|
|サーバー名|**[データ ソース]**|
|認証 (ログイン) 情報|**[統合セキュリティ]** 、または **[ユーザー ID]** と **[パスワード]**<br/>サーバー上のデータベースのドロップダウン リストを表示する場合は、まず、有効なログイン情報を提供する必要があります。|
|データベース名|**初期カタログ**|

![SQL Server 変換先を選ぶ](../../integration-services/import-export-data/media/choose-the-sql-server-destination.jpg)

SQL Server への接続について詳しくは、「[SQL Server データ ソースに接続する](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)」をご覧ください。 ウィザードのこのページについて詳しくは、「[Choose a Destination](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)」([変換先の選択]) をご覧ください。

## <a name="step-5---copy-a-table-instead-of-writing-a-query"></a>ステップ 5 - クエリを記述する代わりにテーブルをコピーする
次の **[テーブルのコピーまたはクエリの指定]** ページでは、ソース データのテーブル全体をコピーすることを指定します。 コピーするデータを選ぶために SQL 言語でクエリを作成することはしません。

![テーブルのコピーを指定する](../../integration-services/import-export-data/media/specify-to-copy-a-table.jpg)

ウィザードのこのページについて詳しくは、「[Specify Table Copy or Query](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)」([テーブルのコピーまたはクエリの指定]) をご覧ください。

## <a name="step-6---pick-the-table-to-copy"></a>ステップ 6 - コピーするテーブルを選ぶ
次の **[コピー元のテーブルおよびビューを選択]** ページでは、データ ソースのコピー先のテーブルを 1 つ以上選びます。 それから、選んだ各コピー元テーブルを新規または既存のコピー先テーブルにマッピングします。

この例では、既定で **[コピー元]** 列の **WizardWalkthrough$** ワークシートが、SQL Server 変換先の同じ名前を持つ新しいテーブルにマップされています (Excel ブックにはワークシートが 1 つだけ含まれます)。
-   コピー元テーブルの名前のドル記号 ($) は、Excel ワークシートであることを示します (Excel の名前付き範囲は名前だけで表されます)。
-   変換先テーブルのアイコンの星形は、ウィザードが新しい変換先テーブルを作成することを示します。

![テーブルを選ぶ (名前変更前)](../../integration-services/import-export-data/media/select-the-table-before-renaming.jpg)

通常は、新しい変換先テーブルの名前からドル記号 ($) を削除します。

![テーブルを選ぶ (名前変更後)](../../integration-services/import-export-data/media/select-the-table-after-renaming.jpg)

ウィザードのこのページについて詳しくは、「[Select Source Tables and Views](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)」([コピー元のテーブルおよびビューを選択]) をご覧ください。

## <a name="optional-step-7---review-the-column-mappings"></a>(省略可能) ステップ 7 - 列のマッピングを確認する
**[コピー元のテーブルおよびビューを選択]** ページを終了する前に、必要な場合は、 **[マッピングの編集]** ボタンをクリックして **[列マッピング]** ダイアログ ボックスを開きます。 ここの **[マッピング]** テーブルで、ウィザードがコピー元ワークシートの列を新しい変換先テーブルの列にマッピングする方法を確認します。

![列マッピングを確認する](../../integration-services/import-export-data/media/view-column-mappings.jpg)

ウィザードのこのページについて詳しくは、「[Column Mappings](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)」([列マッピング]) をご覧ください。

## <a name="optional-step-8---review-the-create-table-statement"></a>(省略可能) ステップ 8 - CREATE TABLE ステートメントを確認する
**[列マッピング]** ダイアログ ボックスを開いている間に、必要に応じて、 **[SQL の編集]** ボタンをクリックして **[テーブル作成 SQL ステートメント]** ダイアログ ボックスを開きます。 ここで、ウィザードが新しい変換先テーブルを作成するために生成した **CREATE TABLE** ステートメントを確認します。 通常、ステートメントを変更する必要はありません。

![CREATE TABLE ステートメントを表示する](../../integration-services/import-export-data/media/view-create-table-statement.jpg)

ウィザードのこのページについて詳しくは、「[テーブル作成 SQL ステートメント](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)」をご覧ください。

## <a name="optional-step-9---preview-the-data-to-copy"></a>(省略可能) ステップ 9 - コピーするデータを確認する
**[OK]** をクリックして **[テーブル作成 SQL ステートメント]** ダイアログ ボックスを閉じた後、 **[OK]** を再びクリックして **[列マッピング]** ダイアログ ボックスを閉じます。 **[コピー元のテーブルおよびビューを選択]** ページに戻ります。 必要に応じて、 **[プレビュー]** ボタンをクリックして、ウィザードがコピーするデータのサンプルを表示します。 この例では、問題ありません。

![コピーするデータを確認する](../../integration-services/import-export-data/media/preview-data-to-copy.jpg)

ウィザードのこのページについて詳しくは、「[Preview Data](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)」([データのプレビュー]) をご覧ください。

## <a name="step-10---yes-you-want-to-run-the-import-export-operation"></a>ステップ 10 - インポートおよびエクスポート操作を実行する
次の **[パッケージの保存および実行]** ページで、 **[すぐに実行する]** を有効のままにして、次のページで **[完了]** をクリックしたらすぐにデータをコピーします。 または、 **[パッケージの保存および実行]** ページで **[完了]** をクリックすると、次のページをスキップできます。

![パッケージを実行する](../../integration-services/import-export-data/media/run-the-package.jpg)

ウィザードのこのページについて詳しくは、「[Save and Run Package](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)」([パッケージの保存および実行]) をご覧ください。

## <a name="step-11---finish-the-wizard-and-run-the-import-export-operation"></a>ステップ 11 - ウィザードを終了し、インポートとエクスポート操作を実行する
**[パッケージの保存および実行]** ページで **[完了]** ではなく **[次へ]** をクリックした場合は、次の **[ウィザードの完了]** ページで、ウィザードが行う処理の概要を確認します。 **[完了]** をクリックして、インポートおよびエクスポート操作を実行します。

![ウィザードの完了](../../integration-services/import-export-data/media/complete-the-wizard.jpg)

ウィザードのこのページについて詳しくは、「[Complete the Wizard](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)」([ウィザードの完了]) をご覧ください。

## <a name="step-12---review-what-the-wizard-did"></a>ステップ 12 - ウィザードが行った処理を確認する
最後のページでは、ウィザードが各タスクを終了するのを確認した後、結果を確認します。 強調表示された行は、ウィザードが正常にデータをコピーしたことを示します。 以上で終了です。

![ウィザード成功](../../integration-services/import-export-data/media/the-wizard-succeeded.jpg)

ウィザードのこのページについて詳しくは、「[操作の実行](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md)」をご覧ください。

## <a name="heres-the-new-table-of-data-copied-to-sql-server"></a>SQL Server にコピーされたデータの新しいテーブル
SQL Server Management Studio で、ウィザードが SQL Server に作成した新しい変換先テーブルを確認します。

![SQL Server にコピーされたデータ](../../integration-services/import-export-data/media/data-copied-to-sql-server.jpg)

やはり SSMS で、ウィザードが SQL Server にコピーしたデータを確認します。

![SQL Server にコピーされたデータ 2](../../integration-services/import-export-data/media/data-copied-to-sql-server-2.jpg)

## <a name="learn-more"></a>詳細情報  
ウィザードのしくみについては、以下を参照してください。
-   **ウィザードのしくみについては、以下を参照してください。** ウィザードの概要をお探しの場合は、「 [SQL Server でサポートされるインポートとエクスポートのデータ ソース](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)」を参照してください。

-   **ウィザードの手順について学習する。** ウィザードの手順についての情報を探している場合は、「[SQL Server インポートおよびエクスポート ウィザードの手順](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md)」の一覧から目的のページを選んでください。 ウィザードのページごとに別のドキュメント ページもあります。

-   **データ ソースおよび変換先に接続する方法を学習する。** データへの接続方法についての情報を探している場合は、「[SQL Server インポートおよびエクスポート ウィザードを使用してデータ ソースに接続する](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md)」の一覧から目的のページを選んでください。 いくつかの一般的に使用されるデータ ソースごとに個別のドキュメントのページがあります。

-   **Excel から、または Excel にデータを読み込む詳細について。** Excel ファイルへの接続、および Excel から、または Excel へのデータの読み込みに関する制限事項と既知の問題に関する情報は、「[Load data from or to Excel with SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)」 (SQL Server Integration Services (SSIS) を使用して Excel から、または Excel にデータを読み込む) を参照してください。
