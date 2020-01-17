---
title: 方法:データベース オブジェクトをデバッグする | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: f5d4584f-e85f-4558-b056-83681c365978
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 57854937595ba57dee8c36bd4877fd05362f2e40
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035197"
---
# <a name="how-to-debug-database-objects"></a>方法:データベース オブジェクトをデバッグする
SQL Server 単体テストは次の内容で構成されています。  
  
-   Visual C\# または Visual Basic で記述された単体テスト コード。 SQL Server 単体テスト デザイナーによって生成されるこのコードは、テストの本文を構成する Transact\-SQL スクリプトを送信します。  
  
-   Visual C\# または Visual Basic で記述された 1 つ以上のテスト条件。 テスト条件をデバッグするには、「[方法:テストの実行中にデバッグする (Visual Studio 2010)](https://msdn.microsoft.com/library/ms182484(VS.100).aspx)」または「[方法:テストの実行中にデバッグする (Visual Studio 2012)](https://msdn.microsoft.com/library/ms182484.aspx)」で説明されている単体テストのデバッグ手順に従ってください。  
  
-   テスト対象のデータベースのオブジェクトに対して実行される 1 つ以上の Transact\-SQL スクリプト。 これらの Transact\-SQL スクリプトをデバッグすることはできません。  
  
ここでは、テスト対象のデータベースのストアド プロシージャ、関数、トリガーなど、特定のデータベース オブジェクトをデバッグする方法について説明します。 データベース オブジェクトをデバッグするには、以下の手順を次の順序で実行します。  
  
1.  テスト プロジェクトで SQL Server デバッグを有効にします。  
  
2.  テスト対象のデータベースをホストする SQL Server インスタンスでアプリケーション デバッグを有効にします。  
  
3.  デバッグするデータベース オブジェクトの Transact\-SQL スクリプトにブレークポイントを設定します。  
  
4.  単体テストをデバッグします。 この手順では、デバッグ モードでテストを実行します。  
  
### <a name="to-enable-sql-debugging-on-your-test-project"></a>テスト プロジェクトで SQL デバッグを有効にするには  
  
1.  **ソリューション エクスプローラー**を開きます。  
  
2.  **ソリューション エクスプローラー**で、テスト プロジェクトを右クリックし、 **[プロパティ]** をクリックします。  
  
    テスト プロジェクトと同じ名前のプロパティ ページが開きます。  
  
3.  プロパティ ページで **[デバッグ]** をクリックします。  
  
4.  **[デバッガーを有効にする]** で、 **[SQL Server デバッグを有効にする]** をクリックします。  
  
5.  変更を保存します。  
  
### <a name="to-set-an-increased-execution-context-timeout-to-enable-debugging-for-your-test-project"></a>増加した実行コンテキスト タイムアウトを設定してテスト プロジェクトのデバッグを有効にするには  
  
1.  **[ファイル]** メニューの **[開く]** をポイントし、 **[ファイル]** をクリックします。  
  
2.  テスト プロジェクトを含むフォルダーを参照し、app.config ファイルをダブルクリックします。  
  
    エディターで app.config ファイルが開きます。  
  
3.  次の例のように、ExecutionContext ノードを変更してコマンド タイムアウトを追加します。  
  
    ```  
    <ExecutionContext CommandTimeout ="300" Provider="System.Data.SqlClient" ConnectionString="Data Source=TargetServerName\TargetInstanceName;Initial Catalog=TargetDatabaseName;Integrated Security=True;Pooling=False" />  
    ```  
  
4.  変更を保存します。  
  
5.  単体テスト プロジェクトをリビルドします。  
  
> [!IMPORTANT]  
> プロジェクトをリビルドしないと、app.config に対して行った変更が単体テストの実行時に適用されず、デバッグは失敗します。  
  
### <a name="to-add-breakpoints-to-your-transact-sql-script"></a>Transact\-SQL スクリプトにブレークポイントを追加するには  
  
1.  **[表示]** メニューで **SQL Server オブジェクト エクスプローラー**を開きます。  
  
2.  **[データ接続]** で、テストするデータベースのノードを展開します。  
  
3.  データベースのアイコンの横に小さな赤い 'x' が表示されている場合は、データベースへの接続が閉じられています。 その場合は、データベースを右クリックして、 **[更新]** をクリックします。 データベースへの接続を開くには、資格情報の指定が必要な場合があります。  
  
4.  **[ビュー]** 、 **[ストアド プロシージャ]** 、または **[関数]** ノードを展開し、デバッグするオブジェクトを検索します。  
  
5.  デバッグするオブジェクトをダブルクリックします。  
  
6.  グレーのサイドバーをクリックして、ブレークポイントを設定します。  
  
### <a name="to-debug-your-sql-server-unit-test"></a>SQL Server 単体テストをデバッグするには  
  
1.  Visual Studio 2010 では、 **[テスト ビュー]** ウィンドウ ([テスト] -> [ウィンドウ]) を開きます。 Visual Studio 2012 では、 **[テスト エクスプローラー]** ウィンドウを開きます。  
  
2.  ブレークポイントを設定したデータベース オブジェクトを使用する Transact\-SQL スクリプトを含むテストを右クリックし、 **[選択範囲のデバッグ]** を選択します。  
  
    データベース オブジェクトのブレークポイントに到達するまで、デバッグ モードでテストが実行されます。  
  
3.  (省略可能) 別のデバッグ ウィンドウを開くには、 **[デバッグ]** メニューを開き、 **[ウィンドウ]** をポイントします。次に、 **[ブレークポイント]** 、 **[出力]** 、または **[イミディエイト]** をクリックします。  
  
## <a name="see-also"></a>参照  
[SQL Server の単体テストの実行](../ssdt/running-sql-server-unit-tests.md)  
[Transact-SQL のデバッグ (Visual Studio 2010)](https://go.microsoft.com/fwlink/?LinkId=163975)  
  
