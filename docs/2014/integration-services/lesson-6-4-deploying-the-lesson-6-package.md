---
title: 手順 4:レッスン 6 パッケージの展開 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b613cef7-7993-4d89-a429-a8251d74d435
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0e04a36ca687c57daae2f286025add57a32632c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767334"
---
# <a name="step-4-deploying-the-lesson-6-package"></a>手順 4:レッスン 6 のパッケージの展開
  パッケージを配置するには、SQL Server インスタンスの Integration Services の SSISDB カタログにパッケージを追加する必要があります。 このレッスンでは、SSISDB カタログへのレッスン 6 パッケージの追加、パラメーターの設定、パッケージの実行を行います。 このレッスンでは、SQL Server Management Studio を使用して SSISDB カタログにレッスン 6 パッケージを追加し、パッケージを配置します。 パッケージを配置したら、新しい場所を指すようにパラメーターを変更し、パッケージを実行します。  
  
 このレッスンの内容  
  
-   SQL Server の SSIS ノードの SSISDB カタログにパッケージを追加します。  
  
-   パッケージを配置します。  
  
-   パッケージ パラメーターの値を設定します。  
  
-   SSMS でパッケージを実行します。  
  
### <a name="to-locate-or-add-the-ssisdb-catalog"></a>SSISDB カタログを検索または追加するには  
  
1.  [スタート] ボタンをクリックし、[すべてのプログラム]、[Microsoft SQL Server] の順にポイントし、[SQL Server Management Studio] をクリックします。  
  
2.  [サーバーへの接続] ダイアログ ボックスで既定の設定を確認し、[接続] をクリックします。 接続を確立するには、[サーバー名] ボックスに、SQL Server がインストールされているコンピューターの名前が入力されている必要があります。 データベース エンジンが名前付きインスタンスの場合は、[サーバー名] ボックスに、<computer_name>\\<instance_name> 形式でインスタンス名も指定します。  
  
3.  オブジェクト エクスプ ローラーで、[Integration Services カタログ] を展開します。  
  
4.  [Integration Services カタログ] の下にカタログが表示されない場合は、SSISDB カタログを追加します。  
  
5.  SSISDB カタログを追加するには、[Integration Services カタログ] を右クリックし、[カタログの作成] をクリックします。  
  
6.  [カタログの作成] ダイアログ ボックスで、[CLR 統合を有効にする] を選択します。  
  
7.  [パスワード] ボックスに新しいパスワードを入力し、[パスワードの再入力] ボックスにもう一度入力します。 入力したパスワードを忘れないようにしてください。  
  
8.  [OK] をクリックして SSISDB カタログを追加します。  
  
### <a name="to-add-the-package-to-the-ssisdb-catalog"></a>SSISDB カタログにパッケージを追加するには  
  
1.  オブジェクト エクスプ ローラーで、[SSISDB] を右クリックし、[フォルダーの作成] をクリックします。  
  
2.  [フォルダーの作成] ダイアログ ボックスで、[フォルダー名] ボックスに「SSIS Tutorial」と入力し、[OK] をクリックします。  
  
3.  SSIS Tutorial フォルダーを展開し、[プロジェクト] を右クリックし、[パッケージのインポート] をクリックします。  
  
4.  [Integration Services プロジェクトの変換ウィザードの概要] ページで、[次へ] をクリックします。  
  
5.  [パッケージの検索] ページの [ソース] の一覧で、ファイル システムが選択されていることを確認し、[参照] をクリックします。  
  
6.  [フォルダーの参照] ダイアログ ボックスで、SSIS Tutorial プロジェクトを含むフォルダーに移動し、[OK] をクリックします。  
  
7.  [次へ] をクリックします。  
  
8.  [パッケージの選択] ページに SSIS Tutorial の 6 つパッケージがすべて表示されます。 [パッケージ] の一覧で、[Lesson 6.dtsx] を選択し、[次へ] をクリックします。  
  
9. [Select Destination (出力先の選択)] ページで、[プロジェクト名] ボックスに「SSIS Tutorial Deployment」と入力し、[次へ] をクリックします。  
  
10. 残りのウィザードの各ページで [次へ] をクリックし、[確認] ページまで進みます。  
  
11. [確認] ページで [変換] をクリックします。  
  
12. 変換が完了したら、[閉じる] をクリックします。  
  
 Integration Services プロジェクトの変換ウィザードを閉じると、Integration Services 配置ウィザードが表示されます。 次に、このウィザードを使用してレッスン 6 パッケージを配置します。  
  
1.  [Integration Services 配置ウィザードの概要] ページで、プロジェクトを配置する手順を確認し、[次へ] をクリックします。  
  
2.  [Select Destination (出力先の選択)] ページで、サーバー名が SSISDB カタログを含む SQL Server のインスタンスであることと、パスが SSIS Tutorial Deployment を示していることを確認し、[次へ] をクリックします。  
  
3.  [確認] ページで概要を確認し、[配置] をクリックします。  
  
4.  配置が完了したら、[閉じる] をクリックします。  
  
5.  オブジェクト エクスプ ローラーで、[Integration Services カタログ] を右クリックし、[更新] をクリックします。  
  
6.  [Integration Services カタログ] を展開し、[SSISDB] を展開します。 プロジェクトが完全に展開されるまで、SSIS Tutorial の下のツリーを展開します。 SSIS Tutorial Deployment ノードのパッケージ ノードの下に Lesson 6.dtsx が表示されます。  
  
 パッケージが完了したことを確認するには、[Lesson 6.dtsx] を右クリックし、[構成] をクリックします。 [構成] ダイアログ ボックスで [パラメーター] を選択し、[コンテナー] に Lesson 6.dtsx のエントリ、[名前] に VarFolderName、[値] に新しいサンプル データへのパスがあることを確認し、[閉じる] をクリックします。  
  
 新しいサンプル データ フォルダーを作成する前に、「Sample Data Two」という名前のフォルダーを作成し、元のサンプル ファイルのうち 3 つをここにコピーします。  
  
### <a name="to-create-and-populate-a-new-sample-data-folder"></a>新しいサンプル データ フォルダーを作成して、データを取り込むには  
  
1.  Windows エクスプローラーで、ドライブのルート レベル (C:\\など) に新しいフォルダーを作成します。このフォルダーには "Sample Data Two" という名前を付けてください。  
  
2.  C:\Program Files\Microsoft SQL Server\110\Samples\Integration Services\Tutorial\Creating a Simple ETL Package\Sample Data フォルダーを開き、このフォルダーから任意の 3 つのサンプル ファイルをコピーします。  
  
3.  コピーしたファイルを New Sample Data フォルダーに貼り付けます。  
  
### <a name="to-change-the-package-parameter-to-point-to-the-new-sample-data"></a>新しいサンプル データを指すようにパッケージ パラメーターを変更するには  
  
1.  オブジェクト エクスプ ローラーで、[Lesson 6.dtsx] を右クリックし、[構成] をクリックします。  
  
2.  [構成] ダイアログ ボックスで、パラメーター値を Sample Data Two へのパスに変更します。 たとえば、C ドライブのルート フォルダーに新しいフォルダーを配置した場合は、C:\Sample Data Two となります。  
  
3.  [OK] をクリックして [構成] ダイアログ ボックスを閉じます。  
  
### <a name="to-test-the-lesson-6-package-deployment"></a>レッスン 6 パッケージの配置をテストするには  
  
1.  オブジェクト エクスプ ローラーで、[Lesson 6.dtsx] を右クリックし、[実行] をクリックします。  
  
2.  [パッケージの実行] ダイアログ ボックスで、[OK] をクリックします。  
  
3.  [メッセージ] ダイアログ ボックスで [はい] をクリックし、[概要レポート] を開きます。  
  
 パッケージの概要レポートには、パッケージの名前と状態の概要が表示されています。 [実行の概要] セクションはパッケージの各タスクの結果を示し、[使用されたパラメーター] セクションはパッケージの実行で使用されたすべてのパラメーターの名前と値を示します (VarFolderName など)。  
  
  
