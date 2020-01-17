---
title: レッスン 2:親レポートのデータ接続とデータ テーブルの定義 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f02dee0c-85ad-45d4-b707-10e9e8541db9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 987e6924fe3fbffb416e4266861ae7cfede16596
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108496"
---
# <a name="lesson-2-define-a-data-connection-and-data-table-for-parent-report"></a>レッスン 2:親レポートのデータ接続とデータ テーブルを定義する
  Visual C# 用の ASP.NET Web サイト テンプレートを使用して新しい Web サイト プロジェクトを作成した後は、親レポートのデータ接続とデータ テーブルを作成します。 このチュートリアルでは、データ接続先として AdventureWorks2008 データベースを使用しますが、 AdventureWorks2012 データベースに接続することもできます。  
  
### <a name="to-define-a-data-connection-and-data-table-by-adding-a-dataset-for-parent-report"></a>DataSet を追加してデータ接続とデータ テーブルを定義するには (親レポート用)  
  
1.  **[Web サイト]** メニューの **[新しい項目の追加]** を選択します。  
  
2.  **新しい項目の追加**ダイアログ ボックスで、**データセット**クリック**追加**します。 入力を求められたら、項目を追加する必要があります、 **App_Code**フォルダーをクリックして**はい**。  
  
     これにより、 **DataSet1.xsd** という新しい XSD ファイルがプロジェクトに追加され、データセット デザイナーが開きます。  
  
3.  [ツールボックス] ウィンドウから **[TableAdapter](https://msdn.microsoft.com/library/bz9tthwx\(v=vs.100\).aspx)** コントロールをデザイン画面にドラッグします。 これにより、 **TableAdapter** の構成ウィザードが起動します。  
  
4.  **データ接続の選択**] ページで [**新しい接続**します。  
  
5.  Visual Studio で初めてデータ ソースを作成する場合は、 **[データ ソースの選択]** ページが表示されます。 **[データ ソース]** ボックスで、 **[Microsoft SQL Server]** を選択します。  
  
6.  **[接続の追加]** ダイアログ ボックスで、次の手順を実行します。  
  
    1.  **サーバー名**ボックスに、サーバーを入力する場所、 **AdventureWorks2008**データベースがあります。  
  
         既定の SQL Server Express インスタンスは **(local)\sqlexpress**です。  
  
    2.  **[サーバーへのログオン]** セクションで、データへのアクセスを提供するオプションを選択します。 既定は **[Windows 認証を使用する]** です。  
  
    3.  **を選択するか、データベース名を入力**ドロップダウン リストでは、をクリックして**AdventureWorks2008**します。  
  
    4.  **[OK]** をクリックし、 **[次へ]** をクリックします。  
  
7.  手順 6. (b) で **[SQL Server 認証を使用する]** を選択した場合は、機密データを文字列に含めるか、またはその情報をアプリケーション コードで設定するかどうかを指定するオプションを選択します。  
  
8.  **アプリケーション構成ファイルへの接続文字列を保存**ページで、接続文字列の名前を入力するか、既定**AdventureWorks2008ConnectionString**します。 **[次へ]** をクリックします。  
  
9. **コマンドの種類を選択**] ページで、[ **SQL ステートメントを使用**、順にクリックします**次**します。  
  
10. **SQL ステートメントを入力します**ページで、データを取得する次の TRANSACT-SQL クエリを入力、 **AdventureWorks2008**データベースをクリックして **[次へ]** 。  
  
    ```  
    SELECT ProductID, Name, ProductNumber, SafetyStockLevel, ReorderPoint FROM  Production.Product Order By ProductID  
    ```  
  
     クリックして、クエリを作成することもできます。**クエリ ビルダー**、クリックして、クエリを確認および**クエリの実行**します。 クエリを実行したときに期待したデータが返されない場合は、以前のバージョンの AdventureWorks を使用している可能性があります。 インストールの詳細については、 **AdventureWorks2008**のバージョンの AdventureWorks を参照してください[チュートリアル。AdventureWorks データベースのインストール](https://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx)します。  
  
11. **生成するメソッドの選択**オフにしてください ページで、 **(GenerateDBDirectMethods) データベースに直接更新を送信するためのメソッドを作成する**、順にクリックします**を完了**.  
  
    > [!WARNING]  
    >  必ずこのチェック ボックスをオフにしてください。  
  
     これで、レポートのデータ ソースとしての ADO.NET DataTable オブジェクトの構成が完了しました。 Visual Studio の [データセット デザイナー] ページに、追加した DataTable オブジェクトにクエリで指定した列が表示されます。 DataSet1 には、クエリに基づいて Product テーブルのデータが含まれています。  
  
12. ファイルを保存します。  
  
13. データをプレビューするには、次のようにクリックします。**データのプレビュー**上、**データ** メニューをクリック**プレビュー**します。  
  
## <a name="next-task"></a>次の作業  
 これで、親レポートのデータ接続とデータ テーブルを作成できました。 次は、レポート ウィザードを使用して親レポートを設計します。  
  
  
