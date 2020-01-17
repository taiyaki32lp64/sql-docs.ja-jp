---
title: SQL Server Integration Services (SSIS) を使用して Azure SQL Data Warehouse にデータを読み込む | Microsoft Docs
description: さまざまなデータ ソースから Azure SQL Data Warehouse にデータを移動するための SQL Server Integration Services (SSIS) パッケージを作成する方法を示します。
documentationcenter: NA
ms.prod: sql
ms.prod_service: integration-services
ms.technology: integration-services
ms.topic: conceptual
ms.custom: loading
ms.date: 08/09/2018
ms.author: chugu
author: chugugrace
ms.openlocfilehash: 3609de02157637ec30f7e21ad4426c5001f31a6e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71282658"
---
# <a name="load-data-into-azure-sql-data-warehouse-with-sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS) を使用して Azure SQL Data Warehouse にデータを読み込む

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



SQL Server Integration Services (SSIS) パッケージを作成して、[Azure SQL Data Warehouse](/azure/sql-data-warehouse/index) にデータを読み込みます。 SSIS データ フローを通過するときに、必要に応じてデータを再構築、変換、およびクレンジングすることができます。

この記事では、以下の操作の実行方法について説明します。

* Visual Studio で新しい Integration Services プロジェクトを作成する。
* データをソースから変換先に読み込むための SSIS パッケージを設計する。
* SSIS パッケージを実行してデータを読み込む。

## <a name="basic-concepts"></a>基本的な概念

このパッケージは SSIS での処理の基本単位です。 関連パッケージがプロジェクト内でグループ化されます。 SQL Server Data Tools を使用して Visual Studio でプロジェクトの作成およびパッケージの設計を行います。 設計プロセスは視覚的なプロセスであり、ツールボックスからデザイン画面にコンポーネントをドラッグ アンド ドロップし、コンポーネント同士を接続し、それらのプロパティを設定します。 パッケージが完成したら、パッケージを実行し、必要に応じて、包括的な管理、監視、およびセキュリティ保護のためにパッケージを SQL Server または SQL Database に配置することができます。

SSIS の詳細については、この記事では説明しません。 詳細については、以下の記事をお読みください。

- [SQL Server Integration Services](sql-server-integration-services.md)

- [ETL パッケージを作成する方法](ssis-how-to-create-an-etl-package.md)

## <a name="options-for-loading-data-into-sql-data-warehouse-with-ssis"></a>SSIS を使用して SQL Data Warehouse にデータを読み込むためのオプション
SQL Server Integration Services (SSIS) とは、SQL Data Warehouse に接続するため、およびデータを読み込みのためのさまざまなオプションを提供する柔軟性に優れたツール セットです。

1. 最適なパフォーマンスを提供する推奨される方法は、[Azure SQL DW アップロード タスク](control-flow/azure-sql-dw-upload-task.md)を使用してデータを読み込むパッケージを作成することです。 このタスクでは、ソースと変換先の情報の両方がカプセル化されます。 ソースのデータは、ローカルの区切りテキスト ファイルに保存されていることを前提としています。

2. また、ソースと変換先を含むデータ フロー タスクを使用するパッケージを作成することもできます。 このアプローチは、SQL Server と Azure SQL Data Warehouse を含む幅広いデータ ソースをサポートしています。

## <a name="prerequisites"></a>Prerequisites
このチュートリアルの手順を実行するには、以下の要素が必要です。

1. **SQL Server Integration Services (SSIS)** . SSIS は SQL Server のコンポーネントであり、使用するには SQL Server のライセンス版、開発者版、または評価版が必要です。 SQL Server の評価版を取得するには、[SQL Server の評価](https://www.microsoft.com/evalcenter/evaluate-sql-server-2017-rtm)に関するページを参照してください。
2. **Visual Studio** (省略可能)。 無料の Visual Studio Community Edition を取得するには、[Visual Studio Community][Visual Studio Community] に関するページを参照してください。 Visual Studio をインストールしない場合は、SQL Server Data Tools (SSDT) のみをインストールできます。 SSDT をインストールすると、機能が制限されたバージョンの Visual Studio がインストールされます。
3. **Visual Studio 用 SQL Server Data Tools (SSDT)** 。 Visual Studio 用 SQL Server Data Tools を取得するには、[SQL Server Data Tools (SSDT) のダウンロード][Download SQL Server Data Tools (SSDT)]に関するページを参照してください。
4. **Azure SQL Data Warehouse データベースとアクセス許可**。 このチュートリアルでは、SQL Data Warehouse のインスタンスに接続し、そのインスタンスにデータを読み込みます。 接続し、テーブルを作成し、データを読み込むことができるアクセス許可が必要です。

## <a name="create-a-new-integration-services-project"></a>新しい Integration Services プロジェクトを作成する
1. Visual Studio を起動します。
2. **[ファイル]** メニューの **[新規 | プロジェクト]** を選択します。
3. **[インストール済み | テンプレート | ビジネス インテリジェンス | Integration Services]** のプロジェクトの種類に移動します。
4. **[Integration Services プロジェクト]** を選択します。 **[名前]** と **[場所]** に値を指定し、 **[OK]** を選択します。

Visual Studio が開き、新しい Integration Services (SSIS) プロジェクトを作成します。 次に Visual Studio は、プロジェクト内の新しい単一の SSIS パッケージ (Package.dtsx) のためのデザイナーを開きます。 次の画面領域が表示されます。

* 左側には、SSIS コンポーネントの**ツールボックス**。
* 中央には、複数のタブを備えたデザイン画面。 通常は、少なくとも **[制御フロー]** タブと **[データ フロー]** タブを使用します。
* 右側には、**ソリューション エクスプローラー**と **[プロパティ]** ウィンドウ。
  
    ![][01]

## <a name="option-1---use-the-sql-dw-upload-task"></a>オプション 1 - SQL DW アップロード タスクを使用する

最初のアプローチは、SQL DW アップロード タスクを使用するパッケージです。 このタスクでは、ソースと変換先の情報の両方がカプセル化されます。 ソースのデータは、ローカルまたは Azure Blob Storage の区切りテキスト ファイルに保存されていることを前提としています。

### <a name="prerequisites-for-option-1"></a>オプション 1 の前提条件

このオプションを選択してチュートリアルを続行するには、次の要素が必要です。

- [Microsoft SQL Server Integration Services Feature Pack for Azure][Microsoft SQL Server 2017 Integration Services Feature Pack for Azure]。 SQL DW アップロード タスクは、Feature Pack のコンポーネントです。

- [Azure Blob Storage](https://docs.microsoft.com/azure/storage/) アカウント。 SQL DW アップロード タスクは、Azure Blob Storage から Azure SQL Data Warehouse にデータを読み込みます。 Blob Storage に既に格納されているファイルから読み込むか、ローカル コンピューターからファイルを読み込むことができます。 ローカル コンピューター上のファイルを選択すると、SQL DW アップロード タスクはまず BLOB Storage にアップロードし、ステージングしてから、SQL Data Warehouse に読み込みます。

### <a name="add-and-configure-the-sql-dw-upload-task"></a>SQL DW アップロード タスクを追加および構成する

1. ツールボックスからデザイン画面の ( **[制御フロー]** タブの) 中央に SQL DW アップロード タスクをドラッグします。

2. タスクをダブル クリックして **SQL DW アップロード タスク エディター**を開きます。

    ![SQL DW アップロード タスク エディターの [全般] ページ](media/load-data-to-sql-data-warehouse/azure-sql-dw-upload-task-editor.png)

3. [Azure SQL DW アップロード タスク](control-flow/azure-sql-dw-upload-task.md)に関する記事のガイダンスを参照して、タスクを構成します。 このタスクで、ソースと変換先の両方の情報と、ソースと変換先のテーブル間のマップがカプセル化されるので、タスク エディターには構成する設定ページが複数あります。

### <a name="create-a-similar-solution-manually"></a>同様のソリューションを手動で作成する

さらに細かく制御するには、SQL DW アップロード タスクによって実行される作業をエミュレートするパッケージを手動で作成する方法があります。 

1. Azure Blob Upload Task を使用して、Azure Blob Storage でデータのステージングを行う。 Azure BLOB アップロード タスクを取得するには、[Microsoft SQL Server Integration Services Feature Pack for Azure][Microsoft SQL Server 2017 Integration Services Feature Pack for Azure] をダウンロードしてください。

2. 次に、SSIS の SQL 実行タスクを使用して、SQL Data Warehouse にデータを読み込む PolyBase スクリプトを起動します。 (SSIS を使用せずに) Azure Blob Storage から SQL Data Warehouse にデータを読み込む例については、「[チュートリアル:Azure SQL Data Warehouse へのデータの読み込み](/azure/sql-data-wAREHOUSE/load-data-wideworldimportersdw)」を参照してください。

## <a name="option-2---use-a-source-and-destination"></a>オプション 2 - ソースと変換先を使用する

2 つ目のアプローチは、ソースと変換先を含むデータ フロー タスクを使用する一般的なパッケージです。 このアプローチは、SQL Server と Azure SQL Data Warehouse を含む幅広いデータ ソースをサポートしています。

このチュートリアルでは、SQL Server をデータ ソースとして使用します。 SQL Server は、オンプレミスまたは Azure の仮想マシン上で実行されます。

SQL Server と SQL Data Warehouse に接続するには、ADO.NET 接続マネージャー、ソース、および変換先を使用するか、OLE DB 接続マネージャー、ソース、および変換先を使用できます。 ADO.NET の構成オプションは最小限なので、このチュートリアルでは ADO.NET を使用します。 OLE DB は、ADO.NET よりもパフォーマンスがやや優れています。

ショートカットとして、SQL Server インポートおよびエクスポート ウィザードを使用して基本パッケージを作成できます。 次にパッケージを保存し、Visual Studio または SSDT で開いて表示し、カスタマイズします。 詳しくは、「[SQL Server インポートおよびエクスポート ウィザードを使用してデータをインポートおよびエクスポートする](import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)」をご覧ください。

### <a name="prerequisites-for-option-2"></a>オプション 2 の前提条件

このオプションを選択してチュートリアルを続行するには、次の要素が必要です。

1. **サンプル データ**。 このチュートリアルでは、SQL Data Warehouse に読み込むソース データとして、SQL Server の AdventureWorks サンプル データベースに格納されているサンプル データを使用します。 AdventureWorks サンプル データベースを取得するには、「[AdventureWorks Sample Databases][AdventureWorks 2014 Sample Databases]」 (AdventureWorks サンプル データベース) を参照してください。

2. **ファイアウォール規則**。 SQL Data Warehouse にデータをアップロードするには、事前にローカル コンピューターの IP アドレスを使用して SQL Data Warehouse に対してファイアウォール規則を作成しておく必要があります。

### <a name="create-the-basic-data-flow"></a>基本的なデータ フローを作成する
1. ツールボックスからデザイン画面の中央にデータ フロー タスクをドラッグします ( **[制御フロー]** タブ上で)。
   
    ![][02]
2. [データ フロー タスク] をダブルクリックして [データ フロー] タブに切り替えます。
3. ツールボックスにあるその他のソースの一覧から、ADO.NET ソースをデザイン画面にドラッグします。 ソース アダプターが選択された状態で、 **[プロパティ]** ウィンドウでその名前を **SQL Server ソース**に変更します。
4. ツールボックスにあるその他の変換先の一覧から、ADO.NET 変換先をデザイン画面にドラッグし、ADO.NET ソースの下に配置します。 変換先アダプターが選択された状態で、 **[プロパティ]** ウィンドウでその名前を **SQL DW 変換先**に変更します。
   
    ![][09]

### <a name="configure-the-source-adapter"></a>ソース アダプターを構成する
1. ソース アダプターをダブルクリックして、**ADO.NET 変換元エディター**を開きます。
   
    ![][03]
2. **ADO.NET 変換元エディター**の **[接続マネージャー]** タブで、 **[ADO.NET 接続マネージャー]** リストの横にある **[新規]** ボタンをクリックして、 **[ADO.NET の接続マネージャーの構成]** ダイアログ ボックスを開き、このチュートリアルでのデータの読み込み元である SQL Server データベースに対する接続設定を作成します。
   
    ![][04]
3. **[ADO.NET 接続マネージャーの構成]** ダイアログ ボックスで、 **[新規]** ボタンをクリックして **[接続マネージャー]** ダイアログ ボックスを開き、新しいデータ接続を作成します。
   
    ![][05]
4. **[接続マネージャー]** ダイアログ ボックスで、次の操作を行います。
   
   1. **[プロバイダー]** で、SqlClient データ プロバイダーを選択します。
   2. **[サーバー名]** に SQL Server の名前を入力します。
   3. **[サーバー ログオン]** セクションで、認証情報を選択または入力します。
   4. **[データベースへの接続]** セクションで、AdventureWorks サンプル データベースを選択します。
   5. **[接続テスト]** をクリックします。
      
       ![][06]
   6. 接続テストの結果をレポートするダイアログ ボックスで、 **[OK]** をクリックして、 **[接続マネージャー]** ダイアログ ボックスに戻ります。
   7. **[接続マネージャー]** ダイアログ ボックスで、 **[OK]** をクリックして **[ADO.NET の接続マネージャーの構成]** ダイアログ ボックスに戻ります。
5. **[ADO.NET の接続マネージャーの構成]** ダイアログ ボックスで、 **[OK]** をクリックして、**ADO.NET 変換元エディター**に戻ります。
6. **ADO.NET 変換元エディター**の **[Name of the table or the view]\(テーブルまたはビューの名前\)** リストで、 **[Sales.SalesOrderDetail]** テーブルを選択します。
   
    ![][07]
7. **[プレビュー]** をクリックして、 **[クエリ結果のプレビュー]** ダイアログ ボックスにソース テーブルの先頭の 200 行のデータを表示します。
   
    ![][08]
8. **[クエリ結果のプレビュー]** ダイアログ ボックスで、 **[閉じる]** をクリックして **ADO.NET 変換元エディター**に戻ります。
9. **ADO.NET 変換元エディター**で、 **[OK]** をクリックしてデータ ソースの構成を完了します。

### <a name="connect-the-source-adapter-to-the-destination-adapter"></a>ソース アダプターを変換先アダプターに接続する
1. デザイン画面でソース アダプターを選択します。
2. ソース アダプターから延びている青い矢印を選択し、それが変換先エディターの所定の位置に固定されるまでドラッグします。
   
    ![][10]
   
    一般的な SSIS パッケージでは、ソースと変換先の間に SSIS ツールボックスからの他の複数のコンポーネントを使用して、データが SSIS データ フローを通過するときにデータの再構築、変換、およびクレンジングを行うことができます。 この例をできるだけ簡単に保持するには、ソースを直接変換先に接続します。

### <a name="configure-the-destination-adapter"></a>変換先アダプターを構成する
1. 変換先アダプターをダブルクリックして、**ADO.NET 変換先エディター**を開きます。
   
    ![][11]
2. **ADO.NET 変換先エディター**の **[接続マネージャー]** タブで、 **[接続マネージャー]** リストの横にある **[新規]** ボタンをクリックして、 **[ADO.NET の接続マネージャーの構成]** ダイアログ ボックスを開き、このチュートリアルでのデータの読み込み先である Azure SQL Data Warehouse データベースに対する接続設定を作成します。
3. **[ADO.NET 接続マネージャーの構成]** ダイアログ ボックスで、 **[新規]** ボタンをクリックして **[接続マネージャー]** ダイアログ ボックスを開き、新しいデータ接続を作成します。
4. **[接続マネージャー]** ダイアログ ボックスで、次の操作を行います。
   1. **[プロバイダー]** で、SqlClient データ プロバイダーを選択します。
   2. **[サーバー名]** に、SQL Data Warehouse の名前を入力します。
   3. **[サーバー ログオン]** セクションで、 **[SQL Server 認証を使用する]** を選択し、認証情報を選択または入力します。
   4. **[データベースへの接続]** セクションで、既存の SQL Data Warehouse データベースを選択します。
   5. **[接続テスト]** をクリックします。
   6. 接続テストの結果をレポートするダイアログ ボックスで、 **[OK]** をクリックして、 **[接続マネージャー]** ダイアログ ボックスに戻ります。
   7. **[接続マネージャー]** ダイアログ ボックスで、 **[OK]** をクリックして **[ADO.NET の接続マネージャーの構成]** ダイアログ ボックスに戻ります。
5. **[ADO.NET の接続マネージャーの構成]** ダイアログ ボックスで、 **[OK]** をクリックして、**ADO.NET 変換先エディター**に戻ります。
6. **ADO.NET 変換先エディター**で、 **[Use a table or view]\(テーブルまたはビューの使用\)** リストの横にある **[新規]** をクリックして **[テーブルの作成]** ダイアログ ボックスを開き、ソース テーブルと一致する列リストが含まれた新しい変換先テーブルを作成します。
   
    ![][12a]
7. **[テーブルの作成]** ダイアログ ボックスで、次の操作を行います。
   
   1. 変換先テーブルの名前を **SalesOrderDetail** に変更します。
   2. **rowguid** 列を削除します。 SQL Data Warehouse では、**uniqueidentifier** データ型はサポートされていません。
   3. **[LineTotal]** 列のデータ型を **[money]** に変更します。 SQL Data Warehouse では、**decimal** データ型はサポートされていません。 サポートされるデータ型に関する情報については、[CREATE TABLE (Azure SQL Data Warehouse、Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)] に関するページを参照してください。
      
       ![][12b]
   4. **[OK]** をクリックして、テーブルを作成し、**ADO.NET 変換先エディター**に戻ります。
8. **ADO.NET 変換先エディター**で、 **[マッピング]** タブを選択して、ソース内の列が変換先の列にどのようにマップされているか確認してください。
   
    ![][13]
9. **[OK]** をクリックして、変換先の構成を完了します。

## <a name="run-the-package-to-load-the-data"></a>パッケージを実行してデータを読み込む
ツールバーの **[開始]** ボタンをクリックするか、 **[デバッグ]** メニューの **[実行]** オプションのいずれかを選択してパッケージを実行します。

以下の段落では、この記事で説明した 2 つ目のオプション、つまりソースと変換先を含むデータ フローを使用してパッケージを作成した場合の表示について説明します。

パッケージが実行を開始すると、アクティビティを示す黄色の糸車と、これまでに処理された行数が表示されます。

![][14]

パッケージが実行を終了すると、成功したことを示す緑色のチェックマークと、ソースから変換先に読み込まれたデータの行数の合計が表示されます。

![][15]

これで、 SQL Server Integration Services を使用して Azure SQL Data Warehouse にデータを読み込むことに成功しました。

## <a name="next-steps"></a>次の手順

- デザイン環境でパッケージのデバッグおよびトラブルシューティングを行う方法について説明します。 こちらから開始:[パッケージ開発のトラブルシューティング ツール][Troubleshooting Tools for Package Development]。

- Integration Services サーバーまたは別の保存場所に SSIS プロジェクトおよびパッケージを配置する方法について説明します。 こちらから開始:[プロジェクトとパッケージの展開][Deployment of Projects and Packages]。

<!-- Image references -->
[01]:  ./media/load-data-to-sql-data-warehouse/ssis-designer-01.png
[02]:  ./media/load-data-to-sql-data-warehouse/ssis-data-flow-task-02.png
[03]:  ./media/load-data-to-sql-data-warehouse/ado-net-source-03.png
[04]:  ./media/load-data-to-sql-data-warehouse/ado-net-connection-manager-04.png
[05]:  ./media/load-data-to-sql-data-warehouse/ado-net-connection-05.png
[06]:  ./media/load-data-to-sql-data-warehouse/test-connection-06.png
[07]:  ./media/load-data-to-sql-data-warehouse/ado-net-source-07.png
[08]:  ./media/load-data-to-sql-data-warehouse/preview-data-08.png
[09]:  ./media/load-data-to-sql-data-warehouse/source-destination-09.png
[10]:  ./media/load-data-to-sql-data-warehouse/connect-source-destination-10.png
[11]:  ./media/load-data-to-sql-data-warehouse/ado-net-destination-11.png
[12a]: ./media/load-data-to-sql-data-warehouse/destination-query-before-12a.png
[12b]: ./media/load-data-to-sql-data-warehouse/destination-query-after-12b.png
[13]:  ./media/load-data-to-sql-data-warehouse/column-mapping-13.png
[14]:  ./media/load-data-to-sql-data-warehouse/package-running-14.png
[15]:  ./media/load-data-to-sql-data-warehouse/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: ../relational-databases/polybase/polybase-guide.md
[Download SQL Server Data Tools (SSDT)]: ../ssdt/download-sql-server-data-tools-ssdt.md
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: ../t-sql/statements/create-table-azure-sql-data-warehouse.md
[Data Flow]: ./data-flow/data-flow.md
[Troubleshooting Tools for Package Development]: ./troubleshooting/troubleshooting-tools-for-package-development.md
[Deployment of Projects and Packages]: ./packages/deploy-integration-services-ssis-projects-and-packages.md

<!--Other Web references-->
[Microsoft SQL Server 2017 Integration Services Feature Pack for Azure]: https://www.microsoft.com/download/details.aspx?id=54798
[SQL Server Evaluations]: https://www.microsoft.com/evalcenter/evaluate-sql-server-2017
[Visual Studio Community]: https://www.visualstudio.com/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks
