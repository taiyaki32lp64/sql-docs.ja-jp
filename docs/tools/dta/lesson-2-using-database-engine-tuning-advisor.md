---
title: 'レッスン 2: データベース エンジン チューニング アドバイザーの使用 | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 3317d4f8-ed9e-4f2e-b5f1-a6bf3a9d6c8d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b2f526510f69a91e3228431953f73717790246f9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68034741"
---
# <a name="lesson-2-using-database-engine-tuning-advisor"></a>レッスン 2 : データベース エンジン チューニング アドバイザーの使用
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
データベース エンジン チューニング アドバイザーでは、データベースをチューニングできるほか、チューニング セッションを管理し、チューニング推奨設定を表示できます。 物理的な設計構造についての高度な知識があれば、このツールを使用して予備的なデータベース チューニング分析を実行できます。 また、データベース チューニングの知識があまりない場合でも、チューニングするワークロードに最適な物理設計構造を見つけられます。 データベース エンジン チューニング アドバイザーのグラフィカル ユーザー インターフェイスを初めて使用するデータベース管理者、および物理設計構造についての広範な知識をお持ちでないシステム管理者のために、このレッスンでは基本的な操作について説明します。  

## <a name="prerequisites"></a>Prerequisites 

このチュートリアルを実行するには、SQL Server Management Studio、SQL Server を実行しているサーバーへのアクセス、および AdventureWorks データベースが必要です。

- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) をインストールします。
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads) をインストールします。
- [AdventureWorks2017 サンプル データベース](https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017)をダウンロードします。


SSMS でデータベースを復元する手順については、[データベースの復元](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms?view=sql-server-2017)に関するページをご覧ください。

  >[!NOTE]
  > このチュートリアルは、SQL Server Management Studio と基本的なデータベース管理タスクの使用に慣れているユーザーを対象としています。 
  
## <a name="tuning-a-workload"></a>ワークロードのチューニング
データベース エンジン チューニング アドバイザーでは、チューニング用に選択したデータベースおよびテーブルについて、最適なクエリ パフォーマンスが得られる物理データベース設計を見つけることができます。  

1.  サンプルの[select](../../t-sql/queries/select-examples-transact-sql.md)ステートメントをコピーし、ステートメントをの[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]クエリエディターに貼り付けます。 このファイルを、探しやすいディレクトリに **MyScript.sql** という名前で保存します。 AdventureWorks2017 データベースに対して動作する例を以下に示します。  

 ```sql
 Use [Adventureworks2017]; -- may need to modify database name to match database
 GO
 SELECT DISTINCT pp.LastName, pp.FirstName 
 FROM Person.Person pp JOIN HumanResources.Employee e
 ON e.BusinessEntityID = pp.BusinessEntityID WHERE pp.BusinessEntityID IN 
 (SELECT SalesPersonID 
 FROM Sales.SalesOrderHeader
 WHERE SalesOrderID IN 
 (SELECT SalesOrderID 
 FROM Sales.SalesOrderDetail
 WHERE ProductID IN 
 (SELECT ProductID 
 FROM Production.Product p 
 WHERE ProductNumber = 'BK-M68B-42')));
 GO
 ```

  ![SQL クエリの保存](media/dta-tutorials/dta-save-query.png)
  
2.  データベース エンジン チューニング アドバイザーを起動します。 SQL Server Management Studio (SSMS) の **[ツール]** メニューから **[データベースチューニングアドバイザー]** を選択します。  詳細については、[データベース エンジン チューニング アドバイザーの起動](lesson-1-basic-navigation-in-database-engine-tuning-advisor.md#launch-database-tuning-advisor)に関する記事をご覧ください。 **[サーバーへの接続]** ダイアログボックスで、SQL Server に接続します。  
  
3.  データベース エンジン チューニング アドバイザー GUI の右側ペインにある **[全般]** タブで、 **[セッション名]** に「**MySession**」と入力します。 
  
4.  **ワークロード**の **[ファイル]** を選択し、双眼鏡アイコンを選択して、**ワークロードファイルを参照**します。 手順 1. で保存した**myscript.sql**ファイルを見つけます。  

   ![以前に保存されたスクリプトの検索](media/dta-tutorials/dta-script.png)
  
5.  **[ワークロード分析用のデータベース]** の一覧で [AdventureWorks2017] を選択し、 **[チューニングするデータベースとテーブルの選択]** グリッドで [AdventureWorks2017] を選択し、 **[チューニング ログを保存する]** を選択します。 **[ワークロード分析用のデータベース]** では、データベース エンジン チューニング アドバイザーがワークロードのチューニング時に最初に接続するデータベースを指定します。 チューニングの開始後に、データベース チューニング アドバイザーは、ワークロードに含まれる `USE DATABASE` ステートメントで指定されたデータベースに接続します。  

  ![Db の DTA オプション](media/dta-tutorials/dta-select-db.png)
  
6.  **[チューニング オプション]** タブをクリックします。この実習ではチューニング オプションを設定しませんが、既定のチューニング オプションをひととおり確認してください。 このタブ ページのヘルプを表示するには、F1 キーを押します。 詳細なチューニング オプションを表示するには、 **[詳細設定オプション]** をクリックします。 **[チューニング オプションの詳細設定]** ダイアログ ボックスに表示されているチューニング オプションの情報を表示するには、このダイアログ ボックスの **[ヘルプ]** をクリックします。 既定のオプションを選択したまま **[キャンセル]** をクリックし、 **[チューニング オプションの詳細設定]** ダイアログ ボックスを閉じます。  

  ![DTA チューニング オプション](media/dta-tutorials/dta-tuning-options.png)
  
7.  ツール バーの **[分析の開始]** ボタンをクリックします。 ワークロードの分析中は、 **[進行状況]** タブで実行状況を監視できます。チューニングが完了すると **[推奨設定]** タブが表示されます。  
  
    チューニング停止の日付と時刻に関してエラーが発生する場合は、 **[チューニング オプション]** タブの **[停止時刻]** の時間を確認します。 **[停止時刻]** の日付と時刻が現在の日付と時刻よりも後になっていることを確認し、必要に応じて変更します。  

  ![DTA 分析の開始](media/dta-tutorials/dta-start-analysis.png)

  
8.  分析が完了したら、 [!INCLUDE[tsql](../../includes/tsql-md.md)] [アクション] **メニューの** [推奨設定の保存] **をクリックし、推奨設定を** スクリプトとして保存します。 **[名前を付けて保存]** ダイアログ ボックスで推奨設定スクリプトを保存するディレクトリに移動し、ファイル名として「 **MyRecommendations**」と入力します。  

  ![DTA の推奨事項を保存する](media/dta-tutorials/dta-save-recommendations.png)

## <a name="view-tuning-recommendations"></a>チューニング推奨設定の表示
  
1.  **[推奨設定]** タブで、 **[推奨インデックス]** のすべての列を表示するには、このページの下部にあるスクロール バーを使用します。 各行は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーによって削除または作成が推奨されているデータベース オブジェクト (インデックスまたはインデックス ビュー) です。 右端の列までスクロールし、 **[定義]** をクリックします。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] **[SQL スクリプトのプレビュー]** ウィンドウが表示されます。このウィンドウには、その行のデータベース オブジェクトを作成または削除する [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトが表示されます。 **[閉じる]** をクリックし、プレビュー ウィンドウを閉じます。  
  
    リンクを含む **[定義]** を見つけにくい場合は、タブ付きページの下部にある **[既存のオブジェクトを表示する]** チェック ボックスをオフにすると、表示される行数が少なくなり、 推奨設定が生成されたオブジェクトのみが [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーに表示されます。 **[既存のオブジェクトを表示する]** チェック ボックスをオンにすると、現在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースに存在するすべてのデータベース オブジェクトが表示されます。 タブ ページ右側のスクロール バーを使用し、すべてのオブジェクトを表示します。

  ![DTA インデックスの推奨事項](media/dta-tutorials/dta-recommendation.png)  
  
2.  **[推奨インデックス]** ペインのグリッドを右クリックします。 このとき表示されるメニューでは、推奨設定を選択または選択解除できます。 また、グリッド テキストのフォントも変更できます。  
 
   ![インデックスの推奨事項の選択メニュー](media/dta-tutorials/dta-index-recommendation-options.png)
  
3.  **[アクション]** メニューの **[推奨設定の保存]** をクリックし、すべての推奨設定を 1 つの [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトに保存します。 このスクリプトの名前として、「 **MySessionRecommendations.sql**」と入力します。  
  
    [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のクエリ エディターで MySessionRecommendations.sql を開き、スクリプトを表示します。 クエリ エディターでこのスクリプトを実行すれば、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースに推奨設定を適用することができますが、ここでは実行しません。 クエリ エディターのスクリプトを実行せずに閉じます。  
  
    また、 **チューニング アドバイザーの** [アクション] **メニューで** [推奨設定の適用] [!INCLUDE[ssDE](../../includes/ssde-md.md)] をクリックし、推奨設定を適用することもできます。しかし、この演習ではこれらの推奨設定は適用しません。  
  
4.  **[推奨設定]** タブに複数の推奨が存在する場合は、 **[推奨インデックス]** グリッドにデータベース オブジェクトが一覧表示されます。この中のいくつかの行をオフにします。  
  
5.  **[アクション]** メニューの **[推奨設定の評価]** をクリックします。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 新しいチューニング セッションが作成されます。ここで、MySession の元の推奨設定の一部を評価することができます。  
  
6.  新しいセッションの **[セッション名]** に「 **EvaluateMySession**」と入力し、ツール バーの **[分析の開始]** ボタンをクリックします。 この新しいセッションに対して手順 2. ～ 3. を繰り返し、推奨設定を表示します。  
  
### <a name="summary"></a>[概要]  
チューニング セッションを実行した後で、チューニング オプションを変更する必要があるとわかった場合は、チューニング推奨設定の一部を評価することができます。 たとえば、最初は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーでインデックス付きビューを考慮するようにチューニング オプションを指定したものの、推奨設定を生成した後で、やはりインデックス付きビューを使用しないことにしたとします。 このような場合、 **[アクション]** メニューの **[推奨設定の評価]** を使用すると、[!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーでインデックス付きビューを考慮せずにセッションを再評価できます。 **[推奨設定の評価]** を実行すると、以前に生成した推奨設定が現在の物理構造に仮想的に適用され、その状態から次のチューニング セッションを実行できるようになります。  
  
チューニング結果の詳細な情報は、このレッスンの次の作業で説明する **[レポート]** タブに表示されます。  

## <a name="view-tuning-reports"></a>チューニング レポートの表示
スクリプトを表示する機能は、チューニング結果の実装に利用できるため便利ですが、データベース エンジン チューニング アドバイザーにはこの他にも便利なレポートが多数用意されています。 これらのレポートは、チューニングするデータベースの既存の物理設計構造、および推奨される構造に関する情報を提供します。 次の実習で説明するように、チューニング レポートを表示するには **[レポート]** タブをクリックします。


1. データベースチューニングアドバイザーの **[レポート]** タブを選択します。 
2. **[チューニング サマリー]** ペインに、このチューニング セッションに関する情報が表示されます。 このペインの内容をすべて表示するには、スクロール バーを使用します。 **[予測向上率]** と **[推奨構成で使用される容量]** を確認してください。 チューニング オプションを設定する際、推奨設定が使用する容量を制限できます。 **[チューニング オプション]** タブで、 **[詳細設定オプション]** を選択します。 **[推奨インデックス用の最大領域を定義する]** チェック ボックスをオンにし、推奨構成で使用できる最大領域を MB 単位で指定します。 このチュートリアルに戻るには、ヘルプ ブラウザーの **[戻る]** ボタンを使用します。 

    ![DTA チューニング サマリー](media/dta-tutorials/dta-tuning-summary.png)
  
3.  **[チューニング レポート]** ペインで、 **[レポートの選択]** ボックスの一覧から **[ステートメント コスト レポート]** を選択します。 レポートを表示するためのスペースがさらに必要な場合は、 **[セッション モニター]** ペインの境界を左方向にドラッグします。 データベース内のテーブルに対して実行される [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのパフォーマンス コストは、ステートメントによって異なります。 テーブル内で、アクセス頻度の高い列に有効なインデックスを作成することによって、このパフォーマンス コストを軽減できます。 このレポートは、ワークロードでの元のステートメント実行コストと、チューニング推奨設定の実装後のコストを比較し、予測向上率を示します。 このレポートに表示される情報量は、ワークロードの規模と複雑さに左右されます。  

    ![DTA レポート-ステートメントコスト](media/dta-tutorials/dta-statement-cost.png)
  
4.  グリッド領域で **ステートメント コスト レポート** を右クリックし、 **[ファイルへエクスポート]** をクリックします。 「 **MyReport**」という名前でレポートを保存します。 ファイル名には、拡張子 .xml が自動的に付加されます。 使い慣れた XML エディターまたは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で MyReport.xml を開き、レポートの内容を表示できます。  
  
5.  データベース エンジン チューニング アドバイザーの **[レポート]** タブに戻り、再び **ステートメント コスト レポート** 右クリックします。 使用できるその他のオプションを確認してください。 表示しているレポートのフォントを変更することも可能です。 ここでフォントを変更すると、他のタブ付きページのフォントも変更されます。  
  
6.  **[レポートの選択]** ボックスの一覧で他のレポートをクリックし、どのようなレポートが表示されるかを確認してください。  
  
### <a name="summary"></a>[概要]  
データベース エンジン チューニング アドバイザー GUI の **[レポート]** タブを使用し、MySession チューニング セッションを検証しました。 同様の手順で、EvaluateMySession チューニング セッションで生成したレポートを調べることができます。 このレポートの内容を検証するには、 **[セッション モニター]** ペインの **[EvaluateMySession]** をダブルクリックします。  


 ## <a name="next-lesson"></a>次のレッスン  
[レッスン 3: DTA コマンド プロンプト ユーティリティの使用](../../tools/dta/lesson-3-using-the-dta-command-prompt-utility.md)  
   
  
  
