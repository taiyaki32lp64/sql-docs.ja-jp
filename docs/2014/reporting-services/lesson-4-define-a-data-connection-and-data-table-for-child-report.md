---
title: レッスン 4:子レポートのデータ接続とデータ テーブルの定義 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a6aa2c56-227c-43c5-a28e-c7104131ac5e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c1008202519f1d9bcbf48dfdc4cd4ef3a3cbbe20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108471"
---
# <a name="lesson-4-define-a-data-connection-and-data-table-for-child-report"></a>レッスン 4:子レポートのデータ接続とデータ テーブルを定義する
  親レポートを設計した後は、子レポートのデータ接続とデータ テーブルを作成します。 このチュートリアルでは、データ接続先として AdventureWorks2008 データベースを使用しますが、 AdventureWorks2012 データベースに接続することもできます。  
  
### <a name="to-define-a-data-connection-and-datatable-by-adding-a-dataset-for-child-report"></a>DataSet を追加してデータ接続と DataTable を定義するには (子レポート用)  
  
1.  **Web サイト** メニューのをクリックして**新しい項目の追加**します。  
  
2.  **新しい項目の追加**ダイアログ ボックスで、をクリックして**データセット**順にクリックします**追加**します。 項目を追加入力を求められたら、 **App_Code**フォルダーをクリックして**はい**します。  
  
     これにより、 **DataSet2.xsd** という新しい XSD ファイルがプロジェクトに追加され、データセット デザイナーが開きます。  
  
3.  [ツールボックス] ウィンドウから **TableAdapter** コントロールをデザイン画面にドラッグします。 これにより、 **TableAdapter** の構成ウィザードが起動します。  
  
4.  **データ接続の選択**] ページで [**新しい接続**します。  
  
5.  **[接続の追加]** ダイアログ ボックスで、次の手順を実行します。  
  
    1.  **サーバー名**ボックスに、サーバーを入力する場所、 **AdventureWorks2008**データベースがあります。  
  
         既定の SQL Server Express インスタンスは **(local)\sqlexpress**です。  
  
    2.  **[サーバーへのログオン]** セクションで、データへのアクセスを提供するオプションを選択します。 既定は **[Windows 認証を使用する]** です。  
  
    3.  **を選択するか、データベース名を入力**ドロップダウン リストでは、をクリックして**AdventureWorks2008**します。  
  
    4.  **[OK]** をクリックし、 **[次へ]** をクリックします。  
  
6.  手順 5. (b) で **[SQL Server 認証を使用する]** を選択した場合は、機密データを文字列に含めるか、またはその情報をアプリケーション コードで設定するかどうかを指定するオプションを選択します。  
  
7.  **アプリケーション構成ファイルへの接続文字列を保存**ページで、接続文字列の名前を入力するか、既定**AdventureWorks2008ConnectionString**します。 **[次へ]** をクリックします。  
  
8.  **コマンドの種類を選択**] ページで、[ **SQL ステートメントを使用**、順にクリックします**次**します。  
  
9. **SQL ステートメントを入力します**ページで、データを取得する次の TRANSACT-SQL クエリを入力、 **AdventureWorks2008**データベースをクリックして **[次へ]** 。  
  
    ```  
    SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail  
    ```  
  
     クリックして、クエリを作成することもできます。**クエリ ビルダー**、クリックして、クエリを確認し**クエリの実行**ボタンをクリックします。 クエリを実行したときに期待したデータが返されない場合は、以前のバージョンの AdventureWorks を使用している可能性があります。 インストールの詳細については、 **AdventureWorks2008**のバージョンの AdventureWorks を参照してください[チュートリアル。AdventureWorks データベースのインストール](https://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx)します。  
  
10. **生成するメソッドの選択**をオフにします ページで、 **(GenerateDBDirectMethods) データベースに直接更新を送信するためのメソッドを作成**、順にクリックします**完了**。  
  
     ADO.NET の構成が完了するようになりました[DataTable](https://msdn.microsoft.com/library/system.data.datatable\(v=vs.100\).aspx)レポートのデータ ソースとして。 Visual Studio の [データセット デザイナー] ページに、追加した **DataTable** にクエリで指定した列が表示されます。 DataSet2 には、クエリに基づいて PurhcaseOrderDetail テーブルのデータが含まれています。  
  
11. ファイルを保存します。  
  
12. データをプレビューするには、次のようにクリックします。**データのプレビュー**上、**データ** メニューをクリック**プレビュー**します。  
  
## <a name="next-task"></a>次の作業  
 これで、子レポートのデータ接続とデータ テーブルを作成できました。 次は、レポート ウィザードを使用して子レポートを設計します。  
  
  
