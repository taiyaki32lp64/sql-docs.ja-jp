---
title: 'レッスン 2: 親レポートのデータ接続とデータ テーブルを定義する | Microsoft Docs'
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: f02dee0c-85ad-45d4-b707-10e9e8541db9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e8bcfe976a8094c6faa22d8aab3db8a4a833d8cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62651600"
---
# <a name="lesson-2-define-a-data-connection-and-data-table-for-parent-report"></a>レッスン 2: 親レポートのデータ接続とデータ テーブルを定義する
Visual C# 用の ASP.NET Web サイト テンプレートを使用して新しい Web サイト プロジェクトを作成した後は、親レポートのデータ接続とデータ テーブルを作成します。 このチュートリアルでは、データ接続先として AdventureWorks2014 データベースを使用します。  
  
## <a name="to-define-a-data-connection-and-data-table-by-adding-a-dataset-for-parent-report"></a>DataSet を追加してデータ接続とデータ テーブルを定義するには (親レポート用)  
  
1.  **[Web サイト]** メニューの **[新しい項目の追加]** を選択します。  
  
2.  **[新しい項目の追加]** ダイアログ ボックスで、 **[DataSet]** をクリックし、 **[追加]** を選択します。 メッセージが表示されたら、 **[はい]** を選択して **App_Code**フォルダーに項目を追加します。  
  
    これにより、 **DataSet1.xsd** という新しい XSD ファイルがプロジェクトに追加され、データセット デザイナーが開きます。  
  
3.  [ツールボックス] ウィンドウから **[TableAdapter](/visualstudio/data-tools/fill-datasets-by-using-tableadapters)** コントロールをデザイン画面にドラッグします。 これにより、 **TableAdapter** の構成ウィザードが起動します。  
  
4.  **[データ接続の選択]** ページで、 **[新しい接続]** をクリックします。  
  
5.  Visual Studio で初めてデータ ソースを作成する場合は、 **[データ ソースの選択]** ページが表示されます。 **[データ ソース]** ボックスで、 **[Microsoft SQL Server]** を選択します。  
  
6.  **[接続の追加]** ダイアログ ボックスで、次の手順を実行します。  
  
    1.  **[サーバー名]** ボックスに、 **AdventureWorks2014** データベースが存在するサーバーを入力します。  
  
        既定の SQL Server Express インスタンスは **(local)\sqlexpress**です。  
  
    2.  **[サーバーへのログオン]** セクションで、データへのアクセスを提供するオプションを選択します。 既定は **[Windows 認証を使用する]** です。  
  
    3.  **[データベース名の選択または入力]** ドロップダウン リストで、 **[AdventureWorks2014]** を選択します。  
  
    4.  **[OK]** を選択し、 **[次へ]** を選択します。  
  
7.  手順 6. (b) で **[SQL Server 認証を使用する]** を選択した場合は、機密データを文字列に含めるか、またはその情報をアプリケーション コードで設定するかどうかを指定するオプションを選択します。  
  
8.  **[接続文字列をアプリケーション構成ファイルに保存する]** ページで、接続文字列の名前を入力するか、既定値の **AdventureWorks2014ConnectionString**をそのまま使用します。 **[次へ]** を選択します。  
  
9. **[コマンドの種類を選択します]** ページで、 **[SQL ステートメントを使用する]** を選択し、 **[次へ]** を選択します。  
  
10. **[SQL ステートメントの入力]** ページで、 **AdventureWorks2014** データベースからデータを取得するための次の Transact-SQL クエリを入力し、 **[次へ]** を選択します。  
  
    ```  
    SELECT ProductID, Name, ProductNumber, SafetyStockLevel, ReorderPoint FROM  Production.Product Order By ProductID  
    ```  
  
    また、 **[クエリ ビルダー]** を選択してクエリを作成し、 **[クエリの実行]** を選択してクエリを確認することもできます。 クエリを実行したときに期待したデータが返されない場合は、以前のバージョンの AdventureWorks を使用している可能性があります。 **AdventureWorks2014** サンプル データベースの取得方法の詳細については、「[AdventureWorks sample databases](https://github.com/Microsoft/sql-server-samples/releases)」 (AdventureWorks のサンプル データベース) を参照してください。  
  
11. **[生成するメソッドの選択]** ページで、 **[更新を直接データベースに送信するためのメソッドを作成する (GenerateDBDirectMethods)]** チェック ボックスをオフにし、 **[完了]** を選択します。  
  
    > [!WARNING]  
    > **[更新を直接データベースに送信するためのメソッドを作成する (GenerateDBDirectMethods)]** は、必ずオフにしてください。  
  
    これで、レポートのデータ ソースとしての ADO.NET DataTable オブジェクトの構成が完了しました。 Visual Studio の [データセット デザイナー] ページに、追加した DataTable オブジェクトにクエリで指定した列が表示されます。 DataSet1 には、クエリに基づいて Product テーブルのデータが含まれています。  
  
12. ファイルを保存します。  
  
13. データをプレビューするには、 **[データ]** メニューの **[データのプレビュー]** を選択し、 **[プレビュー]** を選択します。  
  
## <a name="next-task"></a>次の作業  
これで、親レポートのデータ接続とデータ テーブルを作成できました。 次は、レポート ウィザードを使用して親レポートを設計します。 「 [レッスン 3: レポート ウィザードを使用して親レポートを設計する](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)」を参照してください。  
  

