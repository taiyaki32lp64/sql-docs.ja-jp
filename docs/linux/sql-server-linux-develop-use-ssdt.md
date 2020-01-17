---
title: Linux 用の SQL Server データベースを開発してデプロイする | Microsoft Docs
description: ''
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1e924704-e07c-4a8b-b243-8c1dd8cff0d3
ms.openlocfilehash: 0a7c16f508621297e39df5cd47bde891b7d8a140
ms.sourcegitcommit: 82b70c39550402a2b0b327db32bf5ecf88b50d3c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73033018"
---
# <a name="use-visual-studio-to-create-databases-for-sql-server-on-linux"></a>Visual Studio を使用して SQL Server on Linux 用のデータベースを作成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server Data Tools (SSDT) によって、Visual Studio を SQL Server on Linux 用の強力な開発およびデータベース ライフサイクル管理 (DLM) 環境として使用できます。 ソース管理されたプロジェクトからデータベースを開発、ビルド、テスト、および発行できます。 アプリケーション コードを開発する場合と同様です。

## <a name="install-visual-studio-and-sql-server-data-tools"></a>Install Visual Studio と SQL Server Data Tools をインストールする

1. お使いの Windows コンピューターに Visual Studio がまだインストールされていない場合は、[Visual Studio をダウンロードしてインストール](https://visualstudio.microsoft.com/downloads/)します。 Visual Studio のライセンスをお持ちでない場合は、学生、オープンソースの開発者、個人の開発者向けの全機能を備えた無料の IDE である Visual Studio Community エディションを使用できます。

2. Visual Studio のインストール中に、 **[インストールの種類を選択してください]** オプションで **[カスタム]** を選択します。 **[次へ]** をクリックします。

3. 機能選択の一覧から、 **[Microsoft SQL Server Data Tools]** 、 **[Git for Windows]** 、 **[GitHub Extension for Visual Studio]** を選択します。

   <img src="./media/sql-server-linux-develop-use-ssdt/ssdt-setup.png" alt="ssdt setup" style="width: 400px;"/>

4. Visual Studio のインストールを続行して完了します。 これには数分かかる可能性があります。

## <a name="upgrade-sql-server-data-tools-to-ssdt-170-rc-release"></a>SQL Server Data Tools を SSDT 17.0 RC リリースにアップグレードする

SQL Server on Linux は、SSDT バージョン 17.0 RC 以降でサポートされています。

* [SSDT 17.0 RC2 をダウンロードしてインストールします](https://go.microsoft.com/fwlink/?linkid=837939)。

## <a name="create-a-new-database-project-in-source-control"></a>ソース管理内に新しいデータベース プロジェクトを作成する

1. Visual Studio を起動します。

2. **[表示]** メニューの **[チーム エクスプローラー]** をクリックします。 

3. **[接続]** ページで、 **[ローカル Git リポジトリ]** セクションの **[新規]** をクリックします。

   <img src="./media/sql-server-linux-develop-use-ssdt/git-repository.png" alt="local repository" style="width: 300px;"/>

4. **[作成]** をクリックします。 ローカル Git リポジトリが作成されたら、 **[SSDTRepo]** をダブルクリックします。

5. **[ソリューション]** セクションの **[新規]** をクリックします。 **[新規プロジェクト]** ダイアログで、 **[その他の言語]** ノードの下の **[SQL Server]** を選択します。

   <img src="./media/sql-server-linux-develop-use-ssdt/new-project.png" alt="local repository" style="width: 480px;"/>

6. [名前] に「**TutorialDB**」と入力し、 **[OK]** をクリックして新しいデータベース プロジェクトを作成します。

## <a name="create-a-new-table-in-the-database-project"></a>データベース プロジェクト内に新しいテーブルを作成する

1. **[表示]** メニューの **[ソリューション エクスプローラー]** をクリックします。

2. ソリューション エクスプローラーで **[TutorialDB]** を右クリックして、データベース プロジェクト メニューを開きます。

3. **[追加]** で **[テーブル]** を選択します。

   <img src="./media/sql-server-linux-develop-use-ssdt/create-table.png" alt="create table" style="width: 480px;"/>

4. テーブル デザイナーを使用して、次の図に示すように、[Name] `nvarchar(50)` と [Location] `nvarchar(50)` の 2 つの列を追加します。 デザイナーで列を追加すると、SSDT によって `CREATE TABLE` スクリプトが生成されます。

   <img src="./media/sql-server-linux-develop-use-ssdt/add-columns.png" alt="add columns" style="width: 480px;"/>

5. **Table1.sql**ファイルを保存します。

## <a name="build-and-validate-the-database"></a>データベースをビルドして検証する

1. **[TutorialDB]** のデータベース プロジェクト メニューを開き、 **[ビルド]**  を選択します。 SSDT によって、プロジェクト内の .sql ソース コード ファイルがコンパイルされ、データ層アプリケーション パッケージ (dacpac) ファイルがビルドされます。 これを使用して、Linux 上の SQL Server インスタンスにデータベースを発行できます。 

   <img src="./media/sql-server-linux-develop-use-ssdt/build.png" alt="add columns" style="width: 400px;"/>

2. Visual Studio の **[出力]** ウィンドウで、ビルド成功メッセージを確認します。 

## <a name="publish-the-database-to-sql-server-instance-on-linux"></a>Linux 上の SQL Server インスタンスにデータベースを発行する

1. **[TutorialDB]** のデータベース プロジェクト メニューを開き、 **[発行]** を選択します。

2. **[編集]** をクリックし、Linux 上の SQL Server インスタンスを選択します。

   <img src="./media/sql-server-linux-develop-use-ssdt/publish-dialog.png" alt="publish dialog" style="width: 480px;"/>

3. [接続] ダイアログ ボックスに、Linux 上の SQL Server インスタンスの IP アドレスまたはホスト名、ユーザー名、およびパスワードを入力します。

   <img src="./media/sql-server-linux-develop-use-ssdt/connection-dialog.png" alt="connection dialog" style="width: 400px;"/>

4. [発行] ダイアログで **[発行]** ボタンをクリックします。

5. **[Data Tools の操作]** ウィンドウの発行状態を確認します。

6. **[結果の表示]** または **[スクリプトの表示]** をクリックして、SQL Server on Linux でのデータベースの発行結果の詳細を確認します。

   <img src="./media/sql-server-linux-develop-use-ssdt/publish-result.png" alt="publish result" style="width: 480px;"/>

これで、Linux 上の SQL Server インスタンスに新しいデータベースが作成され、ソース管理されたデータベース プロジェクトを使用してデータベースを開発するための基本を学習できました。

## <a name="next-steps"></a>次の手順

T-SQL を初めて使用する場合は、「[チュートリアル:Transact-SQL ステートメントの作成](../t-sql/tutorial-writing-transact-sql-statements.md)」を参照してください。

SQL Data Tools を使用したデータベースの開発の詳細については、以下の記事を参照してください。

* [Visual Studio をダウンロードしてインストールする](https://www.visualstudio.com/downloads/)
* [SSDT をダウンロードしてインストールする](https://aka.ms/ssdt-download)
* [SSDT MSDN のドキュメント](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)
* [チュートリアル: Transact-SQL ステートメントの作成](https://msdn.microsoft.com/library/ms365303.aspx)
* [Transact-SQL リファレンス (データベース エンジン)](https://msdn.microsoft.com/library/bb510741.aspx)
